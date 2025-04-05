### <p align=center> Bomba Full en P5.js </p> 
```js
let btnAClicked = false;
let btnBClicked = false;
let btnSClicked = false;
let btnTClicked = false;
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
  connectBtn = createButton("");

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
  text("BOOMBA", 25, 100); 
}

function draw() {
  background("#FFECB4");
  textSize(60);
  fill("#FF4B3E");
  text("BOOMBA", 75, 100); 

  fill("#000000");
  square(140, 140, 140, 20);

  if (current_state == state_confi) {
    textSize(50);
    fill("#FFFFFF");
    text(tiempo, 180, 230); 

    if (btnAClicked == true) {
      btnAClicked = false;
      if (tiempo > 10) {
        //Se disminuye el temporizador
        tiempo -= 1;
      }
      //Se muestra el tiempo
    }

    if (btnBClicked == true) {
      btnBClicked = false;
      if (tiempo < 60) {
        //Se aumenta el temporizador
        tiempo += 1;
      }
    }

    if (btnSClicked == true) {
      btnSClicked = false;
      //Evento de shake para armarla
      current_state = state_armada;
      start_time = millis(); //Se guarda el tiempo actual en start_time
      secuencia_user = [];
      print("S armed bomb");
    }
  } else if (current_state == state_armada) {
    textSize(50);
    fill("#FFFFFF");
    text(tiempo, 180, 230); 

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

    if (btnAClicked == true) {
      secuencia_user.push("A");
      btnAClicked = false;
    }

    if (btnBClicked == true) {
      secuencia_user.push("B");
      btnBClicked = false;
    }

    if (btnSClicked == true) {
      secuencia_user.push("S");
      btnSClicked = false;
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

    if (btnTClicked == true) {
      btnTClicked = false;
      // Evento de touch el logo para reiniciar
      tiempo = 20;
      current_state = state_confi; //Vuelve a confi
    }
  } else if (current_state == state_desarmada) {
    displayRestart();

    // si se presiona el botón T se reinicia.
    if (btnTClicked == true) {
      btnTClicked = false;
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
  btnAClicked = true;
}

function sendBtnBClick() {
  btnBClicked = true;
}

function sendBtnSClick() {
  btnSClicked = true;
  print("S was pressed");
}

function sendBtnTClick() {
  btnTClicked = true;
}

```
