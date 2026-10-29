---
tipo: clase
fecha: 2026-09-04
tema: "Expresiones regulares y autómatas finitos"
fecha_original: 2026-04-20
fecha_fuente: nombre de capturas
fecha_inferida: true
---

## Repaso ejercicios práctica 1

![[Pasted image 20260904191741.png]]
![[Pasted image 20260904192416.png]]

---

# Retomamos unidad 2

![[Pasted image 20260904192505.png]]
![[Pasted image 20260904193239.png]]
![[Pasted image 20260904193312.png]]
`ER = a.(a|b)*.c.c*`
![[Pasted image 20260904193534.png]]
Ejemplos de cadenas
![[Pasted image 20260904193840.png]]

![[Pasted image 20260904193904.png]]
Es correcta la regex?
![[Pasted image 20260904193949.png]]
NO.
![[Pasted image 20260904194146.png]]

La ER correcta es
![[Pasted image 20260904194211.png]]
![[Pasted image 20260904194314.png]]

![[Pasted image 20260904194337.png]]
![[Pasted image 20260904194518.png]]
![[Pasted image 20260904194525.png]]
![[Pasted image 20260904194548.png]]

![[Pasted image 20260904194658.png]]
![[Pasted image 20260904194747.png]]
![[Pasted image 20260904194758.png]]

![[Pasted image 20260904194838.png]]
![[Pasted image 20260904194932.png]]
![[Pasted image 20260904194959.png]]

union de los dos casos
![[Pasted image 20260904195114.png]]

![[Pasted image 20260904195448.png]]![[Pasted image 20260904195530.png]]
![[Pasted image 20260904195536.png]]

![[Pasted image 20260904195654.png]]
![[Pasted image 20260904195756.png]]
![[Pasted image 20260904195815.png]]

![[Pasted image 20260904195845.png]]
![[Pasted image 20260904195920.png]]
![[Pasted image 20260904195956.png]]
![[Pasted image 20260904200137.png]]

![[Pasted image 20260904200440.png]]
![[Pasted image 20260904200534.png]]
![[Pasted image 20260904200624.png]]

![[Pasted image 20260904200647.png]]
![[Pasted image 20260904200739.png]]

---

# Unidad 2 - Parte B: Autómatas Finitos

![[Pasted image 20260904201650.png]]
![[Pasted image 20260904201806.png]]
![[Pasted image 20260904201902.png]]
![[Pasted image 20260904202129.png]]
![[Pasted image 20260904202318.png]]

> Descargar JFLAP v7 (ver demo 1:20:43)

![[Pasted image 20260904203025.png]]


![[Pasted image 20260904203238.png]]
![[Pasted image 20260904203829.png]]
![[Pasted image 20260904203904.png]]
![[Pasted image 20260904204027.png]]
![[Pasted image 20260904205448.png]]
![[Pasted image 20260904210515.png]]
![[Pasted image 20260904210908.png]]
![[Pasted image 20260904211500.png]]
![[Pasted image 20260904212028.png]]
![[Pasted image 20260904212151.png]]
![[Pasted image 20260904212546.png]]

![[Pasted image 20260904212702.png]]
![[Pasted image 20260904212938.png]]

---

## Complemento de estudio

### AFD, AFND y equivalencia

Un AFD tiene una transición por estado y símbolo bajo la convención de función total. Un AFND puede tener varias posibilidades y, según el modelo, transiciones ε. Ambos reconocen exactamente los lenguajes regulares.

Para comprobar una expresión regular, probar la cadena mínima, el caso de cero repeticiones, los límites de cada bloque y cadenas que violen una sola condición. Un contraejemplo basta para refutarla; algunos ejemplos favorables no demuestran equivalencia.

La expresión a(a|b)*cc* exige una a inicial, luego una secuencia de a o b y al menos una c final. No se puede declarar correcta o incorrecta sin compararla con el lenguaje objetivo. La anotación «NO» del ejercicio se refiere a su consigna, no a que la expresión sea inválida.
