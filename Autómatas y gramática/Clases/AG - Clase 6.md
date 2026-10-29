---
tipo: clase
fecha: 2026-10-02
tema: Unidad 3
---
# Practica - Unidad 3A
*Gramaticas independientes de contexto*
![[Pasted image 20261009191914.png]]

Leer las reglas recursivas
![[Pasted image 20261009191936.png]]

![[Pasted image 20261009192104.png]]
S -> a elevado n . A . d elevado n
A -> b elevado n . A . c elevado n
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
En la ultima celda tiene que quedar el simbolo distinguido.

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

## Formas de aceptacion
![[Pasted image 20261009203953.png]]
![[Pasted image 20261009204032.png]]
![[Pasted image 20261009204125.png]]![[Pasted image 20261009204142.png]]
![[Pasted image 20261009204237.png]]![[Pasted image 20261009204811.png]]
Hay Automatas de Pila Deterministicos y No Deterministicos
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
