---
tipo: clase
fecha: 2026-10-09
tema: "Gramáticas, CYK y autómatas de pila"
fecha_original: 2026-10-02
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Práctica - Unidad 3A

*Gramáticas independientes de contexto*
![[Pasted image 20261009191914.png]]

Leer las reglas recursivas
![[Pasted image 20261009191936.png]]

![[Pasted image 20261009192104.png]]
Reglas del ejemplo: S → aSd | A; A → bAc | ε. Los exponentes describen derivaciones repetidas, no una sola producción.
an . bm . cm . dn  / n, m >= 0
Respuesta A
![[Pasted image 20261009192826.png]]
![[Pasted image 20261009192936.png]]

![[Pasted image 20261009193240.png]]
S ->
	aSb
	aaSbb
	a(i)Sb(i)
	a(i)Ab(i)
	a(i)c(j)Ab(i)
	a(i)c(j)Ad(k)b(i)
	a(i)c(j)d(k)b(i)
![[Pasted image 20261009193734.png]]

![[Pasted image 20261009194508.png]]

![[Pasted image 20261009194812.png]]
![[Pasted image 20261009195215.png]]
L1
S -> AD | B
A -> aaAc | B
B -> bbB | lambda
D -> dD | lambda
![[Pasted image 20261009195758.png]]
![[Pasted image 20261009195830.png]]
![[Pasted image 20261009200248.png]]

![[Pasted image 20261009194740.png]]![[Pasted image 20261009200525.png]]

---

# Algoritmo CYK

![[Pasted image 20261009200825.png]]
![[Pasted image 20261009201137.png]]
![[Pasted image 20261009201337.png]]
![[Pasted image 20261009201533.png]]![[Pasted image 20261009201622.png]]
![[Pasted image 20261009201910.png]]
![[Pasted image 20261009202020.png]]
En la última celda tiene que quedar el símbolo distinguido.

---

# Unidad 3 - Parte B: Autómatas de Pila

Cuales pueden representarse como una regex?
![[Pasted image 20261009202903.png]]
1. Si
2. Si
3. Si
4. Si
5. Si
6. No
7. No
![[Pasted image 20261009203409.png]]

## Formas de aceptación

![[Pasted image 20261009203953.png]]
![[Pasted image 20261009204032.png]]
![[Pasted image 20261009204125.png]]![[Pasted image 20261009204142.png]]
![[Pasted image 20261009204237.png]]![[Pasted image 20261009204811.png]]
Hay Autómatas de Pila Determinísticos y No Determinísticos
![[Pasted image 20261009205216.png]]

![[Pasted image 20261009205618.png]]
![[Pasted image 20261009205830.png]]
A, A, M, D, D, M
![[Pasted image 20261009210518.png]]
a^n c b^n , con n >= 1
![[Pasted image 20261009210931.png]]
![[Pasted image 20261009211232.png]]

![[Pasted image 20261009212243.png]]
![[Pasted image 20261009213323.png]]![[Pasted image 20261009214156.png]]

![[Pasted image 20261009214736.png]]

![[Pasted image 20261009215006.png]]
![[Pasted image 20261009220013.png]]

---

## Complemento de estudio

### Ejemplo de anidamiento y CYK

Para S → aSd | A y A → bAc | ε, la gramática genera **{aⁿbᵐcᵐdⁿ : n,m ≥ 0}**. Cada aplicación de la primera regla liga una a con una d; la segunda liga una b con una c. Los índices n y m son independientes.

CYK, en su forma estándar, requiere una gramática en forma normal de Chomsky. Cada celda contiene los no terminales que generan una subcadena; se consideran todas sus particiones en dos subcadenas no vacías. Una palabra no vacía se acepta si S aparece en la celda de la palabra completa. ε se trata aparte.

Un AP no determinista puede aceptar por estado final o por pila vacía; ambas convenciones son equivalentes en capacidad con las transformaciones adecuadas. En ambos casos debe consumirse toda la entrada. No trasladar esa equivalencia sin matices a los AP deterministas.

Para aⁿcbⁿ, n ≥ 1, apilar por cada a, cambiar de fase con c y desapilar por cada b.
