#### 1. ¿Para qué se usan estas imágenes? ¿Qué representan?
Estas imagenes se usan para poder cambiar el tipo de pincel por decirlo así. Entonces estas imagenes son basicamente las puntas de pincel.

#### 2. ¿Qué pasaría ahora si das click al botón? 
Si al presionar el botón el puerto está cerrado, entonces se abre. Si al presionar el botón el puerto ya está abierto, entonces este se cierra.

#### 3. ¿Por qué? ¿Podrías leer datos si el puerto está cerrado? ¿Qué pasaría si el puerto está cerrado y el micro:bit envía datos?
Solo se leen datos del micro:bit si el puerto está abierto porque no hay otro canal para comunicar el Microbit con el sketch, a no ser de que yo manualmente se van a comunicar por Bluethoot o radio (ota funcionalidad del Micro).

Si ***port.opened()*** es false, es decir, el puerto está cerrado, el Sketch no puede recibir los datos que el Microbit le manda. Es como si el Microbit hablara y como la puerta está cerrada el Sketch no puede escucharlo.

Si el puerto está cerrado y el Micro manda datos, esos datos se pierden "puf", porque basicamente nadie los está leyendo ni almacenando. Cosa diferente es cuando los datos si pasan por el puerto y se almacenda ese paquete en la variable "data".

#### 4. Qué pasaría si el micro:bit no envía el "\n"?
Si el Microbit no envia el salto de línea, entonces el código no sabe hasta que punto sigue leyendo "readUntil". Sin ese "\n" seguirá leyendo de corrido y será una chorrera de datos, además de que ya lo siguiente del código no funcionará, porque todo está pensado para que sean grupitos de 4 datos.

#### 5. ¿Por qué se suma windowWidth/2 y windowHeight/2 a los valores de x e y?
Porque el Microbit envia las coordenadas teniendo de referencia el origen (0,0) en la mitad del canvas, pero es que en p5.js la coordenada (0,0) está en la esquina de arriba a la izquiera. Y crece hacia abajo y x hacia la derecha.
Al sumar ***windowWidth/2 y windowHeight/2*** lo que se está haciendo es volver a acomodar las coordenadas donde estaban pensadas para estar.

#### 6. ¿Cómo puedes verificar que los eventos de keypressed y keyreleased se están generando?
Podría verficar esto al poner un print dentro de las funciones, de modo que si el código si está entrando entonces se va a printear eso.
Puede ser algo como:

print("la tecla se presionó") y print("la tecla se soltó")

De todas maneras al entender que hace cada tecla se puede evidenciar que keypressed y keyreleased se están generando, porque cambian algo en el arte del canvas.

#### 7. ¿Qué hace? ¿Por qué es necesario almacenar el estado anterior de los botones? ¿Qué pasaría si no se almacenara el estado anterior?
- Si el botón A del Micro estaba false y ahora esta true, quiere decir que se presionó. Al presionarse entonces se randomiza el tamaño del trazo desde 50 hasta 160. Luego la posición en la que estaba el Microbit cuando el boton fue presionado se guarda en clickPosx Y clickPosY.
- Si el botón B del Micro estaba true y luego está false, quiere decir que se soltó. Al soltarse entonces se randomiza el color (C) RGB + transparencia del trazo.

- Luego el nuevo estado de ambos botones se almacena en el previus state para que cuando vuelva a correr si se actualice correctamente: ***prevmicroBitAState = newAState;*** y ***prevmicroBitBState = newBState;***

Si no se almacena el estado anterior el programa se quedaría en el mismo tamaño de trazo y de color, porque al no guardar el nuevo estado como previo lo que va a pasar es que ne la nueva iteración será el mismo de la iteración pasada y ps no tiene gracia.

#### 8. ¿Qué diferencias encuentras? 
La difencia principal que encuentro es que ahora se incluyó el Microbit en el proceso ¿, por ende el puerto serial. 

#### 9. ¿Qué pasó con algunos eventos del mouse? 
Muchos de los eventos del mouse fueron reemplazados por el Microbit, como el uso de los botones el vez de las teclas de mouse y por ejemplo en vez de la posición del mouse la posición del Microbit.

#### 10. ¿Qué paso con la función relacionada con la barra de espacio del teclado?
Esta función ya no está disponible, creería que lo que la reemplazó fue le botón B que es el que cambia el color ahora.

***<p align="center">"No se están recibiendo 4 datos del micro:bit"</p>***

#### 1. ¿Qué significa esto? Analiza si este mensaje ocurre en varios frames o solo en uno.
Este mensaje solo ocurre en un frame, y es en el frame inicial.
Significa que el paquete de datos no está compuesto por 4 datos, sino por menos, entonces no se puede hacer nada porque necesita los 4 datos para poder pintar algo.

#### 2. ¿Por qué? 
Esto pasa porque como es el momento inicial de haberse activado el código aun no recibe input desde el microbit, es decir, en esa primera iteración probablemente aun no se ha presionado ni movido todo lo del microbit. 

#### 3. ¿Qué puedes hacer para solucionar este problema?
No creo que sea necesario solucionarlo, no me parece un problema porque es lógico que al inicio no estén los 4 datos.
Sin embargo lo que se podría hacer es inicializar esos 4 valores como (0,0,false,false), para que al arrancar el programa al menos esté el primer paquete de 4 datos.

