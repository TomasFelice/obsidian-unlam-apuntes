# SOA — Parcial 1C 2026

Fuente: [[Parcial-1c2026.webp]]

## Temario Tiempo Real

1. En un sistema de tiempo real que cuenta con 1 tarea del tipo Hard y 2 del tipo Soft, se decide utilizar planificación por Round Robin. ¿Está de acuerdo con la decisión? Justifique.
No estoy de acuerdo. En un sistema de tiempo real se deben tener en cuenta el periodo de una tarea, para garantizar que no va a ser excedido. En STR se suelen utilizar otro tipo de algoritmos de planificacion tales como RMS (prioridad fija por periodo), EDF (prioridad dinamica por deadline absoluto mas cercano) o LLF (prioridad dinamica por menor "laxitud"). Para el caso del ejemplo, utilizaría un algoritmo como RMS, o una variacion del mismo, para darle prioridad a la tarea de tipo hard, y luego a las de tipo soft.

> **Devolución 1 · 0,60/1,00**
>
> Tu objeción a Round Robin es razonable. La garantía de la tarea hard se mide contra su **deadline**. El período indica cada cuánto se activa una tarea periódica. Round Robin reparte CPU por turnos sin considerar deadlines. RMS, por su parte, prioriza por menor período, independientemente de que la tarea sea hard o soft. Una propuesta concreta es dar prioridad preferente a la hard y verificar que su tiempo de respuesta en el peor caso sea menor o igual a su deadline.

2. El mismo sistema utiliza DMA. ¿Considera que puede afectar alguna característica del sistema?
Sí, absolutamente. El uso de DMA, implica que no podemos conocer de forma deterministica los tiempos. Si bien, el uso de DMA disminuiría el tiempo promedio de acceso, como tendría que competir por el bus con el CPU, podría afectar de forma negativa en algunas ocasiones a otras tareas, generando incertidumbre no deseada para STR, y pudiendo ocasionar el incumplimiento de un deadline.

> **Devolución 2 · 0,80/1,00**
>
> Bien identificada la contención por el bus y su posible impacto en el deadline. La afirmación de que con DMA se pierde el determinismo es demasiado categórica. Si el arbitraje permite acotar la interferencia, podés incorporarla al análisis del peor caso. El beneficio principal del DMA es descargar a la CPU de la transferencia.

## Temario Sistemas Embebidos e IoT

La Selección Argentina de Fútbol lo contrata para desarrollar un sistema embebido que permita a los arqueros entrenar su velocidad mental y sus reflejos. Para ello, Lionel Scaloni le solicita diseñar un sistema que cuente con tres pulsadores: uno de color azul, otro de color amarillo y un tercero de color violeta. Además, el sistema deberá contar con un LED RGB y un potenciómetro.

Scaloni pide que los pulsadores estén ubicados a una distancia de 1 metro entre sí. El entrenamiento deberá tener una duración de 5 minutos. Durante ese período, el LED RGB deberá alternar entre los colores azul, amarillo y violeta, de manera que los arqueros tengan que correr hacia el pulsador correspondiente al color mostrado por el LED RGB. Por otra parte, mediante el potenciómetro, Scaloni podrá variar la velocidad con la que cambia el color del LED RGB.

Si el jugador no presiona el pulsador correspondiente antes de que el LED RGB cambie de color, se le restará un punto. En cambio, si lo presiona a tiempo, sumará un punto.

Scaloni desea iniciar el entrenamiento desde su smartphone Android y visualizar, al finalizar, el puntaje obtenido por el arquero.

3. Indique qué sensores y actuadores utilizaría para crear el sistema, especificando el tipo de señal que maneja cada uno.
Sensores:
- pulsadores (3): Señal digital binaria. HIGH o LOW. Se recibe en ESP32 mediante un GPIO.
- potenciometro: Señal análogica. Se recibe en ESP32 mediante un ADC.
Actuadores:
- LEDs (3): Señal digital binaria. HIGH o LOW. Se envía en ESP32 mediante un GPIO. Podría ser PWM en el caso de que debieramos variar la intensidad, pero en este caso con una señal binaria es suficiente.

> **Devolución 3 · 0,85/1,00**
>
> Correcto lo de los tres pulsadores digitales por GPIO y el potenciómetro analógico por ADC. La salida pedida es **un LED RGB con tres canales**. Podés usar azul solo, rojo + verde para amarillo y rojo + azul para aproximar violeta. PWM sirve para ajustar la intensidad de cada canal.

4. Si utiliza tareas de FreeRTOS, ¿qué elemento debería utilizar para saber cuándo finaliza el entrenamiento de forma automática? Explique con sus palabras de qué manera lo utilizaría.
Para saber cuándo finaliza el entrenamiento, debería utilizar un temporizador.
Para utilizarlo debería segur los siguientes pasos:
- Crearlo -> xTimerCreate(). Lo creo con un nombre, con el tiempo en el cuál deberá avisarme (en ticks, hay un helper que convierte ms a ticks), y con el callback que llamará al transcurrir el tiempo indicado.
- Iniciarlo -> xTimerStart(). Inicia el timer creado anteriormente.
- Detenerlo -> zTimerStop(). Cuando ya finalizaríamos el entrenamiento, no necesitamos mas el timer.

> **Devolución 4 · 0,80/1,00**
>
> El temporizador de software es una buena elección. Configuralo como **disparo único** (`pdFALSE`), con duración `pdMS_TO_TICKS(300000)`, e inicialo cuando arranque el entrenamiento. Al vencer, el callback puede notificar a la tarea que cierra la sesión y publica el puntaje. El temporizador se desactiva al expirar. Para cancelarlo antes, la función es `xTimerStop()`.

5. Scaloni quiere que el sistema tenga un historial de puntos de entrenamientos de cada arquero, que pueda ser consultado desde su smartphone. Teniendo en cuenta estos requerimientos:

   - **a)** ¿Cómo haría el sistema?
Haría que el embebido vaya publicando el resultado del entrenamiento en un topic de MQTT, y que un servidor con mosquitto por ejemplo, se suscriba al topic de MQTT, y realice la lógica necesaria par almacenar los datos estructurados de manera tal que puedan distinguirse los entrenamientos de cada arquero. En este servidor,los datos los almacenariamos en una db.
   - **b)** Realice un diagrama del diseño del sistema IoT, indicando los componentes embebidos y cómo se comunicarían con las aplicaciones mencionadas.

> **Devolución 5 · 0,30/1,00**
>
> **5a (0,30/0,50).** MQTT y una base de datos encajan. Mosquitto actúa como broker, y un servicio suscriptor recibe el resultado y guarda el ID del arquero, la fecha y el puntaje. Falta explicar cómo consulta Android el historial, por ejemplo mediante una API del backend.
>
> **5b (0,00/0,50).** Falta el diagrama. Incluí los pulsadores y el potenciómetro como entradas del ESP32 y el LED RGB como salida. Mostrá `Android → broker MQTT → ESP32` para iniciar, `ESP32 → broker MQTT → Android` para mostrar el resultado y `broker MQTT → backend → base de datos` para guardarlo. Agregá `Android → API del backend` para consultar el historial.


## Temario Android

6. Scaloni quiere que, cuando entrene el Dibu Martínez, el sistema acelere al máximo la velocidad del entrenamiento. A este funcionamiento se lo denomina modo “RapiDibu”. Para activar este modo, Scaloni desea girar el smartphone 180° de derecha a izquierda. En base a esto, responda:

   - **a)** ¿Qué sensor del teléfono debería usar?
Para detectar el giro de 180º en el smartphone, se debería utilizar el giroscopio.
   - **b)** Describa todas las clases del Framework de Android que son necesarias para implementar esta funcionalidad.
Para implementar esta funcionalidad debería tener en cuenta todas las clases necesarias para manejar sensores:
- Sensor -> el sensor como tal, el giroscopio en este caso
- SensorManager -> Mantiene el registro de sensores del sistema, funciona como un singleton, hay que incorporar el Sensor giroscopio alli
- SensorEvent -> Los datos del sensor
- SensorEventListener -> Escucha los cambios de los datos del sensor, implementa el patron observer.

> **Devolución 6 · 0,80/1,00**
>
> **6a (0,50/0,50).** El giroscopio es apropiado para detectar el giro.
>
> **6b (0,30/0,50).** Identificaste las cuatro piezas del framework. `SensorManager` obtiene el `Sensor` que Android ya reconoce y registra el `SensorEventListener`. El listener recibe los `SensorEvent` con velocidad angular y timestamp. Para detectar los 180°, acumulás `velocidad angular × Δt` en el eje y sentido del gesto. Al reconocerlo, la app puede enviar el comando RapiDibu al ESP32.


7. Explique qué realiza el siguiente código de Android:

   ```java
   Intent intent = new Intent(Principal.this, Secundaria.class);
   intent.putExtra("Nombre", "pepe");
   startActivity(intent);
   ```

Este código hace uso de los "Intents", los intents te permiten navegar, dentro o fuera de la app.
En este caso, lo que estamos haciendo es lo siguiente:
- Declaramos el Intent desde Principal hacia Secundaria
- Agregamos un parámetro (Nombre) que viajará al momento de ejecutar al intent
- Realiza el pasaje a Secundaria

> **Devolución 7 · 1,00/1,00**
>
> Correcto. Es un **Intent explícito** que abre `Secundaria` con `startActivity` y le pasa un extra de tipo `String`, con clave `"Nombre"` y valor `"pepe"`.


8. ¿Qué relación existe entre Linux y el sistema operativo Android? Explique la arquitectura de Android indicando las principales capas que la componen y la función de cada una.
Linux le proporciona el kernel al sistema operativo Android.
Arquitectura android:
- Kernel Linux: Proporciona las funciones basicas y mas de bajo nivel del SO. Planificacion, gestion de memoria, etc.
- HAL: Capa de abstraccion de hardware. Todos los dispositivos moviles que poseen android, pueden contener hardware completamente distinto, por ende, cada dispositivo, debe respetar una interfaz definida por la HAL.
- Native C/C++ libraries: No es comun su uso, pero al estar basado en linux, pueden utilizarse.
- Android Runtime: El runtime como tal de android.
- Java API Framework: El conjunto de librerias, interfaces y lenguaje en el cual se realiza una aplicacion en android.
- System Apps: Aplicaciones propias de Android, pueden extenderse y desarrollarse otras distintas.

> **Devolución 8 · 0,65/1,00**
>
> La relación con Linux y las funciones del kernel y la HAL están bien. Desarrollá las otras capas. **ART** ejecuta bytecode DEX y gestiona la memoria de las apps. Las **bibliotecas nativas** implementan funciones de plataforma como gráficos y multimedia. El **Java API Framework** expone APIs y servicios como actividades, recursos y notificaciones. Las **System Apps** ofrecen funciones al usuario y pueden exponer capacidades a otras apps.


## Temario Wearables

9. Scaloni le pide que construya el prototipo de un reloj para que los arqueros puedan ver en un display el tiempo restante hasta el próximo cambio de color del LED RGB. Para ello, usted utiliza un ESP32 alimentado a batería. Primero desarrolla el sistema utilizando una implementación Bare metal y observa que la batería, con carga completa, dura aproximadamente 2 horas. Luego, implementa una nueva versión utilizando tareas de FreeRTOS y nota que la duración de la batería aumenta hasta aproximadamente 5 horas.

   - **a)** ¿Por qué cree usted que se produce esta diferencia en consumo entre ambas versiones?
Se produce esta diferencia de consumo porque con baremetal, cuando queremos verificar si el tiempo del entrenamiento finalizo o no, tenemos que consumir ciclos de CPU, utilizando algo como delay o millis. Mientras que con FreeRTOS, podemos usar directamente un vTaskDelay o un Timer que nos pemite gestionar estos casos de manera mas eficiente, pasando a Bloqueada la tarea y dejando libre al CPU, pudiendo incluso dejar en modo de ahorro al embebido.

> **Devolución 9 · 0,85/1,00**
>
> Identificaste la diferencia entre espera activa y tarea bloqueada. `millis()` solo lee el tiempo. El gasto aparece cuando lo consultás continuamente en un bucle. Con FreeRTOS, la tarea puede bloquearse entre actualizaciones del display. El *light sleep* automático requiere habilitar la gestión de energía y *tickless idle*. Bare metal también puede ahorrar energía si usa interrupciones y reposo.

## Temario Microservicios

10. Nombre y describa al menos 4 características de los microservicios.
Independencia de despliegues: Cada servicio debería tener un despliegue completamente independiente del resto. Debería poder desplegar una nueva version de un servicio sin afectar a otro.
Despliegue en contenedores: Debería poder desplegar los microservicios usando contenedores, para poder replicar la imagen de una forma eficiente.
Mayor resiliencia: 
Escalabilidad horizontal: Cada servicio debería ser capaz de escalar horizontalmente, independientemente del resto. Es decir, si hay mucha carga en el servicio de Stock, deberían poder desplegarse nuevas instancias para ese servicio, mientras que en otros servicios no

> **Devolución 10 · 0,55/1,00**
>
> Despliegue independiente y escalado por servicio están bien explicados. Completá el **aislamiento de fallas** con un ejemplo: si falla reportes, el registro de entrenamientos puede seguir funcionando si no depende de él. Los contenedores son una opción de empaquetado. Como cuarta característica, describí la **separación por capacidad de negocio**, por ejemplo un servicio registra entrenamientos y otro genera reportes.

## Calificación orientativa

**Puntaje total: 7,20/10 (72 %). Nota orientativa: 6,6/10.**

Cada consigna vale 1 punto. En 5 y 6, cada inciso vale 0,50. Se asignó crédito parcial según la precisión técnica y el grado de desarrollo de cada respuesta.

Usé los cortes indicados de **50 % para un 4** y **75 % para un 7**. Para ubicar el 72 % entre ambos, interpolé en forma lineal: 4 + (72 − 50) × (7 − 4) / (75 − 50) = 6,64. El puntaje queda a **0,30 puntos de consigna** del corte para el 7.
