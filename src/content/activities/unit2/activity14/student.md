### <p align="center">Vector de prueba 1</p> 
**Entrada:** Presionar el botón A una vez.

**Estado inicial:** está en estado de configuración, con el tiempo en 20 segundos.

**Resultado esperado:** El tiempo debería disminuir a 19 segundos y mostrarse en pantalla.

**Resultado obtenido:** El tiempo se quedó en 20 y no disminuyó.

**Corrección:** tiempo = 20 estaba dentro del while principal, lo que hacía que se reiniciara en cada ronda. Moví la inicialización de tiempo = 20 fuera del while True.
### <p align="center">Vector de prueba 2</p> 
**Entrada:** Presionar el botón B una vez.

**Estado inicial:** está en estado de configuración, con el tiempo en 20 segundos.

**Resultado esperado:** El tiempo debería aumentar a 21 segundos y mostrarse en pantalla.

**Resultado obtenido:** El tiempo volvió a 20 después de presionar B.

**Corrección:** tiempo = 20 estaba dentro del while principal, lo que hacía que se reiniciara en cada ronda. Moví la inicialización de tiempo = 20 fuera del while True.
### <p align="center">Vector de prueba 3</p> 
**Entrada:** Agitar el micro:bit.

**Estado inicial:** La bomba está en estado de configuración.

**Resultado esperado:** El estado debe cambiar a armada y comenzar la cuenta regresiva.

**Resultado obtenido:** La bomba no cambió de estado.

**Corrección:** Se descubrió que el evento was_gesture('shake') a veces no se detectaba en el momento que era. Intenté con is_gesture('shake') para mayor presición.
### <p align="center">Vector de prueba 4</p> 
**Entrada:** Esperar a que la bomba agote el tiempo desde # a 0.

**Estado inicial:** La bomba está en estado armada, con el temporizador en # segundos.

**Resultado esperado:** Debería reducirse en intervalos de 1 segundo hasta llegar a 0 y luego cambiar a explotada.

**Resultado obtenido:** El temporizador disminuyó correctamente.

**Corrección:** ninguna

### <p align="center">Vector de prueba 5</p> 
**Entrada:** Tocar el logo cuando la bomba está en estado "explotada".

**Estado inicial:** La bomba está en estado explotada, con la pantalla mostrando "BOOM".

**Resultado esperado:** La bomba debe volver al estado configuración y mostrar "AGAIN".

**Resultado obtenido:** La bomba no reiniciaba el estado y la pantalla quedaba en "BOOM" otra vez.

**Corrección:** Se encontró que pin_logo.is_touched() no siempre detectaba el toque en el momento necesario. Agregé una pausa con utime.sleep_ms(200) para mejorar la detección.
