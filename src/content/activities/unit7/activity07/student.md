- 5
- 4
- 4
- 5
- 3
- 5

### 1
Lo más facil fue lo de recibir y procesar los eventos del celu, yo diría que fue lo más fácil porque hemos trabajo en eso de manejar inputs desde el inicio del curso. Ya estoy familiarizada con eso de que es un touch, de tener que guardar el touch anterior, para que cuando haya un cambio los pueda comparar.

### 2
Lo más dificil fue el momento en el que teniamos que modificar el caso de estudio para hacer lo de las particulas. Para lograrlo recordé que tengo que ir en orden, entonces primero borré lo que tenía que ver con mostrar el circulo en la pantalla del pc. Luego en el mobile.js añadi las dos cosas que me pedían y era que ahi se determinara el color y si usaba o no stroke. Luego miré si en el server tenía que cambiar algo. Luego en el desktop, añadi las otras dos cosas que debia procesar (colorcito,useStroke). 

La parte en la que tenía que cambiar el draw de desktop para que mostrar las particulas tambien fue dificil, pero usé como estrategia lo que hicimos en computacionales con las serpientes, entonces ya sabia que debia recorrerla para poder pintarla.

### 3
Imagínate que tienes dos pantallas: una es el celular y la otra es el computador. Lo que hicimos fue conectar esas dos pantallas para que lo que se toque en el celu se vean como particulas en el escritorio.

¿Cómo fluye la información?
1. Tocas la pantalla del móvil.
Cada vez que tocas o arrastras el dedo, se genera un evento. El código en el celu (hecho con p5.js) detecta ese input.

2. Esa info tiene: la posición X/Y de donde hiciste click, un color para la particula y si se debe dibujar con borde o no.

3. Se manda esa info al servidor.
Para eso usamos algo que se llama dev tunnels, permite enviar datos en tiempo real al host del servidor (el compu) aunque el celu sea un dispositivo externo, como si fuera un tunel. Esa info viaja desde el celu hasta el servidor que corre en tu compu con Node.js.

4. El server recibe y reenvía.
El servidor no hace nada con la info, solo es como un repartidor: recibe el mensaje y lo pasa al escritorio. Para eso usamos Socket.IO, una libreria que permite enviar datos en tiempo real, como si fuera un bokitoki

5. El escritorio recibe la info y dibuja.
Ahí también usamos p5.js y esta pantalla está escuchando datos. Cada vez que recibe un nuevo toque desde el servidor, crea una partícula en esa posición, con el color indicado y con o sin borde.

6. Las partículas aparecen y se mueven solitas.

### 4
Se me ocurre que podría usar lo aprendido haciendo que el ipad sea para dibujar, pero lo que dibujo lo veo en el compu. La idea es que no sea solo el ipad, sino tambien en los celulares y que se pueda dibujar como en colaborativo. Es como algo similar al juego de gartic phone, que es muy charro y maybe a futuro pueda hacer algo asi.
