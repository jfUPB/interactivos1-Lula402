<p align= center> Enviar por el puerto serial desde el Microbit </p>
<p align= center> Experimento </p>

#### ¿Qué bytes se enviarían por el puerto serial?
Por el puerto serial se enviarían las parejitas de HEX correspondientes a cada CHAR:

```39 36 39 2c 36 35 32 2c 54 72 75 65 2c 46 61 6c 73 65 0a```

=

``` 9  6  9  ,  6  5  2  ,  T  R  U  E  ,  F  A  L  S  E  \n```

Cada parejita representa un número o una letra (char), cada parejita es de 8 bits, osea 1 byte.

```py
# Imports go at the top
from microbit import *

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if button_a.was_pressed():
        xValue = 969
        yValue = 652
        aState = True 
        bState = False
        data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
        uart.write(data)
```





<p align= center> Preguntas </p>

#### 1. ¿Qué información se está enviando?
Se está enviando la info que hay en data, es decir: xValue, yValue, aState,bState.

#### 2. ¿Cómo se está enviando?
Se está enviando porque si se mueve el Micribit o si se presionan los botones, entonces ese valor se almacena en las variables xValue, yValue, aState, bState.

Esta parte del código significa:

``` py
"{},{},{},{}\n".format(xValue, yValue, aState,bState)
```
Que los valores de xValue, yValue, aState, bState, los estoy mostrando en {},{},{},{} respectivamente y con un salto de linea al final \n, para que cada nuevalectura de esos 4 valores se muestre en el siguiente renglón. Se están convirtiendo esos valores a un String.

#### 3. ¿Qué puedes inferir de la estructura de los datos?
Que es mucho más sencilla que convertir esos valores a un string con JSON, como que toma más espacio y escritura que tan solo hacer lo de esta forma.

#### 4. ¿Por qué se separan los datos con comas y se termina con un salto de línea?
Porque de no ser así, se estaría viendo una linea de corrido en el puerto serial y seria demasiado enredado.

#### 5. ¿Qué crees que pasaría si no se separan los datos con comas y no terminan con un salto de línea?

Sin comas ni salto de linea:

***-8592TrueFalse-16384FalseFalse***

Con comas y salto de linea: 

***-8,592,True,False*** </p>
***-16,384,False,False***

#### 6. Para qué crees que se usa la función sleep(100)? ¿Qué pasaría si no se usara?
Creo que las iteraciones serían muy rápidas y podría pasar que se vuelva a enviar/recibir el mismo valor de la vuelta anterior pues porque ni siquiera ha habido tiempo de mover o presionar el Microbit.
Sleep(100) pausa el código por 100ms, eso quiere decir que el código da 10 vueltas por segunto, porque ***100 x 10 = 1000ms = 1s***

Si cambiamos sleep(100) a sleep(500), Entonces se ejecutaría 2 veces por segundo, porque ***500ms + 500ms = 1000ms = 1s*** y esto haría que corriera más lento.

#### 7. Observa cómo cambian los valores de xValue y yValue a medida que el micro:bit se inclina hacia la izquierda, derecha, adelante y atrás. ¿Qué valores toman xValue y yValue en cada caso?
xValue y yValue en cada caso toman los valores del acelerómetro del Microit que mide la aceleración. A medida que se mueve el Microbit, entonces esos valores cambian de número.

**xValue:** aceleración en X

**yValue:** aceleración en Y

#### 8. ¿Qué valores toman aState y bState cuando presionas los botones A y B?
aState y bState toman los valores de TRUE cuando el botón se presiona.
Cuando los botones están sin presionar entonces toman el valor de FALSE

#### 9. Observa qué ocurre si en vez de is_pressed() usas was_pressed(). ¿Qué diferencias encuentras?
La diferencia es que con ***is_pressed()*** envia tantas vueltas TRUE mientras que esté presionado, mientras que con ***was_pressed()*** no se envía en cada vuelta el TRUE sino solo una vez, porque está analizando es si "fue presionado" y "si, si fue presionado, te envio un TRUE"
