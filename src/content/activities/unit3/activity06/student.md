### <p align= center> Vectores de Prueba - Bomba 3.0 </p>

### #1

**Estado:** config  → **Evento:** Configurar tiempo → **Estado esperado:** config

**Acciones esperadas:** Se muestra interfaz de configuración y permite ingresar tiempo.

**Resultado:** [X] Pasó

### #2

**Estado:** config → **Evento:** Confirmar tiempo (SHAKE) → **Estado esperado:** Armado

**Acciones esperadas:** Se almacena el tiempo ingresado y se inicia la cuenta regresiva.

**Resultado:** [X] Pasó

### #3

**Estado:** explotada → **Evento:** presionar touch → **Estado esperado:** config

**Acciones esperadas:** todo se reinicia a sus valores originales y vuelve a config.

**Resultado:** [X] Pasó


### #4


**Estado:** Armado → **Evento:** Reducción de tiempo → **Estado esperado:** Armado (Aún)

**Acciones esperadas:** Se actualiza el display con el tiempo restante.

**Resultado:** [X] Pasó

### #5

**Estado:** Armado → **Evento:** Introducir código correcto → **Estado esperado:** Desarm

**Acciones esperadas:** La cuenta regresiva se detiene y se muestra mensaje de que vuelve a config.

**Resultado:** [ ] Falló

**Motivo:** El sistema no reconoció correctamente el código de desactivación.

**Corrección:** Se revisó la validación de código, se corrigió la comparación de secuencias y se reintentó la prueba.

**Nuevo resultado:** [X] Pasó tras corrección.

### #6

**Estado:** Armado → **Evento:** Introducir código incorrecto → **Estado esperado:**  Armado (Aún)

**Acciones esperadas:** Se muestra mensaje de error y sigue la cuenta regresiva.

**Resultado:** [X] Pasó

### #7

**Estado:** Armado → **Evento:** Tiempo llega a cero → **Estado esperado:** Explotada

**Acciones esperadas:** Se activa la sim de explosión.

**Resultado:** [X] Pasó


