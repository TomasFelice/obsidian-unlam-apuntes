---
tipo: clase
fecha: 2026-10-27
tema: "Repaso de parcial e industria 4.0"
fecha_original: 2026-09-29
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Cronograma parte final

Para la entrega hay que tener el informe en miel y en el git, junto con todo el código.
El informe debe ser en formato PDF.
Los coloquios son el 17 o 24/11
**PARCIAL**:
- Embebidos
	- Señales
	- Depuración GDB, Indirecta
	- JTAG
	- Compilación cruzada
	- Firmware
	- SO, Bare metal
	- SBC
	- (todo lo de la primera ppt)
	- Nos suelen dar un caso de estudio, nos dan una tematica y decidir que sensores, actuadores, tipos de señales (pwm, analógica, etc). La señal y la etapa de potencia dependen del actuador. En los ejemplos de la cátedra se usan salidas digitales o PWM; no generalizar que ningún actuador admite control analógico.
	- Revisar en la última diapo los sensores y actuadores a estudiar
- Nos ponen un circuito y hay que indicar que esta mal.
	- Ejemplos:
		- Fuente externa, que tiene que compartir?
		- Revisar si los amperajes dan
		- Revisar ejemplo que se dio en clase
- Patron Máquina de Estados
	- Explicar los distintos patrones usamos con nuestras palabras
	- Por tabla / por switch
- Temporizadores
	- hw, sw, y freertos
- Freerttos
- Tiempo real
- Android: Todo lo de la primera PPT
	- Arquitectura, servicios, hilos, etc.
	- Sensores, comunicación mqtt (como funciona el protocolo), comunicación indirecta, etc,
- Microservicios
- IoT en la industria
- Weareables (si llegamos)

> Estilo de preguntas:
> - Caso de estudio
> - Explique si la oracione s correcta o no
> - Preguntas abiertas
> - Multiple choice justificando
> - 10 preguntas por lo general
> - Se puede llegar a tomar un código chiquito de android, y decir que es lo que hace.

> Todo el contenido se puede estudiar directamente de la PPT

---

# Software en la industria

> 1. introducción
> 2. software en la industria
> 3. Rigel
> 4. Tecnologias en la industria 4.0
> 5. Ejemplo grafana

## Introducción:

### Niveles de la piramide de automatizacion

- Nivel de gestión: Sistema de gestión transversal: gestión de compras, remitos, rrhh, etc.
- Nivel de operación: Permite hacer la programación, gestión de turnos, personas, planificación de producción, etc.
- Nivel de supervisión: Software que recoge la información de campo y control
- Nivel de control: Controladores (como esp pero mal polenta)
- Nivel de campo: Dispositivos relacionados directamente con la producción

> De 4 para abajo, es en una planta de producción
![[Pasted image 20261027193833.png]]

> Falta uno que es un WMS, se usa en los warehouses. Cuando ingresa la mercadería, se hace la trazabilidad. Se depositan automáticamente mediante robots, e incluso si lo piden te lo trae de nuevo.

> La piramid de automatizacion, divide en capas lo que podes automatizar en una industria y los distintos sw y hw que se usan en cada capa.

### 1. Nivel de Campo

![[Pasted image 20261027194628.png]]

### 2. Nivel de Control

![[Pasted image 20261027194723.png]]
> En los PLC hay cuestiones de redundancia, mecanismos para que no se caigan, etc.

### 3. Nivel de Supervisión

![[Pasted image 20261027194927.png]]
> Es sw. Tiene un SO. No es lo mismo que un HMI, es mucho más.

![[Pasted image 20261027195014.png]]

### 4. Nivel de Operacion

![[Pasted image 20261027195036.png]]
> MES permite monitorear, controlar y optimizar las operaciones de producción en tiempo real dentro de una planta industrial.
> - Progreso de ordenes de trabajo
> - Consumo de materiales
> - Disponibilidad de máquinas
> - Rendimiento de máquina
> - Paros o fallas
> - Trazabilidad de producto
> - OEE

### 5. Nivel de Gestión

![[Pasted image 20261027195223.png]]

## Software en la Industria

> Ver PPTs

## Rigel

> Mide la eficiencia de la productividad

### ¿Cómo se mide la productividad?

![[Pasted image 20261027195831.png]]

> OEE permite medir la eficiencia de una máquina

![[Pasted image 20261027195904.png]]
![[Pasted image 20261027200047.png]]
> Con dispositivos IoT van midiendo la producción y lo reportan al sistema

![[Pasted image 20261027200317.png]]

![[Pasted image 20261027200410.png]]

## Tecnologias en la Industria 4.0

### Ejes de la industria 4.0

- Automatizacion
- Recoleccion de datos
- Comunicación entre dispositivos
- Monitorizacion
![[Pasted image 20261027200505.png]]

### Automatizacion

![[Pasted image 20261027200521.png]]

### Comunicación y Recoleccion de Datos

![[Pasted image 20261027200538.png]]
> Aca entra nodered

### Middleware

![[Pasted image 20261027200555.png]]

### Visualizacion y Monitorizacion

![[Pasted image 20261027200607.png]]

![[Pasted image 20261027200627.png]]

---

## Complemento de estudio

### Pirámide de automatización y OEE

| Nivel | Función | Ejemplo |
|---|---|---|
| Campo | Medir y actuar | Sensores y actuadores |
| Control | Ejecutar control local | PLC |
| Supervisión | Observar y operar el proceso | SCADA/HMI |
| Operaciones | Gestionar producción | MES |
| Gestión | Planificar recursos empresariales | ERP |

Las fronteras varían entre arquitecturas. Un WMS gestiona almacenes y puede integrarse con otros niveles; no exige robots para existir.

**OEE = disponibilidad × rendimiento × calidad**. Si los factores son 0,90; 0,95 y 0,98, OEE = 0,8379 ≈ 83,8 %. Registrar período, tiempo planificado, ciclo ideal y piezas buenas para interpretar la medida.

Para el parcial, justificar elecciones: señal del sensor, adaptación eléctrica, etapa del actuador, FSM, deadline, comunicación y recuperación de fallos. Las fechas anotadas son información de clase y deben contrastarse con MIEL.
