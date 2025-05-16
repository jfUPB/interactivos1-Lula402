#### 1. Describe con tus propias palabras cuál es la función del servidor Node.js en la arquitectura que exploramos. ¿Por qué los clientes p5.js no se comunican directamente entre sí?
Node.js tiene la función de ser el mediador de las pages, los clientes no se comunican entre si porque es Node.js quien se comunica con cada uno. Me lo imagino como si page1 y page2 estuviesen peleados, entonces page1 le dice al server "dile a page2 que blah blah", entonces server va y le dice a page2 "page1 manda a decir que blah blah". Es mucho más organizado que el server maneje la comunicación entre ambas pages.

#### 2. Explica la diferencia fundamental entre socket.emit() y socket.broadcast.emit() en el contexto de Socket.IO en el servidor. ¿Cuándo usarías cada uno?
Con socket.emit() estoy diciendo "no le hablo a nadie, solo hablo conmigo" mientras que con socket.broadcast.emit() digo "le hablo a todos, menos a mi". 

Los usaría dependiendo si quiero enviarle algo al serve o a otro cliente. Por ejemplo:

Acá uso solo emit, porque le quiero avisar SOLO al server, el log de que me conecté, donde estoy en este momento y mi ID (aunque el server ya lo sabe):

```js
socket.on('connect', () => {
    console.log(socket.id);
    socket.emit('win1update', currentPageData, socket.id);
})
```

Mientras que aqui, uso broadcast porque le quiero decir a todas las otras pages mis nuevos datos, y hay 0 necesidad de decirme a mi misma donde estoy:

```js
   socket.on('win3update', (window3, sendid) => {
        console.log('Received win3update from ID:', socket.id, 'Data:', window3);
        page3 = window3;
        socket.broadcast.emit('getdata3', page3)
    })
```

#### 3. Compara la comunicación mediante Node.js/Socket.IO con la comunicación serial (ASCII y binaria con framing) que viste en unidades anteriores. Menciona al menos una ventaja y una desventaja de cada enfoque según el contexto de aplicación (ej. conectar micro:bit vs. conectar dos navegadores).

Ambas tiene una estructura para comunicarse, es decir, determinar que datos se van a enviar y de que tipo son, determinan en que orden se los van a enviar. Además es diferente para quien envia y para quien recibe en ambas formas de comunicación.

***ventaja microbit:*** es mucho más sencillo mandar los datos por el puerto serial, lo digo porque es comunicación directa, el microbit le habla a p5 y listo.

***Desventaja microbit:*** es más limitado los datos que uno puede enviar por el puerto, es decir, se pueden enviar más cosas, pero de solo pensar lo mucho que tocaría pulir el framing ni me dan ganas.

***ventaja Node.js:*** Permite hacer muchaas cosas creativas, como que las posibilidades de enviar más datos es mayor porque es mucho más sencillo que en el microbit. Creo que le hago más fuerza a Node porque no me toca pensar en binario o en ASCII. Por ejemplo acá con Node estamos mandando, color, posición, ancho, alto, etc, solo imaginarme lo largo que sería el paquete de datos con Binario, noooo.

***Desventaja Node.js:*** Hay que hacer más pasos para comunicar, porque la comunicación no es directa como con el Micro, tenemos el server de por medio, entonces como programadora toca hacer más cositas para poder comunicar varias partes a la vez. La otra desventaja y que si es medio grave, es que esta comunicación depende de el wifi y de que el server esté activo.


#### 4. ¿Qué rol juega el protocolo http y qué rol juega socket.io (que usa WebSockets por debajo) en la aplicación del caso de estudio?
http permite pedirle el html, css, el js al server, para asi poder crear el cliente. Esto solo es para arrancar, como al inicio nadie se está hablando con nadie http es quien dice "dame pues las cositas pa poder crear este cliente. Luego entran los sockets (socket.io, socket.IO y WebSockets), porque ellos ya llegan a cumplir el rol de ser el medio de comunicacipon permanenete del progama. Todo esto porque los sockets son más rapidos y organizados para gestionar eso de la comunicaión.


#### 5. ¿Qué fue lo más sorprendente o interesante que aprendiste sobre la comunicación en red en esta unidad?
Lo más interesante es como un server local, que ni siquiera sabia que podia tener uno en mi compu, se pudiera comunicar con más cosas y que puedo correr los clientes en el buscador, pero NO están en internet, son full locales. Eso fue muy confuso al inicio, pero justo porque no tenia ni idea.
