#### Descripción del proceso
En el python editor de Microbit, modifiqué el código usando funciones como ***speech.say(' ')*** y  ***music.play(music.WEDDING)***. Cuando el botón A es presionado el microbit dice en speech "slow", luego espera con sleep 1s y seguido reproduce la canción de Wedding al tempo que viene por defecto. Cuando el botón B es presionado el microbit dice en speech "fast", luego espera con sleep 1s y seguido reproduce la canción de Wedding al tempo de 250 bpm.

https://github.com/user-attachments/assets/de0dc673-463c-480a-bcfc-90375d9a6078

#### Código Microbit python editor
```python
from microbit import *
import music
import speech

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        speech.say('Slow?')
        sleep(1000)
        music.play(music.WEDDING)            
        sleep(1000)
    if button_b.is_pressed():
        speech.say('Fast?')
        sleep(1000)
        music.set_tempo(bpm=250)           
        music.play(music.WEDDING)  
```
