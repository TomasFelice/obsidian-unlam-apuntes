---
tipo: clase
fecha: 2026-12-29
tema: IA aplicada al desarrollo desde la arquitectura
fecha_fuente:
fecha_por_confirmar: false
---
# IA aplicada al desarrollo desde la arquitectura
## Parte 1 - Hacer crecer el problema
### Situación 1
> Un contador pide un sitio web de presentación

Preguntas:
- ¿Cómo lo encararíamos con IA?
	- Una forma podría ser, pedir un diseño, mandarle lineamientos, y luego pasarla a codigo

Preguntas a responder en la página:
- Quién es?
- Qué servicios ofrece?
- Por qué elegirlo?
- Formulario de contacto
### Situación 2
> Ahora, si queremos venderle sitios web a 100 contadores

Haríamos exactamente lo mismo 100 veces?

La idea es convertir un caso puntual en un proceso repetible

La clave de todo, es **sistematizar**
![[Pasted image 20261029192116.png]]

### Primero el problema, después la IA
Antes de elegir la tecnología, debemos preguntarnos:
- Cuál es el objetivo?
- Qué información entra?
- Qué decisiones existen?
- Qué resultados esperamos?
- Dónde puede fallar?
- etc.
## Parte 2 - Las piezas
### Chat vs agente
- Chat
	- Asistente conversacional. Responde ante una interacción
- Agente
	- Recibe un objetivo e intenta llegar al resultado
	- Razona
	- Planifica
	- Elige pasos
	- Usa herramientas
> La diferencia principal radica en que el agente HACE, y es autónomo. Un chat sólo sirve como un "google" mejorado, sólo de consulta.

### Skill
> Capacidad reutilizable para resolver una tarea concreta
> - Analizar un brief
> - Extraer información de un PDF
> - Generar un sitemap
> - Revisar accesibilidad
> - Crear tickets en Jira

Una skill no es solo un prompt. Una skill define:
- Input
- Reglas
- Herramientas
- Validaciones
- Output
### Agente o código tradicional
- Código determinístico
	- Las reglas son claras
	- Conocemos todos los pasos
	- Necesitamos exactitud
- LLM / Agente
	- El input es ambiguo
	- Hay lenguaje natural
	- Hace falta interpretar
	- Existen múltiples caminos válidos
> Una buena arquitectura combina partes determinísticas con partes probabilísticas.

## Parte 3 - contexto y estado
El modelo sólo puede razonar sobre **lo que tiene disponible**
*todo consume contexto*
> Regla: Contexto **relevante** > contexto **enorme**

### Contexto != estado != memoria
- Contexto
	- Lo disponible ahora para resolver la tarea
- Estado
	- Donde esta el proceso y que produjo hasta ahora
- Memoria
	- Información que queremos conservar para futuras ejecuciones
> La memoria **no es una garantía**. Ayuda, pero para controlar hay que hacer una validación

![[Pasted image 20261029193807.png]]

## Parte 4 - Herramientas y MCP
![[Pasted image 20261029193905.png]]
![[Pasted image 20261029194137.png]]

## Parte 5 - Caso real
![[Pasted image 20261029194632.png]]
