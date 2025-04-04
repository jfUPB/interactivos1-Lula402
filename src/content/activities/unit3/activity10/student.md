### ¿Por qué esta técnica es poderosa para la escalabilidad de tu aplicación en términos de concurrencia y de manejo de eventos?
Porque permite organizar y dividir la lógica de la bomba en partes claras y bien definidas. En lugar de tener un código de manera lineal caótico, cada estado representa una "situación" específica de la bomba. Esto facilita agregar o modificar funcionalidades a futuro, ya que se pueden crear nuevos estados, eventos y acciones sin alterar toda la estructura.

### ¿Qué ventajas y desventajas tiene el tipo de pruebas que realizaste en esta unidad?
#### Ventajas
1. Me ayudaron a asegurarme de que el programa responde como se espera en cada posible situación, lo que aumenta la confiabilidad del sistema.
2. Al probar eventos que no tenía, pude detectar errores que no había previsto en el diseño inicial.
3. Implementar pruebas de regresión me permitió confirmar que las correcciones no generaron nuevos errores en otras partes del código.

#### Desventajas
1. Requieren bastante tiempo y esfuerzo, ya que hay que analizar cada estado y cada posible evento.
2. Si no se crean suficientes vectores de prueba, pueden quedar errores ocultos.
3. Cada vez que se hace una corrección, es necesario volver a ejecutar todas las pruebas desde el principio, lo que puede volverse repetitivo y cansador.

### ¿Por qué son importantes las pruebas de regresión? 
Las pruebas de regresión son importantes porque permiten saber si después de cada nueva versión o modificación el código sigue funcionando o si ya no funciona bien como antes de esa nueva versión. Lo más importante es no seguir cambiando y construyendo cosas en el código sin ni siquiera saber si sobre lo que empecé a construir ya funcionaba correctamente, entonces luego va a ser más difícl el Debbuging.

### ¿Qué pasa si modificas tu aplicación y no haces las pruebas de regresión?
Si modifico mi aplicación y no hago pruebas de regresión, corro el riesgo de que en esta nueva versión del código, la cosa nueva que agregué, impida que lo que antes funcionaba ahora funcione. Esto es malo, ya que, probablemente seguiré modificando el código sin si quiera saber si en cada nueva modificación le estoy haciendo bien al código.
