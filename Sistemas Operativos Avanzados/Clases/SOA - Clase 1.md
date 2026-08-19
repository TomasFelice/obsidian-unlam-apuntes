---
tipo: clase
fecha: 2026-08-18
tema: Introduccion
---
# Cuestiones importantes
Parcial: 10-11
2da Nota un TP de IoT. Entrega y coloquio: 17-11 / 24-11
Recuperatorio: 1-12

## Actividad practoca
- Ciclo de vida iterativo y continuo
- Las V1 y V2 son sin notas (aprobado o reentregar). La V3 es la entrega final
- Que se tiene en cuenta?
	- Defensa
	- Exposicion
	- Si hay maqueta o no
	- Calidad del codigo
	- Patrones de disenio
	- Dedicacion del alumno
	- Trabajo en equipo
	- Desarrollo adicional
### Como va a ser?
Desarrollar una solucion IoT
Se puede desplegar incluso en, por ejemplo, smartwatch. Tambien hay algo qque es node red
Etapas del ciclo de vida:
- Analisis
- Disenio
- Codificacion
- Pruebas
Todo esto x3
1: Sistema simulado
2: Prototipo fisico
3: Prototipo fisico + App android
### V1: Sistema simulado
90% simulado
Usaremos WOKWI
Cirtcuito simulado
Patrones de disenio -FSM
### V2: Prototipo fisico
100% fisico
Realizar el circuito
Conectividad de playstore
Iniciar Edge/Cloud computing (opcional)
### V3: Sumar app android
100% fisico
Completar el circuito
Realizar conectividad con el app de android studio
Finalizar edge/cloud
Desplegar en smartwatch (opcional)
## Ideas
ludico:
- Ruleta trucada
- Juego de luces para ninios
- Auto con camara
social:
- Baston inteligente
- Anteojos para no videntes
- Pastillero inteligente
industrial:
- Mantenimiento predictivo de motores
- Seguridad de operarios en planta
- Monitoreo en condiciones ambientales
- Gestion de equipamiento
- Caroo transportador seguidor de linea
Revisar de la PPT los 17 objetivos de desarrollo sostenible (ODS)
## Trabajo con IA
Comparar trabajos CON IA y SIN IA
## Condiciones
- No nros magicos
- No codigo comentado
- Codigo modular
- Seguir patron maquina de estados
- Que no haya problemas de concurrencia
- Codigo trazable y legible

---
# Introducción a los Sistemas Embebidos
## Que es un SE?
Son sistemas de HW y SW de proposito especifico integrados en algun producto del mercado
Deben realizar algun tipo de procesamiento o control.
Tiene un "cerebro" embebido. Esto realmente determina si es un SE o no.
- Microprocesador: Mas optimizado que los de las computadoras. Consume menos energia
- Microcontrolador: Menos capacidad de procesamiento que los microprocesadores. Tiene distintos componentes.
- ASIC: Circuitos integrados (sumador, comparador, etc.)
- FPGA: Circuito integrado
Estos componentes se pueden usar individualmente o componerlos en conjunto para crear el producto embebido en una placa electronica
## Sensores y Actuadores
**Sensor**: Dispositivo que capta estimulos del ambiente. Ejemplos:
- Pulsador
- Sensor de luz, temperatura
- Microfono
- etc
**Actuador**: Dispositivo que realiza una accion modificando el ambiente. Ejemplos:
- Led
- Motor
- Display
- etc
## Placas de Prototipado para SE

- MCU (microcontrolador)
	- Arduino, ESP32
	- No usa SO (puede ejecutar FreeRTOS)
	- RAM y almacenamiento integrados
	- Control de hw en tiempo real, IoT
- SBC (microprocesador)
	- Raspberry Pi, Smartphone
	- Usa SO
	- RAM y almacenamiento externos
	- Computacion embebida, multimedia, IA
Las mas usadas e importantes son:
- Arduino
- Raspberry PI
- ESP32
### ESP32
> GPIO: Pines que pueden configurarse como entrada o salida segun su tipo

## Baremetal vs SO
> Baremetal -> HW pelado (app->os->drivers->hw)
> SO -> justamente el intermediario entre el HW y mi programa (app->hwlibs->hw)

El firmware puede ejecutar sobre baremetal o sobre un SO

## Compilacion de un SE
**CrossCompilar (Compilacion Cruzada)**: Compilar un programa en una arquitectura para que se ejecute en otra. Conectamos por USB nuestra PC a la ESP y compilamos.
## Depuracion de un SE
Hacemos el paso inverso. Depuramos desde la PC lo que pasa en el ESP
- Depuracion indirecta:
	- printf en un sistema embebido
	- Asi se debuggea en ESP32 / arduino UNO
- GDB:
	- Herramienta que se implementa con el compilador
	- Permite el control de la ejecucion del programa
	- En una PC se corre el cliente para poder controlar remotamente la ejecucion
	- Permite ejecutar paso a paso el programa embebido
	- Haces una arquitectura Cliente-Servidor. Instalo GDB en cliente y GDB server en servidor. GDB necesita de bastante poder de computo
- JTAG
	- Conexion serie que accede a la electronica implementada dentro del procesador para controlae su funcionamiento
	- Puede afectar el reloj del micro y se accede al HW, por direccion de memoria
	- Acceso especifico a las patas del integrado.
## Estructura de un programa en ESP32
- Programacion del ESP32
	- ESP-IDF
	- Framework arduino (usaremos este por practicidad)
*Configuracion inicial*
```
setup()
{
	//////
	//////
}
```
1 vez
|
*Codigo pricipal*
```
loop()
{
	////
	////
}
```
### Protoboard
Es una forma mas facil de conectar cosas. Por ejemplo, conectar una bateria o hacer circuitos

## Tipos de Senales
- Senal digital (1-0)
	- GPIOS Digitales en el pinout
	- Por ejemplo, un pulsador
- Senal analogica de entrada
	- GPIOS ADC
	- Solo vamos a poder usar las entradas analogicas del puerto ADC2 cuando el controlador Wifi no haya sido iniciado (ya que WiFi usa este canal. Usar ADC1 por defecto para este fin)
	- Es una senal que su valor de tension o voltaje varia constantemente y puede tomar cualquier calor (continuo)
	- Senal analoga -> Senal muestreada -> Senal mantenida (digitalizada)
- Senal analogica de salida
	- DAC (pura analogica)
		- Audio por parlantes
	- PWM (digitalizada) (Pulse Width Modulation)
		- Leds
		- Buzzer
		- Motores
		- Servos
## Prototipo vs Producto Final
> Ver en casa

## Como usar WOKWI?
[Wokwi - World's most advanced ESP32 Simulator](https://wokwi.com/)

**Tipos de sensores en simulador**
- Digitales
	- pulsador
	- interruptor deslizable
	- boton de joystick
	- keypad
	- pir
	- sensor de distancia
	- sensor de temperatura
	- receptor ir-control remoto
- analogicos
	- potenciometro
	- sensor de luz (LDR)
	- potenciomentro deslizable
	- joystick (movimiento)
	- ....

**Tipos de actuadores en simulador**
- Digital
	- LED (prendido-apagado)
	- LED RGB (prendido-apagado)
	- Buzzer (prendido-apagado)
	- Motor (prendido-apagado)
	- Rele
	- Display LCD
	- Neopixel
- Analogico
	- Led (intensidad)
	- LED RGB (Cambiar de color)
	- Buzzer (melodia)
	- Moto (Controlar la l=velocidad)
	- Servomotor

los actuadores que seniales usan? Pregunta de parcial

---
# Enunciado API
## V1
Hay que armar el circuito simulado en Wokwi
- Construccion circuito
- Codigo del embebido
	- simulacion sin erroes
	- no esperas bloqueantes
	- maquinas de estado
	- dos tareas con freertos
	- no codigo comentado innecesario
- Informe
	- Por MIEL
	- PDF
	- Formato paper
**Entrega: 22-09**
El circuito fisico es opcional

Para la semana que viene mandar 2 ideas. Indicar:
- Idea del proyecto
- Sensores y actuadores que vamos a usar