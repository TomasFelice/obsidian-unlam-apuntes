---
tipo: clase
fecha: 2026-08-28
tema: "Lenguajes regulares, expresiones regulares y BNF"
fecha_original: 2026-04-20
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Práctica 1 - Unidad 1: Lenguajes

## Ejercicio 1

![[Pasted image 20260828192006.png]]

x=ct, y=ab
 x^2 = ct.ct = ctct
 x^r = (ct)^r = t . (c)^r = tc
 x^r . y^2 . y^r = tc . abab . ba = tcababba

## Ejercicio 2

![[Pasted image 20260828192405.png]]

L1:
Pueden existir las cadenas...
bb => Si (n=0, k=1)
lambda=> Si (por clausura de kleene)
a => No

L2:
lambda => Si (por clausula de kleene)
00 => Si (m=2, n=2)
10 => No (orden invertido, no tiene la forma descripta)

> **0 es par**

a) ab^4 pertenece a L1?
ab^4 => n=1 >= 0, 2k = 4 => k=2 >= 1

![[Pasted image 20260828193349.png]]

![[Pasted image 20260828193440.png]]
![[Pasted image 20260828193633.png]]

## Ejercicio 3

![[Pasted image 20260828193704.png]]
![[Pasted image 20260828194010.png]]
![[Pasted image 20260828194340.png]]
![[Pasted image 20260828194627.png]]

![[Pasted image 20260828194955.png]]

![[Pasted image 20260828195116.png]]
![[Pasted image 20260828195148.png]]

## Ejercicio 6

![[Pasted image 20260828195735.png]]

---

# Unidad 2 - Parte A: Lenguaje Tipo 3 (Lenguajes y Gramáticas Regulares)

## Expresión Regular - REGEX

![[Pasted image 20260828200824.png]]

## Lenguajes Regulares

![[Pasted image 20260828201421.png]]

### Propiedades de Clausura

![[Pasted image 20260828201505.png]]
![[Pasted image 20260828201803.png]]
![[Pasted image 20260828201910.png]]

#### Ejercicio

![[Pasted image 20260828202041.png]]
`(a|b).a.(a|b)*.b.(a|b)`
![[Pasted image 20260828203211.png]]
`(a|b)*.(bbb).b*.a.(a|b)*`
![[Pasted image 20260828204306.png]] La resolución de clase fue esta. Asumiendo que no hay nada antes ni despues. De todas maneras, mi resolución cumple, dada la ambiguedad del enunciado
![[Pasted image 20260828204345.png]]
a.
- 0
- 01
- lambda (mínima)
b.
- ab, cd --> mínimas
- abab
- cdcd
- ababab
c.
- lambda (mínima)
- a
- ae
- aaaaa
- eeeee

![[Pasted image 20260828205956.png]]
![[Pasted image 20260828210157.png]]
![[Pasted image 20260828210223.png]]
1. FALSO
2. FALSO
3. FALSO
4. VERDADERO
5. FALSO
![[Pasted image 20260828211832.png]]
![[Pasted image 20260828211912.png]]

### Propiedades básicas de las regex

![[Pasted image 20260828212243.png]]
![[Pasted image 20260828212448.png]]
![[Pasted image 20260828212935.png]]
![[Pasted image 20260828213408.png]]

## Gramáticas

![[Pasted image 20260828213636.png]]
![[Pasted image 20260828214005.png]]
![[Pasted image 20260828214025.png]]
![[Pasted image 20260828215222.png]]
![[Pasted image 20260828215303.png]]

![[Pasted image 20260828215617.png]]15 reglas en cada caso, por más que cambie la notación
La regex es
`(+|-)(0|1|2|3|4|5|6|7|8|9)(0|1|2|3|4|5|6|7|8|9)*`

![[Pasted image 20260828220323.png]]
![[Pasted image 20260828221250.png]]

> ***"Dos gramáticas son equivalentes si generan el mismo lenguaje"***

### Formas de escribir una gramática

![[Pasted image 20260828221347.png]]

### Gramáticas en notación BNF (Backus-Naur Form)

- Notación formal para describir la sintaxis de lenguajes formales y programación
- Características principales:
	- No terminales entre <>
	- Asignacion con ::=
	- Alternativas se separan con |
	- ...
	![[Pasted image 20260828221651.png]]


	![[Pasted image 20260828221705.png]]
	a. finito
	b. aa, ab, ba, bb
	c. (a|b)(a|b)
![[Pasted image 20260828221956.png]]
- `aaaa(a)*bbb(b)*`
- `aa*bb(bb)*`
![[Pasted image 20260828222615.png]]

![[Pasted image 20260828222717.png]]
![[Pasted image 20260828222746.png]]
![[Pasted image 20260828222808.png]]
![[Pasted image 20260828222904.png]]
![[Pasted image 20260828223029.png]]

---

## Complemento de estudio

### Leer una expresión regular

Unión elige alternativas, concatenación conserva el orden y estrella de Kleene permite cero o más repeticiones. La clausura positiva exige una o más. Por ejemplo, (ab)* contiene ε, ab y abab; no contiene aab.

La expresión (+|-)(0|1|…|9)(0|1|…|9)* representa un signo obligatorio seguido de uno o más dígitos, usando los puntos suspensivos como abreviatura explicativa. En una herramienta real hay que escribir la sintaxis que soporte.

En los ejercicios, justificar pertenencia indicando valores de **todos** los índices y comprobando sus restricciones. Que ε pertenezca al universo Σ* no implica que pertenezca a cualquier lenguaje L.

Una gramática G = (N, Σ, P, S) tiene no terminales, terminales, producciones y símbolo inicial. BNF es una notación para producciones, no una familia distinta de lenguajes. Las respuestas V/F aisladas necesitan el enunciado de sus capturas.
