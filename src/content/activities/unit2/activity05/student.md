### Experimento puerto serial
#### Código
```python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('A'):
                display.show('A')
                sleep(1000)
                display.show(Image.HAPPY)
```
``` asm
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
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send A');
    sendBtn.position(220, 300);
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
#### Documentación
Así es como se ve el canvas de p5.js, donde quedó un botón para cpnectar el Microbit y otro para enviar por el puerto serian un caracter, que en este caso es "A".

<img width="204" alt="image" src="https://github.com/user-attachments/assets/6adb4142-76f5-429d-bc49-c86cd49e594b" />

Luego al oprimir el botón virtual de "Send A", en el display del Microbit se muestra el caracter A. Todo esto gracias a la función en p5.js, que ordena que cuando se oprima ese botón se envia al Microbit el caracter A, en la programación de Python cuando el caracter A llegue por el puerto serial se proyecta una A en el display.

<img width="154" alt="image" src="https://github.com/user-attachments/assets/494a50b5-9717-466c-b2b2-a32907bc5b37" />

