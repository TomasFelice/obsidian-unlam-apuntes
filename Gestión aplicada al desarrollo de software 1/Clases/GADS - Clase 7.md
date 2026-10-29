---
tipo: clase
fecha: 2026-08-20
tema: "Gestión de riesgos: identificación, priorización y respuestas"
fecha_fuente: metadato original sin corroborar
fecha_por_confirmar: true
---

> [!todo] Fecha pendiente de corroborar
> La fecha original puede haber quedado de la plantilla. No hay capturas fechadas en esta nota para corregirla con evidencia.

# Gestión de riesgos

## Riesgo, problema y dato

Un **riesgo** es un evento o condición incierta que puede afectar los objetivos. En esta clase se trabaja principalmente con amenazas. Un **problema** ya ocurrió; un **dato** es una observación que puede servir para detectar uno u otro.

Ejemplos: «las ventas bajaron 6 %» es un dato; «el servidor está caído» describe un problema; «una caída del comercio electrónico podría reducir los cobros y afectar el flujo de caja» expresa un riesgo.

## Estructura causa–evento–consecuencia

Redactar: «Debido a **causa**, podría ocurrir **evento**, lo que produciría **consecuencia**».

Ejemplo: «Por depender de un único proveedor, podría demorarse el sensor, retrasando la prueba del prototipo». La causa no es todavía el evento y la consecuencia debe vincularse a un objetivo.

## Proceso

1. **Identificar:** listar riesgos y sus causas. Pueden clasificarse en genéricos/específicos o técnicos/de negocio/de proyecto. También los específicos deben revisarse durante el proyecto.
2. **Analizar y priorizar:** estimar probabilidad, impacto y horizonte temporal. Acordar escalas para que el equipo puntúe con criterios consistentes.
3. **Planificar respuestas:** elegir estrategia, responsable, acciones, disparadores y contingencia.
4. **Monitorear:** revisar estado, cambios, nuevos riesgos y eficacia de las acciones.

## Matriz de probabilidad e impacto

En el ejercicio se usan valores de 1 a 5 y el producto **P × I**, entre 1 y 25. Es un índice de prioridad sobre escalas ordinales; **no representa un daño monetario esperado**. Diez riesgos puede ser una pauta de actividad, no un número obligatorio para todos los proyectos.

La exposición monetaria esperada se calcula de otro modo: probabilidad numérica × pérdida estimada, cuando ambas medidas son apropiadas.

## Estrategias de respuesta

- **Evitar:** cambiar el plan para eliminar la amenaza o la exposición.
- **Mitigar/reducir:** disminuir probabilidad y/o impacto.
- **Transferir:** acordar que un tercero asuma parte de sus consecuencias; no elimina necesariamente toda responsabilidad.
- **Aceptar:** reconocer el riesgo; puede incluir reservas y contingencia. «Ignorar» no debe confundirse con desconocerlo.
- **Escalar:** derivar su gestión al nivel con autoridad adecuada.

El **plan de contingencia** se ejecuta ante un disparador definido; ese disparador también puede advertir que la materialización es inminente. La mitigación actúa antes para reducir la exposición.

## Ejemplo complementario

| Elemento | Ejemplo |
|---|---|
| Riesgo | Retraso del sensor por proveedor único |
| P e I | P = 3; I = 4; prioridad = 12 |
| Mitigación | Validar un componente alternativo |
| Disparador | No tener despacho confirmado al llegar a la fecha límite interna |
| Contingencia | Usar el componente alternativo y ajustar la prueba |
| Seguimiento | Revisar entrega y disponibilidad en cada reunión |

**Preguntas de parcial:** describir el proceso, redactar un riesgo completo, explicar la matriz y distinguir mitigación de contingencia. Referencia: [SEI: gestión continua de riesgos](https://www.sei.cmu.edu/documents/5836/Continuous_Risk_Management_Guidebook.pdf).
