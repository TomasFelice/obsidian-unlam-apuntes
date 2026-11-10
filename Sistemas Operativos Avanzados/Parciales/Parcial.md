# SOA — Examen parcial del 23/06/2026

**Comisión:** Martes  
**Apellido y nombre:** ____________________  
**DNI:** ____________________

Fuente: [[Parcial.webp]]

## Consideraciones importantes

- Escriba sus datos en todas las hojas que entregue, incluyendo apellido, nombre y página x de y.
- **ATENCIÓN:** Cada pregunta correctamente marcada vale 1 punto.

## Temario Tiempo Real

1. Indique si es correcta la siguiente oración. Justifique.

   > «En un sistema operativo de tiempo real la latencia del planificador **no puede afectar** el tiempo de respuesta de una tarea del tipo hard».
   
FALSO. En un STR, la latencia del planificador si puede afectar el tiempo de respuesta de una tarea hard, pero lo importante es tenerlo controlado. Hay que evaluar si el peor de los casos, cumple con el deadline de la tarea hard.

> **Corrección 1 · 1,00/1,00**
>
> Correcto. La latencia del planificador puede demorar el despacho de una tarea hard y forma parte de su tiempo de respuesta. El criterio que diste es el adecuado: verificar que el tiempo de respuesta en el peor caso sea menor o igual al deadline.


2. Indique si es correcta la siguiente oración. Justifique.

   > «En FreeRTOS cada vez que se crea una tarea, su TCB se crea en el stack de ejecución».

FALSO. El TCB y el stack son dos cosas independientes en temrinos de almacenamiento. Es decir, para una tarea, es necesario que se almacene el TCB en un espacio de memoria, y el stack en otro.
Esto puede ser en memoría dinámica (heap), si la creamos con vTaskCreate(), en la cual el SO se encarga de reservar la memoria necesaria, mientras que si la creamos con vTaskCreateStatic(), tenemos que definir explicitamente donde se va a guardar cada cosa, y no será en memoria dinamica.

> **Corrección 2 · 0,90/1,00**
>
> Correcto en lo central: el TCB y el stack se almacenan en bloques distintos. Ajustá los nombres a `xTaskCreate()` y `xTaskCreateStatic()`. Con la primera, FreeRTOS asigna ambos bloques. Con la segunda, el programa proporciona un buffer para el stack y otro para el TCB. [Referencia de ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/v5.0/esp32/api-reference/system/freertos.html)

## Temario Sistemas Embebidos e IoT

La Confederación Argentina de Básquet lo contrata para desarrollar un sistema embebido que permita a los jugadores entrenar su velocidad de reacción y coordinación.

El sistema deberá contar con tres pulsadores: uno de color rojo, otro de color verde y un tercero de color azul. Además, dispondrá de un LED RGB que indicará el estado actual.

Los pulsadores deberán estar ubicados a una distancia de un metro entre sí. El entrenamiento tendrá una duración de cinco minutos. Durante ese período, el LED RGB mostrará de manera aleatoria alguno de los tres colores disponibles. El jugador deberá desplazarse y presionar el pulsador correspondiente al color mostrado.

Mediante el potenciómetro, el entrenador podrá modificar la velocidad con la que cambia el color del LED RGB.

Si el jugador presiona el pulsador correcto antes de que cambie el color del LED, sumará un punto. Si presiona un pulsador incorrecto o no responde dentro del tiempo establecido, se le restará un punto.

El buzzer deberá emitir un sonido breve cada vez que se detecte una respuesta correcta y un sonido diferente cuando la respuesta sea incorrecta.

El entrenador desea iniciar y detener el entrenamiento desde una aplicación instalada en un smartphone Android. Al finalizar, deberá poder visualizar el puntaje obtenido por el jugador y la cantidad de respuestas correctas e incorrectas.

3. Indique qué sensores y actuadores utilizaría para crear el sistema, especificando el tipo de señal que maneja cada uno.
Sensores:
- Pulsadores (3, rojo, verde, azul). Señal digital binaria. HIGH o LOW
- Potenciometro. Señal analógica. Se convierte a digital mediante un ADC.
Actuadores:
- LED RGB. Señal digital por PWM, con un canal para cada color.
- Buzzer. Señal digital por PWM, para variar el sonido.

> **Corrección 3 · 1,00/1,00**
>
> Identificaste todas las entradas y salidas, con sus señales. Para el sonido, tu planteo corresponde a un buzzer pasivo: variás la frecuencia del PWM para generar tonos distintos. En el LED RGB, el ciclo de trabajo de cada canal controla su intensidad.


4. Para desarrollar el software del sistema embebido se propone utilizar el patrón de máquina de estados. ¿Cuál utilizaría? Justifique su respuesta.
Me parece correcto. En este caso utilizaría el patrón de máquina de estados con switches, ya que no son muchos estados ni eventos. De esta manera dejaríamos el código de una forma mas facil de entender y bien estructurada.

> **Corrección 4 · 1,00/1,00**
>
> La elección de switches está bien justificada para una máquina con pocos estados y eventos, y coincide con el enfoque de [[SOA - Clase 3]]. Podés ilustrarlo con un switch externo por estado (`En espera`, `Entrenando`, `Finalizado`) y uno interno por evento (`Iniciar`, `Pulsación`, `Vencimiento`, `Detener`).


5. Se le solicita que implemente el sistema utilizando FreeRTOS.

   - **a)** ¿Qué elemento de FreeRTOS utilizaría para determinar automáticamente cuándo finalizan los cinco minutos de entrenamiento?
Para este caso utilizaría un temporizador por sw de freertos. Crearía un temporizador con xTimerCreate(), indicando que será de 1 solo uso, configurado para que dure 5 minutos, con xTimerStart() iniciaría el mismo temporizador, y cuando pasen los 5 minutos, se llamará al callback qeu defina en la creacion del timer, en el cual haré el manejo necesario.
No es necesario hacer el xTimerStop() del temporizador ya que lo creaía para una sola vez. Si quisiera hacerlo periodico, o si desería abortar el entrenamiento antes de los 5 minutos, si que deberia ejecutar el stop.
   - **b)** ¿Qué mecanismo de FreeRTOS utilizaría para enviar a la tarea principal la información del pulsador presionado? Justifique si utilizaría una cola, un semáforo, una notificación directa a una tarea u otro mecanismo.
Para enviar la informacion del pulsador a la tarea principal, utilizaria una cola de mensajes. Con esto me garantizo las siguientes cuestiones:
- El orden en el cual ocurren los eventos, es el mismo que recibe la tarea principal, ya que una cola funciona como un FIFO.
- Puedo enviar datos sobre qué pulsador fue presionado
- No se pierde información si la tarea principal demora en ejecutarse.

si utilizaramos, por ejemplo, un semaforo, solo podriamos saber si un pulsador fue presionado o no, pero no sabriamos cual fue, ni si hubo mas de un presionado,

> **Corrección 5 · 0,90/1,00**
>
> **5a (0,50/0,50).** Correcto el temporizador de software de disparo único. Al vencer, el callback puede notificar a la tarea que cierra el entrenamiento. Reservá `xTimerStop()` para una cancelación anticipada o para detener un temporizador periódico.
>
> **5b (0,40/0,50).** La cola FIFO es una buena elección porque conserva el orden de encolado y transporta el ID del pulsador. La garantía de que no se pierden eventos depende de que haya espacio: si la cola se llena, el envío puede fallar. Un semáforo contador puede contar eventos, aunque por sí solo no identifica qué pulsador los generó. [Manual de FreeRTOS sobre colas](https://github.com/FreeRTOS/FreeRTOS-Kernel-Book/blob/main/ch05.md)


## Temario Android

6. En la siguiente imagen complete los estados faltantes del ciclo de vida de una Activity. Además describa en qué momento la Activity pasa a dicho estado.
   ![[Pasted image 20261110154457.png|462]]

- Started -> onStart(), onRestart()->onStart()
- Paused -> onPause()

> **Corrección 6 · 0,45/1,00**
>
> Identificaste **Started** y **Paused** y los vinculaste con los callbacks correctos. Faltó **Destroyed**, en el recuadro inferior derecho, y explicar cuándo se alcanza cada estado. **Started**: la Activity se vuelve visible, tanto al abrirse como al volver desde Stopped. **Paused**: deja de estar en primer plano, aunque puede seguir parcialmente visible. **Destroyed**: la Activity se destruye, por ejemplo al finalizar o al recrearse por un cambio de configuración. [Ciclo de vida de una Activity](https://developer.android.com/guide/components/activities/activity-lifecycle)


7. Explique qué realiza el siguiente código de Android.

   ```java
   super.onCreate(savedInstanceState);

   Button botonAlerta = findViewById(R.id.btnSimular);

   botonAlerta.setOnClickListener(v -> {
       simularTempAlcanzada();
   });
   ```
Ese codigo android es el onCreate de una activity. Comienza llamando al onCreate de su clase padre, Luego, identifica un Botón, el cual cuando se presione, se simulará la temperatura alcanzada.

> **Corrección 7 · 1,00/1,00**
>
> Correcto. El fragmento llama a `super.onCreate`, busca el botón `btnSimular` con `findViewById` y registra un listener. `simularTempAlcanzada()` se ejecuta cuando se presiona el botón.


8. A usted lo contratan para crear una aplicación en Android Studio que muestre un historial de temperaturas sensadas en un ambiente mediante un sistema embebido formado por un ESP32 y un sensor DHT11.

   Para ello, debe proponer una arquitectura de comunicación entre el ESP32 y el smartphone Android.

   Según su criterio, ¿qué arquitectura de comunicación considera más conveniente emplear: comunicación directa, Edge Computing o servidor externo/nube? Seleccione una sola opción, realizando un diagrama del diseño del sistema IoT, indicando:

   - **a)** Cada componente del sistema (embebido, smartphone, etc.).
   - **b)** El protocolo de comunicación que utilizaría.
   - **c)** Dónde ubicaría la base de datos.

En este caso, usaría servidor externo/nube, ya que, si bien voy a estar enviando datos continuamente desde el sensor, no es del todo necesario que la respuesta sea lo mas rapida posbile, por lo que no vería mucho beneficiio en unar Edge Computing, considero que es una capa de complejidad innecesaria.

Tendria los siguientes componentes:

embebido --MQTT--> servidor --HTTP--> Smartphone
					|
					db

El esquema sería algo así, en el embebido enviaria la telemetria del sensor mediante un topic de MQTT, al cual el servidor estará suscripto, e irá almacenando en la db lo que vaya recibiendo.
Por otro lado, desde la app Android del smartphone, se consultará vía HTTP una API REST que expondrá el backend del servidor, el cual consultará los datos almacenados en la db, y devolverá el historial solicitado.

> **Corrección 8 · 0,95/1,00**
>
> La elección de nube está justificada y tu explicación cubre los tres incisos: componentes, protocolos y ubicación de la base. Al diagrama le faltó hacer explícito el **DHT11 → ESP32**. Para que también refleje quién inicia la consulta, dibujá **Android → API REST** como solicitud HTTP y marcá la respuesta con el historial. En la nube, podés distinguir el broker MQTT, el servicio que guarda las lecturas y la base de datos.


## Temario Wearables

9. A usted le solicitan desarrollar un prototipo de un dispositivo wearable con forma de anteojo basado en un ESP32-CAM, el cual incorpora una cámara para detectar objetos en tiempo real mediante un modelo de inteligencia artificial (IA).

   Teniendo en cuenta estas especificaciones:

   - **a)** ¿Qué aspectos importantes deberías considerar durante el desarrollo del wearable?
Para el desarrollo deberían tener en cuenta las siguientes cuestiones:
- Bateria disponible
- Uso o no de un SO
- 
   - **b)** ¿Es necesario que el dispositivo cuente con un sistema operativo? Justifique su respuesta.
No es estrictamente necesario, pero si altamente recomendable. Con un SO vamos a tener mayor facilidad para gestionar las tareas del embebido, y podríamos mejorar el consumo de bateria en momentos de reposo. Adicionalmente a esto, nos podría proporcionar mecanismos ya definidos para trabajar con la camara.

> **Corrección 9 · 0,50/1,00**
>
> **9a (0,15/0,50).** Nombraste la batería y el uso de un SO, pero quedó incompleta. Desarrollá al menos la autonomía y el consumo de cámara e inferencia, los límites de RAM y procesamiento del ESP32-CAM, la latencia o los FPS necesarios para detectar en tiempo real, y el peso, la comodidad y la temperatura del anteojo.
>
> **9b (0,35/0,50).** Bien que un SO sea opcional y que un RTOS pueda organizar captura, inferencia y avisos. El ahorro energético depende de cómo bloquees las tareas y configures el reposo. El soporte de cámara lo brinda el driver o el SDK. Para completar la justificación, explicá que el mismo flujo también se puede implementar en bare metal si se cumplen los requisitos temporales y de memoria.


## Temario Microservicios

10. En el contexto de las API REST, explique la característica de Stateless (sin estado). Compare este modelo con una arquitectura Stateful, detallando dónde se mantiene la información del usuario en cada caso.
La caracteristica de stateless indica que, las apis rest, se asumen que no dependen del estado o secuencia de llamadas a la misma. En cada peticion, el que realiza la misma, debe indicarle a la api quien es, la api realizara la autenticacion y autorizacion correspondiente, y realizará la accion solicitada en caso de que corresponda. 
En una arquitectura stateful, se podrian guardar datos de estado, que es como si fuerna "datos de sesion", estos datos no se persisten en ningun lugar, sino que cuando se cierra la conexion, se pierden

> **Corrección 10 · 0,55/1,00**
>
> La parte **stateless** está bien encaminada: cada petición lleva el contexto necesario y el estado de sesión queda del lado del cliente. El servidor puede guardar datos persistentes del usuario como recursos, por ejemplo su perfil. En **stateful**, el servidor conserva el estado de sesión entre peticiones, en memoria o en un almacén de sesiones, y el cliente puede enviar un ID para recuperarlo. La sesión puede seguir vigente al cerrar una conexión HTTP y terminar por expiración o cierre de sesión. [Fielding, REST](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)

## Calificación orientativa

**Puntaje: 8,25/10 (82,5 %). Nota orientativa: 7,9/10.**

El examen asigna **1 punto por pregunta**. Para esta corrección orientativa apliqué crédito parcial según el desarrollo de cada respuesta y repartí en partes iguales los incisos de las preguntas 5 y 9.

Con los cortes indicados, **50 % equivale a 4** y **75 % a 7**. El 82,5 % supera el corte para el 7 por 7,5 puntos porcentuales. Para estimar una nota por encima de ese corte, tomé **100 % como 10** e interpolé linealmente: 7 + (82,5 − 75) × (10 − 7) / (100 − 75) = **7,9**.

Los mayores descuentos fueron en **6** (faltó un estado y describir cuándo se entra a cada uno), **9** (faltó desarrollar las restricciones del wearable) y **10** (faltó explicar dónde y por cuánto tiempo se mantiene una sesión stateful).
