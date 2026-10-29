---
tipo: clase
fecha: 2026-04-22
tema: "Comunicación y problemas de concurrencia"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

>Colabs de la clase:
>* [Google Colab](https://colab.research.google.com/drive/1Jz2bZQvFYdPLFf9U0kq9BMPoxd3RgDk7?usp=sharing)
>* [Sincronismo - Clase 22/06/2026.ipynb - Colab](https://colab.research.google.com/drive/1bZgHWvqxwxWb-peA3ulk6rxWqoFOscTR?usp=sharing)
>*

# Comunicación

> Puede ser entre procesos o hilos (dependiendo del lenguaje)

## C++

![[Pasted image 20260422192304.png]]

## Python

*Comunicación entre procesos*:
* Señales
* Tuberias (Pipes)
* Tuberias nombradas (FIFOs)
* Colas
* Memoria compartida (multiprocessing)
* Sockets
*Comunicación entre hilos*:
* Variables, TDA, etc.
* Colas (queue)
* Eventos (threading)

## Java

*Comunicación entre procesos*:
* Sockets
*Comunicación entre hilos*:
* Variables, TDA, etc.
* Colas (queue)
* Eventos (threading)

## Señales

![[Pasted image 20260422193050.png]]
> **Permite comunicar la ocurrencia de un evento**

![[Pasted image 20260422193057.png]]
![[Pasted image 20260422193252.png]]

### en Python

![[Pasted image 20260422193503.png]]
> En Python, el handler recibe el número de señal y el frame interrumpido (o None). El frame representa el contexto de ejecución; no es un segmento de memoria compartida.

![[Pasted image 20260422194116.png]]
*En este ejemplo, se crea el típico arbol de procesos*

## Tuberias (Pipes)

![[Pasted image 20260422194533.png]]
* Puede comunicar un padre y varios hijos
* Comunicación **unidireccional**
* Una lectura puede bloquear mientras no haya datos; esto no reemplaza la sincronización del protocolo completo.
* Los datos se leen en el orden que se escribieron.
![[Pasted image 20260422194722.png]]

### En python

![[Pasted image 20260422194844.png]]
![[Pasted image 20260422195202.png]]

## Tuberia con nombre (FIFO)

![[Pasted image 20260422200522.png]]
* Se puede utilizar con procesos no emparentados
* Comunicación **unidireccional**
* Aparece en el sistema de archivos como un archivo más (*si hacer un ls aparece*)

### En Python

![[Pasted image 20260422200808.png]]
![[Pasted image 20260422201221.png]]
![[Pasted image 20260422201424.png]]

## Memoria compartida

* Varios procesos acceden a un segmento de memoria en común
* Permite comunicación bidireccional
* Pueden darse races conditions
![[Pasted image 20260422201505.png]]

### En Python

![[Pasted image 20260422201823.png]]
![[Pasted image 20260422201903.png]]

## Sockets

![[Pasted image 20260422202438.png]]

### En Python

![[Pasted image 20260422202542.png]]
![[Pasted image 20260422202510.png]]
Me falto la parte de cliente

## Señales en Java

![[Pasted image 20260422203155.png]]

## Comunicación en Java

![[Pasted image 20260422203350.png]]
![[Pasted image 20260422203641.png]]

---

# Problemas de concurrencia

![[Pasted image 20260422212159.png]]
![[Pasted image 20260422212205.png]]

## Operación atómica

![[Pasted image 20260422212337.png]]
![[Pasted image 20260422212430.png]]
![[Pasted image 20260422212531.png]]
![[Pasted image 20260422212724.png]]
![[Pasted image 20260422213126.png]]
![[Pasted image 20260422213254.png]]
![[Pasted image 20260422213322.png]]
![[Pasted image 20260422213438.png]]
![[Pasted image 20260422213535.png]]
![[Pasted image 20260422213653.png]]
![[Pasted image 20260422213904.png]]
![[Pasted image 20260422214030.png]]
![[Pasted image 20260422214057.png]]
![[Pasted image 20260422214122.png]]
![[Pasted image 20260422214250.png]]
![[Pasted image 20260422214307.png]]
![[Pasted image 20260422214651.png]]
![[Pasted image 20260422214751.png]]
![[Pasted image 20260422214923.png]]
![[Pasted image 20260422215045.png]]
![[Pasted image 20260422215139.png]]
![[Pasted image 20260422215533.png]]
![[Pasted image 20260422215801.png]]
![[Pasted image 20260422215957.png]]
![[Pasted image 20260422220254.png]]
![[Pasted image 20260422220310.png]]
![[Pasted image 20260422220451.png]]
![[Pasted image 20260422220509.png]]
![[Pasted image 20260422220708.png]]
![[Pasted image 20260422220814.png]]
![[Pasted image 20260422220854.png]]

---

---

## Complemento de estudio

### Comunicación y sincronización

La comunicación transmite información; la sincronización ordena acciones. Compartir memoria resuelve dónde intercambiar datos, pero no quién puede modificarlos ni cuándo. Una **condición de carrera** aparece cuando el resultado depende del orden de accesos concurrentes sin coordinación.

Para un productor y un consumidor, una cola segura para hilos suele ser preferible a una variable global más espera activa. Un mutex protege una región crítica; una condición permite esperar un predicado que debe comprobarse en un bucle.

Un pipe POSIX se trata como flujo de bytes, no como mensajes. Definir delimitadores o longitudes y cerrar los extremos que no se usan para detectar el fin de archivo. En Python, multiprocessing.Pipe() es dúplex por defecto: no confundir esa API con el pipe POSIX unidireccional.

**Repaso:** ¿por qué compartir una variable no garantiza comunicación correcta? ¿Cómo detectarías que el productor terminó?
