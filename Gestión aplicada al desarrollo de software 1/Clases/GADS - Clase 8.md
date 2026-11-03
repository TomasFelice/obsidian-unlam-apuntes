---
tipo: clase
fecha: 2026-10-29
tema: IA aplicada al desarrollo desde la arquitectura
fecha_fuente: "Inferida de los nombres de las capturas (20261029); fecha original del apunte: 2026-12-29"
fecha_por_confirmar: true
---
> [!todo] Fecha pendiente de corroborar
> Se usa provisionalmente el **29/10/2026**, inferido de los nombres de las cinco capturas. La fecha original era **29/12/2026**. La fecha de una captura no confirma por sí sola la fecha de la clase.

# IA aplicada al desarrollo desde la arquitectura

> [!abstract] Idea central
> Aplicar IA a un caso aislado puede ayudar a producir un resultado. Para repetirlo a escala, hay que diseñar un **sistema**: entradas, decisiones, herramientas, estado, validaciones y supervisión humana.

## Parte 1 - Hacer crecer el problema

### Situación 1: un sitio para un contador

> Un contador pide un sitio web de presentación.

Una forma de encararlo con IA es reunir la información del cliente, definir lineamientos, proponer un diseño y convertirlo en código. Antes de generar la página, hay que responder:

- ¿Quién es el profesional y a qué público se dirige?
- ¿Qué servicios ofrece?
- ¿Por qué elegirlo?
- ¿Cómo puede contactarlo una persona interesada?

El formulario de contacto es una posible funcionalidad para resolver la última pregunta; también hay que definir qué sucede cuando alguien lo envía.

### Situación 2: sitios para 100 contadores

Repetir manualmente las mismas instrucciones 100 veces no resuelve la coordinación del trabajo. La idea es convertir el caso puntual en un **proceso repetible**, con criterios comunes y datos particulares para cada cliente.

| Caso aislado | Proceso repetible |
|---|---|
| El humano coordina y la IA ayuda. | El sistema coordina y el humano supervisa. |
| Muchas decisiones quedan en la cabeza de quien trabaja. | Las decisiones, reglas y excepciones se hacen explícitas. |
| Se revisa cada resultado de manera informal. | Se definen criterios de aceptación y puntos de revisión. |

La clave es **sistematizar**. La pregunta de la diapositiva es: «¿Qué decisiones antes estaban en nuestra cabeza?».

![[Pasted image 20261029192116.png]]

### Primero el problema, después la IA

Antes de elegir la tecnología, debemos preguntarnos:

- **Objetivo:** ¿qué problema queremos resolver?
- **Entradas:** ¿qué información recibimos y qué puede faltar?
- **Decisiones:** ¿cuáles tienen reglas claras y cuáles requieren interpretación?
- **Salidas:** ¿qué resultado esperamos y cómo lo aceptamos?
- **Fallos:** ¿dónde puede fallar el proceso y cómo se recupera?
- **Supervisión:** ¿qué decisiones necesitan intervención humana?

## Parte 2 - Las piezas

### Chat, flujo de trabajo y agente

Un **LLM** es un modelo de lenguaje. Una aplicación puede usarlo para conversar, ejecutar pasos predefinidos o decidir cómo avanzar hacia un objetivo.

| Concepto | Característica principal | Ejemplo aplicado |
|---|---|---|
| **Chat** | Interfaz conversacional de interacción con el usuario. | Conversar sobre el diseño del sitio. |
| **Flujo de trabajo o workflow** | El recorrido está definido por el sistema, aunque algunos pasos usen IA. | Recibir brief → generar propuesta → validar → pedir aprobación. |
| **Agente** | El modelo decide dinámicamente los próximos pasos y el uso de herramientas para alcanzar un objetivo. | Inspeccionar el proyecto, elegir qué modificar, ejecutar comprobaciones y ajustar según el resultado. |

La distinción entre workflow y agente se basa en **quién controla el recorrido**, siguiendo el criterio de [Anthropic: Building effective agents](https://www.anthropic.com/research/building-effective-agents).

> [!important] Precisión conceptual
> Un chat puede generar contenido, usar herramientas e incluso servir como interfaz de un agente. No equivale simplemente a un buscador. Un agente tiene un grado de autonomía, limitado por sus herramientas, permisos y condiciones de parada; no implica autonomía total ni resultados correctos garantizados.

### Skill: capacidad reutilizable

En el sentido usado en esta clase, una **skill** organiza lo necesario para resolver una tarea concreta de manera reutilizable. Ejemplos: analizar un brief, extraer información de un PDF, generar un sitemap, revisar accesibilidad o crear tickets en Jira.

No se limita a una consigna aislada: debe dejar claros estos elementos, aunque su implementación varíe según la plataforma:

| Elemento | Pregunta que responde |
|---|---|
| **Entrada (input)** | ¿Qué datos necesita? |
| **Reglas** | ¿Qué criterios y restricciones debe respetar? |
| **Herramientas** | ¿Qué recursos o acciones puede usar? |
| **Validaciones** | ¿Cómo se comprueba el resultado? |
| **Salida (output)** | ¿Qué entrega y en qué formato? |

**Ejemplo complementario:** una skill para analizar un brief recibe el documento, identifica servicios y público objetivo, marca datos faltantes y entrega una ficha estructurada. Su validación debe comprobar que distingue información confirmada de supuestos.

### Código tradicional, LLM o agente

| Necesidad | Enfoque adecuado |
|---|---|
| Reglas explícitas y resultados verificables: campos obligatorios, formatos o cálculos. | Código determinista y validaciones. |
| Interpretar lenguaje natural ambiguo o proponer alternativas. | Una llamada a un LLM puede ser suficiente. |
| Ejecutar una secuencia conocida con algunos pasos de interpretación. | Workflow que combina código y LLM. |
| Elegir y adaptar los pasos según lo que se descubre. | Agente con herramientas y límites definidos. |

Una buena arquitectura **combina partes deterministas con partes probabilísticas**. Que una tarea use IA no significa que necesite un agente. El código tradicional también puede tener errores: hay que verificar tanto las reglas implementadas como los resultados generados.

## Parte 3 - Contexto, estado y memoria

### Contexto relevante antes que contexto enorme

El modelo combina lo aprendido durante su entrenamiento con el contexto disponible en la ejecución. Para trabajar con datos actuales o particulares del cliente, esos datos deben proporcionarse o recuperarse mediante herramientas.

Las instrucciones, el historial, los documentos y los resultados de herramientas incorporados a la entrada ocupan espacio en una **ventana de contexto limitada**. Un archivo guardado no está necesariamente disponible para el modelo: hay que seleccionar y aportar su contenido relevante.

> **Regla práctica:** contexto relevante > contexto enorme.

### Tres conceptos distintos

| Concepto | Qué representa | Ejemplo del sitio |
|---|---|---|
| **Contexto** | Información disponible para la invocación actual del modelo. | Brief, reglas de diseño y contenido del archivo que se está editando. |
| **Estado** | Situación del proceso y resultados producidos hasta ahora. | Brief validado, diseño pendiente de aprobación y versión actual del sitio. |
| **Memoria** | Información persistida para recuperarla en futuras interacciones o ejecuciones. | Preferencias de estilo del cliente. |

Parte del estado o de la memoria puede cargarse en el contexto. Son conceptos relacionados, pero no intercambiables. El estado debe permitir saber qué ocurrió y qué falta; una preferencia recordada no demuestra que una tarea se haya completado.

### La memoria ayuda; la validación controla

No alcanza con pedirle al modelo que «recuerde» una regla crítica. La diapositiva propone controles explícitos:

- **Esquemas (schemas):** comprobar la estructura de entradas y salidas.
- **Pruebas (tests):** verificar comportamientos esperados.
- **Permisos:** limitar las acciones disponibles.
- **Validaciones:** comprobar reglas y criterios de aceptación.
- **Puntos de control (checkpoints):** registrar avances y establecer revisiones antes de continuar.

Por ejemplo, recordar que debe existir un formulario no demuestra que funcione: hay que comprobar su envío y el resultado esperado.

![[Pasted image 20261029193807.png]]

## Parte 4 - Herramientas y MCP

### Del modelo al mundo real

Sin herramientas, el modelo genera una respuesta a partir de su entrada. Con herramientas, la aplicación puede permitirle **consultar información y ejecutar acciones**: acceder a GitHub o Jira, navegar, leer archivos, consultar bases de datos o llamar APIs.

Describir una acción no equivale a ejecutarla. Para afirmar que se creó un ticket, por ejemplo, hay que contar con el resultado de la herramienta correspondiente.

![[Pasted image 20261029193905.png]]

### MCP: Model Context Protocol

**MCP** es un protocolo abierto que estandariza el intercambio entre aplicaciones de IA y servidores que exponen capacidades. Permite ofrecer **herramientas**, **recursos de datos** y **plantillas de prompts** mediante una interfaz común.

La arquitectura distingue una aplicación anfitriona (**host**), clientes MCP y servidores MCP. Un servidor conecta las capacidades disponibles con los sistemas correspondientes, como GitHub o Jira. Fuente: [documentación oficial de MCP: arquitectura](https://modelcontextprotocol.io/docs/learn/architecture).

La diapositiva lo resume así: **agente → MCP → sistemas externos**. Es un esquema conceptual; la aplicación anfitriona y sus clientes participan en la comunicación.

> **Idea clave:** separar la decisión sobre qué hacer de los detalles de integración con cada sistema. MCP facilita esa integración; no reemplaza el razonamiento del agente ni garantiza que una acción sea correcta.

![[Pasted image 20261029194137.png]]

## Parte 5 - Caso real presentado en clase

El problema presentado excedía generar HTML. Consistía en transformar:

**Brief incompleto → decisiones de negocio → diseño → contenido → software funcional.**

Las restricciones de la diapositiva eran:

- Cada cliente es distinto.
- La información está incompleta.
- Hay decisiones subjetivas.
- Existen reglas propias del rubro.
- La calidad del modelo es variable.

Por eso, la arquitectura debe organizar cómo se resuelven las decisiones y cómo se comprueba cada resultado. Una página generada puede verse bien y aun así no responder al objetivo del cliente o tener funcionalidades incompletas.

![[Pasted image 20261029194632.png]]

### Ejemplo complementario: convertir el caso en un proceso

La siguiente propuesta aplica las ideas de la clase; no describe una implementación confirmada del caso real.

| Etapa | Resultado esperado | Control para avanzar |
|---|---|---|
| Relevar el brief | Datos confirmados y preguntas pendientes. | Resolver faltantes críticos sin inventar información. |
| Definir la propuesta | Público, servicios y objetivo del sitio. | Aprobación de las decisiones de negocio. |
| Diseñar y redactar | Estructura, diseño y contenido. | Revisar coherencia con el brief y las reglas del cliente. |
| Implementar | Sitio y funcionalidades acordadas. | Comprobar enlaces, formulario y comportamiento en distintos tamaños de pantalla. |
| Revisar la entrega | Versión aceptada. | Registrar aprobación y pendientes antes de publicar. |

El sistema conserva el **estado** de cada cliente, invoca **skills** reutilizables, aporta el **contexto** necesario y usa **herramientas** para actuar. La IA interpreta y propone; los controles verifican y las personas resuelven las decisiones que requieren su criterio.

## Preguntas de repaso

1. ¿Qué cambia al pasar de un sitio para un contador a sitios para 100 contadores? **Hay que explicitar y coordinar un proceso repetible.**
2. ¿Qué distingue un workflow de un agente? **El recorrido predefinido frente a la decisión dinámica de los pasos.**
3. ¿Qué debe definir una skill? **Entradas, reglas, herramientas, validaciones y salidas.**
4. ¿Por qué contexto, estado y memoria no son lo mismo? **Uno es la información disponible ahora; otro registra el avance; la tercera conserva información para recuperarla después.**
5. ¿Qué aporta MCP? **Una interfaz común para integrar capacidades y datos externos.**
6. ¿Por qué no basta con generar HTML? **Porque también hay decisiones de negocio, información faltante y funcionalidades que validar.**
