---
tipo: examen
fecha: 2026-04-20
tema: Programacion concurrente
unidades: todas
---
# Modelo 1
![[Pasted image 20260620150520.png]]
![[Pasted image 20260620150527.png]]

### Unidad 1
1. Describa, en forma sintetica, las diferencias entre Programacion secuencial, concurrente y paralela.
La *programación secuencial* ejecuta una **única secuencia de instrucciones**, donde cada instrucción comienza luego de finalizar la anterior.
La *programación concurrente* permite la **ejecución de múltiples tareas durante un mismo período de tiempo, intercalando su ejecución** y sin garantizar necesariamente un orden determinístico.
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

4. Que realiza el fragmento de codigo?
El código recorre la colección `node.children` y crea un proceso hijo mediante `fork()` por cada elemento. Cada proceso hijo ejecuta la función `DoWork()` y finaliza inmediatamente. Si la creación de un proceso falla, se informa el error y se termina la ejecución. Una vez creados todos los hijos, el proceso padre espera la finalización de cada uno mediante llamadas a `wait()`. Debido a que los hijos terminan luego de ejecutar `DoWork()`, sólo el proceso padre continúa ejecutando el segundo bucle y realiza las esperas.

### Unidad 3
5. Que mecanismos de comunicacion entre PROCESOS, exclusivamente, existen?
Los principales mecanismos de comunicación entre procesos son **pipes, FIFOs (named pipes), colas de mensajes, memoria compartida, señales y sockets**.
6. En que casos utilizaria un PIPE y en que casos un FIFO? Justifique
Utilizaría un Pipe cuando necesito comunicar procesos relacionados, por ejemplo un proceso padre y un proceso hijo creados mediante `fork()`. Es una solución simple y eficiente para comunicación temporal entre dichos procesos.
Utilizaría un FIFO cuando necesito comunicar procesos que no están relacionados entre sí. Al tener un nombre en el sistema de archivos, distintos procesos pueden abrirlo y utilizarlo como canal de comunicación independientemente de cómo hayan sido creados.

### Unidad 4
7. Que mecanismos de sincronizacion entre HILOS exclusivamente existen? Justifique
Los principales mecanismos de sincronización entre hilos son **mutex, semáforos, variables de condición, barreras y monitores**. Estos mecanismos permiten coordinar la ejecución concurrente de los hilos, evitando condiciones de carrera y garantizando el acceso ordenado a recursos compartidos. 

---
# Modelo 2
1. 1- ventajas y desventajas de la programación concurrente 2- dan un grafo de procesos y un código con un loop y fork y hay que decir si ese grafo es el resultado del programa, justificar
    
    `import os import sys  def create_process(create=0):     pid = os.fork()     if pid < 0:         print("error")         sys.exit(1)      if pid == 0:         if create:             os.fork()         os._exit(0)  for i in range(2):     for j in range(2):         create_process(i * j)`
    
    Grafo: P H1, H2, H3 H4 3- dan un código en C de ejecución de 2 hilos y preguntan que hace y que mejoras harías en el código
    
    `#include <iostream> #include <vector> #include <thread>  using namespace std;  vector<int> nums = {1, 2, 3, 4};  void AddRange(const string& name, int begin, int end) {     int total = 0;     for (int i = begin; i < end; ++i) {         total += nums[i];     }     cout << name << ": " << total << endl; }  int main() {     thread A(AddRange, "A", 0, 2)     thread B(AddRange, "B", 2, 4);      A.join();     B.join();      return 0; }`
    
    4- cuáles son todos los mecanismos de comunicación de procesos 5- mutex, starvation, deadlock, definirlos 6- Explicar
    
    `#include <iostream> #include <omp.h>  int main() {     int num_elements = 10;     int num_threads = 10;      int arr[num_elements];     omp_set_num_threads(num_threads);      #pragma omp parallel for     for (int i = 0; i < num_elements; i++) {         arr[i] = omp_get_thread_num();     }      for (int i = 0; i < num_elements; i++) {         std::cout << arr[i] << " ";     }     std::cout << std::endl;      return 0; }`
    
    7- Diferencias entre nube privada y nube publica 8- mpi: definición de broadcast y scatter 9- proponer un okr y kpi sobre la materia(GPU) 10- Explicar
    
    `__global__ void addVectors(const float* a, const float* b, float* c, int n) {     int idx = blockIdx.x * blockDim.x + threadIdx.x;     if (idx < n) {         c[idx] = a[idx] + b[idx];     } }`

---
# Modelo 3
[[Preguntas Concurrente.pdf]]
	