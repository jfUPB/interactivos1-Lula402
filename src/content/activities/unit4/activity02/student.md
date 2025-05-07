<p align= center>  Explicación del sketch </p>

#### Sketch: http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_1_2_04

#### #1
```js
var tileCount = 20;
var actRandomSeed = 0;
var rectSize = 30;
```
Es esta parte se están creando las variables globales. Tile Count se inicializa en 20, ya que van a ser la cantidad de cuadritos que va a tener una fila o columna. 

Act Random Seed, será para poder seudo-randomizar el patron de los cuadritos, se inicializa en 0 y siempre que esa random seed sea 0, el comportamiento va a ser el mismo hasta que se cambie.

RectSize, es el lado inicial de la recta, se inicializa en 30. Esto es porque cuando uno tiene dos vertices se forma una recta y hay que determinar que tamaño tiene.

#### #2
```js
function setup() {
  createCanvas(600, 600);
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();
  fill(192, 100, 64, 60);
}
```
Esta es la función set up, acá se preparan las cosas basicas que se van a usar en el programa. Se crea un canvas de 600x600, recordemos que son 20 Tiles con un tamaño de recta de 30, entonces ***20 x 30= 600***.

Color mode está usando HSB (hue, saturation, brightness), este determina el color de fondo del canvas.

No stroke es para decir que los cuadritos no van a estar delineados.

fill será para el color de relleno de los cuadritos, está usando también HSB y el último dato que es 60, es para determinar la transparencia, por eso es que al moverlos se alcanzan a sobreponer.

#### #3
```js
function draw() {
  clear();

  randomSeed(actRandomSeed);

  for (var gridY = 0; gridY < tileCount; gridY++) {
    for (var gridX = 0; gridX < tileCount; gridX++) {

      var posX = width / tileCount * gridX;
      var posY = height / tileCount * gridY;

      var shiftX1 = mouseX / 20 * random(-1, 1);
      var shiftY1 = mouseY / 20 * random(-1, 1);
      var shiftX2 = mouseX / 20 * random(-1, 1);
      var shiftY2 = mouseY / 20 * random(-1, 1);
      var shiftX3 = mouseX / 20 * random(-1, 1);
      var shiftY3 = mouseY / 20 * random(-1, 1);
      var shiftX4 = mouseX / 20 * random(-1, 1);
      var shiftY4 = mouseY / 20 * random(-1, 1);

      push();
      translate(posX, posY);
      beginShape();
      vertex(shiftX1, shiftY1);
      vertex(rectSize + shiftX2, shiftY2);
      vertex(rectSize + shiftX3, rectSize + shiftY3);
      vertex(shiftX4, rectSize + shiftY4);
      endShape();
      pop();
    }
  }
}
```
La función Draw es como un while infinito, entonces en esta es que va a pasar la verdadera magia del este sketch.
Al inicio se hace un clear de todo el canvas, para poder evitar que los cuadritos nuevos al moverse se sobrepongan con los del frame anterior.

Luego, tenemos una Random seed que es ya preestablecida por js y le entregamos ActRandomSeed que es para poder que seudo-randomize el patrón de los cuadritos. Luego explicaré como.

Tenemos un ciclo for dentro de otro ciclo for, ambos son para poder recorrer el canvas y pintar. El ciclo externo es para recorrer el eje y, es decir las filas, y el ciclo interno es para recorrer el eje x, es decir las columnas.
En cada iteración gridy aumenta 1, de ahí entra al ciclo de x que aumenta gridx de 1 en 1 hasta tilecount que es 20. Luego vuelve a correr el ciclo del eje Y, es decir se pasa a la siguiente fila, para así pintar todas las columnas de esa fila. De esta manera se va pintando todo el canvas.

Dentro de esos ciclos se crean las variables llamadas "SHIFT", estas son para que según la posición del mouse en (x,y) se randomize un valor entre -1 y 1 y de ahí shift obtenga su valor.
Para que se usan entonces esos SHIFTS? se usan para poder reescribir el valor de los vertex (vertices), cada cuadrito tiene 4 verices y cada vertice tiene coordenadas (x,y), por eso es que cada vertice se randomiza de manera independiente.

```translate(posX, posY);``` Es para hacer una traslación del origen de nuestro plano, es decir la coordenada (0,0) es donde arrancamos a pintar, entonces eso es como el cursor del pincel y si la trasladamos en cada itración de la función draw esto nos va a permitir ir moviendo el pincel por el canvas.

#### #4
```js
function mousePressed() {
  actRandomSeed = random(100000);
}
```
Esta es una función para que al detectar que se presionó el mouse, entonces la semilla se randomize con valores hasta 100k. Recordemos que arriba explique que si la semilla se mantenía en 0, los patrones aunque cambien iban a ser siempre los mismos, de esta manera al dar click entonces seudo-randomizamos esa función de randomSeed.

#### #5
```js
function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}
```
Esta función es para que si la tecla presionada es ***S*** entonces se guarda el canvas como esté en ese exacto momento como un .png. Esta es una manera de crear diferentes instancias de ese mismo arte generativo.
