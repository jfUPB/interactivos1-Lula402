### Bomba 3.0
#### Micro:bit y puerto serial
```python
# Imports go at the top
from microbit import *
import utime
import music

isEvent = False
eventData = ''
state_confi = 0    #esatdo de configuración
state_armada = 1   #estado cuando esta armed
state_explotada = 2 #estado cuando explota
current_state = state_confi #El estado inicial será en de configuración
secuencia_correcta = ['A', 'B', 'A', 'S']
secuencia_user = []  # para almecener la secuencia del user
tiempo = 20        # Valor inicial de 20 segundos
intervalo = 1000   # intervalo de 1 segundo = 1000 ms
start_time = 0     #contador de tiempo que inicia en 0


def tareaBomba():
    global isEvent
    global eventData,current_state,secuencia_user,tiempo,start_time
    
    if current_state == state_confi:
        if isEvent == True:   #Se disminuye el temporizador
            isEvent = False
            if eventData == 'A':   #Se disminuye el temporizador
                if tiempo > 10:
                    tiempo -= 1
                    display.scroll(tiempo)    #Se muestra el tiempo

            if eventData == 'B':  #Se aumenta el temporizador
                if tiempo < 60:
                    tiempo += 1
                    display.scroll(tiempo)    #Se muestra el tiempo}

            if eventData == 'S': #Evento de shake para armarla
                current_state = state_armada
                start_time = utime.ticks_ms()   #Se guarda el tiempo actual en start_time
                secuencia_user.clear()

    elif current_state == state_armada:

        if utime.ticks_diff(utime.ticks_ms(), start_time) > intervalo: #"Si ha pasado más de un segundo desde la última vez que revisé el tiempo..."
            start_time = utime.ticks_ms()  # Reiniciar el temporizador
            tiempo -= 1
            display.scroll(tiempo)    #Se muestra el tiempo
           
            if tiempo == 0:  # Evento de que el tiempo se acabó
                display.scroll('BOOM')    #mostrar BOOM
                music.play(music.FUNERAL) #sonido de BOOM, osea funeral
                current_state = state_explotada

        if isEvent == True:   #Se disminuye el temporizador
            isEvent = False
            if eventData == 'A':
                secuencia_user.append('A')
            if eventData == 'B':              
                secuencia_user.append('B')              
            if eventData == 'S':       
                secuencia_user.append('S')
                display.show('S')
                sleep(250)
                if  secuencia_user==secuencia_correcta:          
                    tiempo = 20
                    display.scroll('RESTART')
                    display.scroll(tiempo)    #Se muestra el tiempo
                    current_state = state_confi  #Vuelve a confi
                else: 
                    display.scroll('ERROR')
                    secuencia_user.clear()

    elif current_state == state_explotada:
        if isEvent == True:   #Se disminuye el temporizador
            isEvent = False
            if eventData == 'T': # Evento de touch el logo para reiniciar
                tiempo = 20
                display.scroll('AGAIN')
                current_state = state_confi  #Vuelve a confi

def tareaEventos():
    global isEvent
    global eventData
    
    if button_a.was_pressed():   #Se disminuye el temporizador
        isEvent = True
        eventData = 'A'

    if button_b.was_pressed():   #Se disminuye el temporizador
        isEvent = True
        eventData = 'B'            

    if accelerometer.was_gesture('shake'):   #Se arma la bomba
        isEvent = True
        eventData = 'S'

    if pin_logo.is_touched():
        isEvent = True
        eventData = 'T'
        
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('A'):
                isEvent = True
                eventData = 'A'
            if data[0] == ord('B'):
                isEvent = True
                eventData = 'B'
            if data[0] == ord('S'):
                isEvent = True
                eventData = 'S'
            if data[0] == ord('T'):
                isEvent = True
                eventData = 'T'
            
while True:
    tareaEventos()
    tareaBomba()
```
