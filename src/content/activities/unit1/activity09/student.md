### Patrón visual de bolitas
**Descripcción:** El patrón visual está creado a base de puntos en el canvas, estos puntos son coordenados en (x,y). A cada punto creado en la función draw le asigné un color diferente. Usé la función de random en el strokeWeight (el grosor del trazo) limitandolo hasta un grosor de 50px y random en la coordenadas (x,y), donde la posición de ambos ejes podía variar hasta los 400.

```javascript
x=0
y=0
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background('black');
  point(x, y)
  
  stroke('#F44336');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#E91E63');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#9C27B0');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#673AB7');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#3F51B5');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#2196F3');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#03A9F4');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
 
  stroke('#00BCD4');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#009688');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#4CAF50');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));

  stroke('#8BC34A');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));

  stroke('#CDDC39');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#FFEB3B');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#FFC107');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#FF9800');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#FF5722');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#795548');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#9E9E9E');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
  
  stroke('#607D8B');
  strokeWeight(random(50));
  point(x=random(400),y=random(400));
}
```

<iframe width="560" height="315" src="https://youtube.com/embed/USWfGQVt5Pk" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
