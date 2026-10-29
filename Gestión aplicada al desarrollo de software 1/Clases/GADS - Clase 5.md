---
tipo: clase
fecha: 2026-08-20
tema: "Estimación de proyectos e indicadores de producto y proceso"
fecha_fuente: metadato original sin corroborar
fecha_por_confirmar: true
---

> [!todo] Fecha pendiente de corroborar
> La fecha original puede haber quedado de la plantilla. No hay capturas fechadas en esta nota para corregirla con evidencia.

# Estimación e indicadores

## Estimar trabajo y costo

La clase contrapone un reparto tradicional —análisis/diseño 30 %, desarrollo 40 %, pruebas 20 % y gestión 10 %— con otro esquema de 10 % para pensar, 80 % para ejecutar actividades combinadas y 10 % para revisar e iterar. Son simplificaciones didácticas, **no porcentajes universales** ni evidencia de que un enfoque haya reemplazado todos los demás.

La estimación debe declarar alcance, supuestos, datos, incertidumbre y unidad. Líneas de código y puntos de función son medidas distintas de tamaño; no hay una conversión universal entre ellas.

COCOMO es una familia de modelos paramétricos que usa tamaño y otros factores para estimar esfuerzo y cronograma. Su esfuerzo suele expresarse en persona-mes; convertir a horas exige fijar una convención. No produce simplemente «horas» por ingresar líneas de código.

Fuente: [SEI: estimación de costos](https://www.sei.cmu.edu/blog/software-cost-estimation-explained/).

## Medir producto y proceso

Los indicadores permiten contrastar el plan con resultados. Medir producto no reemplaza medir proceso. Registrar también trabajo pendiente, tiempo de entrega, retrabajo y defectos según el objetivo del proyecto.

El **aha moment** es el momento en que un usuario percibe valor. Debe formularse como una hipótesis contrastable, por ejemplo completar un primer seguimiento de oportunidad, sin asumir que coincide con registrarse.

## Métricas de producto

| Indicador | Definición operativa |
|---|---|
| Activación | Usuarios que completan una acción clave / usuarios elegibles |
| Retención D1, D7, D30 | Proporción de una cohorte que vuelve o cumple la acción definida en esa ventana |
| Stickiness | DAU/MAU, usando una definición consistente de usuario activo |
| MRR | Ingreso recurrente mensual normalizado de suscripciones |
| ARR | 12 × MRR bajo la convención de anualización |
| CAC | Costos de adquisición / clientes nuevos atribuibles |
| LTV | Valor estimado del cliente durante su relación, con supuestos explícitos |

MRR no equivale a toda la facturación del mes ni a una promesa de cobro futuro. Declarar qué pagos, descuentos y cambios de plan se incluyen. Fuente: [Stripe: MRR](https://stripe.com/gb/resources/more/what-is-monthly-recurring-revenue).

## North Star Metric y complemento

La NSM busca representar valor entregado al usuario y orientar decisiones. No basta con que aumente ni permite predecir automáticamente el negocio. Definir indicadores auxiliares y límites para evitar mejorarla a costa de calidad o sostenibilidad.

Ejemplo para el CRM: oportunidades con seguimiento útil completado por semana. Validar si se relaciona con el valor buscado; registrar cómo se cuenta y qué queda fuera. El círculo de control ayuda a distinguir resultados sobre los que el equipo actúa directamente de factores externos.

**Repaso:** definir cohorte y acción antes de calcular retención. Si 20 de 100 usuarios regresan en D7 según esa regla, la retención D7 es 20 %.
