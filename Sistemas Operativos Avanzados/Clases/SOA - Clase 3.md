---
tipo: clase
fecha: 2026-08-18
tema: Maquina de Estados
---
# Maquinas de estado
## El porque de su uso
> Para evitar codigos extensos y dificiles de seguir, con muuchos ifs y demas falencias, se utilizan las maquinas de estados

![[Pasted image 20260901193020.png]]

## Conceptos basicos
![[Pasted image 20260901193041.png]]
![[Pasted image 20260901193345.png]]
![[Pasted image 20260901193607.png]]
![[Pasted image 20260901193703.png]]
![[Pasted image 20260901193901.png]]
![[Pasted image 20260901194015.png]]

### Representacion matematica
![[Pasted image 20260901194242.png]]

## Programacion de maquinas de estado finito
![[Pasted image 20260901194328.png]]
#### Patron 1 (switches)
![[Pasted image 20260901194512.png]]

#### Patron 2 (tablas)
![[Pasted image 20260901194754.png]]
![[Pasted image 20260901195059.png]]
> Esto tiene la problematica de que se reutiliza poco.
> Para poder reusar codigo, vamos a verlo despues

![[Pasted image 20260901195427.png]]

## Ejemplos
### Estacionamiento
![[Pasted image 20260901200002.png]]

![[Pasted image 20260901200205.png]]
![[Pasted image 20260901200210.png]]
![[Pasted image 20260901200734.png]]
![[Pasted image 20260901202535.png]]![[Pasted image 20260901202547.png]]
![[Pasted image 20260901202703.png]]
> para soluciones pequenias, el patron de switch va bien.



---
# Aclaraciones TP
- Usaremos el repo proporcionado por la catedra
- Embebido
	- sin vc -> Aca trabajamos y hacemos la entrea final
	- con vc -> Para despues
- Android
- Cloud
- Informes

## Tarea de la clase pasada
1. Las cosas que estan mal son:
	- La ESP no deberia tener coenctado el GND enla pista superior (la que tiene la fuente conectada)
	- En la pista inferior, se supera la corriente disponible (100mA disponible vs 123mA consumidos)
2. \[insertar link\]

---

El sensor de corriente lo simulamos con **POTENCIOMETRO**
Para simular el cooler de enfriamiento, usamos un led con pwm
Para simular el cooler de simulacion de condumo,

Buscar ejemplos de cada uno de los sensores
Buscar ejemplos de codigo de cada uno
Maquina de estados (diagrama)
![[Pasted image 20260901223911.png]]