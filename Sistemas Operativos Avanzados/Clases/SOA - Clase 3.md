---
tipo: clase
fecha: 2026-09-01
tema: "Máquinas de estados finitos: implementación con switches y tablas"
fecha_original: 2026-08-18
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Máquinas de estado

## El porque de su uso

> Para evitar códigos extensos y difíciles de seguir, con muchos ifs y demas falencias, se utilizan las máquinas de estados

![[Pasted image 20260901193020.png]]

## Conceptos básicos

![[Pasted image 20260901193041.png]]
![[Pasted image 20260901193345.png]]
![[Pasted image 20260901193607.png]]
![[Pasted image 20260901193703.png]]
![[Pasted image 20260901193901.png]]
![[Pasted image 20260901194015.png]]

### Representación matemática

![[Pasted image 20260901194242.png]]

## Programación de máquinas de estado finito

![[Pasted image 20260901194328.png]]

#### Patron 1 (switches)

![[Pasted image 20260901194512.png]]

#### Patron 2 (tablas)

![[Pasted image 20260901194754.png]]
![[Pasted image 20260901195059.png]]
> Esto tiene la problematica de que se reutiliza poco.
> Para poder reusar código, vamos a verlo despues

![[Pasted image 20260901195427.png]]

## Ejemplos

### Estacionamiento

![[Pasted image 20260901200002.png]]

![[Pasted image 20260901200205.png]]
![[Pasted image 20260901200210.png]]
![[Pasted image 20260901200734.png]]
![[Pasted image 20260901202535.png]]![[Pasted image 20260901202547.png]]
![[Pasted image 20260901202703.png]]
> para soluciones pequeñas, el patrón de switch va bien.


---

# Aclaraciones TP

- Usaremos el repo proporcionado por la cátedra
- Embebido
	- sin vc -> Aca trabajamos y hacemos la entrea final
	- con vc -> Para despues
- Android
- Cloud
- Informes

## Tarea de la clase pasada

1. Las cosas que estan mal son:
	- Revisar la conexión GND de la ESP con el esquema del ejercicio; no deducir una regla general de esta anotación.
	- En la pista inferior, se supera la corriente disponible (100mA disponible vs 123mA consumidos)
2. \[insertar link\]

---

El sensor de corriente lo simulamos con **POTENCIÓMETRO**
Para simular el cooler de enfriamiento, usamos un led con pwm
Para simular el cooler de simulación de consumo,

Buscar ejemplos de cada uno de los sensores
Buscar ejemplos de código de cada uno
Máquina de estados (diagrama)
![[Pasted image 20260901223911.png]]

---

## Complemento de estudio

### Diseñar una FSM antes de programarla

Una máquina de estados finitos define estados Q, eventos E y una transición δ: Q × E → Q. En un modelo Mealy, la salida depende del estado y del evento; en Moore, del estado.

Ejemplo de un motor protegido:

| Estado | Evento | Acción | Siguiente estado |
|---|---|---|---|
| Apagado | Iniciar | Habilitar motor | Encendido |
| Encendido | Sobrecorriente | Cortar motor y avisar | Alarma |
| Encendido | Detener | Cortar motor | Apagado |
| Alarma | Rearme válido | Limpiar aviso | Apagado |

Definir umbrales, antirrebote e histéresis antes de generar eventos. El switch anidado es directo para máquinas pequeñas; una tabla separa la transición de su ejecución. Ambos patrones requieren definir eventos inesperados.

Probar cada transición y casos límite, especialmente si una alarma y una orden de inicio ocurren juntas. La política de prioridad debe ser explícita.
