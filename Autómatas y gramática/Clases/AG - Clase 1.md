---
tipo: clase
fecha: 2026-04-20
tema: Introduccion
---
# Autómatas y Gramáticas
Evaluaciones presenciales
Hay un "Foro de Asistencia"
### Contenidos
- **Unidad 1: Lenguajes (1er Parcial)**
- **Unidad 2: Lenguajes Tipo 3 (1er Parcial)**
	- **Parte A: Lenguajes y Gramáticas Regulares (1er Parcial)**
	- **Parte B: Autómatas Finitas (1er Parcial)**
- *Unidad 3: Lenguajes Tipo 2 (2do Parcial)*
	- *Parte A: Lenguajes y Gramáticas Independientes de Contexto (2do Parcial)*
	- *Parte B: Autómata de Pila (2do Parcial)*
- *Unidad 4: Lenguajes Tipo 1 y Tipo 0 (2do Parcial)*

### Fechas de Parcial
- 1er Parcial: 25/09
- 2do Parcial: 13/11
- Recuperatorio: 27/11
### Software de simulacion
JFLAP

> Ver la clase de hoy en el video

---
# Unidad 1: Lenguajes
> Cualquier sistema de comunicacion que utiliza simbolos y reglas para transmitir informacion

Los lenguajes pueden ser:
- Naturales
- Artificiales
![[Pasted image 20260826203540.png]]
## Lenguaje formal
> Concepto matematico usado en computacion y logica. Caracterizada por:
> - Definicion precisa
> - Base teorica
> - Ausencia de ambiguedad

![[Pasted image 20260826203637.png]]

> Esta basado en un alfabeto.
> son la base de los automatas

![[Pasted image 20260826203737.png]]

## Alfabeto
> Conjunto finito de simbolos
![[Pasted image 20260826203815.png]]

## Palabra o cadena
> Secuencia finita y ordenada de simbolo de un alfabeto

![[Pasted image 20260826203839.png]]

## Conceptos
- Longitud: Cantidad de simbolos que tiene una palabra
- Cadena vacia (lambda): Longitud cero, no esta formada por ningun simbolo
![[Pasted image 20260826203927.png]]

![[Pasted image 20260826204129.png]]

- Apariciones: Nro de veces que aparece un simbolo en una palabra
![[Pasted image 20260826204154.png]]
- Ordenamiento: Para ordenar palabras se considerara como menor:
![[Pasted image 20260826204234.png]]
- Combinaciones: Partiendo del binario => 2^n
![[Pasted image 20260826204339.png]]

Partiendo de un subconjunto del alfabeto castellano
![[Pasted image 20260826204455.png]]
![[Pasted image 20260826214346.png]]

### Operaciones
**Concatenacion**: Juntar las cadenas una detras de otra
![[Pasted image 20260826214439.png]]
**Potencia**: Concatenar la palabra consigo misma **n** veces.
![[Pasted image 20260826214627.png]]
**Reverso**: Es la misma palabra en orden inverso
![[Pasted image 20260826214707.png]]
![[Pasted image 20260826214734.png]]
### Propiedades de una palabra
![[Pasted image 20260826214758.png]]

![[Pasted image 20260826215006.png]]
![[Pasted image 20260826215139.png]]
![[Pasted image 20260826215246.png]]
![[Pasted image 20260826215453.png]]
![[Pasted image 20260826220026.png]]
![[Pasted image 20260826220105.png]]
## Operaciones sobre lenguajes
![[Pasted image 20260826220321.png]]
![[Pasted image 20260826220502.png]]
![[Pasted image 20260826220631.png]]
![[Pasted image 20260826220734.png]]
![[Pasted image 20260826220812.png]]![[Pasted image 20260826220909.png]]
## Homomorfismo en Lenguajes Formales
> Define una funcion que transforma simbolos de un alfabeto en cadenas sobre otro alfabeto, preservando la concatenacion
> Se usa para transformar lenguajes, codificar cadenas y demostrar propiedades en teoria de la computacion

![[Pasted image 20260826221317.png]]
![[Pasted image 20260826221417.png]]
![[Pasted image 20260826221513.png]]
![[Pasted image 20260826221651.png]]
![[Pasted image 20260826221718.png]]
## Jerarquia de Chomsky (1956)
![[Pasted image 20260826221806.png]]
	![[Pasted image 20260826221828.png]]