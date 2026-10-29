---
tipo: materia
cuatrimestre: 4
estado: cursando
correlativas:
  - "[[Paradigmas de programación]]"
  - "[[Sistemas operativos]]"
---
# Programación concurrente

## Clases

```dataviewjs
const folder = dv.current().file.folder + "/Clases";
const pages = dv.pages(`"${folder}"`).sort(p => p.file.name);
if (pages.length === 0) {
  dv.paragraph("_No hay clases cargadas todavía._");
} else {
  dv.table(
    ["Clase", "Fecha", "Tema"],
    pages.map(p => [p.file.link, p.fecha ?? "—", p.tema ?? "—"])
  );
}
```

## Guía de estudio de los apuntes

Revisión del texto y ampliaciones: 29/10/2026. Detalle de alcance y pendientes en [[Revisión integral de apuntes]].

- Distinguir concurrencia, paralelismo, comunicación y sincronización.
- Calcular speedup, eficiencia, costo y overhead.
- Separar gridDim, blockDim y threadIdx; medir cómputo y transferencias.

### Recorrido por las notas

- [[Programación concurrente/Clases/PC - Clase 3|PC - Clase 3]] — Comunicación y problemas de concurrencia
- [[Programación concurrente/Clases/PC - Clase 4|PC - Clase 4]] — GIL, async/await, corutinas, futures y pools
- [[Programación concurrente/Clases/PC - Clase 5|PC - Clase 5]] — Desarrollo asistido por IA y revisión de concurrencia
- [[Programación concurrente/Clases/PC - Clase 6(1)|PC - Clase 6(1)]] — Computación de altas prestaciones
- [[Programación concurrente/Clases/PC - Clase 7|PC - Clase 7]] — Computación de altas prestaciones
- [[Programación concurrente/Clases/PC - Clase 8|PC - Clase 8]] — HPC, métricas, OpenMP, MPI e introducción a GPU
- [[Programación concurrente/Clases/PC - Clase 9|PC - Clase 9]] — Clase sin apuntes: contenido pendiente de recuperar
- [[Programación concurrente/Clases/PC - Clase 10|PC - Clase 10]] — CUDA: kernels, indexación y organización de grillas y bloques
- [[Programación concurrente/Clases/PC - Clase 11|PC - Clase 11]] — GPU: filtros de imágenes y procesamiento de video
- [[Programación concurrente/Clases/PC - Clase 12|PC - Clase 12]] — GPU: jerarquía de memoria, sincronización, atómicas y Sobel
- [[Programación concurrente/Clases/PC - Parcial 1|PC - Parcial 1]] — Repaso de concurrencia, procesos e hilos, OpenMP, MPI y CUDA
