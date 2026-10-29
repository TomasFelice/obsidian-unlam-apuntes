---
tipo: examen
fecha: 2026-06-20
tema: "Repaso de concurrencia, procesos e hilos, OpenMP, MPI y CUDA"
unidades: todas
fecha_original: 2026-04-20
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Modelo 1

![[Pasted image 20260620150520.png]]
![[Pasted image 20260620150527.png]]

### Unidad 1

1. Describa, en forma sintética, las diferencias entre Programación secuencial, concurrente y paralela.
La *programación secuencial* ejecuta una **única secuencia de instrucciones**, donde cada instrucción comienza luego de finalizar la anterior.
La *programación concurrente* permite la **ejecución de múltiples tareas durante un mismo período de tiempo, intercalando su ejecución** y sin garantizar necesariamente un orden determinístico y aprovechando mejor los recursos del sistema.
La *programación paralela* consiste en **ejecutar múltiples tareas simultáneamente utilizando varias unidades de procesamiento**. Si bien todo programa paralelo es concurrente, no toda ejecución concurrente es paralela, ya que la concurrencia puede implementarse sobre un único procesador mediante la alternancia de tareas.

2. Enumere las diferencias entre proceso e hilo
- Un proceso posee su propio espacio de direcciones, mientras que los hilos de un mismo proceso comparten dicho espacio.
- Los hilos comparten recursos del proceso (memoria, código y archivos abiertos), mientras que los procesos poseen recursos independientes.
- La comunicación entre hilos es más simple porque comparten memoria; la comunicación entre procesos requiere mecanismos IPC.
- La creación y destrucción de hilos es menos costosa que la de procesos.
- El cambio de contexto entre hilos suele ser más eficiente que entre procesos.
- Un proceso se administra mediante un PCB, mientras que un hilo se administra mediante un TCB.

### Unidad 2

3. Defina el concepto de atomicidad y cambio de contexto
**Atomicidad**: Es la propiedad por la cual una operación se ejecuta como una unidad indivisible. Ningún otro hilo o proceso puede observar estados intermedios de dicha operación; ésta ocurre completamente o no ocurre.
**Cambio de contexto**: El cambio de contexto es el mecanismo mediante el cual el sistema operativo guarda el estado de ejecución de un hilo o proceso y restaura el estado de otro para permitir que el procesador continúe ejecutándolo. Puede ocurrir por planificación del sistema operativo, interrupciones de hardware o bloqueos de ejecución.

4. Que realiza el fragmento de código?
El código recorre la colección `node.children` y crea un proceso hijo mediante `fork()` por cada elemento. Cada proceso hijo ejecuta la función `DoWork()` y finaliza inmediatamente. Si la creación de un proceso falla, se informa el error y se termina la ejecución. Una vez creados todos los hijos, el proceso padre espera la finalización de cada uno mediante llamadas a `wait()`. Debido a que los hijos terminan luego de ejecutar `DoWork()`, sólo el proceso padre continúa ejecutando el segundo bucle y realiza las esperas.

### Unidad 3

5. Que mecanismos de comunicación entre PROCESOS, exclusivamente, existen?
Los principales mecanismos de comunicación entre procesos son **pipes, FIFOs (named pipes), colas de mensajes, memoria compartida, señales y sockets**.
6. En que casos utilizaria un PIPE y en que casos un FIFO? Justifique
Utilizaría un Pipe cuando necesito comunicar procesos relacionados, por ejemplo un proceso padre y un proceso hijo creados mediante `fork()`. Es una solución simple y eficiente para comunicación temporal entre dichos procesos.
Utilizaría un FIFO cuando necesito comunicar procesos que no están relacionados entre sí. Al tener un nombre en el sistema de archivos, distintos procesos pueden abrirlo y utilizarlo como canal de comunicación independientemente de cómo hayan sido creados.

### Unidad 4

7. Que mecanismos de sincronización entre HILOS exclusivamente existen? Justifique
Entre hilos se usan **mutex, semáforos, variables de condición, barreras y monitores**. No son todos exclusivos de hilos: algunas implementaciones permiten sincronizar procesos, por ejemplo semáforos del sistema o mutex configurados como compartidos entre procesos. Estos mecanismos permiten coordinar la ejecución concurrente de los hilos, evitando condiciones de carrera y garantizando el acceso ordenado a recursos compartidos.
8. Que es lo que realiza el siguiente fragmento de código? Que considera que es necesario que este si o si en el fragmento de código?
El siguiente fragmento de código implementa el patrón Productor-Consumidor. Existe un hilo productor (`producerThread`) que genera un valor aleatorio entre 0 y 99 y lo almacena en la variable compartida `sharedValue`, y un hilo consumidor (`consumerThread`) que consume dicho valor.

En este código son necesarios:
- Los bloques `synchronized(lock)`, que determinan una región crítica y utilizan el objeto `lock` como monitor para garantizar exclusión mutua.
- La variable `isProduced`, que permite indicar si existe un dato disponible para consumir.
- Los `while`, ya que un hilo puede despertarse de un `wait()` sin que la condición que esperaba se haya cumplido (spurious wakeup) o porque otro hilo modificó el estado compartido antes de que recuperara el monitor.
- Los métodos `lock.wait()` y `lock.notify()`, que permiten sincronizar ambos hilos. `wait()` libera el monitor, suspende el hilo y lo coloca en espera. `notify()` despierta a uno de los hilos que están esperando sobre ese monitor para que pueda competir nuevamente por él.

---

# Modelo 2

## 1. Ventajas y desventajas de la programación concurrente

La programación concurrente permite ejecutar **múltiples tareas** durante un **mismo período de tiempo**, mejorando la utilización de los recursos del sistema, la capacidad de respuesta y el aprovechamiento de arquitecturas multinúcleo. Además, resulta fundamental para aplicaciones distribuidas y sistemas que requieren atender múltiples solicitudes simultáneamente.

Sin embargo, introduce una mayor complejidad en el desarrollo, ya que el acceso concurrente a recursos compartidos puede provocar condiciones de carrera, deadlocks y starvation. Asimismo, la depuración y validación de los programas resulta más difícil debido al carácter no determinístico de su ejecución.

---

## 2. Análisis de procesos y `fork()`

Dado el siguiente código:

```python
import os
import sys

def create_process(create=0):
    pid = os.fork()

    if pid < 0:
        print("error")
        sys.exit(1)

    if pid == 0:
        if create:
            os.fork()
        os._exit(0)

for i in range(2):
    for j in range(2):
        create_process(i * j)
```

Y el siguiente grafo:

```text
P
├── H1
├── H2
├── H3
└── H4
```

Determinar:

- Si el grafo representa correctamente la ejecución del programa.
- Justificar la respuesta.
- Indicar cuántos procesos se crean y cuál es la relación entre ellos.

Llamadas a create_process():
1. i=0;j=0 -> create_process(0x0=0)
2. i=0;j=1 -> create_process(0x1=0)
3. i=1;j=0 -> create_process(1x0=0)
4. i=1;j=1 -> create_process(1x1=1)

El grafo no representa correctamente la ejecución del programa ya que no tiene en cuenta el flujo cuando create == 1. Cuando create toma este valor, se ejecuta un fork adicional, ocasionando que se cree otro proceso más.
Analizando el ejemplo completo, podemos ver que create == 1 sólo en una ocasión, por lo que se crearán 4 procesos hijos, y en uno de ellos, se creará otro proceso hijo más. En definitiva, tendremos 6 procesos: el padre, 4 hijos, y 1 "nieto".
```text
P
├── H1
├── H2
├── H3
└── H4
	└── H5
```


---

## 3. Análisis de código multihilo en C++

Dado el siguiente código:

```cpp
#include <iostream>
#include <vector>
#include <thread>

using namespace std;

vector<int> nums = {1, 2, 3, 4};

void AddRange(const string& name, int begin, int end) {
    int total = 0;

    for (int i = begin; i < end; ++i) {
        total += nums[i];
    }

    cout << name << ": " << total << endl;
}

int main() {
    thread A(AddRange, "A", 0, 2);
    thread B(AddRange, "B", 2, 4);

    A.join();
    B.join();

    return 0;
}
```

Responder:

- ¿Qué realiza el programa?
- ¿Qué salida puede producir?
- ¿Qué mejoras podrían aplicarse?

El programa crea 2 hilos que ejecutan la misma función `AddRange()` y luego espera a que finalicen ambos. En esta función lo que se hace es:
- Reciben
	- Nombre del hilo
	- Posición de inicio a recorrer en array de `nums`
	- Posición de fin a recorrer en array de `nums`
- Por cada posición dentro del rango indicado acumula el valor del array `nums` en esas posiciones en la variable `total` .
- Finalmente, muestra por pantalla el nombre del hilo y el valor de `total`.
Este programa no contempla varios de los problemas al programar de forma concurrente.
- `total` es local de cada invocación de `AddRange()`: cada hilo tiene su acumulador. Como `nums` solo se lee, esta suma no presenta una condición de carrera y no necesita una operación atómica. Un acumulador compartido modificable sí requeriría coordinación.
- `cout << name << ": " << total << endl;`: Esta impresión por pantalla, también consiste en varias instrucciones en código máquina. Por lo que al no sincronizarla, puede imprimir en un orden indeseado. Habría que sincronizar esta sección con un mutex para que su ejecución esté controlada. Teniendo en cuenta esto podrían llegar a imprimirse mensajes en orden inesperado, por ejemplo:
	- Partiendo de que total en A = 3 y en B = 7
	- "AB: 7: 3\n\n"
		- Desglosando:
			- Entra A
				- Imprime "A"
			- Entra B
				- Imprime "B"
				- Imprime ": "
				- Imprime "7"
			- Entra A
				- Imprime ": "
				- Imprime "3"
				- Imprime "\n"
			- Entra B
				- Imprime "\n"
Esto es tan solo un ejemplo de una salida que podría llegar a darse. Sin embargo, hay distintas posibilidades e incluso, podría llegar a salir bien la salida, pero no se puede garantizar.
Entre otras mejoras que podrían hacerse estan las siguientes:
- devolver el resultado a la función principal en lugar de solo imprimir. Se podría resolver usando promesas o variables compartidas
- segmentar las posiciones del array en cantidad de hilos para no fijarlos.


---

## 4. Mecanismos de comunicación entre procesos

Los principales mecanismos de comunicación entre procesos son:

- **Pipes**: canales de comunicación unidireccionales generalmente utilizados entre procesos relacionados.
- **FIFOs (Named Pipes)**: pipes con nombre que permiten comunicación entre procesos no relacionados.
- **Colas de mensajes**: intercambio de mensajes estructurados entre procesos.
- **Memoria compartida**: permite que varios procesos accedan a una misma región de memoria.
- **Sockets**: permiten comunicación local o a través de una red.
- **Señales**: permiten notificar eventos o cambios de estado entre procesos.

---

## 5. Definiciones

Definir los siguientes conceptos:
- Mutex
	es un mecanismo de sincronización que permite garantizar que sólo un hilo o proceso acceda a una región crítica a la vez.
- Starvation
	Situación en la que un proceso o hilo espera indefinidamente por un recurso debido a que otros procesos o hilos son favorecidos continuamente por el planificador o mecanismo de sincronización.
- Deadlock
	Un deadlock ocurre cuando dos o más procesos o hilos quedan bloqueados permanentemente debido a que cada uno espera recursos retenidos por otro, generando una espera circular.

---

## 6. OpenMP

Explicar qué realiza el siguiente programa:

```cpp
#include <iostream>
#include <omp.h>

int main() {
    int num_elements = 10;
    int num_threads = 10;

    int arr[num_elements];

    omp_set_num_threads(num_threads);

    #pragma omp parallel for
    for (int i = 0; i < num_elements; i++) {
        arr[i] = omp_get_thread_num();
    }

    for (int i = 0; i < num_elements; i++) {
        std::cout << arr[i] << " ";
    }

    std::cout << std::endl;

    return 0;
}
```

Analizar:

- Paralelismo utilizado.
    El paralelismo utilizado consiste en el uso de OpenMP, especificamente, se realiza un for paralelo (por la sentencia `#pragma omp parallel for`). Se trata de paralelismo de memoria compartida (shared memory parallelism), ya que todos los hilos acceden al mismo espacio de memoria.
- Cantidad de hilos.
    Se solicitan 10 hilos. Pero la cantidad de hilos que realmente se planifican, dependen de otras cuestiones tales como: configuración de omp, variables de entorno, hw disponible o politicas de runtime
- Posible salida.
    Una posible salida seria:
	    0 1 2 3 4 5 6 7 8 9
	    o
	    0 1 2 3 0 1 2 3 0 1
- Funcionamiento de `#pragma omp parallel for`.
    Esta directiva lo que hace es lanzar el for que se escribe a continuacion, pero dividido en la cantidad de hilos que se asignan (en la función `omp_set_num_threads(num_threads)`, dependiente de las condiciones mencionadas)

---

## 7. Computación en la nube

Explicar las diferencias entre:

- Nube pública.
	Una nube pública ofrece recursos a distintos clientes mediante un proveedor, con aislamiento lógico.
- Nube privada.
    Es de uso exclusivo de una organización; puede estar alojada dentro o fuera de sus instalaciones y ser operada por ella o por un tercero. El modelo no depende simplemente de la ubicación física.

---

## 8. MPI

Definir y explicar:

- Broadcast
	Un proceso raíz distribuye el mismo dato a todos los procesos de un comunicador. Se utiliza cuando todos los procesos necesitan acceder a la misma información.. Un emisor, N receptores. El mensaje enviado es el mismo.
	Entre sus usos podemos tener:
	- Enviar señales de sincronización
	- Enviar un mismo contenido a distintos nodos para analizar distintas métricas
	- Distribuir parámetros de configuración.
	- Enviar una matriz o vector común a todos los procesos.
	- Compartir datos iniciales de un cálculo paralelo.
- Scatter
	Un proceso raíz divide un conjunto de datos y distribuye una porción distinta a cada proceso del comunicador. Un emisor, N receptores.
	Entre sus usos podemos tener:
	- Enviar distintas partes de un libro para evaluar, por ejemplo, la cantidad de palabras.
	- Generalmente se usa en conjunto con un Gather, el cual se encarga de recibir N mensajes, juntarlos y enviarlo al receptor (que sería el emisor del Scatter).
	- Dividir un vector o matriz para procesamiento paralelo.
	- Distribuir partes de un archivo entre varios procesos.
	- Repartir carga de trabajo para cálculos distribuidos.

Indicar casos de uso para cada operación.

---

## 9. OKR y KPI

Proponer:

- **Objetivo:** acelerar el procesamiento de imágenes conservando resultados correctos.
- **Resultados clave propuestos:** reducir al menos un 30 % el tiempo total de un lote respecto de la versión secuencial y validar todos los casos con la tolerancia numérica definida. Son metas de ejemplo.
- **KPI:** tiempo total por lote, tiempo del kernel, tiempo de transferencias, FPS y error máximo respecto de la referencia.

---

## 10. CUDA

Explicar qué realiza el siguiente kernel:

```cpp
__global__ void addVectors(
    const float* a,
    const float* b,
    float* c,
    int n
) {
    int idx = blockIdx.x * blockDim.x + threadIdx.x;

    if (idx < n) {
        c[idx] = a[idx] + b[idx];
    }
}
```

Analizar:

- Función del kernel.
    Realiza una suma entre los vectores a y b y almacenta resultado en el vector c.
- Significado de `blockIdx`, `blockDim` y `threadIdx`.
	`blockIdx`: Índice del bloque dentro de la grilla
	`blockDim`: cantidad de hilos por bloque en cada dimensión. La cantidad de bloques de la grilla está en `gridDim`.
	`threadIdx`: Indice del hilo (dentro de un bloque)
- Cómo se distribuye el trabajo entre los hilos.
    Cada hilo procesa la porcion que le corresponde según lo que le toca a su índice.
- Qué ocurre cuando `idx >= n`.
	Cuando idx >= n, no se sigue procesando porque no corresponde a una posición válida dentro del vector. Se agrega esta condición porque se planifican hilos de más.

---

# Modelo 3

![[Preguntas Concurrente.pdf]]

## Paralelismo

1. Paralelismo es un concepto asociado con la existencia de múltiples procesadores ejecutando un algoritmo de forma coordinada y cooperante.
	Sí, la definición es correcta. El paralelismo consiste en la ejecución simultánea de distintas tareas o partes de un algoritmo utilizando múltiples procesadores o núcleos de procesamiento, con el objetivo de reducir el tiempo de ejecución y aumentar el rendimiento.
2. Qué significa el modelo de ejecución MIMD que propuso Flynn? De un ejemplo de uso
	Este modelo significa "Multiple Instruction Multiple Data". Esto indica que múltiples instrucciones están procesando múltiples datos de forma simultánea con la particularidad de que cada unidad de procesamiento puede procesar instrucciones distintas sobre datos distintos.
	Este modelo es el modelo clásico de un procesador multi-core.
3. Enumere 3 paradigmas con los que se puede lograr la computación de alto rendimiento
	1. Memoria compartida (OpenMP)
	2. Memoria distribuida (MPI)
	3. Procesamiento acelerado por GPU (CUDA, OpenCL)

## OpenMP

1. Cuál es el funcionamiento de OpenMP en relación con sus hilos/procesos y los recursos que comparten?
	OpenMP es un modelo de programación paralela basado en memoria compartida. Mediante directivas del compilador se crean regiones paralelas que son ejecutadas por múltiples hilos pertenecientes al mismo proceso. Estos hilos comparten el mismo espacio de memoria y pueden acceder a variables compartidas, aunque también pueden disponer de variables privadas. Cada hilo posee su propio contador de programa y pila de ejecución. La cantidad de hilos utilizados puede configurarse y depende además del hardware y del runtime de OpenMP. Es importante recalcar, que si bien, OpenMP promete que la ejecución será paralela, esto no podemos asegurarlo ya que depende de diversos factores.
2. Cuál es la taxonomía de Flynn implementada en OpenMP? Cómo mejoró en las clasificaciones de paralelismo?
	OpenMP implementa la taxonomía MIMD (Multiple Instruction Multiple Data), ya que múltiples hilos pueden ejecutar simultáneamente distintas secuencias de instrucciones sobre diferentes datos dentro de un mismo espacio de memoria compartida. Este modelo permite aprovechar procesadores multinúcleo y facilita la implementación de paralelismo mediante directivas del compilador, reduciendo la complejidad de programación respecto a otras alternativas.

---

# Preguntas de Plickers

![[OpenMP-MPI 1.pdf]]

![[GPU Clase 1 - Plickers 1.pdf]]

![[GPU Clase3 Memoria - Plickers 1.pdf]]

![[GPU Clase 4 1.pdf]]

![[GPU Clase 2 - Plickers 1.pdf]]

---

## Complemento de estudio

### Revisiones de las respuestas

- En Python, os.fork() lanza OSError si falla; no devuelve un PID negativo. La prueba pid < 0 corresponde a C. fork no está disponible en Windows.
- Se crean cinco procesos nuevos: cuatro hijos y un nieto; contando el original son seis. El padre debe recolectar a sus hijos.
- Atomicidad de memoria significa indivisibilidad para los observadores pertinentes; no implica rollback frente a cualquier fallo.
- En C++ estándar, int arr[num_elements] con tamaño no constante no es válido. Usar std::vector<int>.
- Un mutex alrededor de la impresión completa evita entrelazar líneas, pero no obliga a que A imprima antes que B.
- OpenMP también ofrece SIMD y offloading: MIMD describe el ejemplo con hilos, no todas sus capacidades.

**Autoevaluación:** resolver conteo de procesos y cálculo de grilla sin mirar las respuestas; justificar qué memoria comparte cada trabajador.
