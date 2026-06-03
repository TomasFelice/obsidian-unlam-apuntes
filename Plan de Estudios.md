---
tipo: dashboard
---

# Plan de Estudios — Ingeniería en Informática

## Cursando

```dataview
TABLE cuatrimestre AS "Año", correlativas AS "Correlativas"
FROM ""
WHERE tipo = "materia" AND estado = "cursando"
SORT cuatrimestre ASC, file.name ASC
```

## Aprobadas

```dataview
TABLE cuatrimestre AS "Año", correlativas AS "Correlativas"
FROM ""
WHERE tipo = "materia" AND estado = "aprobada"
SORT cuatrimestre ASC, file.name ASC
```

## Pendientes

```dataview
TABLE cuatrimestre AS "Año", correlativas AS "Correlativas"
FROM ""
WHERE tipo = "materia" AND estado = "pendiente"
SORT cuatrimestre ASC, file.name ASC
```

## Vista completa por año

```dataview
TABLE cuatrimestre AS "Año", estado AS "Estado", correlativas AS "Correlativas"
FROM ""
WHERE tipo = "materia"
SORT cuatrimestre ASC, file.name ASC
```
