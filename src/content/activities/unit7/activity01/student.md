### 1.
Casi que no logro correr el server desde visual code y además lo de los puertos casi que tampoco lo logro, pero se logró, esa escepción del inicio me la dió chatg cuando le mostré el error que me salía, es para que solamente en esa sesión windows permita installer y correr el server sin desconfiar.

### 2.
Salió el mismo mensajito que salia en la terminal de gitbash, avisando que el server ya estaba escuchando.

### 3.
Cuando puse la URL en safari, me salió esta advertencia que me dice que estoy apunto de usar un dev tunel y que solo lo haga si confio en la source: (claramente le di que si)

![Windows](https://github.com/user-attachments/assets/cec62e8f-0721-48c9-a984-0b87bf925a72)

### 4.
Cuando ya empecé a hacer drag con el dedo en el celu, en la terminar de visual ya emepzaban a salir los "recieved message", que son porque el server si estaba receibiendo los mensajes del input del celu.

<img width="785" alt="image" src="https://github.com/user-attachments/assets/b6d43605-7dcd-49aa-9b64-16e686c3f7e9" />


#### <p align=center> ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte? </p>

***Obtuve:*** https://px56d85g-3000.use.devtunnels.ms

Creo que debemos usare esa URL en vez de la de local host, porque a la final no estamos corriendo el server en nuestro celu, sino que está corriendo en el pc. Por eso para habrirla en el compu usamos local host, porque el server está en ese mismo compu, pero para el celu usamos la de devtunnels porque es la manera de conectarlo también a ese server.

#### <p align=center>  Describe brevemente qué hace npm install y npm start. </p>

***npm install*** descarga todas las depencias, las librerias y lo que se necesita para que el server corra.

***npm start*** Es quien dice que arranquemos el server, entonces trae todo lo que ya npm install habia descargado y despierta el server de node.js.

#### <p align=center>  ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores? </p>


El mensaje que observé fue: ```New Client Connected```

Nop, ambos mensajes fueron iguales: 

<img width="258" alt="image" src="https://github.com/user-attachments/assets/0383051f-8ab1-4989-9d93-cc8604c0db4d" />

#### <p align=center>  Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)? </p>
La interacción funcionó bastante bien y funcionó de una aprenas pusiera la URL en el celu. Si hubo latencia, lo noté cuando oprimía y movia el dedo, luego lo soltaba y cuando lo volvía a poner sobre la pantalla como que el circulito rojo tenia una mini enloquecida y ya se volvia a acomodar. Tampoco es como que esa latencia durara mucho, pero si se nota.
