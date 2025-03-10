```js
let connectBtn;
let connectBtnClick;
let sendBtnAClick;
let sendBtnBClick;
let sendBtnSClick;
let sendBtnTClick;
let state_confi    //esatdo de configuración
let state_armada   //estado cuando esta armed
let state_desarmada  //estado cuando explota
let state_explotada //estado cuando explota
let current_state = state_confi  //El estado inicial será en de configuración
let secuencia_correcta = ['A', 'B', 'A', 'SHAKE']
let secuencia_user = []  // para almecener la secuencia del user
let tiempo = 20        //Valor inicial de 20 segundos
let intervalo = 1000   //intervalo de 1 segundo = 1000 ms
let start_time = 0     //contador de tiempo que inicia en 0

function setup() {
  createCanvas(400, 400);
  background('#FFECB4');
  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(135, 100);
  connectBtn.mousePressed(connectBtnClick);
  
  let sendBtnA = createButton('A');
  sendBtnA.position(115, 300);
  sendBtnA.mousePressed(sendBtnAClick);

  let sendBtnB = createButton('B');
  sendBtnB.position(165, 300);
  sendBtnB.mousePressed(sendBtnBClick);

  let sendBtnS = createButton('S');
  sendBtnS.position(215, 300);
  sendBtnS.mousePressed(sendBtnSClick);

  let sendBtnT = createButton('T');
  sendBtnT.position(265, 300);
  sendBtnT.mousePressed(sendBtnTClick);
  
  fill('#000000')
  square(130, 140, 140, 20);
    
  
}

function draw() {
 if (current_state == state_confi)
        if (sendBtnAClick)   //Se disminuye el temporizador
            if (tiempo > 10)
                tiempo = tiempo - 1
                textSize(50);           // Tamaño del texto
                fill('#FFFFFF'); 
                text(tiempo, 170, 230);           //Se muestra el tiempo

        if (sendBtnBClick)   //Se aumenta el temporizador         
            if (tiempo < 60)
                tiempo += 1
        //Se muestra el tiempo}

        if (sendBtnSClick) //Evento de shake para armarla
            current_state = state_armada
            start_time = millis()   //Se guarda el tiempo actual en start_time
}
```
