---
tipo: revision
fecha: 2026-10-29
---
# Revisión integral de apuntes

Se revisaron las **63 fichas de materias** de la bóveda. **Siete materias tienen 55 notas de clase, repaso o trabajo práctico**; esas notas fueron editadas. Las otras **56 fichas no contienen apuntes de clase** y se mantienen como estaban: no se inventó contenido de cursadas sin material.

## Qué se hizo

- Corrección de ortografía, redacción y terminología del texto editable.
- Corrección de errores conceptuales y numéricos, con ampliaciones y preguntas de repaso.
- Reescritura de las notas más fragmentarias de gestión y de las observaciones del TP de arquitectura.
- Conservación de nombres de archivo, capturas, adjuntos y enlaces de referencia. Se añadieron recorridos de estudio en las siete fichas con apuntes.
- Con la aclaración del autor de que fechas y temas podían haber quedado de la plantilla, se corrigieron 24 fechas a partir de las capturas y se ajustaron otros 23 temas al contenido. Los valores de fecha reemplazados se conservan en `fecha_original`. Los estados académicos se mantienen.

Los apartados **Complemento de estudio**, los ejemplos propuestos y las aclaraciones son elaboraciones de esta revisión; no son citas del docente ni soluciones oficiales. Las referencias web se incorporaron junto a los conceptos que sustentan.

## Materias con contenido revisado

| Materia | Notas | Mejoras principales |
|---|---:|---|
| [[Arquitectura de sistemas software/Arquitectura de sistemas software]] | 7 | Estilos, monolito modular, ADR, balanceo/CDN, TOGAF, C4 y redacción del TP |
| [[Auditoría y legislación/Auditoría y legislación]] | 8 | Hecho y acto jurídico, contratos, confidencialidad, firma, licencias, auditoría y evidencia |
| [[Autómatas y gramática/Autómatas y gramática]] | 9 | Lenguajes, conversiones, minimización, ambigüedad, CYK, pila y MT |
| [[Estadística aplicada/Estadística aplicada]] | 3 | Ejemplo geométrico resuelto, intervalo de credibilidad, Poisson y prior truncada |
| [[Gestión aplicada al desarrollo de software 1/Gestión aplicada al desarrollo de software 1]] | 8 | Producto/proceso, negocio, métricas, estimación, planificación y riesgos |
| [[Programación concurrente/Programación concurrente]] | 11 | IPC, GIL, HPC, MPI/OpenMP, CUDA, memoria y respuestas de parcial |
| [[Sistemas Operativos Avanzados/Sistemas Operativos Avanzados]] | 9 | Electrónica, FSM, tiempo real, timers, Android, IoT y microservicios |

## Correcciones que conviene estudiar

1. **CUDA:** blockDim cuenta hilos por bloque; gridDim cuenta bloques. Para 1024 × 768 con bloques de 16 × 19 se lanzan 797.696 hilos, de los que 786.432 corresponden a píxeles.
2. **Concurrencia:** el acumulador local del ejemplo C++ no requiere una atómica. Los mecanismos de sincronización no son todos exclusivos de hilos. Bloqueante/no bloqueante y modo síncrono de MPI son clasificaciones distintas.
3. **Electrónica:** voltaje es diferencia de potencial, no velocidad de corriente. Fuentes con igual tensión nominal no son automáticamente aptas para conexión en paralelo. PWM y DAC no son equivalentes.
4. **Tiempo real y Android:** importa cumplir el plazo; un STR puede procesar datos. Un Service no crea automáticamente un hilo ni excluye Activities. Los callbacks de timers de software FreeRTOS no se ejecutan como ISR.
5. **Estadística:** con los datos geométricos y prior uniforme, la posterior es Beta(5,11). En el ejemplo exponencial, la prior Uniforme(0,1) produce una posterior truncada, aunque la diapositiva la identifica como Gamma sin explicitar esa restricción.
6. **Gestión:** ingresos menos egresos no define por sí solo una tasa de rentabilidad. SaaS y suscripción no son sinónimos. P × I con escalas 1–5 es un índice de prioridad, no daño monetario esperado.
7. **Legislación:** un hecho jurídico también puede ser humano; el NDA no es requisito universal de todo contrato. Se añadieron referencias oficiales para datos personales, firma y propiedad intelectual.

## Duplicados y material incompleto

- [[Estadística aplicada/Clases/Clase 3]] es la versión más completa. [[Estadística aplicada/Clases/Clase 3(1)]] y [[Estadística aplicada/Clases/Clase 4]] repiten su comienzo; se conservaron y enlazaron.
- [[Programación concurrente/Clases/PC - Clase 6(1)]] se superpone con [[Programación concurrente/Clases/PC - Clase 7]]. No se fusionaron porque podrían contener material visual propio.
- [[Autómatas y gramática/Clases/AG - Repaso Parcial 1]] reproduce buena parte de [[Autómatas y gramática/Clases/AG - Clase 4]]; se conserva como acceso de repaso.
- [[Programación concurrente/Clases/PC - Clase 9]] solo registra una inasistencia. Se añadieron enlaces para retomar continuidad, sin atribuirle una clase inventada.
- En ejercicios con respuestas V/F o fórmulas incompletas, contrastar las consignas de las capturas; se señala especialmente la expresión de lenguaje al final de [[Autómatas y gramática/Clases/AG - Clase 5]].
- Confirmar el modelo del sensor de corriente anotado como «ACS721» y la corrección del circuito en [[Sistemas Operativos Avanzados/Clases/SOA - Clase 2]].
- Confirmar en MIEL fechas de examen, entregas, modalidad y alcance de evaluación. Las notas conservan anuncios de clase que pueden haber cambiado.

## Fechas y temas de los metadatos

El autor aclaró que en muchas notas quedaron sin completar tanto la fecha como el tema. Por eso esos campos no se consideran una fuente suficiente para clasificar el contenido.

Se ajustaron **24 fechas** usando los días de los nombres de las capturas como referencia y se revisaron **23 temas adicionales** contra el texto y los títulos de cada nota. Las fechas deducidas llevan el campo **fecha_inferida: true** y la fuente **nombre de capturas**; el valor reemplazado se conserva en **fecha_original**. Son fechas inferidas del material, no una confirmación independiente del día de cursada.

### Fechas corregidas y notas con varios días

Cuando una nota reúne capturas de varios días, **fecha** usa el primero y **fechas_contenido** registra todos. No se dividió la nota ni se descartó material.

| Nota | Fecha anterior | Fecha usada | Días del material |
|---|---|---|---|
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 2]] | 2026-08-18 | 2026-08-25 | 2026-08-25 |
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 3]] | 2026-08-18 | 2026-09-01 | 2026-09-01 |
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 4]] | 2026-08-18 | 2026-09-08 | 2026-09-08, 2026-09-15 |
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 7]] | 2026-09-29 | 2026-10-13 | 2026-10-13 |
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 8]] | 2026-09-29 | 2026-10-20 | 2026-10-20 |
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 9]] | 2026-09-29 | 2026-10-27 | 2026-10-27 |
| [[Programación concurrente/Clases/PC - Clase 10]] | 2026-05-13 | 2026-06-03 | 2026-06-03 |
| [[Programación concurrente/Clases/PC - Clase 12]] | 2026-04-20 | 2026-06-17 | 2026-06-17 |
| [[Programación concurrente/Clases/PC - Clase 5]] | 2026-04-20 | 2026-05-06 | 2026-05-06 |
| [[Programación concurrente/Clases/PC - Parcial 1]] | 2026-04-20 | 2026-06-20 | 2026-06-20 |
| [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 4]] | 2026-08-20 | 2026-09-10 | 2026-09-10 |
| [[Autómatas y gramática/Clases/AG - Clase 1]] | 2026-04-20 | 2026-08-26 | 2026-08-26 |
| [[Autómatas y gramática/Clases/AG - Clase 2]] | 2026-04-20 | 2026-08-28 | 2026-08-28 |
| [[Autómatas y gramática/Clases/AG - Clase 3]] | 2026-04-20 | 2026-09-04 | 2026-09-04 |
| [[Autómatas y gramática/Clases/AG - Clase 4]] | 2026-04-20 | 2026-09-11 | 2026-09-11 |
| [[Autómatas y gramática/Clases/AG - Clase 6]] | 2026-10-02 | 2026-10-09 | 2026-10-09 |
| [[Autómatas y gramática/Clases/AG - Clase 7]] | 2026-10-02 | 2026-10-16 | 2026-10-16, 2026-10-23 |
| [[Autómatas y gramática/Clases/AG - Clase 8]] | 2026-10-02 | 2026-10-23 | 2026-10-23 |
| [[Autómatas y gramática/Clases/AG - Repaso Parcial 1]] | 2026-04-20 | 2026-09-11 | 2026-09-11 |
| [[Auditoría y legislación/Clases/AL - Clase 10]] | 2026-06-09 | 2026-06-23 | 2026-06-23 |
| [[Auditoría y legislación/Clases/AL - Clase 6]] | 2026-05-05 | 2026-05-19 | 2026-05-19 |
| [[Auditoría y legislación/Clases/AL - Clase 7]] | 2026-04-20 | 2026-06-02 | 2026-06-02 |
| [[Auditoría y legislación/Clases/AL - Clase 9]] | 2026-06-09 | 2026-06-16 | 2026-06-16 |
| [[Arquitectura de sistemas software/Clases/AS - Clase 5]] | 2026-04-27 | 2026-04-27 | 2026-04-27, 2026-05-04 |
| [[Arquitectura de sistemas software/Clases/AS - Clase 9]] | 2026-05-18 | 2026-06-01 | 2026-06-01 |

### Fechas pendientes por falta de evidencia

En estas **11 notas** se conserva el valor anterior con **fecha_por_confirmar: true**. No se asignó una fecha por el número de clase ni se completó una secuencia semanal por suposición.

| Nota | Valor sin corroborar |
|---|---|
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 1]] | 2026-08-18 |
| [[Sistemas Operativos Avanzados/Clases/SOA - Clase 5]] | 2026-08-18 |
| [[Programación concurrente/Clases/PC - Clase 11]] | 2026-04-20 |
| [[Programación concurrente/Clases/PC - Clase 8]] | 2026-05-13 |
| [[Programación concurrente/Clases/PC - Clase 9]] | 2026-05-13 |
| [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 2]] | 2026-08-20 |
| [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 3]] | 2026-08-20 |
| [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 5]] | 2026-08-20 |
| [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 6]] | 2026-08-20 |
| [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Clase 7]] | 2026-08-20 |
| [[Gestión aplicada al desarrollo de software 1/Clases/GADS - Parcial 1]] | 2026-08-20 |

## Alcance del material visual

Se conservaron las **1.036 imágenes PNG distintas enlazadas desde las notas** y los adjuntos referenciados. Se utilizó reconocimiento de texto como apoyo y se inspeccionaron visualmente las capturas necesarias para resolver ambigüedades del ejemplo bayesiano. El OCR no permite dar por verificadas todas las fórmulas manuscritas, conexiones de circuitos, diagramas ni respuestas encerradas en imágenes. Las correcciones de texto no modifican las capturas originales, que pueden seguir mostrando simplificaciones o errores del material de clase.

No se transcribieron íntegramente las capturas, no se ejecutaron proyectos de JFLAP/Arduino/Android/CUDA y no se revisaron completos los PDF de bibliografía ni los videos enlazados. Los ejemplos numéricos agregados se comprobaron por cálculo; las pruebas de software mencionadas son propuestas de estudio, salvo indicación expresa.

## Materias sin apuntes cargados

Las siguientes fichas solo contienen metadatos y el listado dinámico de clases. Para revisarlas académicamente hace falta incorporar sus apuntes:

- [[Álgebra y Geometría Analítica 1/Álgebra y Geometría Analítica 1]]
- [[Álgebra y Geometría Analítica 2/Álgebra y Geometría Analítica 2]]
- [[Algoritmos y estructuras de datos/Algoritmos y estructuras de datos]]
- [[Análisis de sistemas/Análisis de sistemas]]
- [[Análisis Matemático 1/Análisis Matemático 1]]
- [[Análisis Matemático 2/Análisis Matemático 2]]
- [[Análisis Matemático 3/Análisis Matemático 3]]
- [[Arquitectura de computadoras/Arquitectura de computadoras]]
- [[Bases de datos Aplicada/Bases de datos Aplicada]]
- [[Bases de datos/Bases de datos]]
- [[Ciencia de datos/Ciencia de datos]]
- [[Computación 1/Computación 1]]
- [[Computación 2/Computación 2]]
- [[Diseño de software/Diseño de software]]
- [[Electiva 1/Electiva 1]]
- [[Electiva 2/Electiva 2]]
- [[Electiva 3/Electiva 3]]
- [[Física 1/Física 1]]
- [[Física 2/Física 2]]
- [[Fundamentos de Sistemas Embebidos/Fundamentos de Sistemas Embebidos]]
- [[Gestión aplicada al desarrollo de software 2/Gestión aplicada al desarrollo de software 2]]
- [[Gestión de la calidad en procesos de sistemas/Gestión de la calidad en procesos de sistemas]]
- [[Gestion de las organizaciones/Gestion de las organizaciones]]
- [[Gestión de proyectos/Gestión de proyectos]]
- [[Ingles 1/Ingles 1]]
- [[Ingles 2/Ingles 2]]
- [[Ingles 3/Ingles 3]]
- [[Ingles 4/Ingles 4]]
- [[Innovación y emprendedorismo/Innovación y emprendedorismo]]
- [[Inteligencia artificial aplicada/Inteligencia artificial aplicada]]
- [[Inteligencia artificial/Inteligencia artificial]]
- [[Introducción a la Gestión de Requisitos/Introducción a la Gestión de Requisitos]]
- [[Introducción a los Proyectos Informáticos/Introducción a los Proyectos Informáticos]]
- [[Introducción a los Sistemas de Información/Introducción a los Sistemas de Información]]
- [[Lenguajes y compiladores/Lenguajes y compiladores]]
- [[Matemática aplicada/Matemática aplicada]]
- [[Matemática Discreta/Matemática Discreta]]
- [[Paradigmas de programación/Paradigmas de programación]]
- [[Práctica profesional supervisada/Práctica profesional supervisada]]
- [[Principios de Calidad de Software/Principios de Calidad de Software]]
- [[Principios de diseño de sistemas/Principios de diseño de sistemas]]
- [[Probabilidad y estadística/Probabilidad y estadística]]
- [[Programación avanzada/Programación avanzada]]
- [[Programación Estructurada Básica/Programación Estructurada Básica]]
- [[Programación inicial/Programación inicial]]
- [[Proyecto final de carrera/Proyecto final de carrera]]
- [[Redes de computadoras/Redes de computadoras]]
- [[Requisitos Avanzados/Requisitos Avanzados]]
- [[Responsabilidad social universitaria/Responsabilidad social universitaria]]
- [[Seguridad aplicada y forensia/Seguridad aplicada y forensia]]
- [[Seguridad de la información/Seguridad de la información]]
- [[Sistemas de Numeración/Sistemas de Numeración]]
- [[Sistemas operativos/Sistemas operativos]]
- [[Taller de integracion/Taller de integracion]]
- [[Tópicos de programación/Tópicos de programación]]
- [[Virtualización de Hardware/Virtualización de Hardware]]
