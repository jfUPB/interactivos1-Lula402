
| Aspectos  | ASCII | BINARIO   | EJEMPLO   |
| ------------- | ------------- | ------------- | ------------- |
| **Eficiencia** | ✖ Es un código de texto, entonces para que la máquina lo entienda toca dar un paso más y lo traduce.| ✔ Es mucho más eficiente porque ya está en lenguaje de máquina. | Cuando usabamos ASCII en el puerto serial se veían ese código ASCII y al llegarle a p5.js, este tenía que trim-searlo, y split-searlo y aparte decir que eso lo tenía que tratar como un ***int***. |
| **Velocidad** | ✖ Para expresar el mismo mensaje, ocupa más bytes, entonces se demora como el doble masomenos en llegar al receptor. | ✔  Para expresar el mismo mensaje, ocupa menos bytes, entonces llega mucho más rápido al receptor.  | Esto lo observé en la consola de p5.js: el código con ASCII demora el doble de tiempo en mostrar por consola los datos que recibe ***vs*** en Binario es casi que inmediado, uno ni logra contar cuanto tiempo.  |
| **Facilidad**  | ✔  Es mucho más fácil para nosotros los humanos, ya que se entiende con ayuda de la tablita, entonces por ejemplo podemos debuggear más rápido.| ✖ Es más dificil para nosotros, porque el binario es más enredado decifrar. | Esto se evidenció cuando al consultar la tablita ya podíamos traducir el paquete de datos es ASCII del puerto. |
| **Usos de recursos**  | ✖ Como el mensaje se demora más tiempo en llegar y además cuando llega toca traducirlo, gasta más recursos.  | ✔  Es más rápido de traducir y de procesar, entonces ahorra ese esfuerzo extra a los sistemas.  |Se nota mucho comparando ambos códigos, ya que los datos se manejan de maneras diferentes, como en ASCII hay varios fitros para asegurar que hayan 4 datos, y en Binario hay más seguridad de que siempre van a ser paquetes de bytes.|

### <p align=center>¿Por qué fue necesario introducir framing en el protocolo binario?</p>
Fue necesario porque es como decir "Este paquetico empieza aquí y termina acá", pero pues uno diria que entonces cual es la gracia si se supone que ya teniamos la certeza que eran 8 bytes siempre. Esto es para evitar errores, el framing permite al receptor saber donde empieza (header) y termina un paquete, de esa manera puede leer en orden correcto los datos y no empezar por la mitad o contar solo 6 byte o 12 bytes. Además como se van a enviar tantos paquetes de datos seguidos es lo mejor para separarlos.

### <p align=center>¿Cómo funciona el framing?</p>
1. **serialBuffer.length >= 8** ahí le estamos diciendo exactamente al receptor que los paquetes van a ser de 8 bytes (en realidad son 6 bytes).

2. **0xaa:** es el header, entonces el receptor sabe que a partir de aqui hace el slice de 8 bytes, es decir a partir de ahí cuenta el paquete, asi no se confunde con lo otro.

3. Se hace el slice y splice de el paquete de 8 datos, es decir, cortamos esos 8 bytes y también los limpiamos de el puerto pues para que no se vuelvan a leer.

4. Luego de esos 8 datos hacemos otro slice de 7 bytes, de los cuales 6 bytes son los datos y el último corresponde al checksum.

5. Luego se compara el checksum computado con el recibido. Esta es como la última prueba de seguridad que hace el framing, porque se asegura que el paquete que se mandó es el mismo que se recibió, por ahi derecho al hacer es checksum se da uno cuenta que si sea de la cantidad de bytes correspondiente.

### <p align=center>¿Qué es un carácter de sincronización?</p>
Es ese byte que se establece como esa cosa que va a marcar cada paquete, de esa manera tanto el emisor (Micro) y el receptor (p5) van a saber donde arranca cada paquete. En este caso el ***header*** es el caracter de sincronización, porque no es realmente un dato sino que se pone para indicar que de ahí de empiezan a contar los 8 bytes.

### <p align=center>¿Qué es el checksum y para qué sirve?</p>
El Checksum es ese byte que va al final del paquete de datos. Lo usamos para chekear que la cantidad de datos que se envió en ese paquete es la misma cantidad de datos del paquete que se recibió. Esto se hace de la siguiente manera: el cheksum hace una suma de los bytes del paquetico y le realiza la operación MOD (módulo) 256, esto es para que el resultado del MOD de la suma de esos 8 bytes quepa en 8bits.
Esto es porque asi se asegura que el mayor resultado pueda ser 1111 1111 = 255

!!!!!!!!


### <p align=center>En la función readSerialData() del programa en p5.js:</p
                                                                           
***- ¿Qué hace la función concat? ¿Por qué?***
```
  let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
```

***Concat*** es para concatenar los nuevos datos que llegan y ponerlos en serialBuffer. En ***newData*** se guardan los nuevos datos quen entren por el puerto ```port.readBytes(available);```. Luego lo que se hace es que se concatena, osea como que se pega ese nuevo dato en el array que tenia ***serialBuffer***, que dato? el nuevo que se guardó en ***newData***. Todo ese nuevo array concatenado se vuelve a guardar en la varible ***serialBuffer***.

***- En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?***
Porque el Buffer es como esa carpetica o bolsa donde metemos los datos, entonces primero pregunto si ya tengo 8 datos dentro de la carpeta, si si tengo 8 datos entonces perfectom la leo, pero si aun no son 8 para que la voy a leer si no está guardado todo lo que necesito.

Es como cuado van a abrir un curso, primero analizo cuantas personas hay inscritas porque solo con cierta cantidad de gente puedo abrir el curso.

***- En el código anterior qué significa 0xaa?***
Ese byte hace el papel de header, es decir el inicio del paquete de datos. En binario significa 10101010 y es fácil de identificar para saber desde cuando empezar a contar.

***- En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?***
Primero que todo lo que se está evaluando en ese while es que el paquete de datos si inicie por el header. Si la condición ```if (serialBuffer[0] !== 0xaa)``` se cumple, osea que el 1er byte no es el header, ***Shift*** lo elimina. Es como si hubiese un vigilante fijandose cuando hay un header y si esa persona en la fila no es un 0xaa entonces llega seguridad (shift) y se lo lleva para que pase el siguiente en la fila.

La instrucción ***continiue*** es para que despues de borrar ese dato que no es el header, el ciclo while vuelva a iniciar y no ejecute lo que hay despues de haber hecho el shift. Esto es para que al borrar ese dato, se vuelva a evaluar si es un header.

***- Si hay menos de 8 bytes qué hace la instrucción break? ¿Por qué?***
Esa instrucción es como otro filtro de seguridad. Se supone que para cuando lleguemos a esa línea ya sabemos que si hay un header de primeras, entonces con un if se evalua que despues de ese header si hayan otros 7 datos para formar el paquete completo, si no hay suficientes datos entonces se hace el ***break***, que es para que salga del ciclo. El break rompe el ciclo del todo porque no tiene sentido seguir si no hay 8 datos.

***- ¿Cuál es la diferencia entre slice y splice? ¿Por qué se usa splice justo después de slice?***
La diferencia está en que slice hace un corte de un pedacito entre todos esos datos, por ejemplo con un pan, si le hago slice es sacar un tajadita. Mientras que splice es limpiar esa tajadita entre todos esos datos.

En este caso se usó splice despues de slice porque el orden es: primero cortar el paquetico de datos con el que quiero trabajar (slice), luego como ya no quiero seguirlo teniendo en la fila de datos del puerto, le hago splice para limpiarlo. ¿por que no quiero seguirlo teniendo en la fila de datos? porque entonces esos datos van a seguir ahi esperando a que yo haga algo con ellos y pues eso es un error en comunicación porque si ya recibí el mensaje no debería porque volverlo a recibir.

***- A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?***
A la función ***reduce*** se le entregan dos varibles, es este caso una es ***acc** que es el acumuludor en el que voy  ir guardando el resultado y ***val** va a ser el valor de cada dato en el array, también se aclara que el acc va a iniciar en 0. Reduce basicamente va reduciendo ese array a un solo valor, porque lo que se está haciendo es sumar todos sus datos. 

El dato #1 se mete en el acc, luego el dato #2 se le suma al acc, luego el dato #3 se le suma al acc...

***- ¿Por qué se compara el checksum enviado con el calculado? ¿Para qué sirve esto?***
Se comparan para asegurarnos que si son 8 bytes en el paquete y además para asegurarnos que el módulo de 256 de la suma de los datos del paquete es la misma cuando fue enviado y cuando fue recibido. Esto sirva para chekear que el paquete no perdió datos y que si se esté contando el paquete como debe ser, por ejemplo en caso de que uno de los datos sea 0xaa como el header.

***- En el código anterior qué hace la instrucción continue? ¿Por qué?***
En esa instrucción ***continiue*** hace lo mismo que hizo ahorita arriba. Se encarga de que si no se cumplió que el checksum enviado es igual al checksum recibido, entonces de una vuelve a hacer una nueva iteración del ciclo sin importar que hay después. Esto es porque no nos interesa seguir con las otras instrucciones si los datos tienen un error, entoces ***continiue*** dice "bueno, volvamos entonces a hacer todo desde arriba, ey while, vuelve a empezar porfa".

***- ¿Qué es un DataView? ¿Para qué se usa?***


***- ¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?***
