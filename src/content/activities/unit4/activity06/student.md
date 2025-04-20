### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Son como las reglas que se van a manejar a la hora de comunicar por serial, es como decir "oye nos vamos a comunicar en este orden y con estas cosas". Es importante este protocolo porque como la comunicación serial se da por Bits, sin el protocolo sería una chorrera de cosas sin un orden y sin sentido, entonce el receptor no va a entender nada de lo que uno quiere que entienda.

### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Se separan con comas para poder que el receptor entienda donde termina un dato del paquete y donde inicia el otro dato, me explico:

No es lo mismo mandar: ***"TRUEFLASE"***

A mandar: ***"TRUE" , "FALSE"***

### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Es necesario para poder que el receptor sepa donde termina en paquetico de datos, en nuestro caso eran paqueticos de a 4 datos, entonce /n simbolizaba que ahi ya estaban los valores de esos 4 datos,

### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
Porque todo se basaba en la comunicación serial del Micro:bt con P5.js entonces, usar una máquina de estados fue necesario para que el programa no intente dibujar ni hacer cosas raras antes de que el micro:bit esté conectado.

### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
Se organizan los datos dentro de un formato como este que fue el que usamos: ***format(xValue, yValue, aState,bState)***
Entones cada que haya un input en el Micro, se guarda corresponientemente en cada una de esas varibales y se va llenando el formato.

Cada dato va dentro de estas llaves: ***"{},{},{},{}\n"***

### ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
ASCII son unos códigos que representan caracteres normales como letras y números usando valores numéricos.
En comunicación serial, significa que el micro:bit está enviando los datos como texto, carácter por carácter, usando esos códigos.
Es el lenguaje común entre máquinas y humanos, la maquina ya entiende esos numeros y los maneja como strings, y a nosotros nos queda saber como traducir con la tablita.

### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
Porque si no hay Bytes disponubles en el puerto serial p5.js va a estar leyendo nada, uno diria que no hay problema pero eso en programación se traduce como null o undefined. 

Es como si p5 le abriera la puerta para dejar entrar lo que mandaron por el puerto pero no le llegaron paquetes sino que le lleno un ventarrón que lo dañó.
A comparación de que si p5.js pregunta antes de abrir la puerta se asegura que si va a recibir paquetes.

### ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
Usamos ***trim()*** para eliminar ese /n al final del paquete de datos, de esa manera ya solo quedaron los 4 datos.

### Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?
Usaría ***split(",")***.

### Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
Porque como el Microbit se comunicó con ASCII y eso p5.js lo interpreta como una cadena, los debe convertir a los numero que le corresponden a (x,y), porque sino estaría trabajando con un char y pues eso no funcionaria porque estamos hablando de posiciones que están dadas por numeros.

### Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?

123= 31 32 33

756= 37 35 36

False= 46 61 6C 73 65

True= 54 72 75 65

**Puerto seríal:**
{31 32 33}, {37 35 36}, {46 61 6C 73 65}, {54 72 75 65} /n

### ¿Qué aprendiste nuevo del micro:bit que no sabías antes?
Que hay que ser muy especificos en como comunico el Micro con otros sistemas.
Aprendí que el Microbit usa por defecto la velociadad de ***uart.init(115200)***, apredí que eso está en Baudios y que es la velocidad a la que viajan los bits. 


### ¿Qué aprendiste nuevo de p5.js que no sabías antes?
Lo de las imagenes, no sabía que uno podía preload-sear cosas antes de arrancar el draw, de modo que ya el sketch esté como alimentado para hacer lo que tenga que hacer.

```js
function preload() {
  lineModule[1] = loadImage("data/02.svg");
  lineModule[2] = loadImage("data/03.svg");
  lineModule[3] = loadImage("data/04.svg");
  lineModule[4] = loadImage("data/05.svg");
}
```
