
### <p align="center"> Micro:bit</p>

### Entradas
1. **USB connector:** permite descarga programas al micro:bit desde un pc y así alimentarlo mediante la conección USB.
2. **Microphone:** permite crear programas que reaccionen a sonidos altos y bajos, también medir los niveles de ruido con el micrófono integrado. El LED del micrófono muestra cuándo el micrófono está recibiendo los sonidos. Justo a la izquierda del LED, hay un huequito pequeño por donde entra el sonido.
3. **Touch logo:** permite ser un input extra. El logotipo también funciona como un sensor táctil. Se puede usar como un botón extra.
4. **Compass and accelerometer:** el acelerómetro mide las fuerzas en 3 dimensiones, incluida la gravedad, para poder saber en qué dirección se está moviendo micro:bit. El Compass permite medir campos magnéticos en tres dimensiones, encontrar el Norte magnético utilizando la brújula. 

### Salidas
1. **Speaker:** permite añadir música y nuevos sonidos a los proyectos con mayor facilidad. Se pueden reproducir notas musicales y voices.
2. **25 LED lights:** forman un display de 5x5 para mostrar imágenes, palabras y números. También pueden actuar como sensores, midiendo cuánta luz cae sobre el micro:bit.
3. **Radio and Bluetooth antena:** puede comunicarse con otros micro:bits por radio, y con otros dispositivos mediante Bluetooth, por lo que envia ondas de radio para lograrlo.
4. **Yellow USB Led:** es una luz LED amarilla, que parpadea cuando el ordenador se está comunicando con el micro:bit a través de USB.

### <p align="center">Funciones Micropython</p>
### Entradas
**Botones A y B:** los botones A y B se pueden usar para configurar acciones en el display, en este caso al recibir el input del click en el botón se proyecta en scroll la letra correspondiente al botón.
```python
from microbit import *
import radio
while True:
    if button_a.was_pressed():
        display.scroll('A')
    if button_b.was_pressed():
        display.scroll('B')
```
**Captar intensidades por el micrófono:** el micrófono como input puede ser usado para captar intensidades y así programar acciones dependiendo del sonido. En este caso cuando hay sonido el display muestra una carita feliz y cuando hay silencio muestra una triste.
```python
from microbit import *
while True:
    if microphone.current_event() == SoundEvent.LOUD:
        display.show(Image.HAPPY)
    elif microphone.current_event() == SoundEvent.QUIET:
        display.show(Image.SAD)
```
**Recibir mensajes por radio:** por medio de la antena de radio, el micro:bit puede recibir mensajes de otro micro:bit que esté sincronizado en el mismo canal. Esto de recibir mensajes se pone en un loop, para poder estar checkeando constantemente cuando ingrese una onda (mensaje).
```python
import radio
while True:
    radio.config(group=23)
    radio.on()
    while True:
        message = radio.receive()
        if message:
            display.scroll(message)
```
https://github.com/user-attachments/assets/d1096bb3-9095-455b-a8dd-cb9aa82b4eda

### Salidas
**Crear imagenes propias en el display:** los LED's del display permiten cambiar su intensidad, entonces se reprensenta con un número entre el 0 (apagado) y 9 (lo más birllante). 
```python
from microbit import *
while True:
    display.show(Image('97530:'
                       '97530:'
                       '97530:'
                       '97530:'
                       '97530'))
```
**Reproducir sonidos por el speaker:** el speaker permite resporducir canciones/melodias predeterminadas, una de ellas es WEDDING.
```python
from microbit import *
import music
while True:
    music.play(music.WEDDING)
    sleep(1000)
```
**Comunicarse con otro micro:bit:** la antena de radio permite conectarse a una grupo, que es como sintonizarse a un canal de radio, luego se debe encender el radio y así enviar mensajes por este como un string.
```python
from microbit import *
import radio
while True:
    radio.config(group=23)
    radio.on()
    radio.send('hello Salo')  
    sleep(1000)
    radio.send('I see youuu')  
    sleep(1000)
```
