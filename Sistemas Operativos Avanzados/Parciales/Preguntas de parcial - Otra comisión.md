# Preguntas de parcial de otra comisión

Preguntas recordadas del parcial del lunes 9 de noviembre de 2026. La redacción es aproximada.

## 1. Característica principal de un STR

**Consigna.** ¿Cuál es la característica más importante de un sistema de tiempo real (STR)?

> [!quote] Tu respuesta
> La caracteristica mas importante de un STR es el cumplimiento de los tiempos de respuesta prometidos. Todas las tareas tienen un deadline, el cual si no llegaran a cumplir, podrían generar una catástrofe.

**Corrección.** Identificaste el cumplimiento de los plazos. Lo que sobra es generalizar que todas las tareas tienen un plazo crítico y que incumplir cualquiera podría provocar una catástrofe. La consecuencia depende de la función y del tipo de requisito temporal.

**Respuesta de examen.** En un STR, la corrección depende tanto del resultado como del momento en que se entrega. El sistema debe responder de forma predecible dentro de los plazos exigidos para cada función. [[SOA - Clase 4]]

## 2. Tiempo real en un tren y una heladera

**Consigna.** ¿En qué se diferencian el STR de un tren y el de una heladera en cuanto a las consecuencias de incumplir un plazo?

> [!quote] Tu respuesta
> En un STR de un tren, si se inclumple algún plazo, las consecuencias podrían ser catastróficas, generando un accidente muy importante, mientras que un plazo incumplido en una heladera, a lo sumo generaría un problema en la mercadería almacenada en ese momento, pero no sería nada grave, ni mucho menos catastrofico.

**Corrección.** Captaste la diferencia de gravedad, pero conviene clasificar la función concreta. El frenado de emergencia de un tren y la actualización de su pantalla informativa pueden tener exigencias distintas. En una heladera doméstica, un retraso ocasional del control térmico puede ser tolerable. Una desviación prolongada sí puede comprometer los alimentos.

**Respuesta de examen.** El frenado de emergencia puede tener un requisito de **tiempo real duro** porque un resultado correcto que llega tarde puede perder su utilidad y poner en riesgo a las personas. El control térmico de una heladera doméstica puede modelarse como **tiempo real blando** si un retraso ocasional degrada el control sin causar un fallo inmediato. [[SOA - Clase 4]]

## 3 y 4. Wokwi, señales y alimentación

Las consignas recordadas eran estas. El circuito original no está disponible.

3. En el ejercicio de Wokwi, ¿dónde se debían colocar los sensores y actuadores y qué tipo de señal correspondía?
4. ¿Qué error tenía el diagrama?

Ejercicio inspirado en la captura de clase. Un ESP32 alimentado por USB lee un potenciómetro y usa su posición para mover un servo. La fuente externa está aislada y solo se conecta por los cables dibujados. Tomá como datos del ejercicio que el ADC está preparado para el rango útil del potenciómetro, el GPIO marcado como salida admite el control del servo y el servo acepta una señal lógica de 3,3 V. El esquema tiene un único error intencional.

![[SOA - Circuito de práctica - Alimentación.svg|800]]

### 3. Componentes y señales

**3.** Identificá el elemento de entrada y el actuador. Para cada señal, indicá de dónde sale, adónde llega y si es analógica o digital. Separá los cables de señal de los de alimentación.

> [!quote] Tu respuesta
> El elemento de entrada es el potenciometro, mientras que el de salida, es el servo.  
> La señal del potenciometro sale desde el cursor, hacia el ADC del ESP32, por lo tanto, la señal es analogica. Por otro lado, para el servo, se toma la salida del GPIO del ESP32, hacia el pin SIG del servo, con una salida digital estandar (no PWM).  
> Los cables de alimentacion son:  
> VCC POT-3V3  
> GND POT-GND ESP  
> VCC SER-5V FUENTE  
> GND SER-GND FUENTE  
> Los cambles de señal son:  
> Cursor-ADC  
> GPIO-SIG

> [!check]- Corrección y respuesta modelo  
> **3. Casi completa.** Identificaste bien el potenciómetro y el servo, el recorrido de ambas señales y los cables de alimentación. El punto a corregir es «salida digital estándar (no PWM)». La señal es digital y va de GPIO a SIG, pero el servo de posición necesita un tren de pulsos: el ancho de cada pulso indica el ángulo solicitado. Dejar el GPIO fijo en alto o bajo no transmite ese ángulo.
>
> **Respuesta modelo.** El potenciómetro es la entrada de posición. Su cursor entrega una tensión analógica al ADC. El servo es el actuador. Recibe desde el GPIO una señal digital de pulsos cuyo ancho representa el ángulo solicitado. El servo se alimenta desde la fuente de 5 V. El GPIO solo lleva la señal de control.

### 4. Error de cableado

**4.** Comprobá si cada alimentación entrega la tensión y corriente requeridas. Después seguí los cables y explicá qué error impediría controlar el servo de forma confiable. Indicá qué conexión agregarías o cambiarías.

> [!quote] Tu respuesta
> Está todo bien, salvo porque la fuente externa y la ESP32 no comparten las masas (negativos), por ende, al no tener el mismo punto de referencia, no se podría controlar el servo de forma confiable.

> [!check]- Corrección y respuesta modelo  
> **4. Diagnóstico correcto, respuesta incompleta.** Detectaste que falta una referencia de masa común y explicaste su efecto. La consigna también pedía justificar que las fuentes alcanzan e indicar qué cable agregar. A 3,3 V, el potenciómetro demanda hasta 5 mA y hay 100 mA disponibles. A 5 V, el servo demanda hasta 800 mA de pico y la fuente admite 2 A. Agregá un cable entre GND del ESP32 y el borne de 0 V de la fuente externa, que ya está conectado al GND del servo. Las líneas positivas de 3,3 V y 5 V quedan separadas.
>
> **Respuesta modelo.** Los presupuestos de corriente alcanzan. El potenciómetro requiere hasta 5 mA frente a los 100 mA disponibles a 3,3 V. El servo puede demandar 800 mA de pico y su fuente de 5 V admite hasta 2 A. El problema es que al servo le llega la señal del ESP32, pero su entrada SIG la interpreta respecto de su propio GND. Las dos redes de tierra están separadas, así que falta una referencia común. Uní el GND del ESP32 con el 0 V de la fuente externa y mantené separadas las líneas positivas de 3,3 V y 5 V. [[SOA - Clase 2]]

## 5. Temporizador en FreeRTOS

**Consigna.** ¿Cómo se puede implementar un temporizador con FreeRTOS?

> [!quote] Tu respuesta
> En freeRTOS podriamos implementar un temporizador usando xTimerCreate(), esta tarea lo que hace es justamente crear una tarea que te avise cuando pase el tiempo indicado, llamando al callback que decidas cuando lo definas. El temporizador lo gestiona el Timer Service Manager (TSM)

**Corrección.** Elegiste bien `xTimerCreate()` y mencionaste el callback. La función crea un temporizador de software inicialmente inactivo. Falta iniciarlo con `xTimerStart()`. Los temporizadores comparten la **Timer Service Task**, que ejecuta sus callbacks. No se crea una tarea nueva para cada temporizador.

**Respuesta de examen.** Creo el temporizador con `xTimerCreate()`, indicando el período en ticks, el callback y si es de un solo disparo (`pdFALSE`) o periódico (`pdTRUE`). Compruebo que se haya creado y lo inicio con `xTimerStart()`. Al vencer, la tarea de servicio llama al callback, que debe ser breve y evitar operaciones bloqueantes. Si hace falta trabajo pesado, el callback puede avisarle a otra tarea. [[SOA - Clase 5]] · [Guía oficial de FreeRTOS](https://www.freertos.org/media/2018/161204_Mastering_the_FreeRTOS_Real_Time_Kernel-A_Hands-On_Tutorial_Guide.pdf)

## 6. FreeRTOS y bare metal

**Consigna.** Si se usa FreeRTOS, ¿el sistema sigue siendo bare metal?

> [!quote] Tu respuesta
> No, al utilizar FreeRTOS, el sistema ya no es más bare metal, ya que incorporamos la abstracción del sistema operativo y podemos tener, por ejemplo, un algoritmo de planificacion de tareas, que en bare metal no.

**Corrección.** La conclusión es correcta. El criterio es si el firmware usa un kernel de sistema operativo. En bare metal también se puede organizar trabajo mediante un bucle, interrupciones o un planificador implementado en la aplicación.

**Respuesta de examen.** Si el firmware ejecuta sobre el kernel de FreeRTOS, usa un RTOS. El kernel ofrece servicios como la planificación de tareas. En bare metal la aplicación organiza la ejecución sin un kernel de sistema operativo. [[SOA - Clase 1]] · [[SOA - Clase 10]]

## 7. Sensores en Android

**Consigna.** ¿Qué clases de Android se usan para trabajar con sensores?

> [!quote] Tu respuesta
> SensorManager: El manejador como tal del sensor en particular  
> SensorEvent: Un evento generado por un sensor, pueden ser cambios en sus valores, parametros, etc  
> SensorEventListener: Servicio que escucha los cambios de los sensores (observer)

**Corrección.** Mencionaste tres tipos relevantes. Te faltó `Sensor`, y conviene distinguir el servicio del sistema de la interfaz de escucha. Tu analogía con *observer* sirve para explicar esta última.

**Respuesta de examen.**

- `SensorManager` permite consultar los sensores disponibles y registrar o quitar listeners.
- `Sensor` representa un sensor específico y permite consultar propiedades como su tipo y rango.
- `SensorEvent` contiene una medición con sus valores, sensor de origen, precisión y marca temporal.
- `SensorEventListener` es la interfaz que implementa la aplicación para recibir `onSensorChanged()` y `onAccuracyChanged()`.

[[SOA - Clase 7]] · [Documentación de sensores de Android](https://developer.android.com/develop/sensors-and-location/sensors/sensors_overview)

## 8. Buenas prácticas de microservicios

**Consigna.** Mencioná al menos tres buenas prácticas de microservicios.

> [!quote] Tu respuesta
> Independencia de despliegues, mayor resiliencia, despliegue en contenedores.

**Corrección.** Los despliegues independientes y el uso de contenedores coinciden con los apuntes. «Mayor resiliencia» describe un objetivo. Para que cuente como práctica, explicá cómo la conseguís, por ejemplo, fijando tiempos máximos de espera y aislando fallos entre servicios.

**Respuesta de examen.**

1. Definir una responsabilidad clara para cada servicio.
2. Automatizar el build y el despliegue por servicio para poder publicar cambios de forma independiente.
3. Dar a cada servicio control sobre sus datos y acceder a ellos mediante su API o sus eventos, evitando que otro servicio escriba directamente en sus tablas.

[[SOA - Clase 8]]

## Práctica adicional — LDR y LED

Este esquema fue creado para practicar. Representa un circuito que podrías reproducir en Wokwi y tiene un error intencional. El programa debe leer la iluminación y encender el LED cuando oscurece. Suponé que el módulo LDR se alimenta a 3,3 V y que su salida AO está dentro del rango de tensión admitido por la entrada.

![[SOA - Circuito de práctica.svg|670]]

### 3. Componentes y señales

**3.** Identificá el sensor y el actuador. Indicá a qué pines están conectados en el dibujo, el sentido de cada señal y si la aplicación necesita una señal analógica o digital.

> [!quote] Tu respuesta
> Sensor: Modulo LDR. Conectado a pin GPIO 34, la señal es de entrada, desde AO, hacia el GPIO 34. La señal es analogica.  
> Actuador: LED. Conectado a pin GPIO 35, la señal es de salida, desde GPIO35 hacia la resistencia, y de la resistencia, al positivo del LED. La señal es digital. Podría ser por PWM o binaria, según el caso, pero según el ejemplo, sería binaria, ya que indica encendido o apagado solamente.

> [!check]- Corrección y respuesta modelo  
> **3. Correcta, con una distinción.** Identificaste bien el módulo LDR, el sentido de su señal analógica y el control binario que requiere el LED. PWM tendría sentido si quisieras regular el brillo. En el dibujo, GPIO35 está **cableado como si fuera una salida**. Esa es la función prevista, aunque el pin no puede cumplirla.
>
> **Respuesta modelo.** El módulo LDR es el sensor. Su salida AO entrega una tensión analógica hacia GPIO34, una entrada con ADC en el ESP32 clásico. El LED es el actuador. Está cableado a GPIO35 por medio de una resistencia en serie y requiere una salida digital para encenderse y apagarse.

### 4. Error de cableado

**4.** Localizá el error de cableado. Explicá qué comportamiento impediría y qué conexión cambiarías.

> [!quote] Tu respuesta
> No logro identificar el error.

> [!check]- Corrección y respuesta modelo  
> **4. El error quedó sin identificar.** Para encontrarlo hacía falta conocer una restricción de GPIO35 que el ejercicio no daba. En la práctica nueva, el error se puede deducir siguiendo los cables y usando los datos del enunciado.
>
> **Respuesta modelo.** GPIO35 es exclusivamente de entrada en el ESP32 clásico, por lo que no puede manejar el LED. Mové el cable del LED a un GPIO que admita salida, por ejemplo GPIO25, y configurá ese pin como salida. Mantené la resistencia en serie y el retorno a GND.
>
> [Referencia de GPIO del ESP32](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/gpio.html)
