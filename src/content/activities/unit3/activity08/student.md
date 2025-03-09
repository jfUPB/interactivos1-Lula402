```js
let connectBtn;
let sendBtnAClick;
let sendBtnBClick;
let sendBtnSClick;
let sendBtnTClick;
let isEvent = False
let eventData = ''
let state_confi = 0    //esatdo de configuración
let state_armada = 1   //estado cuando esta armed
let state_explotada = 2 //estado cuando explota
let current_state = state_confi //El estado inicial será en de configuración
let secuencia_correcta = ['A', 'B', 'A', 'S']
let secuencia_user = []  //para almecener la secuencia del user
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
function tareaBomba(){
  
}

function tareaEventos(){
    if (sendBtnA.mousePressed(sendBtnAClick))   
        isEvent = True
        eventData = 'A'

    if (sendBtnB.mousePressed(sendBtnBClick))   
        isEvent = True
        eventData = 'B'            

    if (sendBtnS.mousePressed(sendBtnSClick))  
        isEvent = True
        eventData = 'S'

    if (sendBtnS.mousePressed(sendBtnSClick))
        isEvent = True
        eventData = 'T'
        
    if (port.write('A'))
        isEvent = True
        eventData = 'A'
  
    if (port.write('B'))
        isEvent = True
        eventData = 'B'
  
    if (port.write('S'))
        isEvent = True
        eventData = 'S'
  
    if (port.write('T'))
        isEvent = True
        eventData = 'T'
}

function draw() {

    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

while (true)
  setup()
  tareaBomba()
  tareaEventos()
```
