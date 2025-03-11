```js
let connectBtn;
let btnAClicked = false;
let btnBClicked = false;
let btnSClicked = false;
let btnTClicked = false;
let isEvent = false;
let eventData = ''
let state_confi = 0    //esatdo de configuración
let state_armada = 1   //estado cuando esta armed
let state_explotada = 2 //estado cuando explota
let state_desarmada  //estado cuando explota
let current_state = state_confi //El estado inicial será en de configuración
let secuencia_correcta = ['A', 'B', 'A', 'S']
let secuencia_user = []  //para almecener la secuencia del user
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
  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(135, 100);
  connectBtn.mousePressed(connectBtnClick);
  
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
function tareaBomba(){
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
     if (isEvent == true){
          isEvent = false;
          if (eventData == 'A')   //Se disminuye el temporizador
              if (tiempo > 10){
                  tiempo -= 1}
            //Se muestra el tiempo

          if (eventData == 'B')       //Se aumenta el temporizador         
              if (tiempo < 60){
                  tiempo += 1}
          //Se muestra el tiempo

          if (eventData == 'S')      //Evento de shake para armarla
              current_state = state_armada
              start_time = millis()     //Se guarda el tiempo actual en start_time
              secuencia_user= []
       }
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
    
           if (isEvent == true){
                isEvent = false;
                if (eventData == 'A'){
                    secuencia_user.push('A');}
                if (eventData == 'B'){              
                    secuencia_user.push('B');}
                if (eventData == 'S'){
                    secuencia_user.push('S');}
                    if  (secuencia_user==secuencia_correcta){        
                        tiempo = 20
                        displayRestart();
                        current_state = state_confi} //Vuelve a confi
                    else {
                        displayError();
                        secuencia_user= []}
                }
            }
  
  
  else if (current_state == state_explotada){
            if (isEvent == true){
                isEvent = false;
                if (eventData == 'T'){ // Evento de touch el logo para reiniciar
                    tiempo = 20
                    displayRestart();
                    current_state = state_confi  //Vuelve a confi
                    }
            } 
     }
}

function tareaEventos(){
    if (sendBtnA.mousePressed(sendBtnAClick))   
        isEvent = True
        eventData = 'A'

    if (sendBtnB.mousePressed(sendBtnBClick))   
        isEvent = True
        eventData = 'B'            

    if (sendBtnS.mousePressed(sendBtnSClick))  
        isEvent = True
        eventData = 'S'

    if (sendBtnS.mousePressed(sendBtnSClick))
        isEvent = True
        eventData = 'T'
        
    if (port.write('A'))
        isEvent = True
        eventData = 'A'
  
    if (port.write('B'))
        isEvent = True
        eventData = 'B'
  
    if (port.write('S'))
        isEvent = True
        eventData = 'S'
  
    if (port.write('T'))
        isEvent = True
        eventData = 'T'
}

function draw() {
  
  tareaBomba();
  tareaEventos();

    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
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
  mensajeColor = "#9E9E9E"; // gris
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

}
```
