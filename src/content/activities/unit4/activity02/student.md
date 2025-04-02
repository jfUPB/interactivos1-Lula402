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
Esta es la función set up, acá se preparan las cosas basicas que se van a usar en el programa. Se crea un canvas de 600x600, recordemos que son 20 Tiles con un tamaño de recta de 30, entonces 20 x 30= 600.
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

#### #4
```js
function mousePressed() {
  actRandomSeed = random(100000);
}
```


#### #5
```js
function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}
```
