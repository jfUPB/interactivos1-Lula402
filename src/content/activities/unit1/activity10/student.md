### Proceso de conexión
1. Conecté el Microbit en el port USB del pc.
2. En microbit Python editor, retiré la parte final del código que era para que al dar click en "send love" saliera un corazón. Luego enviamos el código actualizado al microbit.
3. En p5.js modifiqué el código de la primera actividad que tuvimos con Microbit. Retiré la parte del send love, centré el botón de "connect to Micro:bit", reemplacé los circulos por cuadrados y su tamaño para que quedara centrado y por último cambié los colores que quería.
4. Comprobé que todo funcionara bien.

### Comunicación entre dispositivos
Los botones del Mircrobit son inician la comunicación entre los dispositivos, estos son el input. Al presionarlos generan un cambio en el color del cuadrado que está en la pantalla, esto es el output.

### Código para micro:bit

``` Micro:bit
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
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(500)
```

### Código del programa en p5.js

``` JavaScript
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(135, 300);
    connectBtn.mousePressed(connectBtnClick);
    fill('white');
    square(150,150,100);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('#FFC107');
        }
        else if(dataRx == 'B'){
            fill('#00BCD4');
        }
        else{
            fill('#9E9E9E');
        }
        background(220);
        square(150,150,100);
        fill('black');
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
