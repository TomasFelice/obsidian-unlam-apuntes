---
tipo: clase
fecha: 2026-09-08
tema: "Sistemas de tiempo real y FreeRTOS"
fecha_original: 2026-08-18
fecha_fuente: nombre de capturas
fecha_inferida: true
fechas_contenido:
  - 2026-09-08
  - 2026-09-15
---

> [!note] Material de varias fechas
> Las capturas corresponden a 2026-09-08 y 2026-09-15. El campo `fecha` usa la primera; `fechas_contenido` registra todas.

# Sistemas de Tiempo Real

## Ejemplos

![[Pasted image 20260908195504.png]]

## ¿Qué tienen en común?

- Llegan pedidos que deben ser atendidos
- Rígidas limitaciones de tiempo de atención
- Pueden procesar datos; lo distintivo es cumplir los plazos de respuesta.
- Tiempos de respuesta prefijados
> **Sistema de tiempo real embebido**

## Concepto de tiempo

- La exactitud de un sistema no depende únicamente de la lógica del resultado sino también de cuando es producido
- La medida del tiempo debe ser igual a la del tiempo externo que controla

## STR

> Es aquel al que se le solicita que reaccione ante estímulos del entorno en intervalo de tiempo dictados por el entorno
> No solo requiere que los resultados calculados sean correctos, sino que también esos resultados se produzcan dentro de un período de tiempo determinado

El requisito que los distingue es temporal; pueden realizar procesamiento de información intensivo.
![[Pasted image 20260908195822.png]]

## Características de los embebidos ilustrados en clase

Estas características describen ejemplos de plataforma, no la definición de todo sistema de tiempo real.
- Único propósito
	- Sistema dedicado
	- Atención inmediata
- Tamaño pequeño
	- Sistema integrado
	- Menos de 1MB de memoria
	- Procesador de 8 a 16 bits
- Bajo costo y producción en masa
	- SOC (System on a Chip)
- Requisitos de temporización específicos

## Sistema orientado a BUS

![[Pasted image 20260908200053.png]]
> Desventajas:
> - Latencias por el tiempo de transporte
> - El espacio que ocupa

## System-on-a-Chip

![[Pasted image 20260908200143.png]]
> SoC: integra diversos subsistemas en un mismo circuito integrado; no equivale a una placa completa.

## Requisitos específicos de temporización

![[Pasted image 20260908200238.png]]
HARD: incumplir un plazo constituye un fallo del sistema; no significa simplemente ejecutar lo más rápido posible.

## Limitaciones de los STR

![[Pasted image 20260908200532.png]]

### Multitarea

![[Pasted image 20260908200602.png]]

## Planificación basada en prioridades

Las tareas listas compiten según prioridades. En planificación apropiativa, una tarea de mayor prioridad puede interrumpir a la que ejecuta; analizar también bloqueos sobre recursos.

![[Pasted image 20260908215133.png]]
![[Pasted image 20260908215140.png]]

![[Pasted image 20260908215251.png]]
![[Pasted image 20260908215413.png]]
![[Pasted image 20260908215458.png]]

## Características deseables

![[Pasted image 20260908215633.png]]
![[Pasted image 20260908215731.png]]
![[Pasted image 20260908215825.png]]

## Parámetros de una tarea

Distinguir instante de activación, tiempo de cómputo, período y plazo límite. Ver el ejemplo numérico del complemento.

![[Pasted image 20260908220014.png]]
![[Pasted image 20260908220052.png]]

## Implementando SO de Tiempo Real

![[Pasted image 20260908220128.png]]

## Conceptos básicos

![[Pasted image 20260908220238.png]]

## Minimización de latencia

![[Pasted image 20260908220313.png]]

## Latencia de interrupción

Tiempo desde la petición de interrupción hasta el inicio de su atención; puede crecer por secciones que enmascaran interrupciones.

![[Pasted image 20260908220339.png]]

## Latencia del dispatcher

Tiempo necesario para ceder la CPU y comenzar o reanudar la tarea seleccionada.

![[Pasted image 20260908220356.png]]

## Planificación apropiativa

![[Pasted image 20260908220452.png]]

![[Pasted image 20260908220523.png]]

## Kernels apropiativos

![[Pasted image 20260908220544.png]]

## Tipos de planificadores de tiempo real

![[Pasted image 20260908220605.png]]
![[Pasted image 20260908220624.png]]

## Tipos de activación

Periódica: a intervalos; aperiódica: sin patrón regular; esporádica: con separación mínima entre activaciones bajo el modelo analizado.

![[Pasted image 20260908220805.png]]
![[Pasted image 20260908220819.png]]
![[Pasted image 20260908220848.png]]

![[Pasted image 20260908220907.png]]
![[Pasted image 20260908220928.png]]
![[Pasted image 20260908220956.png]]
![[Pasted image 20260908221013.png]]
![[Pasted image 20260908221035.png]]
![[Pasted image 20260908221049.png]]

---

# FreeRTOS

> Es un SO de tiempo real

![[Pasted image 20260915174812.png]]
- Kernel abierto con documentación y recursos del proyecto FreeRTOS.
- Código abierto
- Sencillo de implementar
- Disponible para numerosas familias de microcontroladores.
- Liviano
- Ofrece un kernel y puertos para distintas plataformas.
Características:
![[Pasted image 20260915175200.png]]
![[Pasted image 20260915180615.png]]
![[Pasted image 20260915180656.png]]
![[Pasted image 20260915180806.png]]

---

## Complemento de estudio

### Tiempo real y planificación

La corrección exige resultado correcto **y plazo cumplido**. Un sistema hard considera el incumplimiento un fallo; uno soft tolera degradación. Un sistema firm puede descartar un resultado tardío aunque tolere algunos incumplimientos.

Para una tarea periódica distinguir **período T**, **tiempo de cómputo C** y **deadline D**. Ejemplo: muestrear cada 20 ms, requerir hasta 3 ms de CPU y terminar antes de los siguientes 20 ms. La utilización C/T = 0,15 no demuestra por sí sola que todo el sistema sea planificable: influyen bloqueos, prioridades e interrupciones.

Tiempo real no exige 8/16 bits ni menos de 1 MB: son ejemplos de plataformas, no condiciones de la definición. Un RTOS ofrece mecanismos de planificación; el diseño debe acotar los tiempos.

En FreeRTOS, evitar espera activa, seleccionar primitivas según contexto y considerar inversión de prioridades. Un mutex puede ofrecer herencia de prioridad; un semáforo binario no equivale a un mutex.
