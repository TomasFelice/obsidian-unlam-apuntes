---
tipo: clase
fecha: 2026-09-29
tema: Android
---
# Cronongrama parte final
Para la entrega hay que tener el informe en miel y en el git, junto con todo el codigo.
El informe debe ser en frmato PDF.
Los coloquios son el 17 o 24/11 
**PARCIAL**:
- Embebidos
	- Seniales
	- Depuracion GDB, Indirecta
	- JTAG
	- Compilacion cruzada
	- Firmware
	- SO, Bare metal
	- SBC
	- (todo lo de la primera ppt)
	- Nos suelen dar un caso de estudio, nos dan una tematica y decidir que sensores, actuadores, tipos de seniales (pwm, analogica, etc). Un actuador no puede ser con senial analogica.
	- Revisar en la ultima diapo los sensores y actuadores a estudiar
- Nos ponen un circuito y hay que indicar que esta mal.
	- Ejemplos:
		- Fuente externa, que tiene que compartir?
		- Revisar si los amperajes dan
		- Revisar ejemplo que se dio en clase
- Patron Maquina de Estados
	- Explicar los distintos patrones usamos con nuestras palabras
	- Por tabla / por switch
- Temporizadores
	- hw, sw, y freertos
- Freerttos
- Tiempo real
- Android: Todo lo de la primera PPT
	- Arquitectura, servicios, hilos, etc.
	- Sensores, comunicacion mqtt (como funciona el protocolo), comunicacion indirecta, etc,
- Microservicios
- IoT en la industria
- Weareables (si llegamos)

> Estilo de preguntas:
> - Caso de estudio
> - Explique si la oracione s correcta o no
> - Preguntas abiertas
> - Multiple choice justificando
> - 10 preguntas por lo general
> - Se puede llegar a tomar un codigo chiquito de android, y decir que es lo que hace.

> Todo el contenido se puede estudiar directamente de la PPT

---
# Software en la industria
> 1. intruduccion
> 2. software en la industria
> 3. Rigel
> 4. Tecnologias en la industria 4.0
> 5. Ejemplo grafana

## Introduccion:
### Niveles de la piramide de automatizacion
- Nivel de gestion: Sistema de gestion transversal: gestion de compras, remitos, rrhh, etc.
- Nivel de operacion: Permite hacr la programacion, gestion de turnos, personas, planificacion de prodduccion, etc.
- Nivel de supervision: Software que recoge la infromacion de campo y control
- Nivel de control: Controladores (como esp pero mal polenta)
- Nivel de campo: Dispositivos relacionados directamente con la produccion

> De 4 para abajo, es en una planta de produccion
![[Pasted image 20261027193833.png]]

> Falta uno que es un WMS, se usa en los warehouses. Cuando ingresa la mercadderia, se hace la trazabilidad. Se depositan automaticamente mediante robots, e incluso si lo piden te lo trae de nuevo.

> La piramid de automatizacion, divide en capas lo que podes automatizar en una industria y los distintos sw y hw que se usan en cada capa.

### 1. Nivel de Campo
![[Pasted image 20261027194628.png]]

### 2. Nivel de Control
![[Pasted image 20261027194723.png]]
> En los PLC hay cuestiones de redundancia, mecanismos para que no se caigan, etc.

### 3. Nivel de Supervision
![[Pasted image 20261027194927.png]]
> Es sw. Tiene un SO. No es lo mismo que un HMI, es mucho mas.

![[Pasted image 20261027195014.png]]

### 4. Nivel de Operacion
![[Pasted image 20261027195036.png]]
> MES permite monitorear, controlar y optimizar las operaciones de produccion en tiempo real dentro de una planta industrial.
> - Progreso de ordenes de trabajo
> - Consumo de materiales
> - Disponibilidad de maquinas
> - Rendimiento de maquina
> - Paros o fallas
> - Trazabilidad de producto
> - OEE

### 5. Nivel de Gestion
![[Pasted image 20261027195223.png]]

## Software en la Industria
> Ver PPTs

## Rigel
> Mide la eficiencia de la productividad

### Como se mide la productividad?
![[Pasted image 20261027195831.png]]

> OEE permite medir la eficienta de una maquina

![[Pasted image 20261027195904.png]]
![[Pasted image 20261027200047.png]]
> Con dispositivos IoT van midiendo la produccion y lo reportan al sistema

![[Pasted image 20261027200317.png]]

![[Pasted image 20261027200410.png]]

## Tecnologias en la Industria 4.0
### Ejes de la industria 4.0
- Automatizacion
- Recoleccion de datos
- Comunicacion entre dispositivos
- Monitorizacion
![[Pasted image 20261027200505.png]]

### Automatizacion
![[Pasted image 20261027200521.png]]

### Comunicacion y Recoleccion de Datos
![[Pasted image 20261027200538.png]]
> Aca entra nodered

### Middleware
![[Pasted image 20261027200555.png]]

### Visualizacion y Monitorizacion
![[Pasted image 20261027200607.png]]

![[Pasted image 20261027200627.png]]

