---
tipo: materia
cuatrimestre: 4
estado: pendiente
correlativas:
  - "[[Virtualización de Hardware]]"
  - "[[Física 2]]"
---
# Sistemas Operativos Avanzados

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

- Justificar señales, adaptación eléctrica y etapas de potencia.
- Diseñar FSM y temporización sin bloquear el control.
- Separar Activity/Service/hilo/proceso y definir el contrato MQTT.

### Recorrido por las notas

- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 1|SOA - Clase 1]] — Introducción a sistemas embebidos, señales y proyecto IoT
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 2|SOA - Clase 2]] — Electrónica básica, alimentación y conexión de sensores y actuadores
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 3|SOA - Clase 3]] — Máquinas de estados finitos: implementación con switches y tablas
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 4|SOA - Clase 4]] — Sistemas de tiempo real y FreeRTOS
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 5|SOA - Clase 5]] — Interrupciones, temporizadores, FSM y arquitectura IoT
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 6|SOA - Clase 6]] — Android: arquitectura, componentes, ciclo de vida y trabajo en segundo plano
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 7|SOA - Clase 7]] — Sensores Android y comunicación IoT
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 8|SOA - Clase 8]] — Microservicios, APIs y comunicación IoT
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 9|SOA - Clase 9]] — Repaso de parcial e industria 4.0
- [[Sistemas Operativos Avanzados/Clases/SOA - Clase 10|SOA - Clase 10]] — Wearables, Wear OS, watchOS y comunicación entre teléfono y reloj
