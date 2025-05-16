### 1.
La función principal de ***express.static('public')***, es que cuando un cliente pide un archivo al server, el está diciendo en esa línea "vea, cuando vengan a buscar algo?, busquelo en public que ahí esta todo". La diferencia entre esta manera y la de las rutas especificas de la unidad pasada, es que en esta no estoy diciendo que archivo en especifico voy a ser el que voy a mandar cuando me pidan algo, que eso es lo que se hizo la unidad anterior. Al contrario en esta manera yo solo digo que todo está en public, entonces si piden un archivo lo mando automaticamente desde la carpeta de public que debe tener el archivo.

### 2.
#### ¿Qué evento lo envía desde el móvil? 

```js
socket.emit('message', JSON.stringify(touchData));
```

#### ¿Qué evento lo recibe el servidor? 
```js
  socket.on('message', (message) => {
        console.log(`Received message => ${message} from ID: ${socket.id}`);
        // Retransmite el mensaje recibido a TODOS los OTROS clientes conectados
        socket.broadcast.emit('message', message);
    });
```

#### ¿Qué hace el servidor con él? 
Envirlo a todos menos a quien fue quien lo envió, osea a los demás clientes menos al dueño del socket que lo envió:

```js
 // Retransmite el mensaje recibido a TODOS los OTROS clientes conectados
        socket.broadcast.emit('message', message);
```

#### ¿Qué evento lo envía el servidor al escritorio? 

```js
socket.broadcast.emit('message', message);
```

#### ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?
Porque ***socket.broadcast.emit*** se lo envía a todos los otros clientes, pero no se lo reenvia a quien lo envió. No se usa ni ***io.emit*** ni ***socket.emit*** porque no tiene lógica en este caso volverle a mandar los datos a quien me envió esos datos. Es como si yo mandara un mensaje a mi abuela y ella en vez de reenviarselo a mi papá me lo reenvía a mi, 0 sentido en este caso.

### 3.
En este caso y la manera en la que tenemos programado el server, lo recibirían ambos compus. Al mandar el mensaje retransmitido ***socket.broadcast.emit*** hace que se envíe a todos lo clientes que hayan, menos a quien lo envió. Tanto pc1 como pc2 van a recibir los datos actualizados de ese touch en el celu.

### 4.
- Server is listening on http://localhost:
- Client disconnected - ID:
- Received message => ${message} from ID: ${socket.id}
- New client connected - ID:

SOn útiles porque me informan lo que va pasando: si el server ya está escuchando, si un cliente se conecta o se desconecta con su correspondiente ID, cuando recibo un mensaje, cual es el mensaje y de quien ID fue ese mensaje.
