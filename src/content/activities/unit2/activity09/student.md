Código completamente funcional.
``` python
from microbit import *
import utime

class Semaforo:
    def __init__(self,redX,redY,redInt,yellowX,yellowY,yellowInt, greenX,greenY,greenInt, initState):
        self.state = initState
        self.pixelState = 9
        self.startTime = 0
        self.interval = 300
        self.redX = redX
        self.redY = redY
        self.redInterval =redInt
        self.yellowX = yellowX
        self.yellowY = yellowY
        self.yellowInterval =yellowInt
        self.greenX = greenX
        self.greenY = greenY
        self.greenInterval =greenInt

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeoutRed"
            # encender el pixel del rojo
            display.set_pixel(2,1,9)
            # preparar el intervalo para el rojo
            self.interval = self.redInterval           
            
        elif self.state == "WaitTimeoutRed":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.redX, self.redY, 0) 
                display.set_pixel(self.yellowX, self.yellowY, 9) 
                display.set_pixel(2,2,self.pixelState)
                self.state = "WaitTimeoutYellow"
                
        elif self.state == "WaitTimeoutYellow":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.yellowX, self.yellowY, 0)
                display.set_pixel(self.greenX, self.greenY, 9) 
                display.set_pixel(2,3,self.pixelState)
                self.state = "WaitTimeoutGreen"
                
        elif self.state == "WaitTimeoutGreen":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.greenX, self.greenY, 0) 
                display.set_pixel(self.redX, self.redY, 9) 
                display.set_pixel(2,1,self.pixelState)
                self.state = "WaitTimeoutRed"

semaforo1 = Semaforo(2,1,1000,2,2,500,2,3,2000,"Init")
    #def __init__(self,redX,redY,redInt,yellowX,yellowY,yellowInt, greenX,greenY,greenInt, initState):

while True:
    semaforo1.update()

```

### Estados
1. Init
2. WaitTimeoutRed
3. WaitTimeoutYellow
4. WaitTimeoutGreen
### Eventos
**1. Init:** en este estado se evalúa que self.state se igual a "Init", es decir asegurandose que el semáforo está en el estado incial.

**2. WaitTimeoutRed:** en este estado se evalúa que self.state se igual a "WaitTimeoutRed", para preparar el pixel y el intervalo del rojo.

**3. WaitTimeoutYellow:** en este estado se evalúa que self.state se igual a "WaitTimeoutYellow", para preparar el pixel y el intervalo del amarillo.

**4. WaitTimeoutGreen:** en este estado se evalúa que self.state se igual a "WaitTimeoutGreen", para preparar el pixel y el intervalo del verde

### Acciones
**1. Init:** la acción es que, se captura el tiempo actual en milisegundos y se guarda en self.startTime. Luego el self.state se hace == a "WaitTimeoutRed". El pixel Red se enciende por 1era vez.

**2. WaitTimeoutRed:** analiza si la diferencia entre el tiempo actual y el tiempo anterior guardado es mayor al intervalo establecido del Yellow. Si lo anterior se cumple entonces el pixel Red se apaga y el yellow se prende.

**3. WaitTimeoutYellow:** analiza si la diferencia entre el tiempo actual y el tiempo anterior guardado es mayor al intervalo establecido del green. Si lo anterior se cumple entonces el pixel yellow se apaga y el green se prende.

**4. WaitTimeoutGreen:**  analiza si la diferencia entre el tiempo actual y el tiempo anterior guardado es mayor al intervalo establecido del red. Si lo anterior se cumple entonces el pixel green se apaga y el red se prende.
