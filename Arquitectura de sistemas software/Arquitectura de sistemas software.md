---
tipo: materia
cuatrimestre: 3
estado: cursando
correlativas:
  - "[[Diseño de software]]"
---
# Arquitectura de sistemas software
## Bibliografía
[[Software-Fundamentals of Software Architecture 1.pdf]]

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

- Comparar estilos a partir de atributos de calidad y restricciones.
- Distinguir modularidad, despliegue, balanceo, autoescalado y CDN.
- Documentar decisiones con ADR y representar alcance con C4.

### Recorrido por las notas

- [[Arquitectura de sistemas software/Clases/AS - Clase 4|AS - Clase 4]] — Estilos arquitectónicos y comparación de arquitecturas
- [[Arquitectura de sistemas software/Clases/AS - Clase 5|AS - Clase 5]] — Patrones de arquitectura y antipatrones de decisión
- [[Arquitectura de sistemas software/Clases/AS - Clase 6|AS - Clase 6]] — Escalabilidad, balanceo y CDN: caso Netflix
- [[Arquitectura de sistemas software/Clases/AS - Clase 7|AS - Clase 7]] — Agentes como servicio y TOGAF
- [[Arquitectura de sistemas software/Clases/AS - Clase 8|AS - Clase 8]] — Proceso de diseño de arquitectura y TOGAF ADM
- [[Arquitectura de sistemas software/Clases/AS - Clase 9|AS - Clase 9]] — Modelo C4
- [[Arquitectura de sistemas software/Clases/Trabajo Practico N2|Trabajo Practico N2]]
