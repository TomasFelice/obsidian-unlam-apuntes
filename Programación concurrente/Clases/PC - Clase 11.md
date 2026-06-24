---
tipo: clase
fecha: 2026-04-20
tema: GPU
---
# GPU
## Ejemplo escala de grises
La cant de bloques, la determina la cantidad de pixeles?

El prog, define la cant de hilos del bloque.
La cant de bloques totales, define el codigo.

Si tenemos una img de 1024x786. Lo primero que tenemos que hacer es dividir en bloques.
- El prog define la cant de hilos de cada bloque
- Ejemplo:
	- 16h para X
	- 19h para Y
	- Bloque(16,19,1)
	- Grilla(64,41,1)
- Segun esto, tenemos 797.696 hilos en total
- a mayor cant de bloques, se afecta la GPU
- la CPU se afecta en cuando mayor cantidad de informacion tenga que transferir. La espera, la velocidad del PCI.
- ESTUDIAR PARA PARCIAL

---
## Formulas
> BYN = 0.299R + 0.587G + 0.114B
> Inversion => C_{final} = 1.0 - C_{original} (si son 3 pixeles, se hace por cada uno)

--- 
## Videos
> Un video es un conjunto de frames, que se reproducen constantemente segun cierta frecuencia.
> Un frame es una imagen estatica

FPS: Frame Por Segundo. A mayor FPS, mas fluido se ve.

### Como hacemos escala de grises a un video?
La forma mas facil es aplicandolo el filtro frame por frame.
OpenCV es una lib de vision artificial que permite manipular videos.

#### Practica
1er inversion
2do escala grises
3er normal
4to brillo