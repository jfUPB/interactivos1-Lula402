### <p align= center> 1. Variables globales y conexión inicial </p>
Si sale el siguiente error:

<img width="410" alt="image" src="https://github.com/user-attachments/assets/19342c8e-c7dd-4d6b-b15e-f650401d3c77" />

Indica que page2 está intentando establecer comunicación con el server usando Socket.IO y con si propio socket.io. Como maté al server el error dice: que no se puede comunicar con el localhost, por el puerto 3000 y con el socket.io. Son dos personas comunicandose y cuando una ya no está, pues no se puede establecer comunicación. 

Si, al iniciar el server y refrescar page2, se corrige el error:

<img width="398" alt="image" src="https://github.com/user-attachments/assets/814672c0-5ab4-4b38-8884-e5c216d01280" />

### <p align= center> 2. Manejando la conexión establecida </p>
¿Qué pasó en page1 antes de que movieras page2? 
Asi se veia page1 antes de mover a page2:

<img width="827" alt="image" src="https://github.com/user-attachments/assets/4e0bc7c5-e3a0-45ee-b7a2-7cdf0fcceaab" />

Basicamente lo que pasó es que no parecía estar sincronizado con page2.

¿Tenía la información correcta sobre page2 desde el principio? 
Nop, tenia solo como los datos estandar que fue los que vimos cuando se establecia la comunicación con el server.

¿Por qué es útil enviar el estado inicial al conectarse? 
Porque enviar el estado inicial permite que uno de los clientes encuentre al otro. Si page1 lo muevo, page2 aunque no se mueva, el servidor le debe mandar el estado inicial a page1 para que lo pueda encontrar.

### <p align= center> 3. Recibiendo datos del servidor </p>

<img width="355" alt="image" src="https://github.com/user-attachments/assets/26044d45-0f1d-4b2f-964d-2fe8a8a89889" />
