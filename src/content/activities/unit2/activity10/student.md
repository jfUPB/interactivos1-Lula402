### Explicación
Este programa no tiene concurrencia, porque todo se hace de manera lineal en este caso. Solo tenemos una variable que guarda el estado, osea que solo puede haber un estado activo a la vez. Además para que cambie de estado y de evento, debe cumplirse una condición, si la condición  no se cumple entonces pasa a evaluar es siguiente estado a ver si se hace la acción o no.

### <p align="center">  Vector 1 </p> 
**Estado:** Init. Es el estado con el que predeterminamente inicia.

**Evento:** ```if current_state == STATE_INIT:```  Si el estado actual es igual a Init, entonces entra al if porque se cumple la condición y a continuación se van a realizar las acciones.

**Acción:**
Como se cumplió la condición que el evento esperaba entonces se hace lo siguiente:
```python
display.show(Image.HAPPY)                 #Se muestra la carita feliz
        start_time = utime.ticks_ms()     #El tiempo actual se guarda en start_time
        interval = HAPPY_INTERVAL         #interval se hace igual al intervalo de la carita feliz
        current_state = STATE_HAPPY       #El estado actual pasa a ser el estado feliz 
```
### El sistema pasó el vector 1 de prueba satisfactoriamente.

### <p align="center">  Vector 2 </p> 
**Estado:** SILLY. Si el estado actual es igual a SILLY, entonces entra al if porque se cumple la condición y a continuación se van a realizar las acciones.
**Evento:** ```if button_a.was_pressed():```  Si el botón A está presionado entonces entra al if porque sí se cumple la condición. A continuación se realizan las acciones dentro del evento.

**Acción:**
Como se cumplió la condición que el evento esperaba entonces se hace lo siguiente:
```python
      display.show(Image.HAPPY)         #Se muestra la carita feliz.
      start_time = utime.ticks_ms()     #El tiempo actual se guarda en start_time
      interval = HAPPY_INTERVAL         #interval se hace igual al intervalo de la carita feliz, para saber cuanto se deja
      current_state = STATE_HAPPY       #El estado actual pasa a ser el estado feliz 
```
### El sistema pasó el vector 1 de prueba satisfactoriamente.

### <p align="center">  Vector 3 </p> 
**Estado:** SAD.  Si el estado actual es igual a SAD, entonces entra al if porque se cumple la condición y a continuación se van a realizar las acciones.
**Evento:** ```if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:``` Si la diferencia del tiempo actual con 

**Acción:**
Como se cumplió la condición que el evento esperaba entonces se hace lo siguiente:
```python
 
```
### El sistema pasó el vector 1 de prueba satisfactoriamente.
