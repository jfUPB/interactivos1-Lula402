### 1.
Se ve de esa manera porque yo le estoy pidiendo especificamente al receptor (la app web) que me muestre las cosas que recibe en texto.

<img width="150" alt="image" src="https://github.com/user-attachments/assets/713a0aab-a780-4346-ba6b-62233f738250" />

### 2.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/cae8dcea-683d-451b-8d5a-b7690b13f3c3" />

Eso aún es ASCII, porque si fuera binario estaría viendo

2 bytes de valueX = 4 bits
2 bytes de valueY = 4 bits
1 byte de A = 2 bits
1 byte de B = 2 bits
**TOTAL=** 12 bits (6 bytes)

### 3. 

#### Ventajas:
1. Es más corto en binario que en ASCII, entonces es más eficiente la comunicación.
2. Como ya estaría en binario estaría listo para la máquina sin tener que traducirlo de ASCII a binario.

#### Desventajas:
1. Al momento de necesitar entender, hacer experimentos o probar nuevas cosas, va a ser un tris más dificl porque es más complicado de interpretar que el ASCII.

### 4.
<img width="500" alt="image" src="https://github.com/user-attachments/assets/bebe07ee-883a-4c53-bef1-f11f389a00c1" />

Se están enviando 20 bits, es decir, 10 bytes por segundo:
```
2d 35 36 2c 31 36 34 2c 46 61 6c 73 65 2c 46 61 6c 73 65 0a
```
Lo anterior significa:
```
- 5 6 , 1 6 4 , F a l s e , F a l s e
```

La verdad aún no veo relación con el formato ***'>2h2B'***, porque aún el receptor está poniendo todo en HEX de ASCII. Se supone que en ***'>2h2B'*** debería estar viendo 12 bites y ahí identifico que se están enviando 20 bits

### 5.
En el formato ***'>2h2B'*** el bite más grande, que es el 1ero por big endian, es quien dice si el número es negativo o positivo. Si es 0 es + y si es 1 es -.

### 6. 
<img width="500" alt="image" src="https://github.com/user-attachments/assets/189c910e-15f5-42b3-90ce-d43c6ca0b815" />

#### Ventajas binario en lugar de texto en ASCII:
1. Es lo ideal para comunicación entre máquinas.
2. lo que un número en binario pueden ser 2 bytes en ASCII definitivamente siempre será más.

#### Desventajas binario en lugar de texto en ASCII:
1. necesitamos sruck para manejarlos, en vez de solo una cadena.
2. Probablemente sea mucho más confuso que tan solo usar la tablita de ASCII.
   
#### Ventajas ASCII en lugar de binario:
1. No necesitamos saber esas reglas de binario que tuvimos que saber al inicio de este curso para manejar el ensamblador.
2. Mucho más legible.
   
#### Desventajas ASCII en lugar de binario:
1. Van a quedar mayor cantidad de bytes que los que habría en binario para decir la misma cosa.
2. A la máquina le toca hacer un pasito más para trabajar con esos datos en lenguaje máquina.
