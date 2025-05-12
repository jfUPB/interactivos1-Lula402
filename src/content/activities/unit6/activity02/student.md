#### <p align=center> ¿Qué pasaría si esa rampa se corta? </p>

Si la rampa se corta, no podemos entrar a la autopista con nuestros vehiculos (celus, pc, etc). Es como si sin el modem, yo no puedo acceder al internet con mi celu.

#### <p align=center>¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?  </p>

Yo soy el cliente y pido sushi, el servidor es el restaurante que me lo da. Pido Sushi del menú, me entregan el sushi hecho.

#### <p align=center> ¿Qué similitudes encuentras?</p>

Que una parte envia algo y la otra la recube. También que hay una ruta para encontrar las información en el server, entonces eso está en comun con los otros protocolos, porque hay que ser específicos en donde se encuentran las cosas.

#### <p align=center> ¿Qué diferencias clave ves?</p>

Super clave que en HTTP quien va a ser el receptor primero debe pedir la info, luego en emisor (server) la envia y ahora si el cliente la recibe, pero en ASCII y Binario no habia que pedir info, era desición de el emisor mandarla.

#### <p align=center> ¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit? </p>

Porque estamos mandando info más compleja en vez de solo bools o ints, esto implica colores, efectos, funciones, usuarios, etc. Además debe ser más complejo porque estamos haciendo todo eso en la autopista del internet, donde hay muchaaas cosas más pasando por ahí y debe ser una locura comunicarse con los protocolos que vimos antes.

### <p align=center> Análisis web fav</p>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/ef1edf30-014d-480a-ad2a-39db2e7007ac" />

#### ¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?
Creo que son los títulos, párrafos, imágenes, botones. Pero no su contenido y estilo sino solo determinar que ahí van.

#### ¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?
Diría que ese ***F1 75*** que está arriba en la izquierda. Todos los otros párrafos que hay ahí también es css quien define estilo, fuente, color, etc.

#### ¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de "contraseña incorrecta" que aparece sin recargar la página)? 
La parte de ese menú toddle, que se muestra una preview de esa página cuando pongo el cursor encima de él. También cuando en la pestaña de "teams" al poner el cursor sobre uno de los carros, se resalta.

#### <p align=center>¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?</p>

Que es mucho más estructurado un modelo de eventos, porque en una web pueden pasar muchas cosas, es decir un usuario puede hacer lo que quiera, entonces un modelo de evento es perfecto para responder al evento CUANDO PASE, sino pasa probablemente se esté ejecutando otro estado. 

#### <p align=center>¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado? </p>

Creo que definitivamente no, porque relentizaria las cosas, por ejemplo: si yo doy un click y eso es un evento, tengo que "esperar" a la propia iteración para que responda. Se que esa espera es demasiado rápida, pero simplemente se puede optimizar con eventos, de modo que no tengo todo siempre funcionando sino que lo despierto cuando lo llamo.

#### <p align=center>¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?</p>

Creo que sería útil porque es hablar en el mismo lenguaje, es decir, lo que el navegador me pida yo como server se lo voy a entregar en js, porque lo hice en js; el navegador lo va a usar en js. De esa manera no toca usar protocolos o traducciones.


#### <p align=center>Diferencia entre HTML tradicional y Sockets</p> 

La diferencia fundamental está en que en el tradicional pido -> me envian -> recibo, mientras que con sockets es mucho más rápido y directo, porque estoy con los oidos abiertos -> me dicen cosas, osea "que me hablen que ya estoy escuchando".

#### <p align=center>¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real? </p>

En word, excel, docx o básicamente lo que sea colaborativo.
