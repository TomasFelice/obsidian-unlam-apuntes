---
tipo: clase
fecha: 2026-08-18
tema: "Interrupciones, temporizadores, FSM y arquitectura IoT"
fecha_fuente: metadato original sin corroborar
fecha_por_confirmar: true
---

> [!todo] Fecha pendiente de corroborar
> La fecha original puede haber quedado de la plantilla. No hay capturas fechadas en esta nota para corregirla con evidencia.

> **Cronograma**
> - Repaso
> - Temporizadores
> - Tips de FSM
> - Entrega Materiales
> - Consultas TPs o empezar con circuito

> **Clase que viene**
> - Entreva V1:
> 	- Circuito Wokwi
> 	- Con FSM, tareas de FreeRTOS y uso de temporizadores
> 	- Informe entregado por MIeL (PDF)
> - Disponibilidad de esteban en el lab
> 	- Lunes, Martes, Miercoles: De 15 a 22
> 	- Sabados: 10:30 a 16
> 	- Sabado 26 clase especial de práctica a las 10:30

---

# Repaso

> **FSM**
> - 2 tipos:
> 	- condicionales
> 	- matriz
> - Sirve para organizar el código de forma lógica
> **STR**
> - Sistemas que deben actuar en un lapso de tiempo determinado
> - Puede ser
> 	- hard -> Estricto, catastrofico si falla (ejemplo: marcapasos)
> 	- soft -> Puede tener un pequeño desfase que no pasa nada (ejemplo: streaming, si se pierde un frame no pasa nada)
> **FreeRTOS**
> - Como es un SO de tiempo real, tenemos planificador
> - Es multitarea
> - Con baremetal deberias planificar todo a mano en un solo hilo de ejecución
> - xTaskCreate utiliza asignación dinámica; xTaskCreateStatic permite aportar memoria estática.
> - Tiene mecanismos de sincronización, mensajes, regiones criticas, etc.

---

# Temporizadores

> - ESP32 lectura por interrupciones
> - ESP32 delay
> - Temporizadores

## Interrupciones ESP32

- Verificar los GPIO disponibles para interrupciones en la placa concreta y sus restricciones de uso.
- ISR es la función handler encargada de atender la IRQ
Las interrupciones de GPIO detectan eventos digitales. Otros periféricos, como ADC y temporizadores, también pueden generar interrupciones.

### Interrupciones externas

Tecnicas:
- LOW - Cuando esta baja la señal digital
- CHANGE - Ante cualquier cambio de nivel (LOW → HIGH o HIGH → LOW)
- RISING - Cuando cambia de low a high
- FALLING - Cuando cambia de high a low
Hay que definir el pin, handler y modo de las interrupciones en el setup()
Si dentro de una ISR debo interactuar con una tarea de FreeRTOS (colas o semaforos), se deben usar funciones especificas porque están diseñadas para ese contexto; atender sus parámetros y la posible solicitud de cambio de contexto:
- xQueueSendFromISR
- xSemaphoreGiveFromISR
Una ISR debe ser breve y respetar las restricciones del procesador y del puerto de FreeRTOS; no bloquear ni asumir que todas las interrupciones quedan deshabilitadas.

## Delay

> Una espera puede implementarse con espera activa o con suspensión; revisar la API concreta.
> En un bucle cooperativo, una espera bloqueante retrasa las demás actividades del mismo flujo.
> En Arduino sobre ESP32, delay suele ceder la CPU a FreeRTOS y bloquea la tarea que lo llama; no necesariamente todo el dispositivo. Evitarlo en la FSM si retrasa la atención de eventos.
> **NO USAR DELAY PARA LA ENTREGA FINAL, para la V1 es aceptable**

- Ventajas
	- Sencillo manejo del tiempo
- Desventajas
	- Puede bloquear el flujo que ejecuta la espera; no confundirlo con asincronía.
> Como podemos reemplazarlo?

## Temporizadores

Hay varios tipos
- Software
	- Sin FreeRTOS
		- Millis: Comparacion de tiempo. Tomo una muestra inicial, en otro momento tomo otra muestra y veo cuanto tiempo paso. Si llegue al tiempo indicado, hago la acción. No es bloqueante. Devuelve el tiempo desde que se encendio el ESP32 hasta que se llama
	- Con FreeRTOS
		- vTaskDelay: Bloquea temporalmente la tares (pasa la tarea a la cola de bloqueados). OJO con usarlo en sensores. Durante ese lapso de tiempo, perdemos las señales enviadas.
		- xTimerCreate: Funciona como una alarma. Cada X tiempo te avisa. Todos ellos son gestionados por una única tarea del SO (Timer Service Task). En el callback no se deben realizar acciones pesadas o bloqueantes. Si eso sucede se debe notificar a otra tarea para que lo haga.
- Hardware: Independiente de si hay SO o no. Se utilizan los registros contadores de tiempo  (Timers) del ESP32. La cantidad y gestión de timers depende del chip y la versión del framework. Pueden ofrecer temporización precisa; tienen un callback que se llama al pasar el tiempo por le ISR. Si dentro de un ISR se debe interactuar con una tarea de FreeRTOS, se deben usar las tareas mencionadas previamente de colas y semaforos.

> ver tabla de resumen

---

# Tips para FSM

>  ver en la wiki Torneo Pinki Cerebro, 2do puesto

Tengo que ver:
- estado
- eventos que salen de el
Con esto, puedo armar el switch de 2 capas (estados y dentro eventos)

> **SIEMPRE HAY QUE PONER EL EVENTO CONTINUE, MANTIENE EL MISMO ESTADO. NO PONERLO EN EL DIAGRAMA**

en el setup(), se pone el estado inicial del sistema
fsm
- obtenemos evento. Esta es la única función que lee los sensores. NUNCA los lee el switch. NO se deben actualizar actuadores y generar el cambio de estado
- switch estado
	- switch evento
		- lógica propia
		- actualizacion de estado (puede ser el mismo)
		- solo poner los eventos que tienen sentido (sin olvidar el continue)
		- Si llega un evento no esperado, va por default. Se puede loguear el error
		- No poner serial print en continue
		- Se deben actualizar actuadores y generar el cambio de estado
		- No hacer ifs en los case. Si es necesario, meterlo en una función. La idea es que la lógica, vaya en una función. En el case solo debe pasar la llamada a la función, y actualizar el estado.
---

# Teoría de IoT

> Complementar con teoría que da el otro profe penizza

**Que es IoT?**
Internet de las Cosas. embedidos que tienen sensores y actuadores que se pueden comunicar a la distancia entre ellos. Son objetos cotidianos con internet. El procesamiento puede estar en el dispositivo, un gateway o servicios remotos.

**Cuando no es IoT?**
M2M (Machine-to-Machine) describe comunicación entre máquinas y puede usar redes locales o Internet. Se superpone con IoT; la distinción no se reduce a Bluetooth frente a Internet.

**Gateway**
> Dispositivo que me permite comunicar distintos **protocolos de redes internas** que usan los controladores, sensores y actuadores **con internet**

**Que puede ser un gateway?**
Cualquier dispositivo que entienda el **protocolo de las redes internas** y permita transferir sus datos por **internet**. Telefono, pc, router, etc. Un gateway puede agrupar varios de estos elementos (gateway combinado).

### Arquitectura básica

Redes internas -> gateway -> Internet (TCP/IP) -> Dispositivos de consulta
El comportamiento sin Internet depende del diseño: el procesamiento local y los lazos de control pueden seguir funcionando y sincronizar los datos al reconectarse.

### Arquitectura por capas

Capa MIST -> Capa FOG -> Capa Cloud -> Dispositivos de consulta

MIST:
- Subredes: BT, Wifi, Ethternet, LoRa, etc.
FOG:
- Gateways. Puedo aplicar procesamiento antes de enviar a internet. Aca entra NodeRED (edge cloud). Para el TP, lo vamos a aplicar con la computadora.
Cloud:
- Servicios remotos de cómputo, almacenamiento y aplicaciones, accesibles por red.

> *MIST-FOG en algunas bibliografias se unifican en la capa EDGE*

---

# Arduino IDE

Se puede usar VSCode pero se recomienda Arduino IDE porque es más sencillo de instalar. VSCode necesita muchos plugins y config.

BOARDS MANAGER > ESP32 (by espressif)

---

# Materiales

Traerlos la semana que viene. Meterlos en una caja para no andar armando y desarmando.
Traer cable micro-usb
A los que nos prestan protoboard, traer cargador usb.
Los materiales se devuelven a fin de cuatrimestre.

---

## Complemento de estudio

### Elegir cómo esperar

| Mecanismo | Contexto | Uso |
|---|---|---|
| Comparación con millis() | Bucle de aplicación | FSM cooperativa sin bloquear |
| vTaskDelay / vTaskDelayUntil | Tarea FreeRTOS | Ceder CPU; el segundo facilita periodicidad |
| Timer de software | Tarea de servicio de timers | Notificar vencimientos con callback breve |
| Timer de hardware | Periférico/ISR | Eventos temporales según el hardware |

El callback de un timer de software no es una ISR: no usar automáticamente las variantes FromISR. En una ISR, usar solo APIs permitidas y mantener el trabajo breve. Las tareas pueden crearse con asignación dinámica o estática, según API y configuración.

Para millis(), comparar la resta sin signo entre instante actual e inicial facilita manejar el desbordamiento del contador. El evento CONTINUE es una convención de la implementación de la cátedra, no un requisito matemático de toda FSM.

**IoT:** M2M también puede usar Internet. Edge/fog/cloud describen dónde se procesa; cloud no es sinónimo de Internet. Diseñar qué funciones siguen operativas sin conexión.

Fuente: [FreeRTOS: timers de software](https://www.freertos.org/Documentation/02-Kernel/02-Kernel-features/05-Software-timers/01-Software-timers).
