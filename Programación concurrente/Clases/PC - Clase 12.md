---
tipo: clase
fecha: 2026-04-20
tema: GPU
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
	- Memoria de constantes
Analogia
![[Pasted image 20260617192755.png]]
Aca podemos ver que a las memorias OnBoard, todos los hilos pueden acceder.
Sin embargo, en las memorias onchip, hay distintos tipos de accesos.

**Memoria global**
![[Pasted image 20260617193102.png]]
![[Pasted image 20260617193153.png]]
La memoria global es la unica que puede acceder la CPU
Es lento su acceso porque esta fuera del chip.
Si quisieramos optmizar esto, podemos usar la memoria compartida.
**Memoria compartida**
![[Pasted image 20260617193410.png]]
Esto del share, se usa dentro del codigo del kernel
![[Pasted image 20260617193510.png]]
**Memoria de registros**
![[Pasted image 20260617193547.png]]
Aqui van a para las variables declaradas dentro del kernel
![[Pasted image 20260617193623.png]]
Como es chica, hay que tener cuidado de no hacer un overflow de la memoria
**Memoria local**
![[Pasted image 20260617193751.png]]
Cuando supero la memoria de registros, se usa la memoria local. Es mas lenta que la de registros. Esta fuera del chip.

---
# Optimizacion
![[Pasted image 20260617193937.png]]
En lo que vimos hasta ahora, siempre usamos memoria global, ya que era lo mas simple. El uso de memoria compartida tiene cierta complejidad.
![[Pasted image 20260617194206.png]]
![[Pasted image 20260617194226.png]]
Basicamente, dividimos el dato original, para pasarlo en pedazos mas pequenios a la memoria compartida.
![[Pasted image 20260617194340.png]]
![[Pasted image 20260617194457.png]]


---
# Mecanismos de sincronizacion
> Como se sincronizan los hilos? Hay sincronismo en GPU?

![[Pasted image 20260617194733.png]]
Como cada hilo trabaja en una posicion distinta, en principio no tenemos problemas de concurrencia
![[Pasted image 20260617194837.png]]
![[Pasted image 20260617194854.png]]
> La variable suma esta en memoria global porque se pasa como param.

![[Pasted image 20260617195038.png]]
Si usamos estas cosas, se empieza a secuencializar la ejecucion. Perdemos paralelismo. No se debe utilizar.
![[Pasted image 20260617195149.png]]
atomicExch -> Asignacion
atomicCass -> Asignacion con condicion
Histograma -> Permite determinar la cantidad de veces que se repite un valor en X set de datos.
![[Pasted image 20260617195409.png]]
![[Pasted image 20260617195434.png]]
![[Pasted image 20260617195959.png]]

---
# Teoria Sobel
![[Pasted image 20260617200341.png]]
![[Pasted image 20260617200357.png]]


---
# Practica Sobel
![[Pasted image 20260617202905.png]]
![[Pasted image 20260617203001.png]]



---
# Final Plickers