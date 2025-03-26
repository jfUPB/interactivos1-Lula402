### <p align=center> Generative by SayamaArts </p>
#### Link: ***https://openprocessing.org/sketch/872176***
#### Qué me llamó la atención? 
Me llamó la atención que es un arte con unas transiciones demasiado limpias, es decir, cuando la bolita cambia de forma se ve super fluido como si de verdad estuviera re-moldeandose.
#### ¿Qué funciones de p5.js se están utilizando? 
1. function setup() {}
2. function draw() {}
3. function noisedSphere(_sphereRadius,dx,dy) {}
4. function drawGeometry(_geo,_id = 'gId',_renderer = renderer) {}
5. function setCol(shader,colStr,shadowColStr) {}
   
#### ¿Qué técnicas de programación se están aplicando? 
Programación estructurada en p5.js, es decir, Java script

#### Modificación
**Descripción:** Este proyecto de arte generativo tiene dos colores bases y de esos se basa el shader para hacer que se vea granuladito. Antes era blanco y negro para poder crear las sombras y luces, pero luego lo cambié a un verde menta claro y uno oscuro.

| Antes | Después |
|------------|-----------|
| <img width="140" alt="image" src="https://github.com/user-attachments/assets/e268daa3-2bb6-4818-8261-989411268e27" /> |<img width="140" alt="image" src="https://github.com/user-attachments/assets/9fd77874-3a50-4e22-9b2d-72a80e023a10" />|
| <img width="140" alt="image" src="https://github.com/user-attachments/assets/13ad610e-a893-4f14-856a-d75aa516011f" /> |<img width="140" alt="image" src="https://github.com/user-attachments/assets/53c10b1b-849a-4812-89e1-542f14e4d189" /> |

### <p align=center> Generative design </p>
#### Link: ***http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_3_3_01***
#### Qué me llamó la atención? 
Me llamó la atención que la preview del proyecto estaba en Alemán, pero ni siquiera habia captado como era la idea. Luego cuando entré me di cuenta de lo cool que era, porque es como si con el cursor al dar click tienes un pincél que pinta palabras. Ahora, lo más interesante es que entre más lento muevas el cursor mientras presionas, más pequeñas son las letras, y si mueves más rápido el cursor mientras lo presionas más grande es la fuente de la letra. 
#### ¿Qué funciones de p5.js se están utilizando? 
1. function setup() {}
2. function draw() {}
3. function mousePressed() {}
4. function keyReleased() {}
5. function keyPressed() {}
   
#### ¿Qué técnicas de programación se están aplicando? 
Programación estructurada en p5.js, es decir, Java script

#### Modificación
**Descripción:**
Antes el color de la letra decía "fill(0);", lo cual es no fill. Lo cambié para que en cada iteración del Draw se randomice el fill de la letra, RGB está ranomizado de 0 a 255 cada uno de la siguiente manera: 
``` js
let c = color(random(0, 255), random(0, 255), random(0, 255));
fill(c);
```

| Antes | Después |
|------------|-----------|
| <img width="500" alt="image" src="https://github.com/user-attachments/assets/effa5efc-bc67-4785-bd0b-84a12a0db664" /> |<img width="500" alt="image" src="https://github.com/user-attachments/assets/f777989a-e655-4563-8345-618086a1a3e9" />|

