### </p><p align="center">Bomba temporizada</p> 
### Video
https://youtube.com/shorts/uI8WmhPNSsM?feature=share

### Código

```python
from microbit import *
import utime
import music

state_confi = 0    #esatdo de configuración
state_armada = 1   #estado cuando esta armed
state_explotada = 2 #estado cuando explota
current_state = state_confi #El estado inicial será en de configuración

tiempo = 20        # Valor inicial de 20 segundos
tiempo_min = 10    #Tiempo minimo
tiempo_max = 60    #Tiempo maximo
intervalo = 1000   # intervalo de 1 segundo = 1000 ms
start_time = 0     #contador de tiempo que inicia en 0

while True: 
    if current_state == state_confi:    
        if button_a.is_pressed():   #Se disminuye el temporizador
            uart.write('A')
            if tiempo > 10:
                tiempo -= 1
                display.scroll(tiempo)    #Se muestra el tiempo
                utime.sleep_ms(200)
    
        if button_b.is_pressed():   #Se aumenta el temporizador
            uart.write('B')
            if tiempo < 60:
                tiempo += 1
                display.scroll(tiempo)    #Se muestra el tiempo}
                utime.sleep_ms(200)
                
        if accelerometer.is_gesture('shake'): #Evento de shake para armarla
            current_state = state_armada
            start_time = utime.ticks_ms()   #Se guarda el tiempo actual en start_time

    elif current_state == state_armada:
        while tiempo>0:
            if utime.ticks_diff(utime.ticks_ms(), start_time) > intervalo: #"Si ha pasado más de un segundo desde la última vez que revisé el tiempo..."
                start_time = utime.ticks_ms()  # Reiniciar el temporizador
                tiempo -= 1
                display.scroll(tiempo)    #Se muestra el tiempo
        if tiempo == 0:  # Evento de que el tiempo se acabó
            current_state = state_explotada
            
    elif current_state == state_explotada:
        display.scroll('BOOM')    #mostrar BOOM
        music.play(music.FUNERAL) #sonido de BOOM, osea funeral
        
        if pin_logo.is_touched(): # Evento de touch el logo para reiniciar
            current_state = state_confi  #Vuelve a confi
            tiempo = 20 
            display.scroll('AGAIN')
```
