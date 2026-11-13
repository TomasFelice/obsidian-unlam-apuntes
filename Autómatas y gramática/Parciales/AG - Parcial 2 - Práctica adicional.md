---
tipo: examen
tema: Práctica adicional para el Parcial 2
---

# AG · Parcial 2 · Práctica adicional

Basado en [[AG - Repaso Parcial 2]]. Resolvé las consignas y después desplegá el solucionario al final. Usá `λ` para la cadena vacía y `□` para el blanco de una cinta.

## 1. Clasificar lenguajes

Para cada lenguaje, indicá cuál es el modelo más simple que lo reconoce entre autómata finito, autómata de pila y máquina de Turing. Justificá tu elección. Los índices `n` y `m` son enteros positivos e independientes entre sí cuando aparecen juntos.

a. `L = { a^(2n) b^m | n, m ≥ 1 }`  -> AF
b. `L = { a^n b^(3n) | n ≥ 1 }`  -> AP
c. `L = { a^n b^m c^(2m) d^n | n, m ≥ 1 }`  -> AP
d. `L = { a^n b^n c^n | n ≥ 1 }` -> MT

## 2. Interpretar una gramática

```text
S → AB
A → aaAb | λ
B → cBdd | cdd
```

1. Escribí la 4-upla `G = (N, T, P, S)`. Contá y numerá las producciones en el orden dado, tomando cada alternativa como una producción.
G=({A, B}, {a, b, c, d}, {1:S->AB, 2:A->aaAb, 3:A->λ, 4:B->cBdd, 5:B->cdd }, S)
2. Encontrá la cadena mínima y describí el lenguaje con índices. Indicá si es regular.
cdd.
a^2n . b^n . c^m . d^2m ; con n>=0 y m >= 1
El lenguaje no es regular. Tiene indices dependientees entre si.
3. Determiná si `aaaabbccdddd`, `aabcdd`, `abcdd` y `ccdddd` pertenecen al lenguaje. Para las que pertenezcan, escribí el orden de las producciones en una derivación más a la izquierda.
- `aaaabbccdddd` -> SI. 1, 2, 2, 3, 4, 5
- `aabcdd` -> SI. 1, 2, 3, 5
- `abcdd` -> NO
- `ccdddd` -> SI. 1, 3, 4, 5

## 3. Formas normales

Clasificá cada producción según la forma de su lado derecho. Indicá si cumple Chomsky (FNC), Greibach (FNG), ambas o ninguna.

a. `A → BC`  -> FNC
b. `B → bAC`  -> FNG
c. `C → c`  -> Ambas
d. `D → aBb`  -> Ninguna
e. `E → BCD` -> Ninguna

## 4. Analizar y normalizar una gramática

```text
S → aaSb | AB
A → a
B → b
```

1. Escribí la 4-upla, el lenguaje y su cadena mínima.
G = ({A, B}, {a, b}, {1:S->aaSb, 2:S->AB, 3:A->a, 4:B->b})
L = a^2n . ab . b^n  con n >= 0
Cadena minima = ab
2. Contá qué producciones cumplen la FNC y cuáles cumplen la FNG. Justificá por qué las restantes quedan fuera de cada forma.
1 -> Ninguna. No cumple las condiciones de nignuna forma. (FNC->1 t o 2 nt;FNG->1 t + 0..n nt)
2 -> FNC
3 -> FNC, FNG
4 -> FNC, FNG
3. Reescribí la gramática en FNC y explicá por qué genera el mismo lenguaje.
```
1: S -> XY
2: S -> AB
3: X -> AA
4: Y -> SB
5: A -> a
6: B -> b
```
4. Derivá `aaabb` más a la izquierda en ambas gramáticas y justificá por qué `aabb` queda fuera de las dos.
aaabb
Gramatica original:
1 -> 2 -> 3 -> 4
Gramatica nueva:
1 → 3 → 5 → 5 → 4 → 2 → 5 → 6 → 6
## 5. Leer transiciones de un autómata de pila

Usá la notación `entrada, tope → reemplazo`, con el tope a la izquierda. Para cada transición, indicá qué se consume, qué queda en el tope y si se apila, se desapila o se mantiene la pila.

a. `a, Z → XZ` - Consume a, la pila estaba vacía, y se apila X
b. `λ, X → λ`  - No consume nada (λ), había X en la pila, y la desapila
c. `b, X → X` - Consume b, había X en la pila y la mantiene

## 6. Interpretar un autómata de pila

El estado inicial es `q0`, la pila empieza con `Z` y el único estado final es `qf`. Para aceptar se debe consumir toda la entrada. Cada fila representa una transición con la notación del ejercicio anterior. Las transiciones que no aparecen en la tabla no están definidas.

| Origen | Entrada, tope → reemplazo | Destino |
| ------ | ------------------------- | ------- |
| q0     | a, Z → AZ                 | q1      |
| q1     | a, A → AA                 | q1      |
| q1     | b, A → BBA                | q2      |
| q2     | b, B → BBB                | q2      |
| q2     | c, B → λ                  | q3      |
| q3     | c, B → λ                  | q3      |
| q3     | d, A → λ                  | q4      |
| q4     | d, A → λ                  | q4      |
| q4     | λ, Z → Z                  | qf      |

1. Expresá el lenguaje con índices e indicá sus valores mínimos.
a^n . b^m . c^2m . d^n , con n, m >= 1
2. Para `aabccccdd`, indicá en qué punto se bloquea el autómata o cómo llega al estado final.
Para esa cadena, el automata se bloquea en el q3, cuando todavía tiene que consumir `ccdd`, pero ya no tiene más B en la pila, por lo tanto no puede seguir consumiendo c.
## 7. Construir un autómata de pila

Diseñá un autómata de pila para `L = { a^(2n) b^n c^m | n ≥ 1, m ≥ 0 }`. Indicá el estado inicial, el fondo de pila, el criterio de aceptación y las transiciones. Armá un conjunto de pruebas para JFLAP que incluya la cadena mínima, un caso con varias `c`, una cantidad impar de `a` y una cadena con el orden de bloques alterado.
![[AG - Parcial 2 - Ejercicio 7 - AP corregido.png]]
- aab
- aabccccc
- aaabc
- cbaa
- caab
- abbc
## 8. Aplicar CYK

Aplicá CYK a `aaba` y `abab` con la siguiente gramática en FNC. Completá todas las celdas por longitud de subcadena e indicá si aparece `S` en la celda de la cadena completa.

```text
S → AB | BC
A → BA | a
B → CC | b
C → AB | a
```

aaba

| {A, C}          |        |        |        |
| --------------- | ------ | ------ | ------ |
| {B}             | {A, C} |        |        |
| {A, C, S}       | {C, S} | {B}    |        |
| ==🟢{A, B, S}== | {B}    | {A, S} | {A, C} |
Aparece S en la ultima celda, por lo tanto, se acepta la cadena.

abab

| {A, C} |        |        |     |
| ------ | ------ | ------ | --- |
| {C, S} | {B}    |        |     |
| {B}    | {A, S} | {A, C} |     |
| {B}    | {C, S} | {C, S} | {B} |
No aparece S en la ultimma celda, por lo tanto, no se acepta la cadena.
## 9. Construir una gramática para el lenguaje de un AP

Construí una gramática independiente de contexto que genere el mismo lenguaje que el autómata del ejercicio 6. Mostrá una derivación más a la izquierda de `aabbccccdd` y elegí dos cadenas para probar en JFLAP que deban rechazarse por motivos diferentes.

Gramatica:
```
S -> aSd | aAd
A -> bAcc | bcc
```

Derivacion:
S -> aSd -> aaAdd -> aabAccdd -> aabbccccdd

Deberian rechazarse:
- ad
- adbc
## 10. Notación de máquinas de Turing

Dibujá las dos transiciones. En cada cinta escribí una terna `(leído, escrito, movimiento)`. Usá `D` para derecha, `I` para izquierda y `Q` para quedarse en el lugar.

1. En `q0`, la cinta principal lee una `b`, la conserva y avanza a la derecha. En la auxiliar, la máquina escribe una `X` sobre el blanco y también avanza a la derecha. El estado sigue siendo `q0`.
2. Desde `q1` hasta `q2`, la cinta principal lee una `b`, la reemplaza por una `B` y retrocede. La auxiliar 1 lee una `X`, la borra y queda en su lugar. La auxiliar 2 lee un blanco, escribe `1` y avanza.

Use la notacion vista en clase. `leido; escrito, movimiento`, con R (derecha), L (izquierda), S (quedarse). "\[\]" lo use para representar el blanco.
![[Pasted image 20261113113528.png]]
## 11. Interpretar una máquina de Turing

La entrada contiene únicamente símbolos de `{0, 1}`. El cabezal empieza sobre el primer símbolo o sobre un blanco si la entrada es vacía. La máquina inicia en `q0` y se detiene al llegar a `qf`. Cada celda indica `(estado siguiente, símbolo escrito, movimiento)`.

| Estado | Lee 0 | Lee 1 | Lee □ |
| --- | --- | --- | --- |
| q0 | (q0, 0, D) | (q1, 1, D) | (qf, 0, Q) |
| q1 | (q1, 0, D) | (q0, 1, D) | (qf, 1, Q) |

1. Describí qué hace la máquina. Explicá qué representa cada uno de los estados `q0` y `q1` durante el recorrido.
La maquina cambia de estado entre q0 y q1 cada vez que lee un 1, y cuando lee un blanco, lo reemplaza por un 0/1 dependiendo de si termino en q0 o q1.
Lo que hace en terminos "funcionales", es contar la cantidad de 1s que hay en una cadena, colocando un 0 al final si la cantidad es par, y un 1 si es impar.
2. Indicá qué queda escrito para las entradas `1011`, `1100` y `λ`.
```
1011 -> 10111
1100 -> 11000
λ -> 0
``` 

## 12. Decodificar una máquina de Turing

Decodificá `5AE975A56EE` y explicá qué transformación realiza sobre una entrada de `{0, 1}*`. Conservá los cuatro bits de cada dígito hexadecimal. Un `0` al inicio y otro al final enmarcan la secuencia. Entre transiciones se usa `00` y entre campos se usa `0`.

Cada transición tiene cinco campos en unario en el orden `estado actual, símbolo leído, estado siguiente, símbolo escrito, movimiento`.

| Campo      | 1            | 11         | 111 |
| ---------- | ------------ | ---------- | --- |
| Estado     | q1 (inicial) | q2 (final) |     |
| Símbolo    | □            | 0          | 1   |
| Movimiento | D            | I          | Q   |

Dibujá las transiciones y probá a mano qué queda escrito para `010` y `λ`.
> a-10, b-11, c-12, d-13, e-14, f-15
> 8421

0*1*0*11*0*1*0*111*0*1*==🟡00==*1*0*111*0*1*0*11*0*1*==🟡00==*1*0*1*0*11*0*111*0*111*0

- 1 11 = 1 111 1 -> q1, 0 = q1, 1, R
- 1 111 = 1 11 1 -> q1, 1 = q1, 0, R
- 1 1 = 11 111 111 -> q1, \[\], = q2, 1, S
![[Pasted image 20261113120205.png]]

```
010 -> 1011
λ -> 1
```
## 13. Computabilidad y decidibilidad

Elegí una opción por pregunta y justificá.

1. Una MT que reconoce `L` entra en un bucle al procesar cierta cadena `w`. ¿Qué se puede concluir?
   - A. `w ∈ L`.
   - =B. `w ∉ L` y `L` es indecidible.=
   - ==C. `w ∉ L`. El comportamiento de esa máquina no alcanza para clasificar la decidibilidad de `L`.==
2. El único algoritmo conocido para un problema de decisión siempre termina y exige un tiempo exponencial en el peor caso. ¿Qué se puede afirmar?
   - ==A. El problema es decidible.==
   - B. Se probó que todo algoritmo para ese problema requiere tiempo exponencial.
   - C. El problema es indecidible en entradas grandes.

Indicá si cada afirmación es verdadera o falsa y justificá.

a. Todo lenguaje decidible tiene un complemento decidible.  V. Si tengo un algoritmo que puede decidir si una cadena pertenece al lenguaje, su complemento tambien lo sera.
b. Si `L` y su complemento son reconocibles, entonces `L` es decidible.  ~~F. Que un lenguaje sea reconocible, no implica que sea decidible. Su complemento no aporta informacion relevante.~~ V. Si L y su complemento son reconocibles, puedo pasar por ambas maquinas una cadena, y si acepta el reconocedor de L, digo SI, si acepta el reconocedor de L complemento, digo NO, ya que la cadena va a pertenecer EXACTAMENTE a 1 conjunto.
c. La tesis de Church-Turing garantiza que todo conjunto de cadenas posee una máquina de Turing que lo reconoce.  F. ~~La tesis garantiza que todo lenguaje decidible es reconocible.~~ La tesis de Church-Turing afirma que todo procedimiento efectivo puede ser realizado por una MT. Que todo lenguaje decidible sea reconocible se sigue de las definiciones. Hay lenguajes sin reconocedor porque hay una cantidad numerable de MT y una cantidad no numerable de lenguajes binarios.
d. Una computadora más rápida vuelve decidible el problema de la parada. F. Si un problema no es decidible, no importa el poder de computo que exista, que no va a ser decidible.

## Solucionario

> [!check]- 1 a 4 · Lenguajes y gramáticas
> **1.** a) Finito. La expresión regular es `(aa)(aa)*bb*`. b) De pila. Por cada `a` se apilan tres marcas y se desapila una por cada `b`. Al aplicar el lema de bombeo para lenguajes regulares a `a^p b^(3p)`, el fragmento bombeado dentro de las primeras `p` posiciones contiene solo `a`. Bombearlo modifica la cantidad de `a` y conserva la de `b`, por lo que el lenguaje no es regular. c) De pila. Se apila una marca por cada `a` y dos de otro tipo por cada `b`. Se retiran las segundas con las `c` y las primeras con las `d`. Si fuera regular, el homomorfismo que borra `a` y `d` produciría un lenguaje regular, pero `{ b^m c^(2m) | m ≥ 1 }` contradice el lema de bombeo por el mismo argumento que en b). d) Máquina de Turing. Puede marcar una `a`, una `b` y una `c` por ronda tras comprobar el orden de los bloques. Para descartar un AP, en el lema de bombeo para lenguajes libres de contexto el tramo bombeable de `a^p b^p c^p` tiene longitud a lo sumo `p` y abarca como máximo dos bloques. Al eliminar los fragmentos bombeables, baja al menos un conteo y queda otro igual a `p`.
>
> **2.** `N = {S, A, B}`, `T = {a, b, c, d}`, símbolo distinguido `S`. Las cinco producciones de `P` son `1. S → AB`, `2. A → aaAb`, `3. A → λ`, `4. B → cBdd`, `5. B → cdd`. El lenguaje es `{ a^(2n) b^n c^m d^(2m) | n ≥ 0, m ≥ 1 }`. Su cadena mínima es `cdd`. No es regular. Si lo fuera, borrar `a` y `b` por homomorfismo daría el lenguaje regular `{ c^m d^(2m) | m ≥ 1 }`, cuya no regularidad se prueba como en 1b.
>
> - `aaaabbccdddd` pertenece. Orden `1, 2, 2, 3, 4, 5`.
> - `aabcdd` pertenece. Orden `1, 2, 3, 5`.
> - `abcdd` queda fuera porque una `b` exige dos `a`.
> - `ccdddd` pertenece. Orden `1, 3, 4, 5`.
>
> **3.** a) FNC. b) FNG. c) Ambas. d) Ninguna, porque mezcla terminales con no terminales y tiene un terminal después del primero. e) Ninguna, porque contiene tres no terminales y empieza con uno de ellos.
>
> **4.** `N = {S, A, B}`, `T = {a, b}`, `P = {S → aaSb, S → AB, A → a, B → b}`, símbolo distinguido `S`. El caso base aporta `ab` y cada recursión agrega dos `a` y una `b`. Así, `L = { a^(2n+1) b^(n+1) | n ≥ 0 }` y la cadena mínima es `ab`. Cumplen FNC tres producciones (`S → AB`, `A → a` y `B → b`). Cumplen FNG dos (`A → a` y `B → b`). `S → aaSb` mezcla terminales y no terminales, con terminales después del primero. `S → AB` comienza con un no terminal.
>
> ```text
> S → AX | AB
> X → AY
> Y → SB
> A → a
> B → b
> ```
>
> La rama `S → AX` expande los auxiliares a `AASB`, que agrega los mismos símbolos que `aaSb`. La rama `S → AB` aporta el mismo caso base.
>
> - Original · `S → aaSb → aaABb → aaaBb → aaabb`.
> - FNC · `S → AX → aX → aAY → aaY → aaSB → aaABB → aaaBB → aaabB → aaabb`.
> - `aabb` queda fuera. Dos `b` requieren una recursión, que da tres `a`.

> [!check]- 5 a 7 · Autómatas de pila
> **5.** a) Consume `a` y apila `X` sobre `Z`. b) No consume entrada y desapila `X`. El símbolo que estaba debajo pasa al tope, si lo había. c) Consume `b` y conserva `X` en el tope.
>
> **6.** Reconoce `{ a^n b^m c^(2m) d^n | n, m ≥ 1 }`. Hay una marca `A` por cada `a` y dos marcas `B` por cada `b`. Cada `c` retira una `B` y cada `d` retira una `A`. Con `aabccccdd`, tras `aabcc` se está en `q3` con `AAZ` en la pila. La tercera `c` bloquea al AP porque el tope es `A`.
>
> **7.** Una construcción posible usa `q0` como inicial, `Z` como fondo y `qf` como único estado final. Acepta por estado final con toda la entrada consumida.
>
> | Origen | Entrada, tope → reemplazo | Destino |
> | --- | --- | --- |
> | q0 | a, Z → Z | q1 |
> | q1 | a, Z → AZ | q2 |
> | q1 | a, A → AA | q2 |
> | q2 | a, A → A | q1 |
> | q2 | b, A → λ | q3 |
> | q3 | b, A → λ | q3 |
> | q3 | λ, Z → Z | qf |
> | qf | c, Z → Z | qf |
>
> Cada vuelta a `q2` completa un par de `a` y suma una marca. El bloque de `b` puede empezar en `q2` y el de `c` puede empezar cuando `q3` ya retiró todas las marcas.
>
> | Aceptar | Rechazar |
> | --- | --- |
> | `aab`, `aabccc`, `aaaabbc` | `λ`, `aaab`, `aaaab`, `aabb`, `aacb` |

> [!check]- 8 y 9 · CYK y construcción de gramática
> **8.** Cada columna numerada corresponde a la posición inicial de la subcadena. Las posiciones sin espacio para una subcadena de esa longitud se marcan con un guion.
>
> | Entrada | Longitud | 1 | 2 | 3 | 4 |
> | --- | --- | --- | --- | --- | --- |
> | `aaba` | 1 | {A, C} | {A, C} | {B} | {A, C} |
> | | 2 | {B} | {C, S} | {A, S} | — |
> | | 3 | {B} | {B} | — | — |
> | | 4 | {A, C, S} | — | — | — |
> | `abab` | 1 | {A, C} | {B} | {A, C} | {B} |
> | | 2 | {C, S} | {A, S} | {C, S} | — |
> | | 3 | {B} | {C, S} | — | — |
> | | 4 | {B} | — | — | — |
>
> Se acepta `aaba`. En la partición `aa · ba`, el par `BA` aporta `A`. En `a · aba`, el par `AB` aporta `C` y `S`. En `aab · a` se obtienen `A` y `S` por `BA` y `BC`. Para `abab`, la única producción aplicable en la celda completa es `B → CC` con la partición `ab · ab`. Se rechaza porque `S` no aparece.
>
> **9.** Con símbolo distinguido `S`, una gramática posible es
>
> ```text
> S → aSd | aMd
> M → bMcc | bcc
> ```
>
> Derivación más a la izquierda de `aabbccccdd` · `S → aSd → aaMdd → aabMccdd → aabbccccdd`.
>
> `abbcccd` se rechaza porque dos `b` requieren cuatro `c`. `aabccd` se rechaza porque dos `a` requieren dos `d`.

> [!check]- 10 a 13 · Máquinas de Turing y decidibilidad
> **10.** Etiquetas de las flechas, con las cintas en el orden dado.
>
> - `q0 → q0` · `(b, b, D) / (□, X, D)`
> - `q1 → q2` · `(b, B, I) / (X, □, Q) / (□, 1, D)`
>
> **11.** `q0` indica que la cantidad de unos leídos es par. `q1` indica que es impar. La máquina conserva los bits de entrada y agrega un bit de paridad que deja una cantidad par de unos en la salida. `1011` queda como `10111`, `1100` como `11000` y `λ` como `0`.
>
> **12.** En binario se obtiene `0101 1010 1110 1001 0111 0101 1010 0101 0110 1110 1110`. Al separar y contar los unos de cada campo se obtiene lo siguiente.
>
> | Campos | Transición |
> | --- | --- |
> | (1, 2, 1, 3, 1) | δ(q1, 0) = (q1, 1, D) |
> | (1, 3, 1, 2, 1) | δ(q1, 1) = (q1, 0, D) |
> | (1, 1, 2, 3, 3) | δ(q1, □) = (q2, 1, Q) |
>
> Las primeras dos transiciones son bucles en `q1` que invierten cada bit y avanzan. La tercera va a `q2` al escribir un `1` en el primer blanco. Para `010` queda `1011` y para `λ` queda `1`.
>
> **13.** 1) **C**. Si `w` perteneciera, todo reconocedor de `L` debería aceptarla. El mismo lenguaje podría tener algún otro reconocedor que se detenga para todas las entradas. 2) **A**. Contar con un algoritmo que siempre termina y responde correctamente alcanza para probar decidibilidad. Su tiempo de ejecución no establece una cota inferior para otros algoritmos.
>
> - a) **Verdadero**. Intercambiá la aceptación y el rechazo del decisor de `L`.
> - b) **Verdadero**. Simulá ambas máquinas de forma intercalada, un paso de cada una por turno. Una de ellas terminará aceptando, porque la entrada pertenece exactamente a uno de los dos lenguajes.
> - c) **Falso**. La tesis se refiere a procedimientos efectivos. Hay una cantidad numerable de máquinas de Turing y una cantidad no numerable de lenguajes sobre un alfabeto binario.
> - d) **Falso**. La velocidad cambia cuánto tardan las simulaciones que terminan. El problema de la parada sigue sin admitir un decisor general.
