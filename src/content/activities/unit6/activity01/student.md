#### <p align=center> ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito? </p>
<img width="800" alt="image" src="https://github.com/user-attachments/assets/1dd8cd71-9381-4843-8b89-136a1eea33d3" />

Cuando ejecuté ```npm install``` ocurre que me avisa cuantos paquetes se cargaron de lo que cloné, también dice que hay unos buscando donaciones y lo más importante que encontró 0 vulnerabilidades. En este momento sale sin vulnerabilidades porque ya lo habimos corregido, pero antes salía en rojito unas vulnerabilidades que arreglamos con ```npm audit fix```.

Su propósito es que todo eso que cloné fue la estructura y al decirle install estoy trayendo todo lo que necesita para que funcione full en mi pc local.

#### <p align=center> ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje? </p>
<img width="800" alt="image" src="https://github.com/user-attachments/assets/089ceb36-9679-4bbc-b963-684a9f126c4f" />

```Server is listening on http://localhost:3000``` Es el mensaje específico que aparece al ejecutar nom start, indica que el servidor está listo para ser usado, osea corriendo full en mi pc, en localhost y especificamente en el puerto 3000. Este servidor local se va a comunicar con los clientes web que van a ser page 1 y page 2.

#### <p align=center> Describe lo que ves inicialmente en page1 y page2 en tu navegador </p>
Inicialmente vi un error, pero era porque sin culpa habia cerrado el server, entonces en consola volvía  abrirlo.
Luego ahora si en page 1 vi un circulo rojo con un palito gris apuntando a una dirección random, lo mismo con page 2.

#### <p align=center>Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente?</p>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/35ca4d1c-2f0d-4767-82d6-6cf921eee89a" />

Primero tuve que forzar que cargara la page 1, para poder que se acomode y le envie a la page 2 su posición actual, luego 
page 2 la moví, para que envié a page 1 su posicipon actual y ahora si quedan sincronizadas.
Si cambió algo visualmente respecto al inicio de cuando apenas abrí las pages y es que los palitos de los circulos parecen estar unidos. Todo esto porque en realidad ambas pages están pintando ambos circulos, solo que al canvas ser tan peque no se logran ver ambas, pero cuando yo junto sufiente ambas ventanas, entonces se logran ver ambos circulos en ambas pages.


#### <p align=center>¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor? </p>

<img width="400" alt="image" src="https://github.com/user-attachments/assets/47a6680a-ea1b-4ac8-af49-182993cb770c" />

<img width="800" alt="image" src="https://github.com/user-attachments/assets/cb7a3443-519c-4d3f-9e80-d8234618d09d" />

Tanto en la consola del navegador como en la terminal se muestra un mensaje con la posición en (x,y) y el width y height del canvas (ventana), basicamente entonces se está mostando lo que se esta enviando de una page a otra. El ID es para saber a que cliente web (a que page) le pertenece ese mensaje.

Para page 1 y page 2 coincide el ID del cliente tanto en la consola del navegador como en la terminal:

#### Page 1
<img width="650" alt="image" src="https://github.com/user-attachments/assets/f2d250e4-48d7-42c8-85ee-d07ba9ea5145" />

<img width="350" alt="image" src="https://github.com/user-attachments/assets/4ea30881-69d9-46f6-a249-20224d46a76b" />

#### Page 2
<img width="650" alt="image" src="https://github.com/user-attachments/assets/9d96fdcd-cacd-4988-93f7-a0fe444ab688" />

<img width="350" alt="image" src="https://github.com/user-attachments/assets/5abd0282-67b3-4fc6-b476-df8a53cd58ea" />


