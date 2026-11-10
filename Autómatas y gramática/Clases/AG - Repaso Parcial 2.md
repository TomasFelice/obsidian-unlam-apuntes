---
tipo: examen
fecha: 2026-11-06
tema: Repaso Temas Parcial 2
fecha_original:
fecha_fuente: nombre de capturas
fecha_inferida: true
---
# Autoguía Parcial 2
### Autómatas
**Anotá tus respuestas y comparalas con la resolución.**

Para cada lenguaje, indicá qué tipo de autómata lo reconoce:

- a) `a^n b^m`, con `n, m > 0` → ==🟢Autómata finito==. Los índices son independientes.
- b) `a^n b^n`, con `n > 0` → ==🟢Autómata de pila==. Se apila una `A` por cada `a` y se desapila una `A` por cada `b`.
- c) `a^n b^m c^m d^n`, con `n, m > 0` → ==🟢Autómata de pila==. Se apila una `A` por cada `a` y una `B` por cada `b`. Luego se desapila una `B` por cada `c` y una `A` por cada `d`.
- d) `a^n b^m`, con `n, m > 0` y `n = 2m` → ==🔴~~Autómata finito~~== **Autómata de pila**. Se apila una marca por cada `a` y se desapilan dos por cada `b`.
- e) `a^n b^m c^n d^m`, con `n, m > 0` → ==🔴~~Autómata de pila~~== **Máquina de Turing**. Las correspondencias se cruzan. Al leer las `c`, las marcas de las `b` quedarían encima de las de las `a` en una sola pila.

### Interpretar una Gramática
Dada la siguiente gramática independiente de contexto, con símbolo distinguido **S**:
```
S → AB
A → aAbb | λ
B → cBd | cd
```
Responder en papel, sin avanzar:
1. Escribir la 4-upla de la gramática e indicar **cuántas producciones** tiene.
   `G = (N, T, P, S) = ({S, A, B}, {a, b, c, d}, {S → AB, A → aAbb, A → λ, B → cBd, B → cd}, S)`. Tiene **5 producciones**.
2. ¿Cuál es la **cadena mínima** que genera?
   La cadena mínima es `cd`.
3. ¿Qué **lenguaje** genera? Expresarlo con la notación que corresponda (regex si es regular; si no, con índices, indicando desde qué valor arranca cada uno).
   El lenguaje es `{a^n b^(2n) c^m d^m | n ≥ 0, m ≥ 1}). No es regular.
4. Para cada una de las siguientes cadenas indicar si **pertenece** al lenguaje. Si pertenece, listar **qué reglas se aplicaron y en qué orden** (numerar las producciones en el orden en que están escritas y usar derivación más a la izquierda):
    - `aabbbbccdd` → Sí. Producciones `1 → 2 → 2 → 3 → 4 → 5`.
    - `abcd` → No.
    - `ccdd` → Sí. Producciones `1 → 3 → 4 → 5`.

**Una vez resuelto en papel, avanzar para comparar con la resolución.**

### Formas Normales - Lenguajes Tipo 2
**Ejercicio 1:**
¿A qué forma normal corresponde la producción `A → aN`?

- _A_ es un símbolo no terminal.
- a es un símbolo terminal (la regla siempre comienza con un terminal).
- **N** es una secuencia (posiblemente vacía) de símbolos no terminales.

En la **forma normal de Chomsky**, el lado derecho contiene exactamente dos símbolos no terminales o un solo terminal.

En la **forma normal de Greibach**, el lado derecho empieza con un terminal, seguido de cero o más no terminales.

Por lo tanto, la producción está en **forma normal de Greibach**.

**Ejercicio 2:**
¿Cuáles de las siguientes producciones cumplen con la FNC?

- `S → ABC` → No.
- `S → aB` → No.
- `A → a` → Sí.
- `B → bC` → No.
- `C → c` → Sí.

**Avanzar una vez pensado para ver la respuesta.**

### Análisis y Normalización de Gramáticas
Dada la siguiente gramática (símbolo distinguido **S**):
```
S → aSbb | AB
A → a
B → b
```
Responder en papel, sin avanzar:
1. Escribir la 4-upla. ¿Qué lenguaje genera? ¿Cuál es su cadena mínima?
   - `G = (N, T, P, S) = ({S, A, B}, {a, b}, {S → aSbb, S → AB, A → a, B → b}, S)`.
   - `L = {a^n ab b^(2n) | n ≥ 0}`.
   - La cadena mínima es `ab`.
2. ¿Está en **Forma Normal de Chomsky (FNC)**? Indicar **cuántas producciones cumplen** y cuáles no, y por qué.
   No. Cumplen tres producciones: la 2 tiene dos no terminales en el lado derecho, y la 3 y la 4 tienen un solo terminal cada una. La producción 1 contiene tres terminales y un no terminal.
3. ¿Está en **Forma Normal de Greibach (FNG)**? Mismo análisis.
   No. Cumplen dos producciones, la 3 y la 4, porque el lado derecho de cada una contiene un solo terminal. La producción 1 tiene terminales después del inicial y la 2 comienza con un no terminal.
4. **Reescribirla en FNC.** La gramática nueva tiene que generar exactamente las mismas cadenas.
%%
_Paso 1 — reemplazar los terminales por no terminales._ `A` y `B` solo sirven para generar `a` y `b` (una única producción cada uno), por eso se pueden usar en el reemplazo: `S → ASBB`. Si tuvieran otras producciones habría que crear no terminales nuevos. Si crearon `C → a` y `D → b` nuevos, también es válido (una producción más cada uno).
_Paso 2 — agrupar de a dos._ `ASBB` tiene cuatro símbolos: me quedo con el primero y agrupo el resto en un no terminal nuevo, y repito hasta que todo quede de a dos:
%%
Paso 1
```
S->ASBB | AB
A->a
B->b
```
Paso 2
```
S->AX | AB
X->SY
Y->BB
A->a
B->b
```
5. Elegir una cadena que pertenezca al lenguaje (que no sea la mínima) y derivarla en la gramática original y en la normalizada. Elegir también una que no pertenezca y comprobar que no se deriva en ninguna de las dos.
   - **Gramática original** · `S → aSbb → aABbb → aaBbb → aabbb`.
   - **Gramática en FNC** · `S → AX → aX → aSY → aABY → aaBY → aabY → aabBB → aabbB → aabbb`.
   - La cadena `aabb` queda fuera de ambas gramáticas. Para generar dos `a`, se necesita `n = 1), lo que produce tres `b`.

**Una vez resuelto en papel, avanzar para comparar con la resolución.**

### Repaso Nomenclatura AP
Observá la figura e identificá en qué transición ocurre cada acción.

- **Apilar** (`e6 → e7`). Lee `a` y reemplaza `Z` por `AZ`, de modo que `A` queda encima del marcador de fondo.
- **Desapilar** (`e4 → e5`). Lee `b` y reemplaza el símbolo `T` del tope por `λ`, lo que lo elimina de la pila.
- **Mantener la pila** (`e1 → e2`). Lee `a` y deja el símbolo `A` en el tope.

![Imagen sobre Repaso Nomenclatura AP](https://miel.unlam.edu.ar/data7/data2/autoguia/3657/1590/6301/basicoPila.jpg) 

### Interpretar AP
Dado el siguiente autómata de pila, indicá qué lenguaje reconoce.
![Imagen sobre Interpretar AP](https://miel.unlam.edu.ar/data7/data2/autoguia/3657/1590/6304/AP_G8.jpg)
`a^n b^(3m) c^m d^n`

### Construir Autómata de Pila
1. Construí un autómata de pila que reconozca el lenguaje `{a^n b^(2n) c^m | n > 0, m ≥ 0}`.
2. Prepará un conjunto de cadenas de prueba para validar el autómata en JFLAP.
![[Pasted image 20261107154815.png]]

### Ejercicio CYK
Aplicá el algoritmo CYK a la gramática de la figura para determinar si `abba` pertenece al lenguaje. Después, compará tu tabla con la resolución.
![Imagen sobre Ejercicio CYK](https://miel.unlam.edu.ar/data7/data2/autoguia/3657/1590/6366/GramaticaCYK.jpg)
Para cada símbolo de `abba`, se anotan los no terminales que lo generan: `w(0,1) = {A, C}` para `a`, `w(1,2) = {B, D}` para `b`, `w(2,3) = {B, D}` para `b` y `w(3,4) = {A, C}` para `a`.

| {A, C} |        |        |        |
| ------ | ------ | ------ | ------ |
|        | {B, D} |        |        |
|        |        | {B, D} |        |
|        |        |        | {A, C} |

Para las subcadenas de longitud 2, se combinan los no terminales de las dos celdas correspondientes y se buscan las producciones que generan cada par.

- `w(0,2) = {A, D}`, por `A → AB` y `D → CD`.
- `w(1,3) = {C, S}`, por `C → BB` y `S → BD`.
- `w(2,4) = {B}`, por `B → DA`.

| {A, C} |        |        |        |
| ------ | ------ | ------ | ------ |
| {A, D} | {B, D} |        |        |
|        | {C, S} | {B, D} |        |
|        |        | {B}    | {A, C} |
![[Pasted image 20261107160122.png]]

Como `S` aparece en la celda correspondiente a la cadena completa, `abba` pertenece al lenguaje.

### Gramática para el AP
Construí una gramática para el lenguaje de la imagen.
![[Pasted image 20261107160349.png]]
Probá en JFLAP cadenas que pertenezcan al lenguaje y cadenas que queden fuera.

```
S → aSd | aAd
A → bbbAc | bbbc
```

### Notación de máquinas de Turing
Dibujá las transiciones solicitadas.

1. En el estado inicial, mientras la máquina lea una `a`, el cabezal de la cinta principal se mueve a la derecha. La máquina escribe un `1` en la celda en blanco de la cinta auxiliar y permanece en el mismo estado.
2. En un estado intermedio, la máquina lee una `b`, la conserva y mueve el cabezal de la cinta principal a la izquierda. En la cinta auxiliar 1, reemplaza el blanco por una `B` y deja el cabezal en su lugar. En la cinta auxiliar 2, lee una `x` y mueve el cabezal a la derecha.

**Compará tus transiciones con la solución.**
![[Pasted image 20261107161817.png]]

### Interpretar MT
Explicá qué hace la siguiente máquina de Turing.

![Imagen sobre Interpretar MT](https://miel.unlam.edu.ar/data7/data2/autoguia/3657/1590/6128/MT_Int.jpg)

La máquina calcula la XOR bit a bit de dos números de cuatro bits. La entrada usa el formato `L[1010;0111]=`, con los números entre corchetes y separados por un punto y coma.

- Si recibe un solo número, escribe `I`: `L[1010]= I`.
- Si los corchetes están vacíos, escribe `V`: `L[]= V`.

El video muestra el análisis paso a paso.

### Decodificar una MT
Decodificá la máquina de Turing representada por `5AD2EBA56EE` y explicá qué hace. El alfabeto de entrada es `{0, 1}`.

**Paso 1. Convertir a binario**

Cada dígito hexadecimal se convierte en un grupo de cuatro bits.

`0101 1010 1101 0010 1110 1011 1010 0101 0110 1110 1110`

**Paso 2. Separar las transiciones**

Cada transición comienza y termina con un `0`. Dentro de la secuencia, dos ceros consecutivos (`00`) marcan la separación entre transiciones.

0==🔵1==0==🔵11==0==🔵1==0==🔵11==0==🔵1== ==🟡00== ==🔵1==0==🔵111==0==🔵1==0==🔵111==0==🔵1== ==🟡00== ==🔵1==0==🔵1==0==🔵11==0==🔵111==0==🔵111==0
Cada transición tiene cinco campos escritos en unario. Un solo `0` separa los campos dentro de una transición.

**Paso 3. Interpretar la función de transición**

`δ(estado actual, símbolo leído) = (estado siguiente, símbolo escrito, movimiento)`. Los códigos de movimiento son `1` para la derecha, `11` para la izquierda y `111` para permanecer en la misma celda.

- 1, 11 = 1, 11, 1
- 1, 111 = 1, 111, 1
- 1, 1 = 11, 111, 111

**Paso 4. Dibujar e interpretar la máquina**

En el campo del símbolo, el código unario `1` representa el blanco.
![[Pasted image 20261107165053.png]]
![[Pasted image 20261107165045.png]]

La máquina recorre la cadena de izquierda a derecha hasta encontrar el primer blanco. Allí escribe un `1`, que queda al final de la cadena.

### Fronteras de la Computabilidad y Análisis de Decidibilidad - Preguntas
Responder a las siguientes preguntas eligiendo la opción correcta:
1. **¿Cuál de las siguientes afirmaciones describe con precisión la diferencia entre un lenguaje Decidible y un lenguaje Reconocible (Recursivamente Enumerable)?**
	1. Un lenguaje decidible solo reconoce cadenas de Tipo 3, mientras que uno reconocible procesa cadenas de Tipo 0.
	2. ***==🟢Para un lenguaje decidible, la Máquina de Turing siempre se detiene (aceptando o rechazando), mientras que para uno reconocible puede entrar en un bucle infinito si la cadena no pertenece.==***
	3. Un lenguaje reconocible siempre se detiene en tiempo polinomial, mientras que uno decidible requiere tiempo exponencial.
	4. No existe diferencia formal; ambos términos son sinónimos según la Tesis de Church-Turing.
2. **Un problema clasificado como impracticable o intratable (ej. de complejidad exponencial O(2^n)):**
	1. Es un problema indecidible para el cual no existe algoritmo.
	2. Es un problema no computable que viola la Tesis de Church-Turing.
	3. ***==🟢Es un problema computable y decidible, pero cuya resolución requiere recursos de tiempo o espacio inviables en la práctica.==***
	4. Es un problema que solo puede ser resuelto por un Autómata Finito Determinístico.

### Análisis Crítico de Afirmaciones Teóricas - Preguntas
**Responder Verdadero o Falso a las siguientes afirmaciones.**
1. Todo problema que sea computable es automáticamente decidible. **Depende de qué se entienda por «computable».** Si existe un algoritmo que siempre termina y responde sí o no, el problema de decisión es decidible. Si solo se exige que el algoritmo acepte las instancias positivas, el problema puede ser reconocible e indecidible, como ocurre con el problema de la parada.
2. Un problema impracticable (intratable) es lo mismo que un problema indecidible. ==🔴**Falso.**== Un problema decidible puede resultar impracticable si los recursos que requiere resolverlo son inviables para el tamaño de entrada considerado. En un problema indecidible, no existe un algoritmo que termine y dé la respuesta correcta para todas las entradas.
3. La tesis de Church-Turing afirma que cualquier procedimiento algorítmico o cálculo efectivo puede ser realizado por una máquina de Turing. ==🟢**Verdadero.**== La tesis vincula la noción intuitiva de cálculo efectivo con la capacidad formal de cómputo de una máquina de Turing.
4. Los lenguajes decidibles forman una subclase estricta de los lenguajes reconocibles (tipo 0). ==🟢**Verdadero.**== Todo lenguaje decidible es reconocible. El lenguaje del problema de la parada es un ejemplo de lenguaje reconocible e indecidible.
5. Si la velocidad de procesamiento de las computadoras aumentara exponencialmente, los problemas indecidibles pasarían a ser decidibles. ==🔴**Falso.**== Aumentar la velocidad de procesamiento reduce el tiempo de ejecución de los algoritmos disponibles. La indecidibilidad se refiere a la inexistencia de un algoritmo que decida correctamente todas las instancias.
