### Código
```python
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
            display.set_pixel(self.redX, self.redY,9)
            # preparar el intervalo para el rojo
            self.interval = self.redInterval

        elif self.state == "WaitTimeoutRed":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.redX, self.redY, 0)
                display.set_pixel(self.yellowX, self.yellowY, 9)
                display.set_pixel(self.yellowX, self.yellowY,self.pixelState)
                self.state = "WaitTimeoutYellow"

        elif self.state == "WaitTimeoutYellow":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.yellowX, self.yellowY, 0)
                display.set_pixel(self.greenX, self.greenY, 9)
                display.set_pixel(self.greenX, self.greenY,self.pixelState)
                self.state = "WaitTimeoutGreen"

        elif self.state == "WaitTimeoutGreen":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.greenX, self.greenY, 0)
                display.set_pixel(self.redX, self.redY, 9)
                display.set_pixel(self.redX, self.redY,self.pixelState)
                self.state = "WaitTimeoutRed"

semaforo1 = Semaforo(0,1,5000,0,2,2000,0,3,3000,"Init")
    #def __init__(self,redX,redY,redInt,yellowX,yellowY,yellowInt, greenX,greenY,greenInt, initState):
semaforo2 = Semaforo(2,1,3000,2,2,1000,2,3,2000,"Init")
    #def __init__(self,redX,redY,redInt,yellowX,yellowY,yellowInt, greenX,greenY,greenInt, initState):
semaforo3 = Semaforo(4,1,4000,4,2,3000,4,3,2000,"Init")
    #def __init__(self,redX,redY,redInt,yellowX,yellowY,yellowInt, greenX,greenY,greenInt, initState):

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
```

### Reflexión
La ventaja principal de usar una clase para un programa como estos es que, se convierte en algo fácil de escalar, ya que tengo un tipo de objeto (semaforo) y quiero crear otros objetos (3 semaforos) que compartan las mismas características pero a su modo, es decir, herencia. De esta manera no tengo que hace un método Update para cada semáforo, sino que solo debo darle nuevos valores a los atributos de cada semáforo y él usará el método Update como los otros.

La técnica de programación basada en máquinas de estado, sirvió para manejar el tiempo de cada color del semáforo. Usando los intervalos y el tiempo actual en la máquina de estados, permitió que el semáforo estuviera ordenado y poniendole el tiempo que uno necesite a cada color. Además también lo hace escalable, ya que se pueden añadir más estados.
