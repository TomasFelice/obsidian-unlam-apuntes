---
tipo: clase
fecha: 2026-08-20
tema: "Planificación: esfuerzo, duración, dependencias y camino crítico"
fecha_fuente: metadato original sin corroborar
fecha_por_confirmar: true
---

> [!todo] Fecha pendiente de corroborar
> La fecha original puede haber quedado de la plantilla. No hay capturas fechadas en esta nota para corregirla con evidencia.

# Planificación de proyectos

## Qué se planifica

Planificar consiste en organizar actividades, dependencias, recursos y criterios para alcanzar objetivos. Un modelo de proceso ayuda a identificar trabajo, pero puede adaptarse al contexto; no es obligatorio elegir siempre una norma IEEE o ISO.

Para cada tarea, definir resultado esperado, responsable y tres aspectos:

- **Esfuerzo:** trabajo necesario, por ejemplo horas-persona.
- **Duración:** tiempo transcurrido de calendario o laborable, según la convención.
- **Dependencias:** qué debe ocurrir antes y qué puede hacerse en paralelo.

Ejemplo: una tarea puede requerir tres horas-persona y extenderse dos días porque depende de una revisión. Duplicar personas no implica reducir a la mitad su duración.

## Restricciones y prioridades

El plan equilibra alcance, tiempo, costo, calidad y disponibilidad del equipo. La calidad incluye satisfacer necesidades y requisitos definidos; no debe tratarse solo como una preferencia subjetiva.

- **Pareto:** heurística para buscar causas o trabajos de gran impacto. El 80/20 no es una proporción garantizada.
- **Costo de oportunidad:** valor de la mejor alternativa a la que se renuncia.
- **Ley de Parkinson:** observación sobre cómo el trabajo puede expandirse al tiempo disponible. Reducir plazos sin fundamento puede perjudicar calidad y sostenibilidad.
- **Rendimientos decrecientes:** más recursos pueden aportar mejoras marginales menores en ciertas condiciones; no siempre desde el primer esfuerzo.
- **Costo hundido:** gasto pasado irrecuperable que no debería determinar por sí solo decisiones futuras.
- **Teoría de las restricciones:** identificar y gestionar el cuello de botella que limita el resultado global.

Según la anotación original, costo hundido y teoría de las restricciones no entraban en ese parcial; confirmar el alcance vigente en MIEL.

## Construcción del plan

1. Desglosar trabajo en entregables y tareas verificables.
2. Identificar dependencias.
3. Estimar esfuerzo y duración, incluyendo revisiones y esperas.
4. Calcular el camino crítico.
5. Asignar responsables y comprobar disponibilidad real.
6. Representar el cronograma y actualizarlo con el avance.

## Camino crítico y ejemplo complementario

El camino crítico es la secuencia de dependencias con mayor duración total en la red del proyecto, bajo los supuestos del plan. Sus tareas tienen holgura total nula en el caso básico. No es la lista de tareas «más importantes».

Si A dura 2 días; B y C dependen de A y duran 3 y 5 días; D dura 1 día y depende de ambas, los caminos son A–B–D = 6 y **A–C–D = 8 días**. C integra el camino crítico. B tiene 2 días de holgura en este ejemplo sin restricciones adicionales de recursos.

Un Gantt muestra tareas y calendario; para usarlo bien, conservar dependencias y supuestos. Si dos tareas paralelas necesitan a la misma persona a tiempo completo, revisar el plan.

**Repaso:** diferenciar esfuerzo y duración y explicar qué cambio puede desplazar el camino crítico.
