---
tipo: clase
fecha: 2026-10-27
tema: "Wearables, Wear OS, watchOS y comunicación entre teléfono y reloj"
fecha_original: 2026-09-29
fecha_fuente: "metadatos previos; pendiente de confirmar"
fecha_inferida: true
fecha_revision: 2026-11-03
---
# Wearables, Wear OS y watchOS

> [!info] Alcance de la revisión
> Base de clase: [[Sistemas Operativos Avanzados/Material de clase/Clase-SO-wearables1°Cuat2025.pptx|PPT de wearables de la cátedra]], especialmente las diapositivas 18 a 29 para Wear OS, watchOS y comunicación. Se conservan las 11 capturas originales y se incorporan tres diagramas de esa PPT. El ejemplo de GitLab se explica a partir de sus archivos fuente. Las precisiones técnicas y los complementos se distinguen del contenido presentado en clase.

> [!note] Fecha pendiente de confirmar
> Se conservan las fechas previas por falta de una fuente concluyente. Los nombres de las capturas corresponden al **02/11/2026**, pero eso no demuestra la fecha en que se dictó la clase.

## 1. ¿Qué es un wearable?

Un **wearable** es un dispositivo tecnológico diseñado para llevarse puesto en el cuerpo o incorporado a la ropa y los accesorios. Puede captar datos del usuario o del entorno, procesarlos, comunicarlos y ofrecer una respuesta mediante pantalla, vibración, sonido u otros mecanismos.

En los ejemplos de la clase se trata de dispositivos externos y no invasivos. **La comodidad y la adaptación a la vida cotidiana son objetivos de diseño**, que deben verificarse en el uso real.

Los ejemplos más conocidos son los **smartwatches** y las **pulseras de actividad** (*fitness trackers*). También hay anillos, anteojos, prendas, calzado y dispositivos para animales.

| Ámbito | Aplicación posible |
|---|---|
| Actividad física y bienestar | Registrar pasos, entrenamientos o frecuencia cardíaca |
| Salud | Registrar variables para seguimiento, según las capacidades y validación del dispositivo |
| Vida cotidiana | Notificaciones, navegación y pagos |
| Entretenimiento y videojuegos | Interacción mediante gestos o accesorios hápticos |
| Industria | Alertas al operario, asistencia y registro de condiciones de trabajo |
| Animales | Localización y seguimiento de actividad |

![[Pasted image 20261102183019.png]]

**Confiabilidad:** una medición puede verse afectada por el sensor, la colocación, el movimiento, la calibración y el algoritmo. Para evaluar un wearable hay que definir qué mide, con qué error y bajo qué condiciones. No corresponde asumir que todos ofrecen prestaciones equivalentes.

La idea anotada de que los wearables reemplazarán a los smartphones es una **proyección**, no una propiedad técnica ni un resultado garantizado. Pueden complementar al teléfono o realizar algunas funciones de manera independiente.

## 2. Hardware y relación con el sistema operativo

Un wearable combina una unidad de procesamiento, memoria, sensores, alimentación y, según el producto, radio, pantalla y actuadores. Un **SoC** (*System on Chip*) integra varios componentes en un chip; no es sinónimo de sistema operativo. Puede incluir uno o varios núcleos, controladores, interfaces y otros bloques.

Para prototipar se pueden utilizar placas Arduino, ESP32 o Raspberry Pi, según los requisitos. No son alternativas equivalentes: una Raspberry Pi de tipo SBC suele tener necesidades de alimentación y recursos distintas de una placa con microcontrolador. La placa de desarrollo sirve para validar funciones; el producto final debe resolver tamaño, batería y ergonomía.

![[Pasted image 20261102183931.png]]

La diapositiva muestra una progresión desde dispositivos básicos hacia otros con más recursos. Es orientativa: el aspecto externo de una pulsera o un reloj no permite determinar qué SO utiliza.

| Alternativa | Organización del software | Criterio de elección |
|---|---|---|
| **Sin SO / bare metal** | Bucle principal, interrupciones, temporizadores y drivers | Funciones acotadas y control directo del hardware |
| **RTOS** | Tareas, prioridades, colas y mecanismos de sincronización | Actividades concurrentes con restricciones temporales y recursos limitados |
| **SO con más servicios** | Aplicaciones, interfaz gráfica, red, almacenamiento y servicios del sistema | Experiencias más complejas y ecosistema de aplicaciones |

**Tener un RTOS no garantiza cumplir todos los deadlines.** Eso depende también del diseño, los tiempos de ejecución, las prioridades y los bloqueos. Del mismo modo, responder rápido en promedio no garantiza tiempo real. Relacionar con [[SOA - Clase 4]].

## 3. Criterios de diseño y consumo de energía

Los puntos centrales del apunte son:

- **Uso sencillo:** curva de aprendizaje corta e interacciones breves.
- **Funciones adecuadas:** priorizar las que se pueden resolver con comodidad en ese formato.
- **Autonomía:** equilibrar capacidad de batería, frecuencia de medición, procesamiento y comunicaciones.
- **Privacidad y seguridad:** controlar el acceso a datos personales y proteger su almacenamiento y transmisión.
- **Costo:** considerar fabricación, mantenimiento y conectividad, además del hardware inicial.

Como complemento, revisar peso, materiales, contacto con la piel, resistencia a condiciones de uso y accesibilidad de la interfaz.

### 3.1. ¿Quién administra la energía?

![[Pasted image 20261102184647.png]]

La diapositiva distingue entre un equipo sin SO, donde el firmware debe organizar el ahorro, y otro con SO, donde existen servicios para administrarlo. La responsabilidad sigue siendo **compartida entre hardware, drivers, SO y aplicación**.

| Capa | Responsabilidad |
|---|---|
| Hardware | Ofrecer estados de bajo consumo, control de alimentación y fuentes de despertar |
| Drivers y firmware | Configurar sensores y periféricos, suspenderlos y restaurarlos correctamente |
| SO, si existe | Coordinar tareas y políticas de suspensión según el soporte disponible |
| Aplicación | Solicitar solo las mediciones, comunicaciones y recursos necesarios |

**Bloquear o suspender un hilo no equivale a poner todo el dispositivo en bajo consumo.** Puede haber otras tareas ejecutándose, periféricos activos o restricciones que impidan dormir al procesador. Además, un sensor puede seguir midiendo mientras la CPU principal duerme, si el hardware lo permite. Zephyr distingue mecanismos de ahorro del sistema y de los dispositivos en su [documentación de gestión de energía](https://docs.zephyrproject.org/latest/services/pm/index.html).

### 3.2. Estrategias de ahorro — complemento de estudio

- Muestrear a la frecuencia que necesita la aplicación y retirar las suscripciones innecesarias.
- Evitar la espera activa; usar temporizadores, eventos e interrupciones.
- Agrupar mediciones y envíos cuando la latencia admitida lo permita.
- Reducir el tiempo de pantalla encendida y el uso innecesario de GPS y radio.
- Elegir un estado de sueño compatible con los datos que se deben conservar y las fuentes de despertar necesarias.

El consumo se debe **medir**: depende del tiempo en cada estado y de los costos de despertar y transmitir. La guía de [ahorro de batería en Wear OS](https://developer.android.com/training/wearables/apps/power) destaca el impacto del acceso a red, pantalla y sensores.

Una estimación ideal, con capacidad y corriente expresadas de forma compatible, es:

$$
I_{\text{promedio}} = \sum_i I_i\,d_i,
\qquad
T\;[h] \approx \frac{C\;[mAh]}{I_{\text{promedio}}\;[mA]}
$$

Aquí, $d_i$ es la fracción de tiempo en cada estado y $\sum_i d_i=1$.

**Ejemplo didáctico:** una batería de 200 mAh, con consumo de 20 mA durante el 10 % del tiempo y 0,1 mA durante el 90 %, da $I_{\text{promedio}}=2,09\;mA$ y una autonomía ideal de aproximadamente **95,7 horas**. La autonomía real también depende de reguladores, temperatura, envejecimiento y capacidad utilizable; hay que incluir todos los consumos relevantes.

## 4. Arquitecturas de comunicación

### 4.1. Arquitectura con nodo central o gateway

![[Pasted image 20261102185122.png]]

Flujo típico del esquema:

**Sensores del wearable → procesamiento local → enlace de corto alcance → gateway → Internet → servicio remoto.**

El **gateway** puede ser un smartphone u otro equipo. Según el diseño, recibe datos de uno o varios wearables, los valida o preprocesa, los muestra, los almacena temporalmente y los envía a un servidor. No es obligatorio que haga todas esas tareas.

BLE o Zigbee son opciones de enlace local según el hardware y el ecosistema; no son intercambiables automáticamente ni proporcionan por sí solos acceso a Internet. Como complemento, en BLE el perfil **GATT** organiza datos en servicios y características, que pueden exponerse mediante operaciones de lectura, escritura o notificación. Véase la [introducción técnica de Bluetooth SIG](https://www.bluetooth.com/bluetooth-le-primer/).

**Ventajas del gateway:** permite descargar trabajo y conectividad del wearable y aprovechar una interfaz más amplia. **Limitaciones:** agrega dependencia de la disponibilidad, proximidad y batería del nodo central.

### 4.2. Arquitectura con acceso directo a la red

![[Pasted image 20261102185503.png]]

![[Pasted image 20261102185731.png]]

Algunos wearables incorporan Wi-Fi o conectividad celular para acceder al servicio remoto sin un smartphone como gateway de aplicación. Siguen necesitando infraestructura de red, como un punto de acceso o la red del operador.

La clase denomina a este esquema «arquitectura mejorada» porque reduce la dependencia del nodo central. **La elección depende del caso de uso:** también incorpora consumo, costo y gestión de la conectividad.

> [!important] Corrección sobre Wi-Fi y tiempo real
> Un wearable con solo Wi-Fi puede transmitir mientras dispone de una red accesible y de conectividad al destino. Fuera de cobertura puede almacenar los datos y enviarlos después, si se diseñó para eso. La falta de conectividad impide la entrega inmediata, pero no implica necesariamente perder la medición. Tampoco Wi-Fi ni LTE garantizan por sí solos un deadline de extremo a extremo.

En Wear OS, las rutas disponibles dependen del hardware y la conexión: el sistema puede utilizar el teléfono, Wi-Fi o red celular. La [documentación de acceso a red](https://developer.android.com/training/wearables/data/network-communication) describe estas alternativas.

| Aspecto | Con gateway | Con acceso directo |
|---|---|---|
| Dependencia principal | Enlace local y disponibilidad del gateway | Cobertura de red propia e infraestructura |
| Procesamiento | Puede delegarse al nodo central | Debe resolverse localmente o en el servidor |
| Energía | Puede reducir el trabajo y la radio necesarios en el wearable | Debe contemplar el costo de su conectividad |
| Sin conexión | Almacenamiento local y sincronización posterior, si están implementados | Igual necesidad de almacenamiento y recuperación |

### 4.3. Datos y recuperación — complemento de estudio

Definir qué ocurre al perder el enlace: capacidad del buffer, prioridad de los datos, descarte al llenarse, reintentos y sincronización posterior. Cada registro debería permitir identificar **dispositivo, valor, unidad, instante de medición y calidad**, cuando corresponda.

Hay que distinguir **momento de medición** de **momento de recepción**. Una muestra antigua reenviada no debe presentarse como actual. Los identificadores o números de secuencia ayudan a detectar duplicados.

Relacionar con [[SOA - Clase 7]] y [[SOA - Clase 8]]: MQTT puede usarse en el tramo hacia un broker si la plataforma lo soporta; no es sinónimo de BLE ni de almacenamiento. JSON es un formato de datos.

## 5. Formas de programación

### 5.1. Programación para una plataforma específica

![[Pasted image 20261102185744.png]]

Se desarrolla usando las APIs, bibliotecas y herramientas de la plataforma. En firmware son habituales C/C++; en otras plataformas se usan los lenguajes admitidos por su SDK.

La aplicación utiliza servicios concretos del sistema y queda acoplada a esas APIs y a las capacidades del dispositivo. Eso facilita aprovechar funciones específicas, pero portar la aplicación puede requerir cambios en sensores, interfaz, permisos y comunicaciones.

### 5.2. Programación mediante middleware

![[Pasted image 20261102190136.png]]

El **middleware** ofrece abstracciones y servicios entre la aplicación y las capas inferiores: comunicación, procesamiento de datos, seguridad, despliegue y administración de recursos, según la solución.

La aplicación puede trabajar con operaciones de mayor nivel en lugar de implementar cada detalle. Por ejemplo, solicitar una métrica de actividad en vez de configurar directamente varios sensores y combinar sus muestras.

**Precisión:** un middleware no resuelve automáticamente toda la seguridad ni toda la gestión de recursos. Abstrae lo que implementa y depende de una configuración y un uso correctos. Puede mejorar la portabilidad, con costos de memoria, ejecución y dependencia de sus interfaces.

### 5.3. SO, API, framework, SDK e IDE

![[Pasted image 20261102190555.png]]

| Concepto | Función |
|---|---|
| **Sistema operativo** | Administra recursos y proporciona servicios de ejecución |
| **API** | Define operaciones y contratos para acceder a una funcionalidad |
| **Framework** | Proporciona una estructura y componentes para construir aplicaciones |
| **SDK** | Reúne herramientas, bibliotecas y recursos para una plataforma |
| **IDE** | Integra edición, compilación, ejecución y depuración |

**Android Studio es un IDE**, no el SDK. Una herramienta puede integrar el uso de varios SDK. Framework y middleware pueden solaparse en una solución, pero los términos describen funciones diferentes.

Algunos fabricantes permiten instalar aplicaciones de terceros; otros exponen solo APIs para consultar servicios o sincronizar datos. Tener una API pública no implica poder ejecutar una aplicación propia dentro del wearable.

## 6. Sistemas operativos y ecosistemas

![[Pasted image 20261102190229.png]]

![[Pasted image 20261102190508.png]]

Las diapositivas mencionan Linux embebido, Tizen, watchOS, Wear OS, Zephyr, RIOT OS, FreeRTOS y sistemas propietarios. La disponibilidad de herramientas y aplicaciones depende del fabricante, modelo y versión; el cuadro de «activo/descontinuado» debe leerse como material de la presentación, no como un inventario actualizado.

**Corrección de denominación:** Zephyr es un RTOS del proyecto Zephyr, alojado en la Linux Foundation; no es una distribución ni el kernel Linux. Está orientado a sistemas embebidos con recursos limitados. Véase la [introducción oficial de Zephyr](https://docs.zephyrproject.org/latest/introduction/index.html).

Como complemento, los ecosistemas tienen herramientas propias: Wear OS utiliza las herramientas de Android; Apple ofrece herramientas y APIs para [watchOS](https://developer.apple.com/watchos/); Garmin dispone de [Connect IQ y su SDK](https://developer.garmin.com/connect-iq/overview/). Compartir una categoría de dispositivo no implica compatibilidad entre sus aplicaciones.

## 7. Wear OS

### 7.1. Arquitectura — diapositiva 18

**Wear OS** es el sistema de Google para wearables. La PPT lo presenta como una adaptación de Android para pantallas pequeñas y hardware con recursos más limitados que un smartphone.

- Su arquitectura es semejante a la de Android, con funciones y servicios adaptados al reloj.
- Su kernel es una variante del **núcleo Linux**.
- Las aplicaciones utilizan **Android Runtime (ART)** y se ejecutan con el aislamiento de aplicaciones de Android.

La diapositiva habla de una «VM propia» por aplicación. Para relacionarlo con [[SOA - Clase 6]], interpretar esa expresión como el entorno de ejecución de la aplicación en su proceso, sin confundirlo con ejecutar un SO completo en una máquina virtual por cada app.

### 7.2. Sincronización y Data Layer — diapositiva 19

La **Wearable Data Layer API**, parte de Google Play services, comunica las aplicaciones del teléfono Android y del reloj Wear OS. Ambas deben tener el mismo nombre de paquete y la misma firma. Véase la [descripción oficial de Data Layer](https://developer.android.com/training/wearables/data/overview).

![[Sistemas Operativos Avanzados/Material de clase/Imagenes Wearables/SOA10 - Sincronizacion Wear OS.png]]

El primer esquema de la PPT muestra un reloj conectado al teléfono por Bluetooth y otro con acceso por Wi-Fi a un nodo de nube. Ilustra rutas de comunicación posibles, sujetas al hardware y a la conectividad disponibles.

![[Sistemas Operativos Avanzados/Material de clase/Imagenes Wearables/SOA10 - APIs Wear OS.png]]

El segundo esquema utiliza nombres históricos de Android Wear. Para leerlo junto al ejemplo de la cátedra:

| Nombre en el esquema | Cliente correspondiente | Función |
|---|---|---|
| **Node API** | `NodeClient` | Consultar nodos, como los dispositivos conectados |
| **Message API** | `MessageClient` | Enviar mensajes breves a un nodo conectado |
| **Data API** | `DataClient` | Sincronizar datos mediante `DataItem` y, para cargas mayores, `Asset` |

**Mensaje y dato sincronizado tienen comportamientos distintos.** `sendMessage()` requiere conexión, no persiste el mensaje ni incorpora reintentos automáticos. `DataClient` permite sincronizar datos al restablecerse la conexión; esa sincronización no sustituye el almacenamiento propio de la aplicación. Véanse la [comparación de clientes](https://developer.android.com/training/wearables/data/client-types) y la [guía de sincronización](https://developer.android.com/training/wearables/data/sync).

Para acceder a un servidor se usan las APIs de red de la plataforma. Data Layer resuelve la comunicación entre dispositivos del ecosistema, no constituye por sí misma una API de backend. Véase la [guía de acceso a red](https://developer.android.com/training/wearables/data/network-communication).

### 7.3. Batería, segundo plano y sensores — diapositiva 20

La PPT reúne estos mecanismos de ahorro:

| Concepto | Función |
|---|---|
| **WorkManager** | Programar trabajo persistente y diferible, como una sincronización |
| **Descanso / Doze** | Restringir actividad de CPU y red en segundo plano durante la inactividad del dispositivo, aplazando tareas, sincronizaciones y alarmas estándar |
| **App Standby** | Aplazar actividad de red en segundo plano de aplicaciones sin interacción reciente del usuario |

> [!important] Precisión sobre la diapositiva
> Doze y App Standby son mecanismos del **sistema Android**, no funciones propias de WorkManager. El trabajo programado debe respetar esas restricciones. WorkManager tampoco ofrece un temporizador con deadlines estrictos. Véase la [explicación oficial de Doze y App Standby](https://developer.android.com/training/monitoring-device-state/doze-standby).

Para acceder a sensores se puede utilizar `SensorManager`, como en [[SOA - Clase 7]]. La PPT recomienda los **servicios de salud del framework** para un uso más eficiente cuando corresponda al dato y al caso de uso.

**Complemento de estudio:** Health Services, disponible desde Wear OS 3, coordina sensores y algoritmos para obtener métricas de actividad y ejercicio. Elegir `MeasureClient` para mediciones breves, `ExerciseClient` para entrenamientos o `PassiveMonitoringClient` para seguimiento pasivo. Comprobar capacidades y permisos según dispositivo y versión. Fuentes: [Health Services](https://developer.android.com/health-and-fitness/health-services) y [permisos](https://developer.android.com/health-and-fitness/health-services/permissions).

### 7.4. Programación y preparación del entorno — diapositivas 23 a 26

La PPT presenta estas opciones para lógica e interfaz. Aunque las columnas originales se llaman «backend» y «frontend», aquí describen partes de las aplicaciones, no necesariamente un servidor remoto.

| Dispositivo | Lógica de la aplicación en la PPT | Interfaz en la PPT |
|---|---|---|
| Smartphone | Java o Kotlin | XML o Jetpack Compose |
| Wearable | Kotlin | Jetpack Compose |

La tabla refleja las opciones enseñadas. Android Studio es el **IDE**, mientras que los SDK y bibliotecas aportan las APIs y herramientas de la plataforma. Para el reloj se utilizan componentes de interfaz adaptados a Wear OS. Véase la [guía de Compose para Wear OS](https://developer.android.com/training/wearables/compose).

La diapositiva 25 enumera crear la app, enlazar el reloj físico o emulador y conectar teléfono y reloj. Como guía para estudiar el ejemplo:

1. Abrir el proyecto y reconocer sus módulos `mobile` y `wear`.
2. Preparar el teléfono y el reloj o sus emuladores, y establecer el emparejamiento correspondiente.
3. Instalar la aplicación de cada módulo en su dispositivo.
4. Verificar que comparten identificador de aplicación y firma, y que Data Layer está disponible.
5. Enviar un texto y observar la recepción, la pantalla y los registros de Logcat.

La diapositiva 26 enlaza otro ejemplo, **Notification_wear**. El proyecto **WearableListenerService**, enlazado en la diapositiva 29 y desarrollado en el apartado 9, es el que se analiza aquí.

### 7.5. Aplicaciones independientes — complemento de estudio

Una app **standalone** completa sus funciones principales sin una app en el teléfono; una **non-standalone** depende de ella. Ser independiente del teléfono no implica funcionar sin Internet ni disponer de LTE. Fuente: [tipos de aplicación Wear OS](https://developer.android.com/training/wearables/apps/standalone-apps).

## 8. watchOS

### 8.1. Arquitectura y herramientas — diapositivas 17 y 21

**watchOS** es el sistema de Apple para sus relojes. La PPT lo describe como una variante de **iOS** y señala que utiliza el kernel híbrido **XNU**, que combina componentes Mach y BSD, principalmente derivados de FreeBSD. La escritura «FREEBDS» de la diapositiva corresponde a **FreeBSD**. Como precisión, la arquitectura de XNU también incluye I/O Kit. Véase la [descripción de la arquitectura del kernel de Apple](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Architecture/Architecture.html).

Para programación, la tabla de clase menciona **WatchKit** y «iOS SDK». Conviene distinguir el framework de las herramientas de desarrollo y del SDK específico del destino watchOS, dentro del ecosistema de Apple.

### 8.2. Sincronización con el iPhone — diapositiva 22

![[Sistemas Operativos Avanzados/Material de clase/Imagenes Wearables/SOA10 - Sincronizacion watchOS.png]]

El esquema de clase contiene:

- En el **Apple Watch**, la Watch app y su **WatchKit extension**, sobre watchOS.
- En el **iPhone**, la aplicación iOS, sobre iOS.
- Entre ambos, el framework **Watch Connectivity**, que permite intercambiar información entre las aplicaciones.

La extensión representa el componente de ejecución de la app del reloj en el modelo dibujado por la PPT. La comunicación se realiza mediante las APIs del framework; el dibujo no representa memoria compartida ni un único proceso entre reloj y teléfono.

**Complemento de estudio:** `WCSession` inicia la comunicación y `WCSessionDelegate` recibe los eventos. El framework admite transferencia de datos y archivos, tanto en segundo plano como mediante comunicación inmediata cuando se cumplen las condiciones correspondientes. Véase la [documentación de Watch Connectivity](https://developer.apple.com/documentation/watchconnectivity).

| Operación de `WCSession` | Uso orientativo |
|---|---|
| `sendMessage` | Mensaje inmediato a la contraparte alcanzable, con posibilidad de respuesta |
| `updateApplicationContext` | Compartir el estado más reciente, reemplazando el contexto anterior |
| `transferUserInfo` | Encolar información para transferencia en segundo plano |
| `transferFile` | Transferir archivos en segundo plano |

Estas operaciones amplían el esquema de clase y no aparecen desarrolladas en la PPT. Su selección depende de si se necesita un mensaje inmediato, el último estado o una transferencia diferida. Fuente: [referencia de WCSession](https://developer.apple.com/documentation/watchconnectivity/wcsession).

### 8.3. Comparación para el parcial

| Aspecto | Wear OS | watchOS |
|---|---|---|
| Fabricante de la plataforma | Google | Apple |
| Familia señalada en la PPT | Android | iOS |
| Kernel | Linux | XNU, híbrido con componentes Mach y BSD |
| Ejecución destacada en clase | Android Runtime | Watch app y WatchKit extension en el esquema presentado |
| Comunicación con la app del teléfono | Wearable Data Layer, mediante Google Play services | Watch Connectivity |
| APIs a reconocer | `NodeClient`, `MessageClient`, `DataClient` | `WCSession` y sus operaciones, como complemento |
| Ejemplo práctico analizado | `mobile` envía texto y `wear` lo recibe con `WearableListenerService` | La PPT presenta el esquema, sin un ejemplo equivalente de código |

Ambas plataformas proporcionan mecanismos de comunicación y administración de recursos. Sus frameworks y aplicaciones pertenecen a ecosistemas distintos.

## 9. Ejemplo de la cátedra: WearableListenerService

Fuente principal: [proyecto WearableListenerService en GitLab](https://gitlab.com/so-unlam/Material-SOA/-/tree/master/Ejemplos%20Android/WearOs/WearableListenerService). El análisis corresponde a la lectura de sus fuentes en `master`, realizada el 03/11/2026; no presupone haberlo compilado ni ejecutado.

### 9.1. Estructura y flujo completo

El proyecto tiene dos módulos Android: **`mobile`** para el smartphone y **`wear`** para el reloj. Ambos declaran `applicationId = "com.example.wearablelistenerservice"` y utilizan la biblioteca `play-services-wearable`.

| Componente | Responsabilidad en el ejemplo |
|---|---|
| `mobile/MainActivity.kt` y `activity_main.xml` | Leer el texto ingresado y atender el botón Enviar |
| `mobile/SendToWearable.kt` | Buscar nodos conectados y enviarles el mensaje |
| `wear/AndroidManifest.xml` | Declarar el servicio y su filtro de recepción |
| `wear/presentation/ListenerService.kt` | Recibir el texto, actualizar el estado y reproducir sonido |
| `wear/presentation/MainActivity.kt` | Mostrar el estado recibido mediante Compose |
| `wear/presentation/theme/Music.kt` | Administrar el `MediaPlayer` de la alarma |

**Flujo:** el usuario ingresa texto, pulsa Enviar y el teléfono busca nodos conectados. Por cada nodo, solicita el envío con el path **`/msg`**. En el reloj, `ListenerService` filtra ese path, decodifica los bytes, actualiza `receivedText` y llama a `Music.play(this)`.

### 9.2. Envío desde el teléfono

En la `MainActivity` del módulo `mobile`, el botón llama a:

```kotlin
sendMessageToWearable(this, "/msg", txtTexto.text.toString())
```

`SendToWearable` crea un `thread`, consulta `Wearable.getNodeClient(context).connectedNodes` y espera su resultado mediante `Tasks.await(...)`. Luego recorre los nodos y utiliza esta llamada central:

```kotlin
Wearable.getMessageClient(context).sendMessage(
    node.id,
    path,
    message.toByteArray()
)
```

El **`node.id` identifica al destinatario**, el **path identifica el tipo de mensaje** y el arreglo de bytes transporta el contenido. `/msg` es una convención de la aplicación; no es una URL HTTP ni un topic MQTT.

La espera de nodos bloquea el hilo creado, no el hilo de interfaz. Cada envío registra callbacks de éxito y error. Si no hay nodos, el bucle no envía nada y el ejemplo no muestra un aviso específico para ese caso. Fuente: [SendToWearable.kt](https://gitlab.com/so-unlam/Material-SOA/-/blob/master/Ejemplos%20Android/WearOs/WearableListenerService/mobile/src/main/java/com/example/wearablelistenerservice/SendToWearable.kt).

### 9.3. Recepción y ciclo de vida del servicio

La diapositiva 27 presenta **`WearableListenerService`** como un servicio para comunicación asincrónica cuyo ciclo de vida administra el sistema. Google Play services se vincula al servicio cuando necesita entregar eventos y deja de hacerlo al terminar el trabajo. No hace falta mantener una `Activity` visible para recibirlos. Véase la [guía de sincronización y ciclo de vida](https://developer.android.com/training/wearables/data/sync).

La frase de la PPT «se crea cuando llega un mensaje y se destruye automáticamente» resume ese funcionamiento. **No implica necesariamente una instancia nueva por mensaje ni destrucción inmediata después del callback.** Sus callbacks se ejecutan por defecto en un hilo de fondo, una particularidad de esta clase que no debe generalizarse a cualquier `Service`. Fuente: [referencia de WearableListenerService](https://developers.google.com/android/reference/com/google/android/gms/wearable/WearableListenerService).

En el módulo `wear`, el manifiesto declara `.presentation.ListenerService`, habilitado y exportado, con:

- Acción `com.google.android.gms.wearable.MESSAGE_RECEIVED`.
- Esquema `wear`.
- Host `*` y prefijo de path `/`, un filtro amplio de mensajes.

Después, el callback verifica el path exacto **`/msg`**. Es decir, el filtro del manifiesto permite la entrega y el código decide cuáles mensajes procesa. Fuente: [AndroidManifest.xml del reloj](https://gitlab.com/so-unlam/Material-SOA/-/blob/master/Ejemplos%20Android/WearOs/WearableListenerService/wear/src/main/AndroidManifest.xml).

### 9.4. Pantalla y alarma en el reloj

`ListenerService` hereda de `WearableListenerService` y redefine `onMessageReceived`. Si coincide el path, convierte `messageEvent.data` en texto, lo registra en Logcat, asigna el valor a **`MainActivity.receivedText.value`** y llama a **`Music.play(this)`**. Sus métodos `onCreate` y `onDestroy` también escriben en Logcat. Fuente: [ListenerService.kt](https://gitlab.com/so-unlam/Material-SOA/-/blob/master/Ejemplos%20Android/WearOs/WearableListenerService/wear/src/main/java/com/example/wearablelistenerservice/presentation/ListenerService.kt).

La actividad del reloj declara `receivedText` como un `mutableStateOf("Esperando texto...")` dentro de su `companion object`. El composable `WearApp` lee ese estado y muestra su valor en un `Text`. Al cambiar el estado, la interfaz que lo observa puede recomponerse. **El servicio no inicia la actividad explícitamente**: recepción y visualización tienen ciclos de vida diferentes. Fuente: [MainActivity.kt del reloj](https://gitlab.com/so-unlam/Material-SOA/-/blob/master/Ejemplos%20Android/WearOs/WearableListenerService/wear/src/main/java/com/example/wearablelistenerservice/presentation/MainActivity.kt).

`Music.play` detiene y libera un reproductor anterior, crea uno para `R.raw.siren2_fixed`, registra su liberación al finalizar y comienza la reproducción. En `ListenerService.onDestroy`, la llamada a `Music.stop()` está **comentada**; no se debe explicar como si se ejecutara. Fuente: [Music.kt](https://gitlab.com/so-unlam/Material-SOA/-/blob/master/Ejemplos%20Android/WearOs/WearableListenerService/wear/src/main/java/com/example/wearablelistenerservice/presentation/theme/Music.kt).

### 9.5. Diferencias entre la PPT y el repositorio

| Aspecto | Diapositiva 28 | Proyecto de GitLab |
|---|---|---|
| Path | `/mi_mensaje` | `/msg` |
| Envío fuera del hilo de interfaz | Función `suspend` con `withContext(Dispatchers.IO)` | `thread { ... }` |
| Recepción | `MyWearableListenerService` registra el mensaje | `ListenerService` registra, cambia el estado y reproduce alarma |

Los dos ejemplos enseñan el mismo patrón de **descubrir nodos, enviar bytes y atender un callback**, pero los nombres y las implementaciones no deben mezclarse. El path del emisor debe coincidir con el que verifica el receptor. La palabra `suspend` por sí sola no selecciona un hilo de fondo; en la diapositiva esa decisión se expresa con `Dispatchers.IO`.

### 9.6. Límites y preguntas para interpretar el código

- **Sin conexión:** el ejemplo no implementa una cola persistente ni reintentos. `MessageClient` realiza un envío de mejor esfuerzo, según la [comparación oficial de clientes](https://developer.android.com/training/wearables/data/client-types).
- **Confirmación:** el callback de éxito de `sendMessage()` indica que se encoló para entrega al nodo conectado. No confirma que el usuario lo haya visto ni que la alarma haya terminado. Para confirmar una acción se necesita una respuesta de la aplicación. Fuente: [contrato de MessageClient](https://developers.google.com/android/reference/com/google/android/gms/wearable/MessageClient).
- **Persistencia:** `receivedText` conserva estado en memoria del proceso, no un historial durable. Un reinicio del proceso puede perderlo.
- **Dirección:** las APIs permiten comunicación en ambos sentidos, pero este ejemplo implementa el envío de texto **del teléfono al reloj**.
- **Privacidad y permisos:** el teléfono solicita permisos Bluetooth y ubicación. Su presencia en el ejemplo no implica que todo uso de Data Layer requiera ese mismo conjunto; hay que revisar las operaciones y las versiones de Android.
- **Standalone:** el manifiesto del reloj marca `standalone=true`, pero el flujo demostrado necesita al teléfono como emisor. Esa marca no demuestra que la función principal sea independiente y debe revisarse según el producto.

**Ejercicio:** si el emisor utiliza `/mi_mensaje` y se mantiene el receptor del repositorio, el callback no procesa el texto porque espera `/msg`. Si el reloj queda desconectado, no se debe suponer que el mensaje aparecerá automáticamente al reconectar.

## 10. Caso integrador — complemento de estudio

**Problema:** una pulsera registra movimiento, avisa al usuario mediante vibración y sincroniza un resumen con un servidor. Debe seguir registrando si el teléfono se aleja.

1. **Hardware:** microcontrolador, acelerómetro, BLE, memoria, batería y actuador háptico con el circuito de manejo adecuado. Justificar alimentación y consumo como en [[SOA - Clase 2]].
2. **Adquisición:** elegir frecuencia y rango del acelerómetro según la actividad; usar temporizadores o interrupciones para evitar espera activa.
3. **Procesamiento local:** filtrar o resumir datos para reducir memoria y transmisiones, conservando lo necesario para el objetivo.
4. **Concurrencia:** separar adquisición, almacenamiento y comunicación. Elegir bare metal o RTOS según complejidad y restricciones temporales.
5. **Conectividad:** enviar por BLE al teléfono, que actúa como gateway hacia el servidor.
6. **Desconexión:** guardar registros con tiempo y secuencia; al reconectar, sincronizar y controlar duplicados. Definir qué ocurre al llenarse la memoria.
7. **Energía y privacidad:** medir consumo por estado, limitar el uso de radio, autenticar los accesos y conservar solo los datos necesarios.

Una FSM posible es **inicialización → registro**, con estados de **sincronización** y **error**. El diseño debe permitir continuar la adquisición durante la sincronización si ese es un requisito; una transmisión bloqueante no debería hacer perder muestras. Relacionar con [[SOA - Clase 3]] y [[SOA - Clase 5]].

## 11. Preguntas de repaso con respuesta orientativa

1. **¿Todo wearable necesita un SO?** No. Puede usar bare metal, RTOS u otro SO según sus funciones y recursos.
2. **¿Suspender una tarea garantiza ahorro de todo el equipo?** No. Hay que considerar las demás tareas, periféricos y estados de energía disponibles.
3. **¿Qué aporta el gateway?** Recibe datos del enlace local y puede procesarlos, mostrarlos, almacenarlos y conectarlos con servicios remotos.
4. **¿Wi-Fi impide transmitir en tiempo real?** No. Importan cobertura, conectividad, latencia y deadline. Una tecnología de red por sí sola tampoco garantiza tiempo real.
5. **¿Perder conexión implica perder datos?** Depende del diseño: un buffer permite conservarlos, aunque no entregarlos inmediatamente y tiene capacidad limitada.
6. **¿Middleware elimina toda dependencia de plataforma?** No. Abstrae ciertas funciones y conserva dependencias de implementación y soporte.
7. **¿Android Studio es un SDK?** No, es un IDE que integra herramientas y SDK.
8. **¿Standalone significa que no requiere Internet?** No. Significa que no depende de una app del teléfono para sus funciones principales.
9. **¿Data Layer y acceso al backend son lo mismo?** No. Resuelven relaciones de comunicación diferentes.
10. **¿Un RTOS garantiza todos los deadlines?** No. El sistema completo debe diseñarse y analizarse para cumplirlos.
11. **¿Qué kernel usa cada plataforma?** Wear OS utiliza Linux; watchOS utiliza XNU, con componentes Mach y BSD.
12. **¿Doze y App Standby son funciones de WorkManager?** Son mecanismos del sistema que condicionan la ejecución del trabajo programado.
13. **¿Qué diferencia hay entre `NodeClient` y `MessageClient`?** El primero permite consultar nodos; el segundo envía mensajes a un nodo.
14. **¿Para qué sirve el path `/msg`?** Identifica el mensaje según el contrato entre emisor y receptor; ambos extremos deben coincidir.
15. **¿Cómo recibe el reloj sin tener la actividad abierta?** Mediante el servicio declarado en el manifiesto, cuyo ciclo de vida administra el sistema.
16. **¿Qué hace el ejemplo al recibir el texto?** Lo registra, actualiza el estado observado por Compose y reproduce una alarma.
17. **¿Qué framework comunica la app del Apple Watch con la del iPhone?** Watch Connectivity; `WCSession` es el objeto de sesión explicado como complemento.

Para estudiar, poder justificar **hardware, SO, consumo, arquitectura de comunicación, pérdida de conectividad y privacidad** a partir de un caso concreto.
