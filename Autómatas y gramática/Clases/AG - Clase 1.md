---
tipo: clase
fecha: 2026-08-26
tema: "Lenguajes, alfabetos, operaciones y jerarquía de Chomsky"
fecha_original: 2026-04-20
fecha_fuente: nombre de capturas
fecha_inferida: true
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

### Software de simulación

JFLAP

> Ver la clase de hoy en el video

---

# Unidad 1: Lenguajes

> Cualquier sistema de comunicación que utiliza símbolos y reglas para transmitir información

Los lenguajes pueden ser:
- Naturales
- Artificiales
![[Pasted image 20260826203540.png]]

## Lenguaje formal

> Concepto matemático usado en computación y lógica. Caracterizada por:
> - Definición precisa
> - Base teórica
> - Reglas explícitas de formación; una gramática formal puede ser ambigua.

![[Pasted image 20260826203637.png]]

> Esta basado en un alfabeto.
> son la base de los autómatas

![[Pasted image 20260826203737.png]]

## Alfabeto

> Conjunto finito y habitualmente no vacío de símbolos
![[Pasted image 20260826203815.png]]

## Palabra o cadena

> Secuencia finita y ordenada de símbolo de un alfabeto

![[Pasted image 20260826203839.png]]

## Conceptos

- Longitud: Cantidad de símbolos que tiene una palabra
- Cadena vacía (lambda): Longitud cero, no esta formada por ningún símbolo
![[Pasted image 20260826203927.png]]

![[Pasted image 20260826204129.png]]

- Apariciones: Nro de veces que aparece un símbolo en una palabra
![[Pasted image 20260826204154.png]]
- Ordenamiento: Para ordenar palabras se considerara como menor:
![[Pasted image 20260826204234.png]]
- Combinaciones: Partiendo del binario => 2^n
![[Pasted image 20260826204339.png]]

Partiendo de un subconjunto del alfabeto castellano
![[Pasted image 20260826204455.png]]
![[Pasted image 20260826214346.png]]

### Operaciones

**Concatenación**: Juntar las cadenas una detras de otra
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

> Define una función que transforma símbolos de un alfabeto en cadenas sobre otro alfabeto, preservando la concatenación
> Se usa para transformar lenguajes, codificar cadenas y demostrar propiedades en teoría de la computación

![[Pasted image 20260826221317.png]]
![[Pasted image 20260826221417.png]]
![[Pasted image 20260826221513.png]]
![[Pasted image 20260826221651.png]]
![[Pasted image 20260826221718.png]]

## Jerarquía de Chomsky (1956)

![[Pasted image 20260826221806.png]]
	![[Pasted image 20260826221828.png]]

---

## Complemento de estudio

### Notación fundamental

Para un alfabeto Σ, **Σ*** contiene todas las cadenas finitas, incluida ε (también escrita λ). **Σ+ = Σ* ∖ {ε}**. Un lenguaje formal es cualquier subconjunto de Σ*; puede ser finito o infinito. No confundir **∅**, lenguaje sin palabras, con **{ε}**, lenguaje que contiene una palabra de longitud cero.

Para cadenas x e y: |xy| = |x| + |y|; x⁰ = ε; (xy)ᴿ = yᴿxᴿ. Si Σ tiene k símbolos, existen kⁿ cadenas de longitud n. Para lenguajes, L⁰ = {ε} y L* es la unión de Lⁿ para n ≥ 0.

| Tipo | Familia | Reconocedor |
|---|---|---|
| 3 | Regular | Autómata finito |
| 2 | Independiente del contexto | Autómata de pila no determinista |
| 1 | Sensible al contexto | Autómata linealmente acotado |
| 0 | Recursivamente enumerable | Máquina de Turing |

Las inclusiones entre familias son propias. La admisión de ε en gramáticas tipo 1 requiere la convención especial correspondiente.
