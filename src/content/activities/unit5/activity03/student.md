### 1. por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario?
Porque en la unidad anterior no sabiamos con exactitud de que tamaño iba a quedar cada valor del paquete de datos, me explico, como se estaba enviando en formato ASCII, eso se tomaba el espacio que se necesitara, por ejemplo:

False -> ocuparía 5 bytes, mientras que true -> ocuparía 4 bytes.

Se debía marcar cada que un dato terminara y el final del paquetico de datos, porque no cada paquete iba a pesar lo mismo.

### 2. Que cambios veo entre este nuevo código y el de la unidad pasada
El cambio principal y el que diría que hace toda la diferencia es que en la parte en la que el sketch en p5.js recibe los datos ya de una vez pregunta si hay **6 BYTES**.

```js
if (port.availableBytes() >= 6) {
```
Luego como está la seguridad de que si o si son 6 bytes, sin rectificar tanto como en el código de la Unidad pasada, en este de una vez se guarda en la variable data.

```js
 let data = port.readBytes(6);
```
Lo siguiente también cambió, pero aun no lo entiendo:
```js
 const buffer = new Uint8Array(data).buffer;
 const view = new DataView(buffer);
```

Además acá de una vez se está procesando como ya se sabe que es, es decir:
microBitX -> 2 bytes de 8 bits cada uno = un Int de 16 bits
microBitY -> 2 bytes de 8 bits cada uno = un Int de 16 bits
microBitAState -> 1 bytes de 8 bits = un Uint de 8 bits
microBitBState -> 1 bytes de 8 bits = un Uint de 8 bits
```js
    microBitX = view.getInt16(0);
    microBitY = view.getInt16(2);
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
```
### 3. Error consola p5.js
En la consola también veo el error de sincronización, porque se supone que en este ensayo estamos enviando siempre los mismo valores por el Micro, entonces no tiene lógica que p5 diga que están llegando cosas diferentes. Aún no se por qué se produce este error.

<img width="538" alt="image" src="https://github.com/user-attachments/assets/1b50f3e8-e312-4a14-b15e-1e8e876f7b17" />

### 4.
Ahora todo se ve en código binario

<img width="721" alt="image" src="https://github.com/user-attachments/assets/d65bd47f-0b71-44e1-8a76-0e7fb347906b" />

Y ahora el error de la consola de p5.js está estable y arreglado:

<img width="347" alt="image" src="https://github.com/user-attachments/assets/c69cb1c6-4304-4202-9a5f-b0dc826e2ab1" />

### 5. 
La diferencia es que en este que es el final, ya si se incluyó de nuevvo el cálculo de ***"windowWidth / 2;"*** y  ***"windowHeight / 2;"***, que sirve para poder acomodar esas cordenadas teniendo en cuenta los ejes y centro de el canvas en p5. Además acá no se está mostrando nada en consola, so el mensaje de que el Micro está concectado y que está listo para dibujar.
```js
function readSerialData() {
.
.
.
    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);
}
```

Mientras que en este que es el anterior, aún se está dejando a ***X*** & ***Y*** tal cúal como llegan, sin volverlos a recentrar respecto al canvas. Además acá se sigue mostrando en consola el paquetico de lo que llega por el puerto: ***microBitX, microBitY, microBitAState, microBitBState.***
```js
function readSerialData() {
.
.
.
    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0);
    microBitY = view.getInt16(2);
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    console.log(
      `microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`
    );
}
```
