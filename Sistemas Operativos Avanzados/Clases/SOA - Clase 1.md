---
tipo: clase
fecha: 2026-08-18
tema: "Introducción a sistemas embebidos, señales y proyecto IoT"
fecha_fuente: metadato original sin corroborar
fecha_por_confirmar: true
---

> [!todo] Fecha pendiente de corroborar
> La fecha original puede haber quedado de la plantilla. No hay capturas fechadas en esta nota para corregirla con evidencia.

# Cuestiones importantes

Parcial: 10-11
2da Nota un TP de IoT. Entrega y coloquio: 17-11 / 24-11
Recuperatorio: 1-12

## Actividad práctica

- Ciclo de vida iterativo y continuo
- Las V1 y V2 son sin notas (aprobado o reentregar). La V3 es la entrega final
- Que se tiene en cuenta?
	- Defensa
	- Exposición
	- Si hay maqueta o no
	- Calidad del código
	- Patrones de diseño
	- Dedicación del alumno
	- Trabajo en equipo
	- Desarrollo adicional

### ¿Cómo va a ser?

Desarrollar una solución IoT
Se puede desplegar incluso en, por ejemplo, smartwatch. También hay algo que es node red
Etapas del ciclo de vida:
- Análisis
- Diseño
- Codificación
- Pruebas
Todo esto x3
1: Sistema simulado
2: Prototipo físico
3: Prototipo físico + App android

### V1: Sistema simulado

90% simulado
Usaremos WOKWI
Circuito simulado
Patrones de diseño -FSM

### V2: Prototipo físico

100% físico
Realizar el circuito
Conectividad de playstore
Iniciar Edge/Cloud computing (opcional)

### V3: Sumar app android

100% físico
Completar el circuito
Realizar conectividad con el app de android studio
Finalizar edge/cloud
Desplegar en smartwatch (opcional)

## Ideas

lúdico:
- Ruleta trucada
- Juego de luces para niños
- Auto con cámara
social:
- Bastón inteligente
- Anteojos para no videntes
- Pastillero inteligente
industrial:
- Mantenimiento predictivo de motores
- Seguridad de operarios en planta
- Monitoreo en condiciones ambientales
- Gestión de equipamiento
- Carro transportador seguidor de línea
Revisar de la PPT los 17 objetivos de desarrollo sostenible (ODS)

## Trabajo con IA

Comparar trabajos CON IA y SIN IA

## Condiciones

- No números mágicos
- No código comentado
- Código modular
- Seguir patrón máquina de estados
- Que no haya problemas de concurrencia
- Código trazable y legible

---

# Introducción a los Sistemas Embebidos

## ¿Qué es un SE?

Son sistemas de HW y SW de propósito específico integrados en algún producto del mercado
Deben realizar algún tipo de procesamiento o control.
Tiene un "cerebro" embebido. Esto realmente determina si es un SE o no.
- Microprocesador: CPU de propósito general que puede integrarse en un sistema embebido; consumo y prestaciones dependen del modelo.
- Microcontrolador: integra CPU, memoria y periféricos para controlar un dispositivo. No se define solo por tener menor capacidad de procesamiento.
- ASIC: circuito integrado diseñado para una aplicación específica.
- FPGA: circuito integrado cuya lógica puede configurarse después de su fabricación.
Estos componentes se pueden usar individualmente o componerlos en conjunto para crear el producto embebido en una placa electrónica

## Sensores y Actuadores

**Sensor**: Dispositivo que capta estímulos del ambiente. Ejemplos:
- Pulsador
- Sensor de luz, temperatura
- Micrófono
- etc
**Actuador**: Dispositivo que realiza una acción modificando el ambiente. Ejemplos:
- Led
- Motor
- Display
- etc

## Placas de Prototipado para SE

- MCU (microcontrolador)
	- Arduino, ESP32
	- Puede ejecutarse sin SO o con un RTOS como FreeRTOS.
	- RAM y almacenamiento integrados
	- Control de hw en tiempo real, IoT
- SBC (microprocesador)
	- Una Raspberry Pi es un ejemplo de SBC. Un smartphone es un sistema embebido completo, no necesariamente una placa de prototipado.
	- Usa SO
	- RAM y almacenamiento externos
	- Computación embebida, multimedia, IA
Las más usadas e importantes son:
- Arduino
- Raspberry PI
- ESP32

### ESP32

> GPIO: Pines que pueden configurarse como entrada o salida según su tipo

## Baremetal vs SO

> Bare metal: aplicación → bibliotecas/controladores → hardware, sin sistema operativo.
> Con SO: aplicación → servicios del sistema operativo/controladores → hardware.

El firmware puede ejecutar sobre baremetal o sobre un SO

## Compilación de un SE

**CrossCompilar (Compilación Cruzada)**: Compilar un programa en una arquitectura para que se ejecute en otra. Conectamos por USB nuestra PC a la ESP y compilamos.

## Depuración de un SE

Hacemos el paso inverso. Depuramos desde la PC lo que pasa en el ESP
- Depuración indirecta:
	- printf en un sistema embebido
	- Asi se debuggea en ESP32 / arduino UNO
- GDB:
	- Depurador que puede usar símbolos generados durante la compilación.
	- Permite el control de la ejecución del programa
	- En una PC se corre el cliente para poder controlar remotamente la ejecución
	- Permite ejecutar paso a paso el programa embebido
	- GDB en la computadora puede comunicarse con un servidor o una sonda de depuración; el mecanismo depende de la plataforma.
- JTAG
	- Conexion serie que accede a la electrónica implementada dentro del procesador para controlar su funcionamiento
	- Puede afectar el reloj del micro y se accede al HW, por dirección de memoria
	- Acceso específico a las patas del integrado.

## Estructura de un programa en ESP32

- Programación del ESP32
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
*Código principal*
```
loop()
{
	////
	////
}
```

### Protoboard

Es una forma más fácil de conectar cosas. Por ejemplo, conectar una batería o hacer circuitos

## Tipos de Señales

- Señal digital (1-0)
	- GPIOS Digitales en el pinout
	- Por ejemplo, un pulsador
- Señal analógica de entrada
	- GPIOS ADC
	- Solo vamos a poder usar las entradas analógicas del puerto ADC2 cuando el controlador Wifi no haya sido iniciado (ya que WiFi usa este canal. Usar ADC1 por defecto para este fin)
	- Una señal analógica puede tomar valores continuos dentro de su rango; no necesariamente varía todo el tiempo. El ADC la muestrea y cuantiza.
	- Señal análoga -> Señal muestreada -> Señal mantenida (digitalizada)
- Señal analógica de salida
	- DAC (pura analógica)
		- Audio por parlantes
	- PWM (Pulse Width Modulation): señal digital con ciclo de trabajo variable.
		- Leds
		- Buzzer
		- Motores
		- Servos

## Prototipo vs Producto Final

> Ver en casa

## ¿Cómo usar WOKWI?

[Wokwi - World's most advanced ESP32 Simulator](https://wokwi.com/)

**Tipos de sensores en simulador**
- Digitales
	- pulsador
	- interruptor deslizable
	- botón de joystick
	- keypad
	- pir
	- sensor de distancia
	- sensor de temperatura
	- receptor ir-control remoto
- analógicos
	- potenciómetro
	- sensor de luz (LDR)
	- potenciómetro deslizable
	- joystick (movimiento)
	- ....

**Tipos de actuadores en simulador**
- Digital
	- LED (prendido-apagado)
	- LED RGB (prendido-apagado)
	- Buzzer (prendido-apagado)
	- Motor (prendido-apagado)
	- Relé
	- Display LCD
	- Neopixel
- Control de intensidad, velocidad o posición (la señal puede ser PWM u otro protocolo, según el dispositivo)
	- Led (intensidad)
	- LED RGB (Cambiar de color)
	- Buzzer (melodía)
	- Motor (controlar velocidad mediante una etapa adecuada)
	- Servomotor

los actuadores que señales usan? Pregunta de parcial

---

# Enunciado API

## V1

Hay que armar el circuito simulado en Wokwi
- Construcción circuito
- Código del embebido
	- simulación sin errores
	- no esperas bloqueantes
	- máquinas de estado
	- dos tareas con freertos
	- no código comentado innecesario
- Informe
	- Por MIEL
	- PDF
	- Formato paper
**Entrega: 22-09**
El circuito físico es opcional

Para la semana que viene mandar 2 ideas. Indicar:
- Idea del proyecto
- Sensores y actuadores que vamos a usar

---

## Complemento de estudio

### Conceptos que conviene distinguir

Un microcontrolador integra CPU, memorias y periféricos; un microprocesador suele requerir más componentes externos. No definirlos solo por su velocidad o consumo. **Firmware** es software asociado al dispositivo y puede ejecutarse con o sin SO.

Compilación cruzada significa generar ejecutables para una plataforma destino distinta de la de desarrollo; compilar y cargar por USB son pasos diferentes. GDB puede controlar la depuración remota mediante un servidor o sonda; no siempre se instala un GDB server completo dentro del microcontrolador.

**PWM** es una señal digital que modifica el ciclo de trabajo; no es una salida DAC. Un actuador puede requerir una etapa de potencia: el GPIO no alimenta directamente un motor. En ESP32, pines, ADC, DAC e interacción con Wi-Fi dependen de la variante del chip.

**Repaso:** explicar sensor, actuador, firmware y compilación cruzada con el proyecto propio. Separar requisitos de la cátedra de propiedades generales de los embebidos.
