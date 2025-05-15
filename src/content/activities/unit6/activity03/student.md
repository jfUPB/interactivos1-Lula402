### <p align=center> 1. Dependencias: las herramientas necesarias </p>
#### <p align=center> ¿Por qué crees que es útil usar módulos o librerías en lugar de escribir todo desde cero? ¿Qué ventajas aporta? </p>

Creo que es útil usar librerias porque, por qué vamos a escribir algo desde 0? sabiendo que podemos ahorrarnos ese tiempo de trabajo y tomar la libreria. Basicamente para eso existen las librerias es como ese paquetico que ya hace lo que tu quieres que tu proyecto haga, la usas y ya está, añades lo extra que quieras. La ventaja principal es facilitar el flujo de trabajo.

### <p align=center> 4. Sirviendo los archivos del cliente </p>
#### <p align=center> ¿Qué ocurre? ¿Por qué? ¿Qué mensaje ves en el navegador o en su consola de desarrollador (F12)? </p>

En la consola si me dejó arrancar el server.
El server no puede iniciar y escuchar porque no encuentra los files necesarios para cumplir lo que el navegador le pide. El propio error dice que se debe a que no encuentra los files o el directory que intentamos acceder no existe.

En el navegador veo el típico mensajito de:

***"No se puede acceder a este sitio web
La página localhost ha rechazado la conexión."***

Esto es porque para empezar aunque se inició el server, no existe ese archivo que el cliente le pide al server para mandarselo.

### <p align=center> 5. Rutas: ¿Qué enviar cuando se pide una URL? </p>
#### <p align=center> Page 1 -> pagina_uno  </p>

Con /page 1 no funciona sale el siguiente error: 

<img width="150" alt="image" src="https://github.com/user-attachments/assets/c89a4106-7fb7-40c4-b6f0-dd6060fbf7e0" />

Con /pagina_uno si funciona, muestra el ID, me salió: b4427UtXnDJ8YbkiAAAD. Y también se ven los circulos en la ventana.

#### <p align=center> ¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? </p>
Aunque cambie la ruta de acceso, con tal de que le siga diciendo que archivo es el que tiene que mandar, todo sigue funcionando bien. Es decir, aunque cambie la ruta de acceso a ***/pagina_uno*** con tal de que siga diciendo en code que debe enviar ***page1.html***, todo sigue funcionando.

Pero debo tener en cuenta que el cliente debe tener esa misma ruta de acceso porque sino estoy intentando ver un navegador que no existe: ***not found***

### <p align=center> 6. ¡La Magia de Socket.IO! La Conexión </p>
#### <p align=center>  Socket.IO </p>

#### Abriendo page1

Veo lo siguiente en la terminal:

<img width="500" alt="image" src="https://github.com/user-attachments/assets/1b752b75-5f14-442d-bd9d-4e58467b10ae" />

**ID =** sJYMxTEieIDMa7ZYAAAB

#### Abriendo page2

Veo lo siguiente en la terminal:

<img width="706" alt="image" src="https://github.com/user-attachments/assets/234038d5-f78e-444d-8c89-212ae5ae5a55" />

**ID =** bdyPPjBeqQw0ISHVAAAD

#### Cerrando page1

Si coincide con el ID que anoté:

<img width="316" alt="image" src="https://github.com/user-attachments/assets/c9dce3a9-51a9-4646-b94e-ed169bbeebd1" />

#### Cerrando page2

Si coincide con el ID que anoté:

<img width="315" alt="image" src="https://github.com/user-attachments/assets/e49a1598-662c-42e1-9470-e0d943b453c5" />

### <p align=center> 7. Escuchando Mensajes de los Clientes </p>
#### <p align=center>  Win1update - Win2update </p>
#### Moviendo page1
Se registra el evento Win1update. Los datos que veo son {x, y, widht, height}

<img width="698" alt="image" src="https://github.com/user-attachments/assets/9a8e30a3-70ba-4608-aa93-711267c11045" />

#### Moviendo page2
Se registra ahora el evento Win2update. Los datos que veo son {x, y, widht, height}

<img width="694" alt="image" src="https://github.com/user-attachments/assets/c01a9477-7045-49e0-8b9d-e853bda208e1" />

#### Experimento broadcast
Cuando muevo page1 no se actualiza la visualización en page2. No se actualiza porque como le quite el broadcast ya no se le está mandado eso a todos los otros clientes, aun está el emit y ese emit envia un mensaje con las cositas actualizadas de page 1 pero me está hablando solito consigo mismo ese cliente. Todo eso porque broadcast es "a todos menos a mi", entonces si lo quito es "a nadie, solo a mi".

Es como si socket.broadcast hiciera un mensaje de difusión en Whatsapp y con emit le manda ese mensaje a todos los chats (clientes). Como ya no estoy haciendo ese mensaje de difusión me estoy mandando ese mensaje a mi mismo.

### <p align=center> 8. Poner en marcha el Servidor </p>

#### Experimento port
1. 
<img width="109" alt="image" src="https://github.com/user-attachments/assets/adaa43fe-a380-4f21-ab75-27ccd5359d38" />

En consola veo que el server si está escuchando y que escucha por el puerto 3001: ```Server is listening on http://localhost:3001```

### localhost:3000/page1
No funciona, sale que no se puede acceder al sitio web.

### localhost:3001/page1
Si funciona.

### ¿Qué aprendiste sobre la variable port y la función listen?
Aprendí que con la varibale port yo como server determino por cual puerto me voy a comunicar con los clientes, si lo cambio también los clientes deben cambiar a ese puerto para que funcione.

La función listen es cuando el server coge un copito y se limpia el oido (ahí llama a listen), entonces listen le dice "Listo, empieza a escuchar por este oido en específico", el oido vendría siendo el puerto.
