<p align=center> Aplicación original sin modificar </p>
Embed: <iframe src="https://editor.p5js.org/Lula402/full/gHpdPJr8m"></iframe>

Fullscreen: https://editor.p5js.org/Lula402/full/gHpdPJr8m

<p align=center> Código de p5.js para la versión modificada </p>

```js

let renderer;
const CYCLE = 180;
let sh;

let port;
let connectBtn;
let microBitConnected = false;

let currentCol = "#FFFFFF";
let currentShadowCol = "#111111";

let smoothRotX = 0;
let smoothRotY = 0;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

var vert = `

		precision highp float;

    // attributes, in
    attribute vec3 aPosition;
    attribute vec3 aNormal;
    attribute vec2 aTexCoord;

    // attributes, out
    varying vec3 var_vertPos;
    varying vec3 var_vertNormal;
    varying vec2 var_vertTexCoord;
		varying vec4 var_centerGlPosition;//原点
    
    // matrices
    uniform mat4 uModelViewMatrix;
    uniform mat4 uProjectionMatrix;
    uniform mat3 uNormalMatrix;

    void main() {
      vec3 pos = aPosition;  
      gl_Position = uProjectionMatrix * uModelViewMatrix * vec4(pos, 1.0);

      // set out value
      var_vertPos      = pos;
      var_vertNormal   =  aNormal;
      var_vertTexCoord = aTexCoord;
			var_centerGlPosition = uProjectionMatrix * uModelViewMatrix * vec4(0., 0., 0.,1.0);
    }
`;

var frag = `

precision highp float;

uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;
uniform vec3 u_lightDir;
uniform vec3 u_col;
uniform vec3 u_Scol;
uniform mat3 uNormalMatrix;

//attributes, in
varying vec4 var_centerGlPosition;
varying vec3 var_vertNormal;




float random (in vec2 st) {
   	highp float a = 12.9898;
    highp float b = 78.233;
    highp float c = 43758.5453;
    highp float dt= dot(st.xy ,vec2(a,b));
    highp float sn= mod(dt,3.14);
    return fract(sin(sn) * c);
}

float noise(vec2 st) {
    vec2 i = vec2(0.);
		i = floor(st);
    vec2 f = vec2(0.);
		f = fract(st);
    vec2 u =  vec2(0.);
		u = f*f*(3.0-2.0*f);
    return mix( mix( random( i + vec2(0.0,0.0) ),
                     random( i + vec2(1.0,0.0) ), u.x),
                mix( random( i + vec2(0.0,1.0) ),
                     random( i + vec2(1.0,1.0) ), u.x), u.y);
}

float grid(vec2 uv){
	uv *= 10.;
  uv = fract(uv);
  float v = uv.x >= 0. && uv.x < 0.1 || uv.y >= 0. && uv.y < 0.1 ? 1. : 0.;
  return v;
}

float gridGra(in vec2 uv , float gridNum){
    float scale = gridNum;
    uv *= scale;
    uv = fract(uv);
    float o = abs(uv.y + -0.5)*2.;
		o *= abs(uv.x + -0.5)*2.;
    return o;
}

void main() {
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
		st.x *= u_resolution.x/u_resolution.y;

		vec2 centerPos = var_centerGlPosition.xy/var_centerGlPosition.w;//スクリーン変換
		centerPos = (centerPos + 1.0)*.5*2.;//gl_FragCoordと座標を合わせる pixelDensityによって係数が変化する
		centerPos.x *= u_resolution.x/u_resolution.y;//gl_FragCoordと座標を合わせる
		vec3 vertNormal = normalize(uNormalMatrix * var_vertNormal);
    float dot = dot(vertNormal,normalize(u_lightDir));
    dot = (dot *.5) + .5;


    float noise1 = noise((st-centerPos)*700.);
		float noise2 = noise((st-centerPos)*1000.);
		float tone = step(noise1,dot);
		vec3 col = u_col * tone + (u_Scol) * (1.-tone);
		col += noise2*.15;
    vec3 color = vec3(0.);
    color = vec3(st.x,st.y,abs(sin(u_time)));

	gl_FragColor = vec4(col,1.0);
}

`;

function setup() {
  renderer = createCanvas(windowWidth, windowHeight, WEBGL);
  //shader
  
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
  
  function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}
  
  sh = createShader(vert, frag);
  this.shader(sh);
  sh.setUniform("u_resolution", [width, height]);
  sh.setUniform("u_lightDir", [-1, -0.1, 0]);
  noStroke();
  pixelDensity(2);
  
  
}

function updateButtonStates(newAState, newBState) {
  // Generar eventos de keypressed
  if (newAState === true && prevmicroBitAState === false) {
    // create a new color
    currentCol = "#FF69B4";
    currentShadowCol = "#111111";
    print("A pressed");
  }
  // Generar eventos de key released
  if (newBState === false && prevmicroBitBState === true) {
    currentCol = "#30D4D4";
    currentShadowCol = "#333333";
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function draw() {
    //******************************************
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");
    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
  }
  //*******************************************
  
    switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      // No puede comenzar a dibujar hasta que no se conecte el microbit
      // evento 1:
      if (microBitConnected === true) {
        // Preparo todo para el estado en el próximo frame
        print("Microbit ready to draw");
        strokeWeight(0.75);
        c = color(181, 157, 0);
        noCursor();
        appState = STATES.RUNNING;
      }

      break;

    case STATES.RUNNING:
      // EVENTO: estado de conexión del microbit
      if (microBitConnected === false) {
        print("Waiting microbit connection");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
      }
  
  background(240);
  setCol(sh, currentCol, currentShadowCol);
  let targetRotX = map(microBitY, 0, height, -PI, PI, true);
  let targetRotY = map(microBitX, 0, width, -PI, PI, true);
        
  smoothRotX = lerp(smoothRotX, targetRotX, 0.1);
  smoothRotY = lerp(smoothRotY, targetRotY, 0.1);
        
  print(targetRotX, targetRotY);
  rotateX(smoothRotX);
  rotateY(smoothRotY);
  rotateZ((frameCount / CYCLE / 3) * TWO_PI);
        
  noisedSphere(min(width, height) * 0.25, 50, 50);
}

function noisedSphere(_sphereRadius, dx, dy) {
  let geometry = new p5.Geometry(dx, dy);
  let noiseAmount = map(sin(frameCount / 30), -0.99, -0.2, 0, -0.5, true);

  for (let yi = 0; yi <= dy; yi++) {
    let yRadian = map(yi, 0, dy, PI / 2, -PI / 2);
    let y = sin(yRadian) * _sphereRadius;
    let radius = cos(yRadian) * _sphereRadius;
    for (let xi = 0; xi <= dx; xi++) {
      let r = (xi * TWO_PI) / dx;
      let x = cos(r) * radius;
      let z = sin(r) * radius;
      if (yi == 0 || yi == dy) {
        x = 0;
        z = 0;
      }
      let nv = noise(x / radius, y + frameCount / 30, z / radius);
      nv = map(nv, 0, 1, 1, 1 + noiseAmount);
      geometry.vertices[xi + (dx + 1) * yi] = createVector(
        x * nv,
        y * nv,
        z * nv
      );
    }
  }

  //face
  geometry.computeFaces();
  for (let i = geometry.faces.length - 1; i >= 0; i--) {
    if (
      (i < dx * 2 && i % 2 == 0) ||
      (i > geometry.faces.length - dx * 2 && i % 2 == 1)
    )
      geometry.faces[i] = [];
  }
  for (let i = geometry.faces.length - 1; i >= 0; i--) {
    if (geometry.faces[i].length == 0) geometry.faces.splice(i, 1);
  }

  //normal
  geometry.computeNormals();
  geometry.averageNormals();

  //draw
  drawGeometry(geometry);
}

function drawGeometry(_geo, _id = "gId", _renderer = renderer) {
  _renderer.createBuffers(_id, _geo);
  _renderer.drawBuffers(_id);
}

}

function setCol(shader, colStr, shadowColStr) {
  let col = color(colStr);
  let colArray = col._array;
  colArray.pop();
  shader.setUniform("u_col", colArray);

  let shadowCol = color(shadowColStr);
  let shadowColArray = shadowCol._array;
  shadowColArray.pop();
  shader.setUniform("u_Scol", shadowColArray);
}
```

#### Comentario
Tuve un error porque el movimiento se veía muy laggeado o brusco, entonce no parecia como coordinado con lo que uno movía en el Micro:bit. Entonces ahí aprendí sobre ***lerp()*** que es pare interpolar. Basicamente se suavizó el momviemiento, porque ahora la esfera no se mueve inmediatamente según la posición del Micro, sino que la va siguiendo lentamente como acercandose y eso lo smoothsea.

<p align=center> Aplicación modificada en p5.js. </p>

Embed: <iframe src="https://editor.p5js.org/Lula402/full/8xLQGcfoO"></iframe>

Fullscreen: https://editor.p5js.org/Lula402/full/8xLQGcfoO

<p align=center> Capturas de pantalla de mi aplicación modificada </p>

Se ve mucho mejor en un video:

https://youtu.be/f-dt0fIf_jI

