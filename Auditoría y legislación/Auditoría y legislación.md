---
tipo: materia
cuatrimestre: 3
estado: cursando
correlativas:
  - "[[Seguridad de la información]]"
---
# Auditoría y legislación

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

- Distinguir hecho/acto jurídico, contrato, licencia y confidencialidad.
- Comparar firma digital y electrónica con la Ley 25.506.
- Relacionar criterio, evidencia, hallazgo y recomendación; preservar trazabilidad.

### Recorrido por las notas

- [[Auditoría y legislación/Clases/AL - Clase 3|AL - Clase 3]] — Derecho informático y protección de datos personales
- [[Auditoría y legislación/Clases/AL - Clase 4|AL - Clase 4]] — Contratos Informáticos
- [[Auditoría y legislación/Clases/AL - Clase 5|AL - Clase 5]] — Contratos informáticos, confidencialidad y anexos
- [[Auditoría y legislación/Clases/AL - Clase 6|AL - Clase 6]] — Contratos de hosting, continuidad y escrow de código fuente
- [[Auditoría y legislación/Clases/AL - Clase 7|AL - Clase 7]] — Firma digital, documento electrónico y propiedad intelectual
- [[Auditoría y legislación/Clases/AL - Clase 8|AL - Clase 8]] — Firma electrónica, identidad digital y licencias
- [[Auditoría y legislación/Clases/AL - Clase 9|AL - Clase 9]] — Compliance, auditoría de sistemas y evidencia de auditoría
- [[Auditoría y legislación/Clases/AL - Clase 10|AL - Clase 10]] — Pericias y delitos informáticos
