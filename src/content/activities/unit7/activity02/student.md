#### <p align=center> Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente? </p>

Dev Tunnels es necesario porque necesitamos aceder el server local desde un dispositivo experno. El server está corriendo localmente en el pc y como queremos accederlo y comunicarnos con el desde el celu, necesitamos Dev Tunnels para establecer esa comunicación. Sin Dev Tunnels la otra opación sería usar la IP del compu, pero tanto el celu como el pc tendrian que estar en la misma wifi y además probablemente hayan firewalls que no van a dejar que uno acceda a la IP asi como asi.

Los dev tunnels funcionan así: hacen de mediador en la comunicación de un dispositivo externo al server local, reciben los request del celu, los mandan al server, luego el server responde y el dev tunnel le entrega eso al celu, todo eso haciendolo seguro porque igual sigue siendo un dispositivo externo intentandose comunicar con mi dispositivo local (pc).

![Imagen de WhatsApp 2025-05-16 a las 12 15 20_0823d10a](https://github.com/user-attachments/assets/974062ac-7e1b-4d48-9f32-de25f9b1e25d)

#### <p align=center> ¿Por qué usamos JSON.stringify() en el emisor (móvil) y JSON.parse() en el receptor (escritorio)? ¿Qué problema resuelve JSON aquí?  </p>

Solucionan el problema de que en comunicación casi siempre se manda un string, porque no es como que yo pueda mandar una variable por ahí solita sin contexto, entonces toca convertir la info a un strign y luego desconvertirla otra vez a datos normales.
***JSON.stringify()*** manda los datos como una cadena de strings y luego el server al recibirlo, hace ***JSON.parse()*** para volverlos a tratar como los datos originales que eran.


#### <p align=center> Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil. </p>
La función ***touchMoved()*** se encarga que en la página de p5.js (osea la del celu) se esté pendiente y se almacene la posición en (x,y) del donde el dedo está haciendo click. Entonces cuando el dedo hace click en una esquina, se guarda esa posición (x.y) del canvas y cuando lo mueve hasta la otra esquina guarda todo ese recorrido de cordenadas (x,y).

El threshold se usa porque un dedo puede moverse por accidente un tris o puede temblar, entonces funciona como un umbral. Si el movimiento fue mini el treshold dice "eso fue un bobada de cambio, nos quedamos donde estamos", entonces no se manda ningún cambio al server, mientras que si el movimiento fue significativo y supera el treshold entonces dice "nos movimos suficiente, actualicemos (x,y)".

#### <p align=center>  ¿Qué otros eventos táctiles existen en p5.js y para qué tipo de interacciones podrían ser útiles (ej. un botón virtual, detectar un tap)? </p>
La verdad es que a la mayoría de eventos tactiles se les puede sacar buen provecho, solo toca ser creativo. Por ejemplo detectar un tap puede hacer que el circulo cambie de color, un boton virtual puede hacer que al presionarlo haga que el circulo vuelva a la mitad. touchStarted() y touchEnded() podrían servir para esperar eventos.

#### <p align=center>  Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno? </p>

#### Dev Tunnels
***Ventajas:***
1. Funciona desde cualquier wifi/datos.
2. Te da una URL pública, entonces puedo acceder desde cualquier navegador actual.
3. Lo puedo probar en múltiples dispositivos o mostrarle a alguien más sin que esté en el mismo wifi.

***Desventajas:***
- Latencia.
- cambiar la URL cada vez que hago foward del port.

#### IP 
***Ventajas:***
1. Es directo.
2. No necesito dev tunnels.

***Desventajas:***
1. Solo sirve si el celu y el PC están en la misma red WiFi.
2. Menos seguro si no se si la source es segura.
