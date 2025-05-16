### <p align=center>Código Micro:bit</p>
```python
from microbit import *

uart.init(baudrate=115200)

fireworks = [
    Image('00000:'
          '00000:'
          '00900:'
          '00000:'
          '00000'),
    
    Image('00000:'
          '00300:'
          '03930:'
          '00300:'
          '00000'),
    
    Image('30303:'
          '03630:'
          '69996:'
          '03630:'
          '30303'),
    
    Image('30603:'
          '06960:'
          '69996:'
          '06960:'
          '30603'),
    
    Image('60906:'
          '09990:'
          '99999:'
          '09990:'
          '60906'),
    
    Image('00000:'
          '01310:'
          '03930:'
          '01310:'
          '00000'),

    Image('00000:'
          '00000:'
          '00900:'
          '00000:'
          '00000'),

    Image('00000:'
          '00000:'
          '00000:'
          '00000:'
          '00000')  
]


while True:
    display.show(fireworks, delay=200, loop=False, clear=True)
    if button_a.was_pressed():
        uart.write('A')
        sleep(500)
    if button_b.was_pressed():
        uart.write('B')
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('S')
        sleep(500)
    if pin_logo.is_touched():
        uart.write('T')
        sleep(500)
```

### <p align=center>Código p5.js</p>

```js
let port;
let isEvent;
let eventData;
let connectBtn;
let state_confi = "state_confi"; //esatdo de configuración
let state_armada = "state_armada"; //estado cuando esta armed
let state_desarmada = "state_desarmada"; //estado cuando explota
let state_explotada = "state_explotada"; //estado cuando explota
let state_error = "state_error"; //estado cuando explota
let current_state = state_confi; //El estado inicial será en de configuración
let secuencia_correcta = ["A", "B", "A", "S"];
let secuencia_user = []; // para almecener la secuencia del user
let tiempo = 20; //Valor inicial de 20 segundos
let intervalo = 1000; //intervalo de 1 segundo = 1000 ms
let intervaloError = 1500; //intervalo de 1.5 segundos para mostrar error
let start_time = 0; //contador de tiempo que inicia en 0
let BOOM = "BOOM";
let RESTART = "RESTART";
let ERROR = "ERROR";
let mensaje = "";
let mensajeColor = "#FFFFFF";

function setup() {
  createCanvas(400, 400);
  background("#FFECB4");
  port = createSerial();
  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(140, 350);
  connectBtn.mousePressed(connectBtnClick);

  let sendBtnA = createButton("A");
  sendBtnA.position(115, 300);
  sendBtnA.mousePressed(sendBtnAClick);

  let sendBtnB = createButton("B");
  sendBtnB.position(165, 300);
  sendBtnB.mousePressed(sendBtnBClick);

  let sendBtnS = createButton("S");
  sendBtnS.position(215, 300);
  sendBtnS.mousePressed(sendBtnSClick);

  let sendBtnT = createButton("T");
  sendBtnT.position(265, 300);
  sendBtnT.mousePressed(sendBtnTClick);

  fill("#000000");
  square(140, 140, 140, 20);

  textSize(80);
  fill("#FF4B3E");
  text("BOOMBA", 25, 100); // Dibujar el número actualizado
}

function tareaBomba() {
  if (current_state == state_confi) {
    textSize(50);
    fill("#FFFFFF");
    text(tiempo, 180, 230); // Dibujar el número actualizado

    if (isEvent == true && eventData == "A") {
      isEvent = false;
      if (tiempo > 10) {
        //Se disminuye el temporizador
        tiempo -= 1;
      }
      //Se muestra el tiempo
    }

    if (isEvent == true && eventData == "B") {
      isEvent = false;
      if (tiempo < 60) {
        //Se aumenta el temporizador
        tiempo += 1;
      }
    }

    if (isEvent == true && eventData == "S") {
      isEvent = false;
      //Evento de shake para armarla
      current_state = state_armada;
      start_time = millis(); //Se guarda el tiempo actual en start_time
      secuencia_user = [];
      print("S armed bomb");
    }
  } else if (current_state == state_armada) {
    textSize(50);
    fill("#FFFFFF");
    text(tiempo, 180, 230); // Dibujar el número actualizado

    if (millis() - start_time > intervalo && tiempo > 0) {
      //"Si ha pasado más de un segundo desde la última vez que revisé el tiempo..."
      start_time = millis(); // Reiniciar el temporizador
      tiempo -= 1;
      print("State armada timeout");
      if (tiempo == 0) {
        //Evento de que el tiempo se acabó
        print("BOOOOOOOM");
        current_state = state_explotada;
      }
    }

    if (isEvent == true && eventData == "A") {
      secuencia_user.push("A");
      isEvent = false;
    }

    if (isEvent == true && eventData == "B") {
      secuencia_user.push("B");
      isEvent = false;
    }

    if (isEvent == true && eventData == "S") {
      secuencia_user.push("S");
      isEvent = false;
    }

    if (
      secuencia_user.length === secuencia_correcta.length &&
      JSON.stringify(secuencia_user) === JSON.stringify(secuencia_correcta)
    ) {
      tiempo = 20;
      secuencia_user = [];
      current_state = state_desarmada;
      print("desarmada");
    } else if (secuencia_user.length === secuencia_correcta.length) {
      print("secuencia error");
      start_time = millis();
      current_state = state_error;
    }
  } else if (current_state == state_explotada) {
    displayBoom();

    if (isEvent == true && eventData == "T") {
      isEvent = false;
      // Evento de touch el logo para reiniciar
      tiempo = 20;
      current_state = state_confi; //Vuelve a confi
    }
  } else if (current_state == state_desarmada) {
    displayRestart();

    // si se presiona el botón T se reinicia.
    if (isEvent == true && eventData == "T") {
      isEvent = false;
      tiempo = 20;
      current_state = state_confi; // Vuelve a configuración
    }
  } else if (current_state == state_error) {
    displayError();

    if (millis() - start_time > intervaloError) {
      secuencia_user = [];
      start_time = millis();
      current_state = state_armada; // Vuelve a descontar
    }
  }
}

function displayRestart() {
  mensaje = "RESTART";
  mensajeColor = "#A5E65A"; // Verde
  textSize(30);
  fill(mensajeColor);
  text(mensaje, 142, 240);
}

function displayBoom() {
  mensaje = "BOOM";
  mensajeColor = "#FF4B3E"; // Rojo
  textSize(30);
  fill(mensajeColor);
  text(mensaje, 165, 240);
}

function displayError() {
  mensaje = "ERROR";
  mensajeColor = "#9E9E9E"; // Gris
  textSize(30);
  fill(mensajeColor);
  text(mensaje, 155, 240);
}

function sendBtnAClick() {
    isEvent = true;
    eventData = "A";
}

function sendBtnBClick() {
    isEvent = true;
    eventData = "B";
}

function sendBtnSClick() {
      isEvent = true;
      eventData = "S";
}

function sendBtnTClick() {
      isEvent = true;
      eventData = "T";
}

function tareaSerial() {
  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx == "A") {
      isEvent = true;
      eventData = "A";
    } else if (dataRx == "B") {
      isEvent = true;
      eventData = "B";
    } else if (dataRx == "S") {
      isEvent = true;
      eventData = "S";
    } else if (dataRx == "T") {
      isEvent = true;
      eventData = "T";
    }
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}

function draw() {
  background("#FFECB4");
  textSize(60);
  fill("#FF4B3E");
  text("BOOMBA", 75, 100); // Dibujar el número actualizado

  fill("#000000");
  square(140, 140, 140, 20);
  tareaBomba();
  tareaSerial();

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

```
