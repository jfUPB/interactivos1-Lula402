
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
El Checksum es ese byte que va al final del paquete de datos. Lo usamos para chekear que la cantidad de datos que se envió en ese paquete es la misma cantidad de datos del paquete que se recibió. Esto se hace de la siguiente manera: el cheksum hace una suma de los bytes del paquetico y le realiza la operación MOD (módulo) 256, esto es para que la suma de esos 8 bytes quepa en 8bits.
Esto es !!!!!!!!!!


### <p align=center>En la función readSerialData() del programa en p5.js:</p
                                                                           
***- ¿Qué hace la función concat? ¿Por qué?***

***- En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?***
Porque el Buffer es como esa carpetica o bolsa donde metemos los datos, entonces primero pregunto si ya tengo 8 datos dentro de la carpeta, si si tengo 8 datos entonces perfectom la leo, pero si aun no son 8 para que la voy a leer si no está guardado todo lo que necesito.

Es como cuado van a abrir un curso, primero analizo cuantas personas hay inscritas porque solo con cierta cantidad de gente puedo abrir el curso.

***- En el código anterior qué significa 0xaa?***
Ese byte hace el papel de header, es decir el inicio del paquete de datos. En binario significa 10101010 y es fácil de identificar para saber desde cuando empezar a contar.

***- En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?***

***- Si hay menos de 8 bytes qué hace la instrucción break? ¿Por qué?***

***- ¿Cuál es la diferencia entre slice y splice? ¿Por qué se usa splice justo después de slice?***

***- A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?***

***- ¿Por qué se compara el checksum enviado con el calculado? ¿Para qué sirve esto?***

***- En el código anterior qué hace la instrucción continue? ¿Por qué?***

***- ¿Qué es un DataView? ¿Para qué se usa?***

***- ¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?***
