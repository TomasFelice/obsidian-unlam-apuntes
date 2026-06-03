---
tipo: clase
fecha: 2026-05-13
tema: Computacion de altas prestaciones
---
 Computacion de Altas Prestaciones (HPC)
![[Pasted image 20260513192706.png]]
## Introduccion
### Concurrencia vs Paralelismo
![[Pasted image 20260513192733.png]]
### Necesidad de paralelismo
![[Pasted image 20260513192923.png]]
![[Pasted image 20260513193042.png]]
> MapReduce: es un modelo de programación (y un framework de procesamiento) diseñado para procesar y analizar volúmenes masivos de datos (Big Data) de forma paralela y distribuida a través de un clúster de computadoras. *"dividir un trabajo gigante en miles de tareas pequeñas, ejecutarlas al mismo tiempo en distintas máquinas y luego juntar los resultados sin que todo colapse"*

![[Pasted image 20260513193402.png]]

![[Pasted image 20260513193538.png]]

![[Pasted image 20260513193632.png]]

### Evolucion de Paralelismo en Monoprocesadores
![[Pasted image 20260513193719.png]]
### Paralelismo en multiprocesadores
> + es mejor...

## Taxonomia de Flynn
> Define cuantas instrucciones e puede ejecutar sobre los datos

![[Pasted image 20260513194140.png]]

- SISD: Simple Instruction Simple Data
- SIMD: Simple Instruction Multiple Data
- MISD: Multiple Instruction Simple Data
- MIMD: Multiple Instruction Multiple Data
### SISD
![[Pasted image 20260513194244.png]]
### SIMD
![[Pasted image 20260513194258.png]]
### MISD
![[Pasted image 20260513194358.png]]
### MIMD
![[Pasted image 20260513194616.png]]
#### Paradigmas
![[Pasted image 20260513194706.png]]
![[Pasted image 20260513194922.png]]
![[Pasted image 20260513195123.png]]
![[Pasted image 20260513195403.png]]
![[Pasted image 20260513195416.png]]
![[Pasted image 20260513195521.png]]
## Estrategias de Paralelismo
### Paradigmas
#### Divide y venceras
![[Pasted image 20260513195558.png]]
![[Pasted image 20260513195726.png]]
![[Pasted image 20260513195739.png]]
##### MapReduce
![[Pasted image 20260513195920.png]]
### Metricas de rendimiento
#### Medidas de prestaiones en algoritmos paralelos
![[Pasted image 20260513200718.png]]
##### SpeedUp
> Que tan rapida es la version paralela en comparacion con la secuencial

![[Pasted image 20260513200940.png]]
##### Eficiencia
> Normaliza la ganancia por la cantidad de procesadores que se usaron

![[Pasted image 20260513201032.png]]
##### Coste
> Tiempo realizado por todo el sistema en la resolucion del problema

![[Pasted image 20260513202118.png]]
##### Funcion Overhead
> Diferencia entre Coste y tiempo secuencial. Mientras mayor es, peor es el comportamiento paralelo

![[Pasted image 20260513202233.png]]

## GRID
- Sistema heterogeneo con multiples SO
- Equipos dispersos geograficamente
- Mejora el rendimiento compartiendo recursos subutilizados de otros equipos
- Cada nodo funciona de forma independiente
![[Pasted image 20260513202440.png]]
## CLUSTER
![[Pasted image 20260513202902.png]]
> Por que el cluster es tan importante ahora?

![[Pasted image 20260513203257.png]]
## Cloud Computing
![[Pasted image 20260513203436.png]]
### Riesgos par