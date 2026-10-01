---
tipo: clase
fecha: 2026-08-18
tema: Temporizadores - Tips FSM - IoT
---
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
> 	- Sabado 26 clase especial de practica a las 10:30

---
# Repaso
> **FSM**
> - 2 tipos:
> 	- condicionales
> 	- matriz
> - Sirve para organizar el codigo de forma logica
> **STR**
> - Sistemas que deben actuar en un lapso de tiempo determinado
> - Puede ser
> 	- hard -> Estricto, catastrofico si falla (ejemplo: marcapasos)
> 	- soft -> Puede tener un pequenio desfasaje que no pasa nada (ejemplo: streaming, si se pierde un frame no pasa nada)
> **FreeRTOS**
> - Como es un SO de tiempo real, tenemos planificador
> - Es multitarea
> - Con baremetal deberias planificar todo a mano en un solo hilo de ejecucion
> - Las tareas se crean en el heap (memoria dinamica) (create, termina usando malloc porque reservamos bytes)
> - Tiene mecanismos de sincronizacion, mensajes, regiones criticas, etc.

---
# Temporizadores
> - ESP32 lectura por interrupciones
> - ESP32 delay
> - Temporizadores

## Interrupciones ESP32
- Todos los pines GPIO del ESP32 pueden manejar interrupciones
- ISR es la funcion handler encargada de atender la IRQ
Las interrupciones son para seniales digitales solamente. No son para analogicas
### Interrupciones externas
Tecnicas:
- LOW - Cuando esta baja la senial digital
- CHANGE - Cuando esta alta la senial digital
- RISING - Cuando cambia de low a high
- FALLING - Cuando cambia de high a low
Hay que definir el pin, handler y modo de las interrupciones en el setup()
Si dentro de una ISR debo interactuar con una tarea de FreeRTOS (colas o semaforos), se deben usar funciones especificas ya que estan optimizadas para IRQ, volviendo a permitir interrupciones:
- xQueueSendFromISR
- xSemaphoreGiveFromISR
En una ISR se deshabilitan las interrupciones, por lo que hay que ser cuidadoso con lo que hacemos ya que podria bloquear el sistema.
## Delay
> Por lo general es un while true que tiene un contador de tiempo. Lo finaliza cuando pasa el tiempo
> Bloquea todo el embebido en estos casos si hay una tarea
> En arduino no es recomendable porque bloqueas todo el embebido (no hay multitarea)
> **NO USAR DELAY PARA LA ENTREGA FINAL, para la V1 es aceptable**

- Ventajas
	- Sencillo manejo del tiempo
- Desventajas
	- Bloquea el SE (asincronico)
> Como podemos reemplazarlo?

## Temporizadores
Hay varios tipos
- Software
	- Sin FreeRTOS
		- Millis: Comparacion de tiempo. Tomo una muestra inicial, en otro momento tomo otra muestra y veo cuanto tiempo paso. Si llegue al tiempo indicado, hago la accion. No es bloqueante. Devuelve el tiempo desde que se encendio el ESP32 hasta que se llama
	- Con FreeRTOS
		- vTaskDelay: Bloquea temporalmente la tares (pasa la tarea a la cola de bloqueados). OJO con usarlo en sensores. Durante ese lapso de tiempo, perdemos las seniales enviadas.
		- xTimeCreate: Funciona como una alarma. Cada X tiempo te avisa. Todos ellos son gestionados por una unica tarea del SO (Timer Service Task). En el callback no se deben realizar acciones pesadas o bloqueantes. Si eso sucede se debe notificar a otra tarea para que lo haga.
- Hardware: Independiente de si hay SO o no. Se utilizan los registros contadores de tiempo  (Timers) del ESP32. Tiene 4 timers el ESP32. Hay que tener en cuenta que los sensores y actuadores lo usan y podrian haber problemas de concurrencia. La nueva version del framework arduino selecciona automaticamente el registro de timer que vas a usar. Hay riesgo de que se seleccione uno usado por otro componente. Son mas precisos, tienen un callback que se llama al pasar el tiempo por le ISR. Si dentro de un ISR se debe interactuar con una tarea de FreeRTOS, se deben usar las tareas mencionadas previamente de colas y semaforos.

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
- obtenemos evento. Esta es la unica funcion que lee los sensores. NUNCA los lee el switch. NO se deben actualizar actuadores y generar el cambio de estado
- switch estado
	- switch evento
		- logica propia
		- actualizacion de estado (puede ser el mismo)
		- solo poner los eventos que tienen sentido (sin olvidar el continue)
		- Si llega un evento no esperado, va por default. Se puede loguear el error
		- No poner serial print en continue
		- Se deben actualizar actuadores y generar el cambio de estado
		- No hacer ifs en los case. Si es necesario, meterlo en una funcion. La idea es que la logica, vaya en una funcion. En el case solo debe pasar la llamada a la funcion, y actualizar el estado.
---
# Teoria de IoT
> Complementar con teoria que da el otro profe penizza

**Que es IoT?**
Internet de las Cosas. embedidos que tienen sensores y actuadores que se pueden comunicar a la distancia entre ellos. Son objetos cotidianos con internet. Si no procesan datos, no son IoT

**Cuando no es IoT?**
M2M (Machine2Machine). Subconjunto de IoT. Las IoT deben transmitir datos a internet, a traves de un gateway y esos datos deben ser procesados y utilizados con un fin. M2M se usa cuando no hay conexion a internet (BT por ejemplo).

**Gateway**
> Dispositivo que me permite comunicar distintos **protocolos de redes internas** que usan los controladores, sensores y actuadores **con internet**

**Que puede ser un gateway?**
Cualquier dispositivo que entienda el **protocolo de las redes internas** y permita transferir sus datos por **internet**. Telefono, pc, router, etc. Un gateway puede agrupar varios de estos elementos (gateway combinado).

### Arquitectura basica
Redes internas -> gateway -> Internet (TCP/IP) -> Dispositivos de consulta
Si no hay conexion a internet, no funciona el sistema. No tiene quien procese los datos.

### Arquitectura por capas
Capa MIST -> Capa FOG -> Capa Cloud -> Dispositivos de consulta

MIST:
- Subredes: BT, Wifi, Ethternet, LoRa, etc.
FOG:
- Gateways. Puedo aplicar procesamiento antes de enviar a internet. Aca entra NodeRED (edge cloud). Para el TP, lo vamos a aplicar con la computadora.
Cloud:
- Internet.

> *MIST-FOG en algunas bibliografias se unifican en la capa EDGE*

---
# Arduino IDE
Se puede usar VSCode pero se recomienda Arduino IDE porque es mas sencillo de instalar. VSCode necesita muchos plugins y config.

BOARDS MANAGER > ESP32 (by espressif)

---
# Materiales
Traerlos la semana que viene. Meterlos en una caja para no andar armando y desarmando.
Traer cable micro-usb
A los que nos prestan protoboard, traer cargador usb.
Los materiales se devuelven a fin de cuatrimestre.
