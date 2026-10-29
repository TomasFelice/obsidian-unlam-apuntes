---
tipo: clase
fecha: 2026-10-02
tema: "Gramáticas independientes del contexto y ambigüedad"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Unidad 3 - Parte A: Lenguajes Tipo 2

> Gramáticas Independientes de Contexto

![[Pasted image 20261002192450.png]]
![[Pasted image 20261002193353.png]]
![[Pasted image 20261002193826.png]]
![[Pasted image 20261002195034.png]]
![[Pasted image 20261002195204.png]]
a. F
b. V
c. F
d. V
e. F

![[Pasted image 20261002200132.png]]
a. F
b. F
c. F
d. V
e. V

![[Pasted image 20261002200945.png]]

1,3,3,4,6
![[Pasted image 20261002201521.png]]
![[Pasted image 20261002201518.png]]
![[Pasted image 20261002202003.png]]![[Pasted image 20261002202324.png]]
![[Pasted image 20261002202406.png]]
![[Pasted image 20261002202724.png]]
![[Pasted image 20261002203913.png]]
![[Pasted image 20261002204325.png]]![[Pasted image 20261002205656.png]]
![[Pasted image 20261002210359.png]]![[Pasted image 20261002210403.png]]
![[Pasted image 20261002210809.png]]
![[Pasted image 20261002211012.png]]
![[Pasted image 20261002211150.png]]

## Interpretar Gramáticas

![[Pasted image 20261002212521.png]]
![[Pasted image 20261002212620.png]]

A: a^n
B: (bb)^2m a^m
C: (bba)^m

**Borrador por verificar:** la anotación original fue «a^n | (bb)^2m a^m | (bba)^m, con n >= 0, m >= 0, k >= 1». No tomarla como solución hasta contrastar producciones, unión o concatenación y cotas.

![[Pasted image 20261002213623.png]]

![[Pasted image 20261002214134.png]]
![[Pasted image 20261002214226.png]]![[Pasted image 20261002214358.png]]
![[Pasted image 20261002215158.png]]![[Pasted image 20261002215650.png]]
![[Pasted image 20261002215808.png]]

---

## Complemento de estudio

### Derivación, lenguaje y ambigüedad

En una GIC, cada producción tiene un solo no terminal a la izquierda. El lenguaje contiene las cadenas de terminales derivables desde S. Distinguir una forma sentencial que todavía contiene no terminales de una palabra terminada.

Una gramática es ambigua si alguna palabra tiene dos árboles de derivación distintos; elegir diferente orden de expansión de nodos independientes puede dar el mismo árbol y no prueba ambigüedad. Comparar dos derivaciones izquierdas distintas es una forma de demostrarla.

Al interpretar reglas, usar índices independientes para recursiones independientes y el mismo índice cuando una regla agrega símbolos ligados. Ejemplo: S → aSb | ε genera {aⁿbⁿ : n ≥ 0}.

**Pendiente de validación:** la fórmula final anotada para A, B y C mezcla índices y una unión. Antes de usarla como respuesta, reconstruir cada bloque desde sus producciones y comprobar si S los concatena o los ofrece como alternativas.
