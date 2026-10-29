---
tipo: clase
fecha: 2026-04-20
tema: "GPU: filtros de imágenes y procesamiento de video"
fecha_fuente: metadato original sin corroborar
fecha_por_confirmar: true
---

> [!todo] Fecha pendiente de corroborar
> La fecha original puede haber quedado de la plantilla. No hay capturas fechadas en esta nota para corregirla con evidencia.

# GPU

## Ejemplo escala de grises

La cantidad de bloques, la determina la cantidad de píxeles?

El prog, define la cantidad de hilos del bloque.
La cantidad de bloques totales, define el código.

Si tenemos una img de 1024 × 768. Lo primero que tenemos que hacer es dividir en bloques.
- El prog define la cantidad de hilos de cada bloque
- Ejemplo:
	- 16h para X
	- 19h para Y
	- Bloque(16,19,1)
	- Grilla(64,41,1)
- Según esto, tenemos 797.696 hilos en total
- La cantidad y el tamaño de los bloques influyen en ocupación y planificación; más bloques no siempre mejoran ni empeoran el rendimiento.
- la CPU se afecta en cuando mayor cantidad de información tenga que transferir. La espera, la velocidad del PCI.
- ESTUDIAR PARA PARCIAL

---

## Formulas

> BYN = 0.299R + 0.587G + 0.114B
> Inversión => C_{final} = 1.0 - C_{original} (si son 3 píxeles, se hace por cada uno)

---

## Videos

> Un video es un conjunto de frames, que se reproducen constantemente según cierta frecuencia.
> Un frame es una imagen estática

FPS: Frame Por Segundo. A mayor FPS, más fluido se ve.

### ¿Cómo hacemos escala de grises a un video?

La forma más fácil es aplicandolo el filtro frame por frame.
OpenCV es una lib de visión artificial que permite manipular videos.

#### Práctica

1er inversión
2do escala grises
3er normal
4to brillo

---

## Complemento de estudio

### Valores y unidades de los filtros

Para canales de 8 bits, invertir significa **255 − C**. En [0,1], usar **1 − C**. Aplicar a cada canal, sin confundir píxel con canal.

El gris 0,299R + 0,587G + 0,114B combina canales. Verificar su orden: OpenCV suele representar color en BGR.

El tiempo total de video incluye decodificación, transferencias, kernel y escritura o visualización. **FPS = cuadros / segundos**. Comparar contra una referencia y comprobar bordes, tamaños no divisibles por el bloque y rangos de intensidad.
