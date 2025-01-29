### Solución del problema
Para lograr que más imagenes se pudieran ver en el display del Microbit, dupliqué lo que se había hecho con el botoón de "Send love", a cada nueva variable la definí diferente y la inicialicé al crear el botón. En la función de cada botón, indiqué que el puerto escribiera un letra (a,b,c,d) para que el Microbit python editor lo leyera y supiera que imagen estaba relacionada a esa letra. De esta manera, al presionar los botones se proyectaba la imagen correspondiente. 
Escogí un corazón, una carita feliz, un carita triste y un pacman.

### Código del programa en p5.js
```JavaScript
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background('#EDD9F1');
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(140, 150);
    connectBtn.mousePressed(connectBtnClick);
  
    let sendBtn1 = createButton('Send Love');
    sendBtn1.position(140, 170);
    sendBtn1.mousePressed(sendBtn1Click);
  
    let sendBtn2 = createButton('Be Happy');
    sendBtn2.position(140, 190);
    sendBtn2.mousePressed(sendBtn2Click);
  
    let sendBtn3 = createButton('Be Sad');
    sendBtn3.position(140, 210);
    sendBtn3.mousePressed(sendBtn3Click);

    let sendBtn4 = createButton('Send Pacman');
    sendBtn4.position(140, 230);
    sendBtn4.mousePressed(sendBtn4Click);
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

function sendBtn1Click() {
    port.write('a');
}

function sendBtn2Click() {
    port.write('b');
}

function sendBtn3Click() {
    port.write('c');
}

function sendBtn4Click() {
    port.write('d');
}
```
### Código para micro:bit
```Micro:bit
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('a'):
                display.show(Image.HEART)
            if data[0] == ord('b'):
                display.show(Image.HAPPY)
            if data[0] == ord('c'):
                display.show(Image.SAD)
            if data[0] == ord('d'):
                display.show(Image.PACMAN)
```
