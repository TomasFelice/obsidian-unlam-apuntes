---
tipo: clase
fecha: 2026-05-13
tema: Computacion de altas prestaciones
---
# MIMD Paradigmas
- Memoria compartida -> Multiples CPU consumen la misma memoia
- Memoria distribuida -> Cada cpu tiene su espacio de memoria, y se comunican con otros cpu mediante una red (lan, wan, etc.). Cada CPU incluso puede tener un SO distinto.
Partiendo desde memoria distribuida podemos ahondar en conceptos como Grid (no compuadoras homogeneas) o Cluster (computadora homogeneas)
Grid -> No asegura que tengas la misma capacidad de computo
Cluster -> A priori si. Es lo que mas se usa.
# Paradigmas de computacion paralela
> Partiendo de que estamos en un **cluster**

*"Dividir es mejor"*
La idea es dividir la problematica en subproblemas mas chicos.
> MapReduce (Es un divide y venceras):
> - Tenemos un nodo Master que coordina los workers
> - Los workers hacen procesamiento puro (Map)
> - Se juntan los resultados con una fase de Reduce

# Metricas
- SpeedUp
	- Velocidad secuencial / Velocidad paralela -> Si el programa paralelo es mas rapido o no
- Eficiencia
	- SpeedUp / Cant nucleos -> Cuanto estas aprovechando los nucleos. Mas cercano a 1 es mejor
- Coste
	- nro de cpus * tiempo del algoritmo -> El computo total realizado
- Funcion Overhead
	- Coste - tiempo secuencial -> mientras mayor es, quiere decir que es peor el comportamiento paralelo
# Cloud computing
Pasar computo *in house* hacia computo consumido a traves de internet
Hay multiples servicios segun el fin.
- pay-per-use
- capacidad elastica
- recursos virtualizados (heterogeneidad)
- el usuario desconoce ubicacion fisica de los recursos
## Riesgos
Donde estan los datos? Sobre todo los sensibles
Confidencialidad
Que legislacion aplica ante un conflicto?
Con que facilidad se puedevolver atras?
Conectividad en *la ultima milla*.
Se puede migrar de un proveedor a otro?

# OpenMP - MPI
- OpenMP
	- Se usa para memoria compartida. Por mas que promete que sea paralelismo, desconfiamos de esto ya que usa un recurso compartido.
	- Tiene
		- directivas (codigo)
		- biblioteca de funciones (include)
		- variables de entorno (al compilar? o ejecutar?)
	- Pilares
		- complejidad (section)
		- volumen (for)
		- calculo paralelo (reduction)
- MPI
	- Se usa para recursos distribuidos
	- Usa procesos
	- Utiliza el traspaso de mensajes
	- Tipos de comunicacion
		- Segun temporalidad
			- Sincronico (bloq)
			- Asincronico (no bloq)
		- Segun cantidad
			- P2P (2 nodos, emisor y receptor)
				- Mensaje directo de un proceso al otro
			- Colectivas (multiples nodos)
				- Sincronizaciones
					- Barreras (sincronismo masivo, bloqueo y hasta que no terminan todas de procesar, no avanzo)
				- Movimientos de datos
					- Broadcast (unico emisor, el resto recibe EL MISMO MENSAJE)
					- Scatter (unico emisor, el resto recibe un mensaje especifico para cada uno) (necesito saber de antemano el lote de informacion)
					- Gather (multiples emisores, el resto me envia mensajes distintos. Se busca reconstruir un mensaje)
					- Scatter/Gather suelen usarse en conjunto.
				- Computaciones colectivas
					- Reductions (un mie,bro recoge los datos de otros para hacer operaciones)
	- Para la distribucion de mensajes se usa mucho un hash (para que sea parejo)

---
> 2da parte de la clase

> Premios...
> 1. Morcipan
> 2. Chori
> 3. Mila
> 4. Cajita misteriosa

La app que usamos para preguntas es Plickers
# GPU
Temas
- Filosofia GPU
- Arquitectura de la GPU
- Programacion del GP GPU
- Programacion multidimensional
## Filosofia GPU
> GPU: Unidad de Procesamiento Grafico
> GPU-GP: Unidad de Procesamiento Grafico de G... P...

**2 corrrientes de desarrollo**
- Multi-core (4 cores, un CPU, por ejemplo): No tenes control del paralelismo
- Many-core (240 coures, GPU, por ejemplo): Se intenta garantizar el paralelismo
> *La CPU esta pensada para acelerar aplicaciones secuenciables o paralelas secuenciables*

> *La GPU esta pensada paa mejorar el desempenio y los calculos de la aplicacion que lo use*

Las GPUs tienen multiples ALUs, por eso permiten un poder de calculo mucho mayor a un CPU, que suele haber pocas ALUs en comparacion.
En GPU hay un ancho de banda de instrucciones muy superior comparado a CPU
## CUDA
Compute Unified Device Architecture
Pipeline de renderizado de graficas
Vertices                -> primitivas      -> fragmentos -> fragmentos -> texturas
Proc Geometrico -> Rasterizacion -> Proc de colorear? -> operacionde de textura?
Proceso que dadas unas coordenadas se intenta dibujar algo
> Evolucion GPGPU
> - Habia varias empresar de GPGPU
> - Aparecio NVidia, compro todo
> - Antes cada placa tenia una forma distinta de trabajar
> - nVIDIA implemento CUDA

- Inicialmente el procesador d elas placas de video solo realizaba calculos graficos a traves del pipeline
- Disrupcion cuando aparece el lenguaje de programacion CUD para el procesador de la placa de video
- Se empezo a utilizar para proposito general llamandose GP-GPU
-