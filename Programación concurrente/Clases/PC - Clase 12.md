---
tipo: clase
fecha: 2026-06-17
tema: "GPU: jerarquía de memoria, sincronización, atómicas y Sobel"
fecha_original: 2026-04-20
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Division de memoria

![[Pasted image 20260617192616.png]]
Estan las memorias de dentro y fuera del chip
- Memoria OnBoard (DRAM)
	- Memoria global
	- Memoria local
	- Memoria de texturas
- Memoria OnChip
	- Memoria compartida
	- Memoria de registros
	- Caché de constantes (los datos residen en memoria del dispositivo)
Analogia
![[Pasted image 20260617192755.png]]
La ubicación física y el alcance son conceptos distintos: la memoria local reside fuera del chip, pero es privada de cada hilo.
Sin embargo, en las memorias onchip, hay distintos tipos de accesos.

**Memoria global**
![[Pasted image 20260617193102.png]]
![[Pasted image 20260617193153.png]]
En el modelo básico, la CPU reserva y transfiere datos hacia la memoria del dispositivo mediante la API de CUDA; no accede directamente a registros ni a memoria compartida de los bloques.
Es lento su acceso porque esta fuera del chip.
Si quisieramos optimizar esto, podemos usar la memoria compartida.
**Memoria compartida**
![[Pasted image 20260617193410.png]]
Esto del share, se usa dentro del código del kernel
![[Pasted image 20260617193510.png]]
**Memoria de registros**
![[Pasted image 20260617193547.png]]
Aqui van a para las variables declaradas dentro del kernel
![[Pasted image 20260617193623.png]]
Como es chica, hay que tener cuidado de no hacer un overflow de la memoria
**Memoria local**
![[Pasted image 20260617193751.png]]
El compilador puede usar memoria local para derrames de registros y para otras variables privadas que no puede ubicar en registros. Es más lenta que la de registros. Esta fuera del chip.

---

# Optimización

![[Pasted image 20260617193937.png]]
En lo que vimos hasta ahora, siempre usamos memoria global, ya que era lo más simple. El uso de memoria compartida tiene cierta complejidad.
![[Pasted image 20260617194206.png]]
![[Pasted image 20260617194226.png]]
Basicamente, dividimos el dato original, para pasarlo en pedazos más pequeños a la memoria compartida.
![[Pasted image 20260617194340.png]]
![[Pasted image 20260617194457.png]]


---

# Mecanismos de sincronización

> Como se sincronizan los hilos? Hay sincronismo en GPU?

![[Pasted image 20260617194733.png]]
Como cada hilo trabaja en una posición distinta, en principio no tenemos problemas de concurrencia
![[Pasted image 20260617194837.png]]
![[Pasted image 20260617194854.png]]
> La variable suma esta en memoria global porque se pasa como parámetro.

![[Pasted image 20260617195038.png]]
Las operaciones atómicas pueden generar contención, pero son necesarias cuando varios hilos actualizan un mismo dato sin otra estrategia de coordinación. Hay que medir su costo y considerar reducciones por bloque.
![[Pasted image 20260617195149.png]]
atomicExch -> Asignacion
atomicCAS -> Asignacion con condicion
Histograma -> Permite determinar la cantidad de veces que se repite un valor en X set de datos.
![[Pasted image 20260617195409.png]]
![[Pasted image 20260617195434.png]]
![[Pasted image 20260617195959.png]]

---

# Teoría Sobel

![[Pasted image 20260617200341.png]]
![[Pasted image 20260617200357.png]]


---

# Práctica Sobel

![[Pasted image 20260617202905.png]]
![[Pasted image 20260617203001.png]]


---

# Final Plickers

---

## Complemento de estudio

### Alcance de memoria y coordinación

| Recurso | Alcance habitual | Observación |
|---|---|---|
| Registros | Hilo | Asignados por el compilador |
| Local | Hilo | Reside en memoria del dispositivo |
| Compartida | Bloque | Útil para reutilizar datos |
| Global | Todos los hilos | Persiste mientras siga reservada |
| Constante | Lectura por hilos | Espacio con caché |

__syncthreads() coordina los hilos de un bloque. No es barrera global; no ubicarla en ramas que no alcanza todo el bloque. Una atómica protege una actualización, no cualquier secuencia de operaciones.

**Sobel:** obtener gris, calcular Gx y Gy con vecindades 3 × 3 y combinar magnitudes. Definir tratamiento de bordes. Cada hilo escribe un píxel, pero lee vecinos: evitar sobrescribir la entrada que otros aún necesitan.

Fuente: [CUDA](https://docs.nvidia.com/cuda/cuda-programming-guide/).
