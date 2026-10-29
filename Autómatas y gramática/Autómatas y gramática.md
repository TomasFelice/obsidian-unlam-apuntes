---
tipo: materia
cuatrimestre: 4
estado: cursando
correlativas:
  - "[[Paradigmas de programación]]"
---
# Autómatas y gramática

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

- Dominar ε, ∅, operaciones y jerarquía de Chomsky.
- Practicar Thompson → Rabin–Scott → minimización.
- Justificar índices ligados, ambigüedad, CYK, pila y estrategia de MT.

### Recorrido por las notas

- [[Autómatas y gramática/Clases/AG - Clase 1|AG - Clase 1]] — Lenguajes, alfabetos, operaciones y jerarquía de Chomsky
- [[Autómatas y gramática/Clases/AG - Clase 2|AG - Clase 2]] — Lenguajes regulares, expresiones regulares y BNF
- [[Autómatas y gramática/Clases/AG - Clase 3|AG - Clase 3]] — Expresiones regulares y autómatas finitos
- [[Autómatas y gramática/Clases/AG - Clase 4|AG - Clase 4]] — Thompson, Rabin–Scott y minimización de Moore
- [[Autómatas y gramática/Clases/AG - Clase 5|AG - Clase 5]] — Gramáticas independientes del contexto y ambigüedad
- [[Autómatas y gramática/Clases/AG - Clase 6|AG - Clase 6]] — Gramáticas, CYK y autómatas de pila
- [[Autómatas y gramática/Clases/AG - Clase 7|AG - Clase 7]] — Repaso de pila, lenguajes tipo 1 y 0 y máquinas de Turing
- [[Autómatas y gramática/Clases/AG - Clase 8|AG - Clase 8]] — Diseño y prueba de máquinas de Turing
- [[Autómatas y gramática/Clases/AG - Repaso Parcial 1|AG - Repaso Parcial 1]] — Repaso: Thompson, Rabin–Scott, Moore y regularidad de lenguajes
