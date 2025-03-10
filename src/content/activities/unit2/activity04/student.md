### Manipulando Entradas Digitales
#### Experimento 1
##### ¿Qué querías comprobar?
Quería comprobar que lo que pasaba en el display era coordinado con la acción de presionar los botones.
##### ¿Cuál fue tu hipótesis?
Al presionar ambos botones alternadamente, el display va a proyectar un corazón que parecerá palpitando. Al sacudir el Microbit, este se pondrá triste, porque su display mostrará una carita trsite.
##### Los códigos involucrados en el experimento
``` python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        display.show(Image.HEART)
    if button_b.is_pressed():
        uart.write('B')
        display.show(Image.HEART_SMALL)
    if pin_logo.is_touched():
        display.show(Image.HAPPY)
        sleep(500)
    if uart.any():
        data = uart.read(1)
```
##### Descripción de lo resultados
Al presionar el botón A el display mostró un corazón grande, al presionar el botón B el display mostró un corazón pequeño, ambos sin demorarse un tiempo en hacer la transisión entre si. Al presionar el touch (logo) el display mostró una carita feliz como se esperaba.
##### Análisis de esos resultados
Los resultados fuerone exitosos. Quitar en el código el sleep entre acciones con los botones A y B, permitió que el display simulara un corazón palpitando sin retrasos.
##### Conclusiones
La hipotesis fue verdadera, se cromprobó los beneficios creativos de poder usar ambos botones y se cumplió con exito lo esperado del experimento, que era investigar e intentar.

#### Experimento 2
##### ¿Qué querías comprobar?
Quería comprobar si al realizar operaciones en el código, el resultado se podría mostrar en el display de la pantalla para simular un score.
##### ¿Cuál fue tu hipótesis?
Al presionar A el microbit sumará 1 a la variable "score" y mostrará el resultado en el display, al presionar B el microbit restará 1 a la variable "score" y mostrará el resultado en el display. Al presionar el logo touch el display pasará en scroll un letrerito que diga "Score".
##### Los códigos involucrados en el experimento
``` python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)
score = 0
while True:
    if button_a.is_pressed():
        uart.write('A')
        score += 1
        display.scroll(score)       
    if button_b.is_pressed():
        uart.write('B')
        score -= 1
        display.scroll(score) 
    if pin_logo.is_touched():
        display.scroll('score')
        sleep(500)
    if uart.any():
        data = uart.read(1)
```
##### Descripción de lo resultados
Al presionar el botón A el microbit sumó 1 a la variable "score", que iniciaba en 0, y en el display se mostró el resultado de la operación. Al presionar el botón B el microbit restó 1 a la variable "score", que iniciaba en 0, y en el display se mostró el resultado de la operación. Al presionar el logo touch el display pasó en scroll un letrerito que dice "Score".
##### Análisis de esos resultados
Los resultados fueron acertados respecto a la hipotesis. El display de el Microbit quedó simulando un tablero que dice la palabra "score", que mantiene track del score y que se incrementa o aumenta con el input de los botones.
##### Conclusiones
La hipotesis fue verdadera, se cromprobó los beneficios creativos de poder usar operaciones matemáticas dentro del código y se cumplió con exito lo esperado del experimento, que era investigar e intentar.
