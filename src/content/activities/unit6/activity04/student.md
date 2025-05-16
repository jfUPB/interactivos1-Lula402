### <p align= center> 1. Variables globales y conexión inicial </p>
Si sale el siguiente error:

<img width="410" alt="image" src="https://github.com/user-attachments/assets/19342c8e-c7dd-4d6b-b15e-f650401d3c77" />

Indica que page2 está intentando establecer comunicación con el server usando Socket.IO y con si propio socket.io. Como maté al server el error dice: que no se puede comunicar con el localhost, por el puerto 3000 y con el socket.io. Son dos personas comunicandose y cuando una ya no está, pues no se puede establecer comunicación. 

Si, al iniciar el server y refrescar page2, se corrige el error:

<img width="398" alt="image" src="https://github.com/user-attachments/assets/814672c0-5ab4-4b38-8884-e5c216d01280" />

### <p align= center> 2. Manejando la conexión establecida </p>
#### ¿Qué pasó en page1 antes de que movieras page2? 
Asi se veia page1 antes de mover a page2:

<img width="827" alt="image" src="https://github.com/user-attachments/assets/4e0bc7c5-e3a0-45ee-b7a2-7cdf0fcceaab" />

Basicamente lo que pasó es que no parecía estar sincronizado con page2.

#### ¿Tenía la información correcta sobre page2 desde el principio? 
Nop, tenia solo como los datos estandar que fue los que vimos cuando se establecia la comunicación con el server.

#### ¿Por qué es útil enviar el estado inicial al conectarse? 
Porque enviar el estado inicial permite que uno de los clientes encuentre al otro. Si page1 lo muevo, page2 aunque no se mueva, el servidor le debe mandar el estado inicial a page1 para que lo pueda encontrar.

### <p align= center> 3. Recibiendo datos del servidor </p>

#### ¿Se dispara el log "Page 2 received..."? ¿Qué datos muestra?
Sí se dispara, muestra los datos {x, y, width, height}:

<img width="350" alt="image" src="https://github.com/user-attachments/assets/26044d45-0f1d-4b2f-964d-2fe8a8a89889" />

#### ¿Se dispara este log? ¿Por qué sí o por qué no? (Pista: ¿Quién envía el evento getdata?) 
No se dispara el log. No sale el log, porque nosotros en getdata solo estamos esperando y escuchando los datos de la otra ventana (osea page1). dataWindow me la manda el server y contiene los datos de la otra ventana, luego esos datos yo los guardo en mi propia variable designada para es ventana (page1) remota. Basicamente en ningun momneto estamos usando los datos de page 2 en este evento.

### <p align= center> 4. Detectando cambios y enviando actualizaciones </p>
#### ¿Cuándo aparece el mensaje "Page 2 detected change..."?
Aparece, muy rápido aunque la haya movido un tris, osea a la vista uno ni siquiera ve un cambio grande pero de una lo detecta:

<img width="404" alt="image" src="https://github.com/user-attachments/assets/e814b54d-1199-4219-9a2a-bc2c4e4dc692" />

#### Deja la ventana de page2 quieta. ¿Aparece el mensaje?
No, si dejo la ventana quieta no sale ningun mensaje en la consola

#### ¿Por qué es eficiente esta estrategia de comparar con el estado anterior antes de enviar datos por la red? 
Es eficiente porque si ya envíe esos datos, por que lo querría mandar otra vez? es que sería llenar la consola para nada, es mucho mejor solo hablar cuando hubo un cambio real. Esto es eficiente porque es mucho más facil hacer experimentos, entender lo que sale en consola y hacer un seguimiento de como se esta moviendo la ventana y de que datos está enviando.

### <p align= center> 5. La visualización (draw) </p>
Al usar el (remotePageData.width), tuve que dividir entre 2 ese valor, porque si no no quedaba chevere, porque quedaba gigante, mientras que así sigue funcionando respecto al ancho de la otra page, pero sí se logra ver bien.

https://youtu.be/0M2g9Qab16E
