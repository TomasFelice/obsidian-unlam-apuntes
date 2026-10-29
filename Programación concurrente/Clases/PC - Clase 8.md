---
tipo: clase
fecha: 2026-05-13
tema: "HPC, métricas, OpenMP, MPI e introducción a GPU"
fecha_fuente: metadato original sin corroborar
fecha_por_confirmar: true
---

> [!todo] Fecha pendiente de corroborar
> La fecha original puede haber quedado de la plantilla. No hay capturas fechadas en esta nota para corregirla con evidencia.

# MIMD Paradigmas

- Memoria compartida -> Múltiples CPU consumen la misma memoria
- Memoria distribuida -> Cada cpu tiene su espacio de memoria, y se comunican con otros cpu mediante una red (lan, wan, etc.). Cada CPU incluso puede tener un SO distinto.
Los sistemas de memoria distribuida pueden organizarse como clústeres o federarse en grids. Un clúster suele administrarse de forma coordinada y puede ser heterogéneo; un grid reúne recursos que pueden pertenecer a distintas administraciones. La distinción no depende únicamente de que los equipos sean iguales.

# Paradigmas de computación paralela

> Partiendo de que estamos en un **cluster**

*"Dividir es mejor"*
La idea es dividir la problematica en subproblemas más chicos.
> MapReduce (Es un divide y venceras):
> - Tenemos un nodo Master que coordina los workers
> - Los workers hacen procesamiento puro (Map)
> - Se juntan los resultados con una fase de Reduce

# Métricas

- SpeedUp
	- Tiempo secuencial / Tiempo paralelo -> Si el programa paralelo es más rápido o no
- Eficiencia
	- SpeedUp / Cant núcleos -> Cuanto estas aprovechando los núcleos. Mas cercano a 1 es mejor
- Coste
	- número de cpus * tiempo del algoritmo -> El cómputo total realizado
- Función Overhead
	- Coste - tiempo secuencial -> mientras mayor es, quiere decir que es peor el comportamiento paralelo

# Cloud computing

Pasar cómputo *in house* hacia cómputo consumido a través de internet
Hay múltiples servicios según el fin.
- pay-per-use
- capacidad elastica
- recursos virtualizados (heterogeneidad)
- el usuario desconoce ubicación física de los recursos

## Riesgos

Donde estan los datos? Sobre todo los sensibles
Confidencialidad
Que legislación aplica ante un conflicto?
Con que facilidad se puede volver atrás?
Conectividad en *la última milla*.
Se puede migrar de un proveedor a otro?

# OpenMP - MPI

- OpenMP
	- Se usa principalmente para paralelismo de memoria compartida. Compartir memoria no impide ejecutar hilos simultáneamente; requiere coordinar los accesos que puedan entrar en conflicto.
	- Tiene
		- directivas (código)
		- biblioteca de funciones (include)
		- variables de entorno del runtime, como OMP_NUM_THREADS
	- Pilares
		- complejidad (section)
		- volumen (for)
		- cálculo paralelo (reduction)
- MPI
	- Se usa para recursos distribuidos
	- Usa procesos
	- Utiliza el traspaso de mensajes
	- Tipos de comunicación
		- Según retorno de la llamada y modo del envío (dimensiones distintas)
			- Modo síncrono: el envío se completa cuando existe una recepción correspondiente.
			- No bloqueante: la llamada inicia la operación y devuelve un request. Es una clasificación distinta del modo del envío.
		- Según cantidad
			- P2P (2 nodos, emisor y receptor)
				- Mensaje directo de un proceso al otro
			- Colectivas (múltiples nodos)
				- Sincronizaciones
					- Barreras (sincronismo masivo, bloqueo y hasta que no terminan todas de procesar, no avanzo)
				- Movimientos de datos
					- Broadcast (único emisor, el resto recibe EL MISMO MENSAJE)
					- Scatter (único emisor, el resto recibe un mensaje específico para cada uno) (necesito saber de antemano el lote de información)
					- Gather (múltiples emisores, el resto me envia mensajes distintos. Se busca reconstruir un mensaje)
					- Scatter/Gather suelen usarse en conjunto.
				- Computaciones colectivas
					- Reductions (un miembro recoge los datos de otros para hacer operaciones)
	- Para la distribución de mensajes se usa mucho un hash (para que sea parejo)

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
- Filosofía GPU
- Arquitectura de la GPU
- Programación del GP GPU
- Programación multidimensional

## Filosofía GPU

> GPU: Unidad de Procesamiento Gráfico
> GPGPU: cómputo de propósito general sobre unidades de procesamiento gráfico.

**2 corrientes de desarrollo**
- Multi-core: varios núcleos de propósito general. El paralelismo depende del programa y del planificador.
- Many-core: gran cantidad de unidades de cómputo orientadas a alto throughput; la ocupación depende de la carga y del dispositivo.
> *La CPU esta pensada para acelerar aplicaciones secuenciables o paralelas secuenciables*

> *La GPU esta pensada paa mejorar el desempeño y los cálculos de la aplicación que lo use*

Las GPUs tienen múltiples ALUs, por eso permiten un poder de cálculo mucho mayor a un CPU, que suele haber pocas ALUs en comparación.
Las GPU suelen ofrecer alto ancho de banda de memoria; comparar arquitecturas y cargas concretas en lugar de asumir superioridad en todo tipo de instrucciones.

## CUDA

Compute Unified Device Architecture
Pipeline de renderizado de gráficas
Vértices                -> primitivas      -> fragmentos -> fragmentos -> texturas
Procesamiento de geometría → rasterización → sombreado de fragmentos → operaciones de salida (esquema simplificado).
Proceso que dadas unas coordenadas se intenta dibujar algo
> Evolución GPGPU
> - Habia varias empresar de GPGPU
> - NVIDIA desarrolló CUDA para sus GPU; existen otras plataformas de cómputo acelerado.
> - Antes cada placa tenia una forma distinta de trabajar
> - nVIDIA implemento CUDA

- Inicialmente el procesador d elas placas de video solo realizaba cálculos gráficos a través del pipeline
- CUDA facilita programar cómputo general para GPU NVIDIA; es una plataforma y modelo de programación, no solo un lenguaje.
- Se empezo a utilizar para propósito general llamandose GP-GPU

---

## Complemento de estudio

### Precisiones para el parcial

**Speedup = tiempo secuencial / tiempo paralelo**, no cociente de velocidades. Eficiencia = speedup / p.

MPI puede ejecutarse en una sola computadora o entre nodos. Bloqueante/no bloqueante indica cuándo retorna una llamada; estándar/síncrono/buffered/ready indica el modo del envío. Una operación no bloqueante requiere completarse con Wait/Test antes de reutilizar su buffer.

Broadcast distribuye el mismo contenido; scatter reparte partes; gather las reúne en la raíz; reduce combina valores. Una colectiva no es automáticamente una barrera.

**GPGPU** significa General-Purpose Computing on Graphics Processing Units. CUDA no garantiza que cualquier algoritmo se acelere: importan volumen de trabajo, accesos y transferencias.

Fuente: [MPI Forum](https://www.mpi-forum.org/docs/mpi-1.1/mpi-11-html/node44.html).
