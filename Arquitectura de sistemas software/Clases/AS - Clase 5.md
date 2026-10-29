---
tipo: clase
fecha: 2026-04-27
tema: "Patrones de arquitectura y antipatrones de decisión"
fecha_fuente: nombre de capturas
fecha_inferida: true
fechas_contenido:
  - 2026-04-27
  - 2026-05-04
---

> [!note] Material de varias fechas
> Las capturas corresponden a 2026-04-27 y 2026-05-04. El campo `fecha` usa la primera; `fechas_contenido` registra todas.

# Patrones de arquitectura

> Como saber cual elegir?

## Monolito

Es malo cuando se implementa mal.
Su conveniencia depende de los límites internos, requisitos y costos de operación.
Lo que define el monolito, es que todo el despliegue ocurre a la vez (todo junto)

## Microservicios

Se intenta usar como "marketing" para vender que es escalable (hype).
La mayoría de las empresas que no pudieron implementarlo bien, es que no tenian el suficiente conocimiento del dominio y por falta de criterio.

## Monolito a Microservicios

La clave de la migración es separarlo en **etapas**

## Arquitectura por capas

Puede ser como lo prefieras. Por ejemplo:
- Comunicación (HTTP, tRPC, api, CLI)
- Dominio
- Acceso a datos (db, memoria, etc.)

### Clean / Hexagonal

Plantean las capas de una manera particular.
Buscan aislar el dominio de detalles externos mediante límites y dependencias explícitas. No requieren conocer todo el dominio antes de comenzar.

## Monolito Modular

... (hasta acá vimos el video de BettaTech. Continuar. [https://www.youtube.com/watch?v=q3YQy1lJutw&t=14s](https://www.youtube.com/watch?v=q3YQy1lJutw&t=14s "https://www.youtube.com/watch?v=q3yqy1ljutw&t=14s"))

---

# Antipatrones de Software

## Antipatrones de Decisiones

![[Antipatrones.jpg]]

### Covering Your Assets

> *Miedo a decidir*: El arquitecto **evita** o pospone tomar una **decisión arquitectonica importante**

Esto pasa por ejemplo cuando, se quedan dando vueltas entre:
- Documentando alternativas
- Análisis de pros y contras de las tecnologias
- POCs
y nunca cierran la decisión

#### ¿Cómo evitarlo?

Tomar la decisión en el Último Momento Responsable:
- No decidir demasiado temprano
- No dejar que pase el momento en que tengo información suficiente
Colaborar tempranamente y continuamente con equipos
- No decidir solo
- Incorporar a los developers
Usar ADRs desde el primer momento para documentar el razonamiento

### Groundhog Day

> *Dia de la marmota*: Una decisión se toma sin justificación clara y bien documentada. Provoca que una **discusión ocurra una y otra vez**

#### ¿Cómo evitarlo?

Documentar con ADRs (Architecture Decisión Records):
- Contexto
- Decisión
- Razones técnicas y de negocio
- Trade-offs aceptados
- Alternativas y motivos de descarte
- Fechas y responsables

### Email-Driven Architecture

> Las decisiones arquitectonicas quedan dispersas en distintas fuentes:
> - mails
> - chats (Slack, Teams)
> - reuniones verbales

Las causas más habituales son "ya lo hablamos/ya lo mande por mail/etc".

## Gran Bola de Lodo

![[Pasted image 20260427203244.png]]![[Pasted image 20260504194137.png]]
Una gran bola de lodo presenta dependencias desordenadas y límites poco claros. Puede aparecer dentro de un monolito o de un microservicio.

---

## Complemento de estudio

### Modularidad y decisiones

Un **monolito modular** mantiene un despliegue conjunto y establece límites internos claros. Esos límites pueden facilitar una futura extracción de servicios, pero la migración solo se justifica si resuelve una necesidad concreta.

En Clean Architecture y arquitectura hexagonal, los detalles externos dependen de interfaces del núcleo, de modo que dominio y casos de uso puedan probarse sin una base de datos o transporte específico.

Un ADR registra contexto, decisión, estado y consecuencias, incluidas alternativas descartadas. Ejemplo: «Mantener despliegue único porque el equipo y la carga actuales no justifican operación distribuida; revisar si aparece necesidad de escalado independiente». Registrar un criterio de revisión evita reabrir discusiones sin nueva evidencia.
