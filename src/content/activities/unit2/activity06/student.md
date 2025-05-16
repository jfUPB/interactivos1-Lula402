### Explicación del funcionamiento
Cuando en la pantalla del Pc se presiona el botón A, este envia el caracter "A" por el puerto serial al Microbit. Este caracter tiene una función asignada, la cual es mostrar en el display las 4 caritas con expresiones diferentes, y con un tiempo de sleep de 1000 entre cada una.

https://github.com/user-attachments/assets/608f5dd0-f866-4ec2-94fc-358854137fc4

### Código Microbit python editor
```python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('A'):
                display.show(Image.HAPPY)
                sleep(1000)
                display.show(Image.SAD)
                sleep(1000)
                display.show(Image.ANGRY)
                sleep(1000)
                display.show(Image.SURPRISED)
```
### Código p5.js
```java
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
}

let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 200);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send A');
    sendBtn.position(220, 200);
    sendBtn.mousePressed(sendBtnClick);
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

function sendBtnClick() {
    port.write('A');
}
```
