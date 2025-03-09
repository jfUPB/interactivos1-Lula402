### Bomba 3.0 desde p5.js
```js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background('#FFACA6');
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(140, 150);
    connectBtn.mousePressed(connectBtnClick);

    let sendBtn1 = createButton('A');
    sendBtn1.position(200, 170);
    sendBtn1.mousePressed(sendBtn1Click);

    let sendBtn2 = createButton('B');
    sendBtn2.position(200, 190);
    sendBtn2.mousePressed(sendBtn2Click);

    let sendBtn3 = createButton('S');
    sendBtn3.position(200, 210);
    sendBtn3.mousePressed(sendBtn3Click);

    let sendBtn4 = createButton('T');
    sendBtn4.position(200, 230);
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
    port.write('A');
}

function sendBtn2Click() {
    port.write('B');
}

function sendBtn3Click() {
    port.write('S');
}

function sendBtn4Click() {
    port.write('T');
}
```
