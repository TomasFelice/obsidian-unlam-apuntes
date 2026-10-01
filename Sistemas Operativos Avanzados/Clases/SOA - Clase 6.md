---
tipo: clase
fecha: 2026-09-29
tema: Android
---
# Sistemas Embebidos Android
> Se puede trabajar con Kotlin/Java principalmente.
> Estos lenguajes ofrecen sentencias/sintaxis especifica que solo tiene sentido para dispositivos mobile.
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

> Si necesitar persistir algun dato entre activities, poder usar shared preferences, sqlite, entre otras

![[Pasted image 20260929194148.png]]

onCreate() es el unico que es obligatorio hacr @Override. No renderiza interfaz, solo incializa lo principal
onStart() empieza a renderizarse la pantalla (pero oculto)
onResume() estado que termina de renderizar y pone en funcionamiento la activiy
onPause() la aplicacion esta visible pero no esta en primer plano (un modal por ejemplo)
onStop() aplicacion oculta completamente (fui al incio del dispositivo, abri otra app, tc)
onRestart() cuando vuelvo a ingresar a la app
onDestroy() se destruye la aplicacion, s borran los datos

### Broadcast Receivers & Announcements
![[Pasted image 20260929194943.png]]
> Mensaje de difusion hacia apps interesadas
> Funciona como un observer. Escucho un evento, y cuando ocurre, hago determinada accion
> Se usa mucho para escuchar eventos del SO (modo avion, bluetooth, internet, etc.)
> Para escuchar creo una clase BroadcastReceiver que va a suscribirse al evento.
> Podria usarlo incluso para comunicar 2 procesos en mi propia app. Crearia una accion curstom, y enviar un mensaje de difusion que los comunique.
![[Pasted image 20260929195319.png]]
### Content Providers
![[Pasted image 20260929195311.png]]
Permiten compartir y consumir contenido de otra aplicacion.
Si quisiera reutilizar la galeria, por ejemplo, puedo hacerlo con esto.
Se usa un cursor para consultar datos. Es una especie de iterator.
Podemos tambien crear nuestro content provider.
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
> Hasta aca es el intent explicito
> EL intent implicito es:
> - Cuando no le indico explicitamente a donde voy a ir.
> - Es comun usarse con broadcast.

![[Pasted image 20260929200442.png]]

### Adicionales
Manifest:
- Contrato entre app y so
- configuracion inicial
	- permisos (camara, ubicacion, etc)
	- eventos a los que me suscribo (broadcast)
	- estetica
	- icono
	- nombre de la app
	- etc
- Ver ejemplos de codigo

---
# Aplicaciones
## Principios Basicos
![[Pasted image 20260929204348.png]]
![[Pasted image 20260929204357.png]]
![[Pasted image 20260929204654.png]]
![[Pasted image 20260929204705.png]]
> Herramientas que podemos usar para trabajos en background (services). Hay mecanismos para comunicar **hilos**. Colas de mensajes por ejemplo. Como comunicar un hilo con el hilo principal es muy comun, existe el **AsyncTask**: Un hilo que requiere actualizar la UI. Ya incorpora handlers, colas de mensajes, etc. Sin embargo, AsyncTask esta deprecado desde API30. En su lugar se usan **ExecutorService + Handler (Java) o corrutinas (Kotlin)**.
> Los **Services** es como una activity (proceso pesado), pero sin UI. Esta pensado para hacr una aplicacion de servicios pura. No sta pensado para que convivan Services y Activities. Compiten por recursos.
> **WorkManager**: Tareas que podes schedulear. Podes hacer que se ejecute algo a tal hora, o cuando ocurra tal cosa (wifi, carga, etc).


### Threads + Handler
![[Pasted image 20260929205602.png]]

### AsyncTask
![[Pasted image 20260929205717.png]]

doInBackground() es quivaleente a run() de los Thread

### WorkManager
![[Pasted image 20260929205923.png]]

### Services
![[Pasted image 20260929210509.png]]
![[Pasted image 20260929210516.png]]
![[Pasted image 20260929210525.png]]
- Background service: En segundo plano. El usuario no se entera que corre. No hay ninguna senial de que el mismo corre
- Foreground service: En segundo plano. Da evidencia al usuario de que hay algo corriendo. La app da aviso de que esta haciendo algo
- Bound service: Permite trabajar el servicio como si fuera un singleton. Sirve por ejemplo, si quiero obtener algo en varias activities. Es una especie de agrupador de funciones.
#### Ciclo de vida de un servicio
![[Pasted image 20260929210745.png]]
> Comparando contra una Activity, podemos ver que los eventos relacionados a la interfaz de usuario, no estan.

---
## NDK / Cross-compilation
El NDK nos permite ejecutar codigo C/C++ en la aplicacion. No se va a usar pero existe.
![[Pasted image 20260929211826.png]]

## Consola ADB
![[Pasted image 20260929211932.png]]
> Gestion de procesos muy a bajo nivel.


---
# Practica: Pasaje de Wokwi a Fisico
1. Instalar Arduino IDE/VSCode con PlatformIO
2. Configurar la placa (Seleccionar Placa/Puerto)
3. Hacer BlinkLed (probar todos los componentes individualmente)

Probar cada sensor y actuador por separado
Seguir la conexion del ejemplo de wokwi
1. LED, Pulsadores, RGB, Rele
2. Sensor de temperatura, Cooler
3. Puente H, etc.


Cuando tengamos armado el fisico, NO PEGUEMOS DIRECTAMENTE EL WOKWI.Es probable que no funcione. Lo que se recomienda es ir copiando de a porciones la maquina de estados e ir probando.

## V2 y V3 TP
**V2**: Prototipo fisico (20-oct)
**V3**: App Android (17-nov)

**V2**
Pasar el wokwi al fisico
Bajar en Play Store una app que es un servicio hqtt o http. Es como el monitor serial. Permite recibir comandos, hacer prints. Es lo que ya hicimos en wokwi con el serial, con los comandos y demas
(obligatorio)
fisico <-> servicio enlazado <-> app (MyMqtt)
(opcional, suma puntos)
fisico <-> servicio enlazado <-> node-red <-> app (MyMqtt)

**V3**
fisico <-> servicio enlazado <-> node-red <-> Android App
2 Activity como minimo
1- Boton y campo de texto
2- Al menos un sensor del smartphone, que realice alguna accion en el celu o en arduino


> V2 no tiene entrega formal. Solo hay que mostrar lo que hicimos en clase

Estructura de carpetas

- Embebido: Archivo .INO y bibliotecas
	- Proyecto sin vibe
	- Proyecto con vibe
- Android: Proyecto de Android Studio
	- Proyectyo sin vibe
	- Proyecto con vibe
- Edge-Cloud: Docker, DB, servidores
- Informe: Informes de las actividades

Entrega final:
- Mostrar en funcionamiento
- Toman coloquio
	- Preguntas del codigo en forma general
- Informe
