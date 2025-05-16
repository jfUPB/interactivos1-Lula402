### <p align=center> ¿Qué tanto aprendí en esta unidad? </p>
### Conceptos que aprendí
1. maquina de estados
2. uso de funciones para ordenar el código
3. Función draw
4. Varibles globales y locales a profundidad

#### Ejemplos
1.
```js
let state_confi = "state_confi"; //esatdo de configuración
let state_armada = "state_armada"; //estado cuando esta armed
let state_desarmada = "state_desarmada"; //estado cuando explota
let state_explotada = "state_explotada"; //estado cuando explota
let state_error = "state_error";
```
2.
```js
  function draw() {
```
3. Todas las que pongo por fuera de cualquier función, en este caso al inicio de todo el programa son globales y las puedo usar dentro de funciones. Si declaro una variable dentro de una función esta será local.
   
#### ¿por qué considero que aprendí esos conceptos?
Considero que aprendíe estos conceptos porque los entiendo por mi cuenta, se en que parte y momento usarlos y que poner dentro de ellos. 

### Conceptos que no aprendí
1. sendBtnB.mousePressed(sendBtnBClick);
2. Como funciona a profundidad el port desde p5.
#### Ejemplos
1. ```js sendBtnT.mousePressed(sendBtnTClick); ```
   Se que sendBtnTClick es una función, se que sendBtnT es una variable, pero no se que viene a ser mousePressed en esa línea.
2.
```js
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
```
#### ¿por qué considero que aprendí esos conceptos?
Depronto porque solo entendí superficialmente como funcionan y que lo necesito ahí, pero no profundicé que son cada uno.

###  Estrategias
Para los conceptos qu eno aprendí pienso seguir practicando y usando este tipo de estructura de máquina de estados para tener esos momentos de "ensayo y error". También repasar los ejercicios del curso y código antiguo para seguir repasando. También ChatG para tutorearme.

Le dedicaré las horas de clase y aproximadamente dos horas extras por fuera. Desde que empezamos a trabajar con p5.js básicamente comencé.
