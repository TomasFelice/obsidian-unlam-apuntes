---
tipo: materia
cuatrimestre: 0
estado: opcional
correlativas:
  - "[[Arquitectura de computadoras]]"
  - "[[Bases de datos]]"
  - "[[Tópicos de programación]]"
  - "[[Introducción a los Proyectos Informáticos]]"
  - "[[Introducción a la Gestión de Requisitos]]"
  - "[[Principios de Calidad de Software]]"
  - "[[Sistemas de Numeración]]"
  - "[[Introducción a los Sistemas de Información]]"
  - "[[Programación inicial]]"
  - "[[Matemática Discreta]]"
---
# Taller de integracion

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
