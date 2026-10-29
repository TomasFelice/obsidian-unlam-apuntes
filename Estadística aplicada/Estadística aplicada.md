---
tipo: materia
cuatrimestre: 4
estado: cursando
correlativas:
  - "[[Probabilidad y estadística]]"
---
# Estadística aplicada

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

- Fijar soporte y parametrización antes de calcular.
- Distinguir verosimilitud, prior, posterior, media y MAP.
- Usar Clase 3 como versión completa; revisar la prior truncada del ejemplo exponencial.

### Recorrido por las notas

- [[Estadística aplicada/Clases/Clase 3|Clase 3]] — Inferencia bayesiana: modelo geométrico y proceso de Poisson
- [[Estadística aplicada/Clases/Clase 3(1)|Clase 3(1)]] — Inferencia bayesiana: modelo geométrico y proceso de Poisson
- [[Estadística aplicada/Clases/Clase 4|Clase 4]] — Inferencia bayesiana: modelo geométrico y proceso de Poisson
