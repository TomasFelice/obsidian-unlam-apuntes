---
tipo: clase
fecha: 2026-06-03
tema: "CUDA: kernels, indexación y organización de grillas y bloques"
fecha_original: 2026-05-13
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Posibles preguntas de parcial

- OpenMP se utiliza para la memoria compartida y se basa en directivas del compilador
	- verdadero
- MPI memoria distribuida y paso explícito de mensajes entre procesos
	- Verdadero
- MPI se adapta a la arquitectura de
	- memoria distribuida - memoria compartida y distribuida

---

# 5 Pasos de la GPU

1. Reservar memoria
2. Copiar la memoria a la GPU
3. Lanzar el kernel compilado para que los hilos lo ejecuten
4. Leer el resultado
5. Liberar la memoria
---

# Programación multidimensional

Para GPU, solamente vamos a estar viendo CUDA. Arquitectura G80
> TPC -> Dentro hay SM -> Dentro hay SP (SP termina siendo un CUDA core en nVIDIA)

Actividades 1 y 2 se vieron la clase pasada

## Imágenes

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
	- 1024 × 768 = 786.432 píxeles; con un hilo por píxel se necesitan 786.432 hilos útiles.
![[Pasted image 20260603204959.png]]
> Como funcionan las matrices en memoria
> En GPU se usa el acceso unidimensional. **fila . cantCol + col**
> En estos ejercicios usamos almacenamiento lineal e índices calculados a partir de fila y columna. CUDA también admite otros tipos de almacenamiento, como arreglos y texturas.

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
> Pasos para pasar un código secuencial a paralelo gpu
> - arrays unidimensionales
> - sacar fors
> - agregar if para no procesar de más, ya que casi siempre planifico hilos de más

> Al ejemplo le faltaria el identificador de bloque.

> Los hilos tienen un identificador compuesto: X, Y

Organización de bloques 3D
![[Pasted image 20260603211634.png]]
![[Pasted image 20260603212149.png]]
En esta imagen vemos que la grilla tiene un índice de bloque, y el bloque tiene índice de los hilos
![[Pasted image 20260603212240.png]]
Organización de grillos-bloques
![[Pasted image 20260603212622.png]]
![[Pasted image 20260603212722.png]]
1024/16=64
768/19=40.42...~41
Esto representa la grilla (que contiene bloques)
Dentro de estos bloques tenemos 16\*19 hilos
![[Pasted image 20260603214603.png]]
Agregamos el identificador real del hilo (usando los datos del bloque)
`blockDim` indica los hilos por bloque: (16, 19, 1). `gridDim` indica los bloques de la grilla: (64, 41, 1).
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
El tamaño de la grilla \* el tamaño del bloque.
grilla -> 4x4x4
bloque -> 4x4x4
![[Pasted image 20260603215948.png]]

---

## Complemento de estudio

### Cálculo completo de una grilla 2D

Para una imagen de 1024 × 768 con bloques de 16 × 19:

- gridDim.x = ceil(1024/16) = 64.
- gridDim.y = ceil(768/19) = 41.
- Hilos lanzados: 64 · 41 · 16 · 19 = **797.696**.
- Píxeles útiles: **786.432**. Hilos sobrantes: **11.264**.

Coordenadas: x = blockIdx.x · blockDim.x + threadIdx.x; y = blockIdx.y · blockDim.y + threadIdx.y. Verificar x < ancho e y < alto antes de acceder al índice y · ancho + x.

El bloque lo elige el programador dentro de los límites del dispositivo. Su rendimiento depende también de warps y recursos del kernel.

Fuente: [Guía CUDA](https://docs.nvidia.com/cuda/cuda-programming-guide/).
