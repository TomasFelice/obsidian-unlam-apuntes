---
tipo: clase
fecha: 2026-04-27
tema: Complete el tema
---
# Patrones de arquitectura
> Como saber cual elegir?

## Monolito
Es malo cuando se implementa mal.
Cuando esta bien implementado, esta muy bien.
Lo que define el monolito, es que todo el despliegue ocurre a la vez (todo junto)
## Microservicios
Se intenta usar como "marketing" para vender que es escalable (hype).
La mayoria de las empresas que no pudieron implementarlo bien, es que no tenian el suficiente conocimiento del dominio y por falta de criterio.
## Monolito a Microservicios
La clave de la migración es separarlo en **etapas**
## Arquitectura por capas
Puede ser como lo prefieras. Por ejemplo:
- Comunicacion (HTTP, tRPC, api, CLI)
- Dominio
- Acceso a datos (db, memoria, etc.)
### Clean / Hexagonal
Plantean las capas de una manera particular.
Es necesario que todo el dominio del sistema este definido.
## Monolito Modular
... (hasta aca vimos el video de BettaTech. Continuar. [https://www.youtube.com/watch?v=q3YQy1lJutw&t=14s](https://www.youtube.com/watch?v=q3YQy1lJutw&t=14s "https://www.youtube.com/watch?v=q3yqy1ljutw&t=14s"))

---
# Antipatrones de Software
## Antipatrones de Decisiones
![[Antipatrones.jpg]]
### Covering Your Assets
> *Miedo a decidir*: El arquitecto **evita** o pospone tomar una **decision arquitectonica importante**

Esto pasa por ejemplo cuando, se quedan dando vueltas entre:
- Documentando alternativas
- Analisis de pros y contras de las tecnologias
- POCs
y nunca cierran la decision
#### Como evitarlo?
Tomar la decision en el Ultimo Momento Responsable:
- No decidir demasiado temprano
- No dejar que pase el momento en que tengo informacion suficiente
Colaborar tempranamente y continuamente con equipos
- No decidir solo
- Incorporar a los developers
Usar ADRs desde el primer momento para documentar el razonamiento
### Groundhog Day
> *Dia de la marmota*: Una decisión se toma sin justificación clara y bien documentada. Provoca que una **discusión ocurra una y otra vez**
#### Como evitarlo?
Documentar con ADRs (Architecture Decision Records):
- Contexto
- Decision
- Razones tecnicas y de negocio
- Trade-offs aceptados
- Alternativas y motivos de descarte
- Fechas y responsables
### Email-Driven Architecture
> Las decisiones arquitectonicas quedan dispersas en distintas fuentes:
> - mails
> - chats (Slack, Teams)
> - reuniones verbales

Las causas mas habituales son "ya lo hablamos/ya lo mande por mail/etc".
## Gran Bola de Lodo
![[Pasted image 20260427203244.png]]![[Pasted image 20260504194137.png]]
Esta podria ser la arqui de un microservicio. Los demasa pueden ser iguakes o no.