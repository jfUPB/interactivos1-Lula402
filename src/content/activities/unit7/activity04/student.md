### <p align=center>Reflexiona (Móvil)</p>

1. es útil porque da orden a la comunicación. Es mucho mejor yo decir a quien le pertenece ese valor, por ejemplo es mejor decir ***{'x= ' 150, 'y= ' 200}*** que decir ***{150, 200}**, porque a uno le toca basicamente memorizarse el orden de los datos.
2. Podrían haber lags y más latencia, y creo que la bolita se veria shaky en la pantalla. Es sobrecargar el server y los clientes innecesariamente.
3. Modificaría el código para que no solo espere el evento de touch, sino que tambien esté abierto a recibir el evento del click del mouse, entonces tambien tendria sus variables correspondientes a (x,y). Con mousepressed es que empiezo a ponerle atención, es decir, seria lo que yo espero en el evento. Luego con mousemoved si empiezo a leer la posición.

### <p align=center>Reflexiona (Móvil)</p>
1. Porque si JSON.parse() no es válido el script se detiene entonces deja de funcionar el programa. Es importante usar el try...catch, para que primero mire si si se puede usar ese JSON.parse() y si saca error, el error se quede en ese bloque y no dañe todo. Todo esto porque puede que por algun motivo el JSON.parse() venga sin todas las comillas o sin todos los datos que debe tener dentro.
2. Usaria map para transformar el valor del canvas del celu al valor que deberia ser en el canvas del pc. Si el del celu es 300x300, entonces lo mínimo es 0 y lo max es 300, Si el pc es 600x600 lo min es 0 y lo max es 600.

Lo que quiero transformar es el valor de la variable touchX. Lo que haría en map es como lo que hicimos en computacionales para manejar la opacidad, que dependiendo del la posición del nodo, se le asignaba un valor de opacidad proporcional.

Se calcula que si entre 0 a 300 hay un valor, cual sería el equivalente en un rango de 0 a 600.

```map(touchX, 0, 300, 0, 600);```

3. Tendría que cambiar acá:

```js
    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
        try {
            let parsedData = JSON.parse(data);
            if (parsedData && parsedData.type === 'touch') {
                circleX = parsedData.x;
                circleY = parsedData.y;
            }
        } catch (e) {
            console.error("Error parsing received JSON:", e);
        }
    });
```
Que en vez de verificar si le llega algo que se llame 'message', verifique que se llame 'updateDesktop', porque ese es el que va a tener a ***data*** con toda la info para actualizar.

### <p align=center> Reporta en tu bitácora</p>

1. La función principal de mobile/sketch.js y desktop/sketch.js. es decir que va a pasar en su canvas, como van a recibir mensajes y como van a mandar mensajes.

Ya con más detalle mobile/sketch.js es donde se captura la info del touch en el celu, donde se guarda esa info y donde se la envia al server.

desktop/sketch.js. es donde se dibuja el background, el circulo, donde se recibe la info que el server le manda (la que le mandó mobile/sketch.js) y donde la procesa y actualiza el circulo.

------------------------------------------------------------------------------------------------------------------------------

2. La función touchMoved() está ahí pendiente cada vez que uno mueve el dedo en la pantalla. Pero no quiere reaccionar a cualquier mini temblor del dedo, por eso usamos un threshold. Si el movimiento fue tan chiquito que parece un error o un temblor random, se ignora. Pero si muevo el dedo lo suficiente (o sea padando el threshold), entonces guarda la nueva posición (x, y) y la prepara para mandarla.

Como no podemos mandar objetos así directo por el socket (tipo una variable), usamos JSON.stringify() para convertir esos datos en un string que sí se puede enviar. Así el servidor lo entiende y después el pc puede reconvertirlo con JSON.parse().

------------------------------------------------------------------------------------------------------------------------------

3. El pc escucha con socket.on('message') y cuando llega un dato usa JSON.parse() para reconvertirlo de string a objeto. Luego revisa si el tipo (type) de ese objeto es 'touch'. Si si es touch, agarra las coordenadas (x,y) del objeto y actualiza la posición del círculo. Así sabe dónde toqué la pantalla del celu.

