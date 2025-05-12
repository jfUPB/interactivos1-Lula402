#### <p align=center> ¿Por qué crees que es útil usar módulos o librerías en lugar de escribir todo desde cero? ¿Qué ventajas aporta? </p>

Creo que es útil usar librerias porque, por qué vamos a escribir algo desde 0? sabiendo que podemos ahorrarnos ese tiempo de trabajo y tomar la libreria. Basicamente para eso existen las librerias es como ese paquetico que ya hace lo que tu quieres que tu proyecto haga, la usas y ya está, añades lo extra que quieras. La ventaja principal es facilitar el flujo de trabajo.

#### <p align=center> ¿Qué ocurre? ¿Por qué? ¿Qué mensaje ves en el navegador o en su consola de desarrollador (F12)? </p>

En la consola si me dejó arrancar el server.
El server no puede iniciar y escuchar porque no encuentra los files necesarios para cumplir lo que el navegador le pide. El propio error dice que se debe a que no encuentra los files o el directory que intentamos acceder no existe.

En el navegador veo el típico mensajito de:

***"No se puede acceder a este sitio web
La página localhost ha rechazado la conexión."***

Esto es porque para empezar aunque se inició el server, no existe ese archivo que el cliente le pide al server para mandarselo.

#### <p align=center> Page 1 -> pagina_uno  </p>

Con page 1 no funciona sale el siguiente error: 

<img width="150" alt="image" src="https://github.com/user-attachments/assets/c89a4106-7fb7-40c4-b6f0-dd6060fbf7e0" />

Con pagina_uno si funciona, muestra el ID, me salió: b4427UtXnDJ8YbkiAAAD. Y también se ven los circulos en la ventana.

#### <p align=center> ¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? </p>
Aunque cambie la ruta de acceso, con tal de que le siga diciendo que archivo es el que tiene que mandar, todo sigue funcionando bien. Es decir, aunque cambie la ruta de acceso a ***/pagina_uno*** con tal de que siga diciendo en code que debe enviar ***page1.html***, todo sigue funcionando.

Pero debo tener en cuenta que el cliente debe tener esa misma ruta de acceso porque sino estoy intentando ver un navegador que no existe: ***not found***


#### <p align=center> Page 1 -> pagina_uno  </p>
