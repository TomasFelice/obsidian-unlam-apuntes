---
tipo: clase
fecha: 2026-08-18
tema: Tiempo Real + FreeRTOS
---
# Sistemas de Tiempo Real
## Ejemplos
![[Pasted image 20260908195504.png]]
## Que tienen en comun?
- Llegan pedidos que deben ser atendidos
- Rigidas limitaciones de tiempo de atencion
- No hay procesamiento de datos
- Tiempos de respuesta prefijados
> **Sistema de tiempo real embebido**

## Concepto de tiempo
- La exactitud de un sistema no depende unicamente de la logica del resultado sino tambien de cuando es producido
- La medida del tiempo debe ser igual a la del tiempo externo que controla
## STR
> Es aquel al que se le solicita que reaccione ante estimulos del entorno en intervalo de tiempo dictados por el entorno
> No solo requiere que los resultados calculados sean correctos, sino que tambien esos resultados se produzcan dentro de un periodo de tiempo determinado

La aplicacion principal NO es procesar informacion
![[Pasted image 20260908195822.png]]
## Caracteristicas principales
- Unico proposito
	- Sistema dedicado
	- Atencion inmediata
- Tamanio pequenio
	- Sistema intgrado
	- Menos de 1MB de memoria
	- Procesador de 8 a 16 bits
- Bajo costo y produccion en masa
	- SOC (System on a Chip)
- Requisitos de temporizacion especificos

## Sistema orientado a BUS
![[Pasted image 20260908200053.png]]
> Desventajas:
> - Latencias por el tiempo de transporte
> - El espacio que ocupa

## System-on-a-Chip
![[Pasted image 20260908200143.png]]
> Todo incluido en la misma placa (circuito integrado)

## Requisitos especificos de temporizacion
![[Pasted image 20260908200238.png]]
HARD -> Lo mas rapido posible
## Limitaciones de los STR
![[Pasted image 20260908200532.png]]

### Multitarea
![[Pasted image 20260908200602.png]]

## Planificacion basada en prioridades
![[Pasted image 20260908215133.png]]
![[Pasted image 20260908215140.png]]

![[Pasted image 20260908215251.png]]
![[Pasted image 20260908215413.png]]
![[Pasted image 20260908215458.png]]

## Caracteristicas deseables
![[Pasted image 20260908215633.png]]
![[Pasted image 20260908215731.png]]
![[Pasted image 20260908215825.png]]

## Parametros de una tarea
![[Pasted image 20260908220014.png]]
![[Pasted image 20260908220052.png]]

## Implementando SO de Tiempo Real
![[Pasted image 20260908220128.png]]
## Conceptos basicos
![[Pasted image 20260908220238.png]]

## Minimizacion de latencia
![[Pasted image 20260908220313.png]]
## Latencia de interrupcion
![[Pasted image 20260908220339.png]]
## Latencia del dispatcher
![[Pasted image 20260908220356.png]]
## Planificacion apropiativa
![[Pasted image 20260908220452.png]]

![[Pasted image 20260908220523.png]]

## Kernels apropiativos
![[Pasted image 20260908220544.png]]

## Tipos de planificadores de tiempo real
![[Pasted image 20260908220605.png]]
![[Pasted image 20260908220624.png]]

## Tipos de activacion
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
- Mantenido actualmente por amazon(AWS)
- Codigo abierto
- Sencillo de implementar
- Optimizado para muchos microcontroladore
- Liviano
- Tiene una base std que puede ser adaptada a cada plpataforma
Caracteristicas:
![[Pasted image 20260915175200.png]]
![[Pasted image 20260915180615.png]]
![[Pasted image 20260915180656.png]]
![[Pasted image 20260915180806.png]]
