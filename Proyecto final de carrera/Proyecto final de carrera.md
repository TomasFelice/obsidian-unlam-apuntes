---
tipo: materia
cuatrimestre: 5
estado: pendiente
correlativas:
  - "[[Gestión de la calidad en procesos de sistemas]]"
  - "[[Sistemas Operativos Avanzados]]"
  - "[[Estadística aplicada]]"
  - "[[Gestión aplicada al desarrollo de software 1]]"
---
# Proyecto final de carrera

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
