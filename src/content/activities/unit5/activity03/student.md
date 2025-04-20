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
POR REVISAR
Ahora no veo nada en la consola de p5.js 😕, osea si veo lo de "Connected to serial port" "Microbit ready to draw", pero a partir de ahí la consola quedó vacía y aunque mueva el Micro no me muestra nada.

### 5. 
POR TERMINAR
