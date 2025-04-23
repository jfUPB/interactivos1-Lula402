
| Aspectos  | ASCII | BINARIO   | EJEMPLO   |
| ------------- | ------------- | ------------- | ------------- |
| **Eficiencia** | ✖ Es un código de texto, entonces para que la máquina lo entienda toca dar un paso más y lo traduce.| ✔ Es mucho más eficiente porque ya está en lenguaje de máquina. | Cuando usabamos ASCII en el puerto serial se veían ese código ASCII y al llegarle a p5.js, este tenía que trim-searlo, y split-searlo y aparte decir que eso lo tenía que tratar como un ***int***. |
| **Velocidad** | ✖ Para expresar el mismo mensaje, ocupa más bytes, entonces se demora como el doble masomenos en llegar al receptor. | ✔  Para expresar el mismo mensaje, ocupa menos bytes, entonces llega mucho más rápido al receptor.  | Esto lo observé en la consola de p5.js: el código con ASCII demora el doble de tiempo en mostrar por consola los datos que recibe ***vs*** en Binario es casi que inmediado, uno ni logra contar cuanto tiempo.  |
| **Facilidad**  | ✔  Es mucho más fácil para nosotros los humanos, ya que se entiende con ayuda de la tablita, entonces por ejemplo podemos debuggear más rápido.| ✖ Es más dificil para nosotros, porque el binario es más enredado decifrar. | Esto se evidenció cuando al consultar la tablita ya podíamos traducir el paquete de datos es ASCII del puerto. |
| **Usos de recursos**  | ✖ Como el mensaje se demora más tiempo en llegar y además cuando llega toca traducirlo, gasta más recursos.  | ✔  Es más rápido de traducir y de procesar, entonces ahorra ese esfuerzo extra a los sistemas.  |Se nota mucho comparando ambos códigos, ya que los datos se manejan de maneras diferentes, como en ASCII hay varios fitros para asegurar que hayan 4 datos, y en Binario hay más seguridad de que siempre van a ser paquetes de bytes.|

### <p align=center>¿Por qué fue necesario introducir framing en el protocolo binario?</p>
Fue necesario porque es como decir "Este paquetico empieza aquí y termina acá", pero pues uno diria que entonces cual es la gracia si se supone que ya teniamos la certeza que eran 8 bytes siempre. Esto es para evitar errores, el framing permite al receptor saber donde empieza (header) y termina un paquete, de esa manera puede leer en orden correcto los datos y no empezar por la mitad o contar solo 6 byte o 12 bytes. Además como se van a enviar tantos paquetes de datos seguidos es lo mejor para separarlos.

### <p align=center>¿Cómo funciona el framing?</p>
1. **0xaa:** es el header, entonces el receptor sabe que a partir de aqui cuenta el paquete, asi no se confunde con lo otro.
2. **serialBuffer.length >= 8** ahí le estamos diciendo exactamente al receptor que los paquetes van a ser de 8 bytes (en realidad son 6 bytes).
3. 
