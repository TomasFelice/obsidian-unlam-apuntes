---
tipo: materia
cuatrimestre: 4
estado: pendiente
correlativas:
  - "[[Probabilidad y estadística]]"
  - "[[Paradigmas de programación]]"
---
# Inteligencia artificial

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
