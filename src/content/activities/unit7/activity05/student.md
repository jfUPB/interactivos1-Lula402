### Código server
```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    console.log('New client connected');
    socket.on('message', (message) => {
        console.log(`Received message => ${message}`);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

### Código cliente celular
```js
let socket;
let lastTouchX = null; 
let lastTouchY = null; 
const threshold = 5;

function setup() {
    createCanvas(300, 400);
    background(220);

    // Conectar al servidor de Socket.IO
    //let socketUrl = 'http://localhost:3000';
    socket = io();

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
    });

    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });
}

function draw() {
    background(220);
    fill(255, 128, 0);
    textAlign(CENTER, CENTER);
    textSize(24);
    text('Touch to move the circle', width / 2, height / 2);
}

function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY,
                colorcito: { r: random(0, 255), g: random(0, 255), b: random(0, 255) },  
                useStroke: random(true, false) 
            };
            socket.emit('message', JSON.stringify(touchData));

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}

```

### Código cliente escritorio
```js
let socket;
let particles = [];
const port = 3000;

class Particle {
  constructor(x, y, colorcito, useStroke) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.lifespan = 255;
    this.size = random(5, 20);
    this.noiseOffset = random(1000);
    this.colorcito = colorcito;
    this.useStroke = useStroke;
  }
    update() {
    // Se utiliza ruido Perlin para definir la dirección de la fuerza
    let angle =
      noise(this.pos.x * 0.005, this.pos.y * 0.005, this.noiseOffset) *
      TWO_PI *
      2;
    let force = p5.Vector.fromAngle(angle);
    force.mult(0.5);
    // Se aplica la fuerza a la velocidad
    this.vel.add(force);
    this.vel.limit(4);
    this.pos.add(this.vel);
    // La vida de la partícula disminuye gradualmente
    this.lifespan -= 3;
  }

  display() {
    if (this.useStroke) {
         stroke(255);
    } else {
        noStroke();
     }
    fill(red(this.colorcito), green(this.colorcito), blue(this.colorcito), this.lifespan);
    ellipse(this.pos.x, this.pos.y, this.size);

  }

  isDead() {
    return this.lifespan < 0;
  }
}

function setup() {
    createCanvas(300, 400);
    background(220);

    //let socketUrl = 'http://localhost:3000';
    socket = io(); 

    // Evento de conexión exitosa
    socket.on('connect', () => {
        console.log('Connected to server');
    });

    // Recibir mensaje del servidor
    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
        try {
            let parsedData = JSON.parse(data);
            if (parsedData && parsedData.type === 'touch') {
                circleX = parsedData.x;
                circleY = parsedData.y;
                let colorcito = color(parsedData.colorcito.r, parsedData.colorcito.g, parsedData.colorcito.b);
                let useStroke = parsedData.useStroke;
                particles.push(new Particle(parsedData.x, parsedData.y, colorcito, useStroke));
            }
        } catch (e) {
            console.error("Error parsing received JSON:", e);
        }
    });    

    // Evento de desconexión
    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });
}

function draw() {
    background(220);
      for (let i = particles.length - 1; i >= 0; i--) {
        particles[i].update();
        particles[i].display();
    if (particles[i].isDead()) {
        particles.splice(i, 1);
    }
  }
}

```
-----------------------------------------------------------------------------------------------------------------------------

1. Los cambios clave que hice en mobile/sketch.js, son que ahora envio más datos, envio: x,y,colorcito,useStroke. Colorcito lo randomicé y useStroke tambien randomicé si iba a ser true o false. Estos datos los sigo enviando de la misma manera que en el caso de estudio y los sigo enviando en el mismo momento que es el caso de estudi, que vendria siendo dentro de la función touchMoved cuando se detecta que moví el dedo.
   
```js
    if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY,
                colorcito: { r: random(0, 255), g: random(0, 255), b: random(0, 255) },  
                useStroke: random(true, false) 
            };
            socket.emit('message', JSON.stringify(touchData));
```

2.  Los cambios clave que hice en desktop/sketch.js, son que ahora al recibir e interpretar los datos incluyo colorcito y useStroke dentro del bloque try-catch, entonces al momento de hacer el push de la nueva particula incluye colorcito y useStroke:

```js
  socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
        try {
            let parsedData = JSON.parse(data);
            if (parsedData && parsedData.type === 'touch') {
                circleX = parsedData.x;
                circleY = parsedData.y;
                let colorcito = color(parsedData.colorcito.r, parsedData.colorcito.g, parsedData.colorcito.b);
                let useStroke = parsedData.useStroke;
                particles.push(new Particle(parsedData.x, parsedData.y, colorcito, useStroke));
            }
        } catch (e) {
            console.error("Error parsing received JSON:", e);
        }
    });    

```

En el setup() quite lo del circulo de caso de estudio y puse el array de particles ```let particles = [];```, para ahí ir metiendo las particulas.

En el draw(), cambió full, quité lo de la elipse y lo del fill. Ahora hay un ciclo for para poder recorrer el array de las particles y pintar una por una. Para pintarlas se necesita revisar varias cosas:
- el update para actualizar el lifespan
- El display() porque ahi se determina el color y si lleva o no stroke
- El isDead() para saber si la particula ya se le acacó su lifespan
- Si isDead() devuelve un true, osea que ya debe morir, se hace un splice como el que hacíamos en una unidad pasada. Entonces hace un splice de i, que es la posición del array en la que estpa la particula que debe morir, y hace el corte de solo 1 particula a partir de i.

```js
function draw() {
    background(220);
      for (let i = particles.length - 1; i >= 0; i--) {
        particles[i].update();
        particles[i].display();
    if (particles[i].isDead()) {
        particles.splice(i, 1);
    }
  }
}
```

3. No tuve que modificar el server, porque ya me servía la comunicación y los cambios solo eran en mobile y en desktop.
-----------------------------------------------------------------------------------------------------------------------------
### Video

https://youtu.be/QndRORwEJts
