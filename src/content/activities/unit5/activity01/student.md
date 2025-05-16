#### <p align=center> Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit? </p>
El Micro:bit y el sketch de p5.js se están comunicando por el puerto serial. El Micro:bit recibe sus inputs, luego los guarda y los envía por medio del puerto serial a p5.js. p5.js recibe esos paquetes de datos como input, los procesa, los guarda, y el output se ve en el canvas.

El microbit envía 4 datos: xValue, yValue, aState, bState.

&nbsp;<br><br>

#### <p align=center> ¿Cómo es la estructura del protocolo ASCII usado? </p>
La siguiente es la estructura del protocolo ASCII que se maneja en este programa:

```python
"{},{},{},{}\n".format(xValue, yValue, aState,bState)
```

Se organizan los cuatro datos en una sola cadena de texto, separados por comas, y al final un salto de línea (\n) para indicar el final del paquetico. Todo se codifica en ASCII para que pueda ser leído correctamente por p5.js a través del puerto serial.

&nbsp;<br><br>
#### <p align=center> Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla. </p>

En esta parte se verifica que si hayan datos por leer antes de leerlos. Entonces si lso bytes disponibles son mayores a 0, osea que si sí hay bytes disponibles entonces que entre al if. Dentro del if lo que se hace es que el puerto lea hasta que encuentre un "/n", y que eso lo amacene en la variable data.
```js
if (port.availableBytes() > 0) {
      let data = port.readUntil("\n")
```

En esta parte se vuelve a asegurar de que si haya algo guardado en la variable data, para poder procesarlo. Cuando entra al if lo primero que se hace es que usamos la función trim(), que recorta es ese salto de linea del final y lo volvemos a guardar en data. Después creamos una variable values y de una vez la definimos usando otra función de data que se llama split y lo que hace es que separa cada uno de los datos que le llegaron por el puerto seria por comas asi: ","
```js
      if (data) {
        data = data.trim();
        let values = data.split(",");
```

Otro filtro de asegurar si son 4 datos, porque se if pregunta si la longitud de la varible values (que se creó arriba) es = 4.

Cuando entra al if acá es donde los datos se transforman a como los necesitamos en p5. En las variables microBitX & microBitY vamos a guardar respectivamente el value en la 1era posición: values[0] y el value en la 2da posición values[1]. En esta parte de una vez se transforma esos values y se empiezan a tratar como ints, además de hacerse un calculito que se necesitará.

En las variables microBitAState y microBitBState se guarda respectivamente el values[2] y values[3], para ambos se usa la función toLowerCase() que sirve para que si se manda algo con mayusculas se convierta a minusculas.

De una vez se actuliza elestado de los botones con esa nueva info que entró.
 
```js
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
```

&nbsp;<br><br>
#### <p align=center> ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit? </p>

1. se presionan alguno de los botones en el microbit.
2. el microbit lo almacena en la variable correspondiente. False si no se presiona, true si si se presiona.
3. al enviar el paquete de datos por el puerto serial ahí ya van incluidos los datos correspondientes a los botones.
4. p5.js recibe los datos, los procesa y guarda como expliqué en la pregunta anterior.
5. al momento de guardar los datos hay una línea que dice ```updateButtonStates(microBitAState, microBitBState);```, en esta si venía un ***true*** o un ***false*** se guardan en esas varibles de microBitAState y microBitBState.
6. En la función updateButtonStates es que se generan los eventos de A pressed y B released, como?
   
   Si A tenía un false y luego en este paquete le llega un true, entonces A es presionado. 
   Si B tenía un true y luego en este paquete le llega un false, entonces B estaba presionado y lo soltaron.

7. de esta manera ya con condicionales se rectifican esos eventos que mencioné y entra a las correspondientes acciones.

&nbsp;<br><br>
#### <p align=center> Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch. </p>

<p align=center>
<img width="500" alt="image" src="https://github.com/user-attachments/assets/1d050bd1-ab71-47a3-b9d0-b202cc2745ce" />
</p>

<p align=center>
<img width="500" alt="image" src="https://github.com/user-attachments/assets/9b613edb-2a24-4e76-9f44-068d682f32d0" />
</p>
