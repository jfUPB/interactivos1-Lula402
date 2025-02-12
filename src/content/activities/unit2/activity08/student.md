**¿Puedes identificar algún estado?**  Hay dos estados en el programa. Init: es el estado inicial del pixel, en este estado se espera a capturar y alamacenar el tiempo que el programa lleva corriendo.

**¿Puedes identificar algún evento?** Hay dos eventos en este programa. Spregunta si el estado del pixel es 0, osea apagado o se pregunta si el estado es 9, que el pixel está encendido.

**¿Puedes identificar alguna acción?** Hay dos acciones, si el pixel esta en 0 (evento) entonces se cambia a 9, esa es la acción en respuesta de la pregunta del evento. Si el pixel esta en 9 (evento) entonces se cambia a 0, esa es la acción en respuesta de la pregunta del evento. Aunque estas acciones dependen del intervalo establecido del pixel.

### ¿cómo funciona?
```python
from microbit import *  
import utime                          #acá importa la biblioteca utime, para poder medir y manejar tiempos

class Pixel:   #Se creó la clase llamada pixel
    def __init__(self,pixelX,pixelY,initState,interval):  #Se crea un constructor parametrizado llamado init
        self.state = "Init"           #es un atributo, que representa el estado del pixel, que en este caso se define inicialmente como "Init"
        self.startTime = 0            #El milisegundo en el que inicia
        self.interval = interval      #Es el tiempo en milisegundos para alternar el estado del píxel, osea el initState.
        self.pixelX = pixelX          #Coordenada del pixel en x
        self.pixelY = pixelY          #Coordenada del pixel en y
        self.pixelState = initState   #initState es el estado del píxel, brillo 0 (apagado) o 9 (full encendido).

    def update(self):                 #es un método llamado update, que permite que el pixel parpadee y actualice su estado.

        if self.state == "Init":      #Como al crear la clase pixel, se definió el atributo self.state como Init, esto se cumple
            self.startTime = utime.ticks_ms()  #utime.ticks_ms() captura el tiempo actual y ese resultado se almacena en self.startTime, el cual inició en 0
            self.state = "WaitTimeout" #se cambia el estado del pixel a "WaitTimeout", para así saber que no es la 1ra vez que se usa el método update
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState) #Dibuja el pixel en el display, con sus respectivas coordenadas y brillo

        elif self.state == "WaitTimeout":   #La siguiente parte controla el parpadeo del pixel
                                            #Sino se cumplió el if, si el estado del pixel está en "WaitTimeout", se ejecuta lo siguiente:
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval: #utime.ticks_diff sacá la diferencia entre: utime.ticks_ms - self.startTime = unos ms, entonces si ese resultado es mayor que el intervalo establecido, se cambia el estado del pixel a continuación.
                self.startTime = utime.ticks_ms()  #El tiempo actual se vuelve a guardar self.startTime
                if self.pixelState == 9:           #Este condicional evalua si el pixel está encendido, si sí está encendido entonces:
                    self.pixelState = 0            # Poner el estado del pixel en 0, osea apagarlo
                else:                              # Sino está en estado 9, eso quiere decir que estaba en estado 0, entonces se hace lo contrario que es encenderlo (9). 
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState) # Se ponen las coordenadas y estado en el que se va a mostrar el pixel

pixel1 = Pixel(0,0,0,1000)                         #Se crea un obejto tipo pixel, llamado pixel1, se inicia en 0, esta en
                                                   #las coordenadas (0,0), el intervalo de tiempo de 1000ms
pixel2 = Pixel(4,4,0,500)                          #Se crea un obejto tipo pixel, llamado pixel2, se inicia en 0, esta en
                                                   #las coordenadas (4,4), el intervalo de tiempo de 500ms

while True:                                        #Ciclo infinito
    pixel1.update()                                #El pixel1 corre el método update, para poder parpadear
    pixel2.update()                                #El pixel2 corre el método update, para poder parpadear
```
