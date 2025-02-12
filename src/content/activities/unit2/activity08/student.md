```python
from microbit import *  
import utime   #acá importa la biblioteca utime, para poder medir y manejar tiempos

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
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,4,0,500)

while True:
    pixel1.update()
    pixel2.update()
```
