---
tipo: clase
fecha: 2026-09-29
tema: "Android: arquitectura, componentes, ciclo de vida y trabajo en segundo plano"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Sistemas Embebidos Android

> Se puede trabajar con Kotlin/Java principalmente.
> Kotlin y Java son lenguajes de propósito general; el SDK de Android aporta APIs y componentes de la plataforma.
> IDEs: Android Studio (Jetbrains) (permite compilar e instalarlo en el dispositivo, por ejemplo, emuladores, etc.) (Se integra con firebase, g analytics, permite publicar directamente)

## Arquitectura Android

- Linux kernel
- Hardware Abstraction Layer (HAL)
- Android Runtime
- Native C/C+ Libraries
- Java API Framework
- System Apps
![[Pasted image 20260929192715.png]]
![[Pasted image 20260929192812.png]]

## Componentes esenciales

![[Pasted image 20260929193050.png]]

### Activities + Layout

![[Pasted image 20260929193136.png]]
> Haciendo analogia a desarrollo web: Activity->Controlador mezclado con JS del front. Layout->HTML

El comportamiento por defecto de las Activities, es que se van apilando en un stack. Por lo tanto, hay que tener presente que hay que ir finalizandolas.

> Para persistir datos entre pantallas o ejecuciones, elegir almacenamiento según el dato: preferencias para valores simples y una base de datos para información estructurada.

![[Pasted image 20260929194148.png]]

Los callbacks describen el ciclo de vida de una Activity, no de toda la aplicación:
- **onCreate():** inicialización, creación o asociación de la interfaz y recuperación del estado.
- **onStart():** pasa a ser visible.
- **onResume():** entra en estado reanudado, normalmente interactivo.
- **onPause():** pierde el estado reanudado; puede seguir visible.
- **onStop():** deja de ser visible.
- **onRestart():** se llama antes de volver a iniciar una Activity detenida.
- **onDestroy():** destruye esa instancia; puede ocurrir por rotación o finalización. No se garantiza si el proceso es terminado.

### Broadcast Receivers & Announcements

![[Pasted image 20260929194943.png]]
> Mensaje de difusion hacia apps interesadas
> Funciona como un observer. Escucho un evento, y cuando ocurre, hago determinada acción
> Se usa mucho para escuchar eventos del SO (modo avion, bluetooth, internet, etc.)
> Para escuchar creo una clase BroadcastReceiver que va a suscribirse al evento.
> Podria usarlo incluso para comunicar 2 procesos en mi propia app. Crearia una acción personalizada, y enviar un mensaje de difusion que los comunique.
![[Pasted image 20260929195319.png]]

### Content Providers

![[Pasted image 20260929195311.png]]
Permiten compartir y consumir contenido de otra aplicación.
Si quisiera reutilizar la galeria, por ejemplo, puedo hacerlo con esto.
Se usa un cursor para consultar datos. Es una especie de iterator.
Podemos también crear nuestro content provider.
![[Pasted image 20260929195816.png]]

### Shared Preferences

> Sistema de almacenamiento basado en key-value.

![[Pasted image 20260929195842.png]]

![[Pasted image 20260929200134.png]]

### Intents

![[Pasted image 20260929200142.png]]
> Permiten la navegacion entre 2 Activities o componentes distintos
> Es un clase que le decis desde donde hacia donde vas.
> Tiene un objeto interno (un mapa, bundle), mediante el cual se pueden pasar mensajes de un componente a otro.
> Hasta acá es el intent explícito
> EL intent implícito es:
> - Cuando no le indico explícitamente a donde voy a ir.
> - Es común usarse con broadcast.

![[Pasted image 20260929200442.png]]

### Adicionales

Manifest:
- Contrato entre app y so
- configuración inicial
	- permisos (cámara, ubicación, etc)
	- eventos a los que me suscribo (broadcast)
	- estética
	- icono
	- nombre de la app
	- etc
- Ver ejemplos de código

---

# Aplicaciones

## Principios Básicos

![[Pasted image 20260929204348.png]]
![[Pasted image 20260929204357.png]]
![[Pasted image 20260929204654.png]]
![[Pasted image 20260929204705.png]]
> Herramientas que podemos usar para trabajos en background (services). Hay mecanismos para comunicar **hilos**. Colas de mensajes por ejemplo. Como comunicar un hilo con el hilo principal es muy común, existe el **AsyncTask**: Un hilo que requiere actualizar la UI. Ya incorpora handlers, colas de mensajes, etc. Sin embargo, AsyncTask esta deprecado desde API30. En su lugar se usan **ExecutorService + Handler (Java) o corrutinas (Kotlin)**.
> Un **Service** es un componente sin interfaz que puede convivir con Activities. Por defecto se ejecuta en el proceso y el hilo principal de la aplicación: no crea un hilo de trabajo automáticamente.
> **WorkManager:** ejecuta trabajo persistente con restricciones y planificación flexible. No garantiza una hora exacta; elegirlo según la necesidad del trabajo.


### Threads + Handler

![[Pasted image 20260929205602.png]]

### AsyncTask

![[Pasted image 20260929205717.png]]

En AsyncTask, doInBackground() contenía el trabajo de fondo. La comparación con run() ayuda a ubicar ese trabajo, pero no vuelve equivalentes ambos mecanismos.

### WorkManager

![[Pasted image 20260929205923.png]]

### Services

![[Pasted image 20260929210509.png]]
![[Pasted image 20260929210516.png]]
![[Pasted image 20260929210525.png]]
- Background service: En segundo plano. El usuario no se entera que corre. No hay ninguna señal de que el mismo corre
- Foreground service: En segundo plano. Da evidencia al usuario de que hay algo corriendo. La app da aviso de que esta haciendo algo
- Bound service: expone una interfaz a componentes clientes vinculados; su ciclo de vida depende de esos vínculos y de si también fue iniciado.

#### Ciclo de vida de un servicio

![[Pasted image 20260929210745.png]]
> Comparando contra una Activity, podemos ver que los eventos relacionados a la interfaz de usuario, no estan.

---

## NDK / Cross-compilation

El NDK nos permite ejecutar código C/C++ en la aplicación. No se va a usar pero existe.
![[Pasted image 20260929211826.png]]

## Consola ADB

![[Pasted image 20260929211932.png]]
> ADB permite comunicarse con un dispositivo o emulador: instalar aplicaciones, consultar logs y ejecutar comandos, entre otras tareas.


---

# Práctica: Pasaje de Wokwi a Fisico

1. Instalar Arduino IDE/VSCode con PlatformIO
2. Configurar la placa (Seleccionar Placa/Puerto)
3. Hacer BlinkLed (probar todos los componentes individualmente)

Probar cada sensor y actuador por separado
Seguir la conexión del ejemplo de wokwi
1. LED, Pulsadores, RGB, Relé
2. Sensor de temperatura, Cooler
3. Puente H, etc.


Cuando tengamos armado el físico, NO PEGUEMOS DIRECTAMENTE EL WOKWI.Es probable que no funcione. Lo que se recomienda es ir copiando de a porciones la máquina de estados e ir probando.

## V2 y V3 TP

**V2**: Prototipo físico (20-oct)
**V3**: App Android (17-nov)

**V2**
Pasar el wokwi al físico
Bajar en Play Store una app que es un servicio MQTT o http. Es como el monitor serial. Permite recibir comandos, hacer prints. Es lo que ya hicimos en wokwi con el serial, con los comandos y demas
(obligatorio)
físico <-> servicio enlazado <-> app (MyMqtt)
(opcional, suma puntos)
físico <-> servicio enlazado <-> node-red <-> app (MyMqtt)

**V3**
físico <-> servicio enlazado <-> node-red <-> Android App
2 Activity como mínimo
1- Botón y campo de texto
2- Al menos un sensor del smartphone, que realice alguna acción en el celu o en arduino


> V2 no tiene entrega formal. Solo hay que mostrar lo que hicimos en clase

Estructura de carpetas

- Embebido: Archivo .INO y bibliotecas
	- Proyecto sin vibe
	- Proyecto con vibe
- Android: Proyecto de Android Studio
	- Proyecto sin vibe
	- Proyecto con vibe
- Edge-Cloud: Docker, DB, servidores
- Informe: Informes de las actividades

Entrega final:
- Mostrar en funcionamiento
- Toman coloquio
	- Preguntas del código en forma general
- Informe

---

## Complemento de estudio

### Activity, hilo, proceso y Service

Una Activity representa una interfaz con ciclo de vida. Un hilo ejecuta instrucciones; un proceso aloja componentes y memoria. Un Service representa trabajo sin interfaz; no es un «proceso pesado» ni excluye usar Activities en la misma aplicación.

No realizar red ni trabajo prolongado en el hilo principal. Un bound service expone una interfaz a clientes; no es simplemente un singleton. Un foreground service debe informar al usuario mediante notificación y está sujeto a restricciones de plataforma.

WorkManager sirve para trabajo persistente que puede ejecutarse bajo restricciones. Para actualizar la UI, respetar el ciclo de vida y el hilo principal. onDestroy() no es un lugar confiable para guardar por primera vez datos importantes.

Fuentes: [ciclo de vida](https://developer.android.com/guide/components/activities/activity-lifecycle), [procesos e hilos](https://developer.android.com/guide/components/processes-and-threads), [WorkManager](https://developer.android.com/develop/background-work/background-tasks/persistent).
