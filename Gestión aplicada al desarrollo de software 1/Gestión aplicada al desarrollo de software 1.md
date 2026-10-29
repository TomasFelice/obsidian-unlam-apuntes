---
tipo: materia
cuatrimestre: 4
estado: pendiente
correlativas:
  - "[[Requisitos Avanzados]]"
  - "[[Gestion de las organizaciones]]"
  - "[[Diseño de software]]"
---
# Gestión aplicada al desarrollo de software 1

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

- Distinguir producto, proceso, ciclo de vida y modelo de negocio.
- Definir indicadores con unidad, período y denominador.
- Resolver esfuerzo/duración, camino crítico y causa–evento–consecuencia.

### Recorrido por las notas

- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 1|GADS - Clase 1]] — Producto, proceso, proyecto y modelos de negocio
- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 2|GADS - Clase 2]] — Ciclos de vida, selección de modelos y modelos de negocio
- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 3|GADS - Clase 3]] — Marketing digital: propuesta de valor, embudo e indicadores
- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 4|GADS - Clase 4]] — Modelos de procesos
- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 5|GADS - Clase 5]] — Estimación de proyectos e indicadores de producto y proceso
- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 6|GADS - Clase 6]] — Planificación: esfuerzo, duración, dependencias y camino crítico
- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 7|GADS - Clase 7]] — Gestión de riesgos: identificación, priorización y respuestas
- [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Parcial 1|GADS - Parcial 1]] — Repaso: negocio, visión y ciclo de vida
