```js
let btnAClicked = false;
let btnBClicked = false;
let btnSClicked = false;
let btnTClicked = false;
let connectBtn;
let state_confi    //esatdo de configuración
let state_armada   //estado cuando esta armed
let state_desarmada  //estado cuando explota
let state_explotada //estado cuando explota
let current_state = state_confi  //El estado inicial será en de configuración
let secuencia_correcta = ['A', 'B', 'A', 'SHAKE']
let secuencia_user = []  // para almecener la secuencia del user
let tiempo = 20        //Valor inicial de 20 segundos
let intervalo = 1000   //intervalo de 1 segundo = 1000 ms
let start_time = 0     //contador de tiempo que inicia en 0
let BOOM = "BOOM";
let RESTART = "RESTART";
let ERROR = "ERROR";
let mensaje = ""; 
let mensajeColor = "#FFFFFF";



function setup() {
  createCanvas(400, 400);
  background('#FFECB4');
  connectBtn = createButton('');
  
  let sendBtnA = createButton('A');
  sendBtnA.position(115, 300);
  sendBtnA.mousePressed(sendBtnAClick);

  let sendBtnB = createButton('B');
  sendBtnB.position(165, 300);
  sendBtnB.mousePressed(sendBtnBClick);

  let sendBtnS = createButton('S');
  sendBtnS.position(215, 300);
  sendBtnS.mousePressed(sendBtnSClick);

  let sendBtnT = createButton('T');
  sendBtnT.position(265, 300);
  sendBtnT.mousePressed(sendBtnTClick);
  
  fill('#000000')
  square(130, 140, 140, 20);
  
  textSize(80)
  fill('#FF4B3E');
  text('BOOMBA', 25, 100); // Dibujar el número actualizado
  
   
}

function draw() {
  fill('#000000');
  square(130, 140, 140, 20); // Redibujar la pantalla
  
  textSize(50);
  fill('#FFFFFF');
  text(tiempo, 170, 230); // Dibujar el número actualizado
  

  if (mensaje !== "") {
      textSize(40);
      fill(mensajeColor); 
      let x;
      text(mensaje, x, 100);
  }
  
 if (current_state == state_confi){
        if (btnAClicked == true)   //Se disminuye el temporizador
            if (tiempo > 10){
                tiempo -= 1}
          //Se muestra el tiempo
            btnAClicked = false;

        if (btnBClicked == true)       //Se aumenta el temporizador         
            if (tiempo < 60){
                tiempo += 1}
        //Se muestra el tiempo
            btnBClicked = false;

        if (btnSClicked == true)      //Evento de shake para armarla
            current_state = state_armada
            start_time = millis()     //Se guarda el tiempo actual en start_time
            secuencia_user= []
            btnSClicked = false;
     }   
   
 else if (current_state == state_armada){
         limpiarMensaje() 
         while (tiempo>=0)
           if ((millis-start_time) > intervalo){ //"Si ha pasado más de un segundo desde la última vez que revisé el tiempo..."
              start_time = millis()  // Reiniciar el temporizador
              tiempo -= 1}
              //Se muestra el tiempo

              if (tiempo == 0){              //Evento de que el tiempo se acabó
                  displayBoom();    //mostrar BOOM
                  current_state = state_explotada}
    
        if (btnAClicked == true){
            secuencia_user.push('A'); 
            btnAClicked = false;}
        if (btnBClicked == true){              
            secuencia_user.push('B');
            btnBClicked = false;}
        if (btnSClicked == true){
            secuencia_user.push('S'); 
            btnSClicked = false;}
            if  (secuencia_user==secuencia_correcta){        
                tiempo = 20
                displayRestart();
                current_state = state_confi} //Vuelve a confi
            else {
                displayError();
                secuencia_user= []}
 }
  
 else if (current_state == state_explotada){
        if (btnTClicked == true){ // Evento de touch el logo para reiniciar
            tiempo = 20
            displayRestart();
            current_state = state_confi  //Vuelve a confi
            }
         }   
}

function displayRestart() {
  mensaje = "RESTART";
  mensajeColor = "#A5E65A"; // Verde
  x = 130;
}

function displayBoom() {
  mensaje = "BOOM";
  mensajeColor = "#FF4B3E"; // Rojo
  x = 140;
}

function displayError() {
  mensaje = "ERROR";
  mensajeColor = "#9E9E9E"; // Gris
  x = 140;
}

// Función para borrar el mensaje
function limpiarMensaje() {
  mensaje = ""; 
}


function sendBtnAClick() {
    btnAClicked = true
}

function sendBtnBClick() {
    btnBClicked = true
}

function sendBtnSClick() {
    btnSClicked = true
}

function sendBtnTClick() {
    btnTClicked = true
}
```
