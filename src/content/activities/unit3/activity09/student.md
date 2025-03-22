### <p align=center> Vectores de prueba </p>
#### Vector 1
**Estado:** config → **Evento:** Configurar tiempo → **Estado esperado:** config
**Acciones esperadas:** Se muestra la interfaz de configuración y permite ingresar tiempo.
**Resultado:** [X] Pasó
#### Vector 2
**Estado:** config → **Evento:** Shakear → **Estado esperado:** armada
**Acciones esperadas:** Se guarda el tiempo configurado y el sistema inicia la cuenta regresiva.
**Resultado:** [X] Pasó
#### Vector 3
**Estado:** armada → **Evento:** pendiente de inputs → **Estado esperado:** armada
**Acciones esperadas:** Se inicia la cuenta regresiva en la pantalla y el se monitorea eventos externos.
**Resultado:** [X] Pasó
#### Vector 4
**Estado:** armada → **Evento:** Tiempo llega a cero → **Estado esperado:** explotada
**Acciones esperadas:** Se activa la muestra de "BOOM".
**Resultado:** [X] Pasó

### Fuentes de Eventos
#### Desde el micro:bit
1. Botón A presionado → Se envía ‘A’ por UART.
2. Botón B presionado → Se envía ‘B’ por UART.
3. Shake → Se envía ‘S’ por UART.
4. Touch en el logo → Se envía ‘T’ por UART.

#### Desde p5.js
1. Evento de recepción de UART → Desde el Micro:bit.
2. Botón digital A presionado
3. Botón digital B presionado
4. Botón digital S presionado
5. Botón digital T presionado


### <p align=center> Pruebas de regresión </p>
| Prueba | Descripción | Resultado | Corrección |
|--------|------------|-----------|------------|
| 1 | Presionar botón A | Correcto | N/A |
| 2 | Presionar botón B | Correcto | N/A |
| 3 | Presionar botón S | Falló: No se armaba | Se corrigió la forma en que se registraba el True |
| 4 | Presionar botón T | Correcto | N/A |
| 5 | Agitar micro:bit | Correcto | N/A |
| 6 | Presionar A y B muy rápido | Falló: Solo se registró un botón | Es una limitación del sistema físico |
| 7 | Agitar repetidamente | Falló: Se desarmaba y armaba de una | Se implementó un nuevo estado de desarmada de por medio |

