---
tipo: clase
fecha: 2026-05-13
tema: GPU
---
# Posibles preguntas de parcial
- OpenMP se utiliza para la mem comp y se basa en directivas del compilador
	- verdadero
- MPI mem distribuida y paso explicito de mensajes entre procesos
	- Verdadero
- MPI se adapta a la arquitectura de 
	- memoria distribuida - memoria compartida y distribuida

---
# 5 Pasos de la GPU
1. Reservar memoria
2. Copiar la memoria a la GPU
3. Transferir el kernel y ejecutar los hilos
4. Leer el resultado
5. Liberar la memoria
---
# Programacion multidimensional
Para GPU, solamente vamos a estar viendo CUDA. Arquitectura G80
> TPC -> Dentro hay SM -> Dentro hay SP (SP termina siendo un CUDA core en nVIDIA)

Actividades 1 y 2 se vieron la clase pasada
## Imagenes
![[Pasted image 20260603204108.png]]
En 2 dimensiones
![[Pasted image 20260603204129.png]]
Podemos asignar cada hilo a una letra
![[Pasted image 20260603204343.png]]
> Que KPIs (o KRs) hay que mirar al trabajar con GPU?
> - Cuantos accesos estoy haciendo
> - En cuanto voy a dividir
> (minuto 9:50 de la grabacion)

![[Pasted image 20260603204831.png]]
- Cuantos hilos necesito para procesar esta imagen en paralelo?
	- 1024*768=768432 hilos
![[Pasted image 20260603204959.png]]
> Como funcionan las matrices en memoria
> En GPU se usa el acceso unidimensional. **fila . cantCol + col**
> SIEMPRE HAY QUE USAR ACCESO UNIDIMENSIONAL

![[Pasted image 20260603205419.png]]
![[Pasted image 20260603205519.png]]
![[Pasted image 20260603205615.png]]
O->Origen
R->Destino
> Pixel = R * 0.3 + G * 0.59 + B * 0.11

Ejemplo de forma secuencial
![[Pasted image 20260603205921.png]]
![[Pasted image 20260603210055.png]]
![[Pasted image 20260603210507.png]]
> Pasos para pasar un codigo secuencial a paralelo gpu
> - arrays unidimensionales
> - sacar fors
> - agregar if para no procesar de mas, ya que casi siempre planifico hilos de mas

> Al ejemplo le faltaria el identificador de bloque.

> Los hilos tienen un identificador compuessto: X, Y

Organizacion de bloques 3D
![[Pasted image 20260603211634.png]]
![[Pasted image 20260603212149.png]]
En esta imagen vemos que la grilla tiene un indice de bloque, y el bloque tiene indice de los hilos
![[Pasted image 20260603212240.png]]
Organizacion de grillos-bloques
![[Pasted image 20260603212622.png]]
![[Pasted image 20260603212722.png]]
1024/16=64
768/19=40.42...~41
Esto representa la grilla (que contiene bloques)
Dentro de estos bloquesn tenemos 16\*19 hilos
![[Pasted image 20260603214603.png]]
Agregamos el identificador real del hilo (usando los datos del bloque)
blockDim es la dimension general de los blqoues definidos (64x41)
3D
![[Pasted image 20260603215030.png]]
![[Pasted image 20260603215043.png]]
Lo que estuvimos viendo hasta ahora, es CUDA
En OpenCL:
- Grilla->NDRange
- Block -> Workgroup
- Thread -> Work item
![[Pasted image 20260603215606.png]]
![[Pasted image 20260603215616.png]]
El tamanio de la grilla \* el tamanio del bloque.
grilla -> 4x4x4
bloque -> 4x4x4
![[Pasted image 20260603215948.png]]
