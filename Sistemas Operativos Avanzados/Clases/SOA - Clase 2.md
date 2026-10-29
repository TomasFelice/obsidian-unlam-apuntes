---
tipo: clase
fecha: 2026-08-25
tema: "Electrónica básica, alimentación y conexión de sensores y actuadores"
fecha_original: 2026-08-18
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Introducción a la Electrónica

## Conceptos básicos

> Unir directamente los bornes de una pila produce un cortocircuito: la baja resistencia puede causar una corriente excesiva y calentamiento. Los componentes transfieren energía; no consumen electrones.

> Corriente: Cantidad de cargas por segundo en un circuito
> Voltaje: diferencia de potencial eléctrico, es decir, energía por unidad de carga; se mide en voltios.
![[Pasted image 20260825193436.png]]

> + -> ROJO
>  - -> NEGRO

![[Pasted image 20260825193548.png]]

## Componentes electrónicos

![[Pasted image 20260825193625.png]]

La conexión de fuentes o baterías depende de la tensión y capacidad requeridas y de su compatibilidad; no deben ponerse siempre en serie.
Al poner en serie las fuentes, se incrementa el voltaje, pero no la corriente.
Al poner en paralelo las fuentes, se mantiene el voltaje, pero se incrementa la corriente.
> Que pasa que las fuentes son de distintos voltaje/corriente en ambos casos?

En serie:
- **Distinto voltaje ($V_1 \neq V_2$):**
    - **Comportamiento:** Los voltajes se suman directamente: $V_{\text{total}} = V_1 + V_2$ (o se restan si se conectan con polaridad invertida).
    - **Consecuencia:** La suma es válida como cálculo ideal; la conexión real exige compatibilidad de las fuentes y respetar sus especificaciones. No mezclar baterías de distinta química, capacidad o estado de carga como regla de diseño.
- **Distinta capacidad de corriente ($I_{\text{máx }1} \neq I_{\text{máx }2}$):**
	- **Comportamiento:** Por leyes de Kirchhoff, la corriente es exactamente la misma en todo el lazo en serie ($I = I_1 = I_2$).
	- **Consecuencia:** La corriente máxima segura queda **limitada por la fuente más débil**. Si se exige más corriente de la que soporta la menor, esta se sobrecalienta o se quema. En baterías químicas, la de menor capacidad se agota primero y las demás comenzarán a forzar corriente a través de ella, provocando inversión de polaridad y daño irreversible.
En paralelo:
- **Distinto voltaje ($V_1 \neq V_2$):**
    - **Comportamiento:** **Es una configuración peligrosa y no recomendada.** Se produce una corriente parásita interna que fluye directamente desde la fuente de mayor voltaje hacia la de menor voltaje, limitada únicamente por sus resistencias internas ($R_{\text{int}}$):    $$I_{\text{circulante}} = \frac{V_1 - V_2}{R_{\text{int }1} + R_{\text{int }2}}$$
    - **Consecuencia:** Como $R_{\text{int}}$ suele ser de fracciones de ohm, circula una corriente muy elevada sin que haya carga conectada. Esto provoca sobrecalentamiento severo, descarga rápida, hinchazón de baterías o riesgo de fuego/explosión.
- **Distinta capacidad de corriente ($I_{\text{máx }1} \neq I_{\text{máx }2}$) con igual voltaje:**
    - **Comportamiento:** El voltaje se mantiene y la corriente total entregada a la carga es la suma de ambas ($I_{\text{total}} = I_1 + I_2$).
    - **Consecuencia:** El mismo voltaje nominal no garantiza compatibilidad. Conectar en paralelo solo fuentes previstas para compartir carga o baterías con el sistema de protección y gestión adecuado.

**Fuente de alimentación (continua)**
![[Pasted image 20260825195258.png]]
**Resistencia**
![[Pasted image 20260825195325.png]]
![[Pasted image 20260825195519.png]]
**Semiconductores**
![[Pasted image 20260825195602.png]]
> Los LEDs siempre van con una resistencia.
> La resistencia, depende del color, ya que cada color usa distinto ohmiaje.
> Se suele usar, para testing, 1 resistencia std de 1kOmh. No van a prender al máximo, pero sirve para testing

## Conexiones protoboard (wokwi)

![[Pasted image 20260825195915.png]]
> Respetar la convencion para el TP

![[Pasted image 20260825200009.png]]
> Cables horizontales y verticales. NO DIAGONALES.

## Leyes de electrónica

### Ley de Ohm

![[Pasted image 20260825200124.png]]
> Teniendo una fuente y una carga (resistencia en este caso). Esta ley, nos permite calcular la corriente del circuito, por ejemplo.

### Ley de Kirchhoff

![[Pasted image 20260825200226.png]]
> La corriente que entra en un circuito es la misma que sale.
![[Pasted image 20260825200826.png]]
![[Pasted image 20260825200920.png]]
![[Pasted image 20260825201210.png]]
![[Pasted image 20260825201223.png]]
> Si sigo agregando?

![[Pasted image 20260825201318.png]]
![[Pasted image 20260825201356.png]]
> Si se reinicia muchas veces, puede llegar a quemarse la placa.

## Como alimentar el circuito

![[Pasted image 20260825201550.png]]
![[Pasted image 20260825201723.png]]
![[Pasted image 20260825201941.png]]
> Si empezamos a agregar actuadores y sensores, nos vamos a quedar sin corriente disponible
![[Pasted image 20260825202209.png]]
![[Pasted image 20260825202252.png]]
> En circuitos sin aislamiento galvánico, las señales entre la placa y los periféricos necesitan una referencia GND común. No unir los positivos de fuentes distintas sin un diseño que lo permita. En circuitos aislados, revisar el esquema específico.

![[Pasted image 20260825203106.png]]
![[Pasted image 20260825203124.png]]
> Siempre dejar un margen de un 10% de la fuente.

![[Pasted image 20260825203737.png]]
![[Pasted image 20260825204258.png]]

## Tarea

![[Pasted image 20260825204536.png]]
1. Las cosas que estan mal son:
	- Observación del ejercicio: revisar la conexión GND de la ESP en la pista superior con el esquema original; no extrapolar esta observación a todos los circuitos.
	- En la pista inferior, se supera la corriente disponible (100mA disponible vs 123mA consumidos)
2. \[insertar link\]

## Divisor de voltaje (tensión)

![[Pasted image 20260825204826.png]]
![[Pasted image 20260825204835.png]]
![[Pasted image 20260825205219.png]]
![[Pasted image 20260825210341.png]]

![[Pasted image 20260825211710.png]]

## Ejemplos wokwi

### Conceptos teoricos y aclaraciones

> Ver video

Usar ESP32-devkit v1 [wokwi-esp32-devkit-v1 - Wokwi ESP32, STM32, Arduino Simulator](https://wokwi.com/projects/385332723752265729)

#### Consejos

1. Elegir sensores y actuadores a usar
2. Revisar el modelo
3. Buscar ejemplos y tutoriales en internet
4. Averiguar como funciona teoricamente el dispositivo
5. Averiguar si funciona con
	1. 5v o 3,3v
	2. Consumo de corriente
6. Buscar ejemplos de wokwi

### Funcionamiento del ultrasonido

> Usado para detectar distancia de un objeto
![[Pasted image 20260825212552.png]]
![[Pasted image 20260825212817.png]]
> Si no hay nada en frente, el sensor tiene una especie de timeout (38ms en este caso)
> Funciona con 5V
> Para conectarlo a la ESP32, hay que aplicar el **divisor de tensión**

### Funcionamiento de Transistor y Relé

![[Pasted image 20260825213253.png]]
> Son como una tecla de  luz. Permiten prender o apagar cosas
![[Pasted image 20260825213527.png]]
> Esto es un Relé. Funciona con una bobina por inductancia
> Algunos funcionan con 3,3V

![[Pasted image 20260825213644.png]]

### Motor DC

> Simulado con un led en wokwi

### Funcionamiento del Servomotor

![[Pasted image 20260825213750.png]]
Usa un PWM modificado
![[Pasted image 20260825213844.png]]
> Funcionan con 5V

### Sensor Pir

### Puente H

![[Pasted image 20260825214132.png]]
![[Pasted image 20260825214204.png]]
![[Pasted image 20260825214331.png]]

### Ejemplo combinado

---

# Revisión Propuesta TP

> PAra evitar usar corriente altera, podemos usar un cooler. Trabaja en tre 5 y  12v.

El cargador lo conectamos a 12 o 5v.
Relé habilita la corriente
El sensor de corriente (SC), mide cuanto consume el cooler
Cuando el SC supera el umbral, corta el relé
Con la tira led vamos indicando cuanto queda de consumo
Cuando cortamos el relé, el cooler dejaria de andar
Podemos agregar, por ejemplo, un pulsador, para que el cooler comience a consumir corriente.
![[Pasted image 20260825223757.png]]

Si quisieramos incorporar un cooler para refrigerar, deberiamos incorporar otro relé


Podriamos usar un potenciómetro para variar la intensidad del motor


en lugar del aro led, tiene más sentido usar un display

![[Pasted image 20260825224931.png]]
> El modelo del sensor de corriente debe confirmarse con la etiqueta o ficha técnica; el identificador original «ACS721» podría estar mal transcrito.

---

## Complemento de estudio

### Fórmulas básicas

- Corriente: I = ΔQ/Δt, medida en amperios.
- Tensión: V = ΔE/Q, medida en voltios.
- Ley de Ohm para un resistor: V = I · R.
- Potencia eléctrica: P = V · I.
- Divisor sin carga apreciable: Vsalida = Ventrada · R₂/(R₁ + R₂), tomando la salida sobre R₂.

Ejemplo: un LED con caída de 2 V y corriente objetivo de 5 mA, alimentado con 3,3 V, necesita aproximadamente R = (3,3 − 2)/0,005 = 260 Ω. Elegir un valor comercial y verificar corriente y potencia; el color por sí solo no determina la resistencia.

La corriente nominal de una fuente indica su capacidad, no cuánto «empuja» siempre al circuito. Verificar el consumo total, picos y capacidad de reguladores y GPIO. Un margen fijo del 10 % es una pauta de clase, no garantía universal.

**Pendiente:** la corrección del circuito de la tarea depende de su esquema. No quitar una masa común por una regla memorizada; identificar primero qué riel corresponde a cada tensión.
