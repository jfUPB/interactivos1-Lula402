### Código
```python
# Imports go at the top
from microbit import *
import utime
import music

state_confi = 0    #esatdo de configuración
state_armada = 1   #estado cuando esta armed
state_desarmada = 2 #estado cuando explota
state_explotada = 2 #estado cuando explota
current_state = state_confi #El estado inicial será en de configuración
secuencia_correcta = ['A', 'B', 'A', 'SHAKE']
secuencia_user = []  # para almecener la secuencia del user

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

        if accelerometer.was_gesture('shake'): #Evento de shake para armarla
            current_state = state_armada
            start_time = utime.ticks_ms()   #Se guarda el tiempo actual en start_time

    elif current_state == state_armada:

        if utime.ticks_diff(utime.ticks_ms(), start_time) > intervalo: #"Si ha pasado más de un segundo desde la última vez que revisé el tiempo..."
            start_time = utime.ticks_ms()  # Reiniciar el temporizador
            tiempo -= 1
            display.scroll(tiempo)    #Se muestra el tiempo
           
            if tiempo == 0:  # Evento de que el tiempo se acabó
                display.scroll('BOOM')    #mostrar BOOM
                music.play(music.FUNERAL) #sonido de BOOM, osea funeral
                current_state = state_explotada
    
        if button_a.was_pressed():
            secuencia_user.append('A') 
        if button_b.was_pressed():              
            secuencia_user.append('B') 
        if button_a.was_pressed():
            secuencia_user.append('A') 
        if accelerometer.was_gesture('shake'):       
            secuencia_user.append('SHAKE') 
            if  secuencia_user==secuencia_correcta:          
                tiempo = 20
                display.scroll('RESTART')
                current_state = state_confi  #Vuelve a confi

            else: 
                display.scroll('ERROR')

            secuencia_user.clear()
            if accelerometer.was_gesture('shake'):
                pass


    elif current_state == state_explotada:
        if pin_logo.is_touched(): # Evento de touch el logo para reiniciar
            tiempo = 20
            display.scroll('AGAIN')
            current_state = state_confi  #Vuelve a confi
```

### Cómo implementé la secuencia de desactivación?
La secuencia de desarmed, la implementé como eventos dentro del estado de armada. Si se cumplen las condiciones (eventos) de que los botones fueron presionados en el orden correcto entonces la bomba se desarma, se resetea el tiempo = 20, se muestra un mensaje al usuario de "RESTART" y se regresa al estado de configuración. Si el patrón es incorrecto, entonces se muestra "ERROR".

