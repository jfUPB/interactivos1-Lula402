### Mapeo de los botones
El circulo se mueve de esa manera porque está programado para que al presionar el botón **A**, la posición en **X** se hace = -10, mientras **Y¨** se mantiene = 150. Al contrario al presionar el botón **B**, la posición **Y** se hace = + 50, mientras **X** se mantiene = 150.

### Código del programa en p5.js

```JavaScript
let port;
let connectBtn;
let x= 150;
let y= 150;
let d= 100;
function setup() {
    createCanvas(400, 400);
    background('black');
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    fill('#71D2DE');
    circle(x, y, d);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            circle (x=-10, y=150 , 100);
        }
        else if(dataRx == 'B'){
            circle (x=150 , y=+10, 100);
        }
        background('black');
        circle(x, y, d);
        fill('#71D2DE');
        text(dataRx, width / 2, height / 2);
    }


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
    port.write('h');  
}
```

### Código para micro:bit
```Micro:bit
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
```
