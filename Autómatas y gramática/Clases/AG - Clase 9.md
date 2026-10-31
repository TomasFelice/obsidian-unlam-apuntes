---
tipo: clase
fecha: 2026-10-30
tema: Computabilidad, Complejidad y Máquinas de Turing
fecha_original: 2026-10-30
fecha_fuente:
fecha_inferida: false
---

# Computabilidad, complejidad y máquinas de Turing

> [!abstract] Idea central
> **Computabilidad** pregunta si existe un algoritmo que resuelva un problema. **Complejidad** estudia cuánto tiempo y espacio necesita. La aplicación a blockchain permite comparar dos diseños: restringir el lenguaje de la capa base (Bitcoin) o permitir programas generales y limitar cada ejecución mediante gas (Ethereum).

Estos apuntes desarrollan el texto y las capturas de la clase. Las aclaraciones conceptuales corrigen simplificaciones del material; las capturas originales se conservan al final de cada bloque temático.

## 1. Sistemas Turing completos

Un sistema es **Turing completo** si puede simular una máquina de Turing y, por lo tanto, expresar cualquier cómputo que esta pueda realizar, bajo la idealización de recursos sin una cota fija.

En los lenguajes imperativos, esto suele lograrse mediante decisiones, iteración o recursión y memoria potencialmente ilimitada. Es una guía intuitiva: la definición formal depende de la capacidad de simulación, no de que existan palabras reservadas como `if` o `while`.

- **C, C++, Java y Python:** se consideran Turing completos al abstraer las limitaciones de sus implementaciones físicas.
- **Assembler:** un modelo con saltos condicionales, operaciones y memoria extensible puede ser universal. Los saltos permiten implementar bucles; no hace falta una instrucción llamada `while`. La justificación es esa capacidad de simulación, no que otros lenguajes se compilen a assembler.
- **HTML, JSON y YAML:** por sí solos describen estructura o datos; no ofrecen un mecanismo general de ejecución de algoritmos.
- **SQL, CSS y hojas de cálculo:** hay que precisar la variante y las extensiones. SQL básico sin recursión no equivale a SQL con procedimientos o consultas recursivas; una hoja simple tampoco equivale a una con macros. No conviene clasificar toda una familia a partir de su uso más sencillo.

> [!important] Turing completo no significa «puede resolver cualquier problema»
> Significa que puede expresar cualquier cómputo de una MT. Los problemas indecidibles siguen sin tener un algoritmo general que siempre termine y responda correctamente.

## 2. Lenguajes decidibles, reconocibles y no reconocibles

Para estudiar un problema de decisión se codifican las instancias como cadenas sobre un alfabeto finito. El lenguaje $L$ contiene las instancias cuya respuesta es **sí**.

| Clase | Si $w\in L$ | Si $w\notin L$ |
|---|---|---|
| Decidible o recursivo | Acepta y se detiene | Rechaza y se detiene |
| Reconocible o recursivamente enumerable (RE) | Acepta y se detiene | Puede rechazar o continuar indefinidamente |
| No reconocible | No existe una MT que reconozca exactamente todas las instancias positivas | No hay un reconocedor para el lenguaje |

Todo lenguaje decidible es reconocible, pero existen reconocibles indecidibles:

$$\mathrm{DEC}\subsetneq\mathrm{RE}\subsetneq\mathcal P(\Sigma^*).$$

Un lenguaje es **indecidible** cuando ninguna MT lo decide. Esto incluye tanto lenguajes reconocibles indecidibles como lenguajes no reconocibles.

> [!warning] Precisión sobre «computable»
> Para una función total, computable significa que un algoritmo produce su valor y termina para cada entrada. En problemas de decisión, resolver completamente la pertenencia equivale a decidir el lenguaje. Reconocerlo es una garantía más débil. Por eso, el dibujo de las capturas que separa «lenguajes computables» de los RE debe leerse con cuidado: no es una tercera clase estándar que contenga estrictamente a RE.

### 2.1. El problema de la parada

Dado un programa $M$ y una entrada $w$, se pregunta si $M$ se detendrá al ejecutarse sobre $w$:

$$\mathrm{HALT}=\{\langle M,w\rangle:M\text{ se detiene sobre }w\}.$$

Es **reconocible**: simulamos $M$ sobre $w$ y aceptamos si termina. Es **indecidible**: no existe un algoritmo que siempre responda correctamente tanto para las ejecuciones que terminan como para las que no.

La idea de la demostración es suponer un decisor universal de parada y construir un programa que, al analizarse a sí mismo, haga lo contrario de lo predicho: entre en bucle cuando se prediga que termina y termine cuando se prediga que entra en bucle. Ambas respuestas producen una contradicción.

Que una simulación siga ejecutándose no demuestra que nunca terminará. Tampoco significa que no pueda analizarse la parada de programas particulares: la imposibilidad afecta a un método **general para todos los programas y entradas**.

Otros límites mencionados en las capturas:

- **Teorema de Rice:** toda propiedad semántica no trivial del lenguaje reconocido por una MT es indecidible. No se aplica a cualquier propiedad sintáctica del código.
- **Entscheidungsproblem:** no existe un procedimiento general para decidir la validez de todas las fórmulas de la lógica de primer orden.
- **Décimo problema de Hilbert:** no existe un algoritmo general que decida si una ecuación diofántica arbitraria tiene solución entera.
- **Mortalidad de matrices:** ciertas formulaciones del problema de determinar si algún producto finito de matrices dadas resulta nulo son indecidibles; importa especificar dimensiones y dominio.

## 3. Relación con la jerarquía de Chomsky

| Tipo | Lenguajes | Modelo de reconocimiento |
|---|---|---|
| 3 | Regulares | Autómata finito |
| 2 | Independientes del contexto | Autómata de pila no determinista |
| 1 | Sensibles al contexto | Autómata linealmente acotado |
| 0 | Recursivamente enumerables | Máquina de Turing |

$$\mathrm{REG}\subsetneq\mathrm{CFL}\subsetneq\mathrm{CSL}\subsetneq\mathrm{DEC}\subsetneq\mathrm{RE}.$$

Los lenguajes de tipo 1, 2 y 3 son decidibles. Los de tipo 0 incluyen tanto decidibles como reconocibles indecidibles. Los no reconocibles quedan fuera de esta jerarquía de lenguajes generados por gramáticas.

**No hay que identificar «indecidible» con «fuera de la jerarquía»:** HALT es indecidible y pertenece al tipo 0. Tampoco existe un nivel adicional de Chomsky llamado «decidible»: los decidibles forman una subclase de los RE.

La jerarquía clasifica familias de lenguajes por su capacidad expresiva; no asigna por sí sola una complejidad temporal a cualquier problema relacionado con ellas. Además, la sintaxis de un lenguaje de programación puede describirse mediante una gramática independiente del contexto aunque su semántica permita cómputo universal.

## 4. Complejidad de una máquina de Turing

Una vez que sabemos que un problema es decidible, podemos estudiar los recursos necesarios para resolverlo. Si $n$ es el tamaño de la entrada:

- **Tiempo $T(n)$:** cantidad de pasos de la MT, habitualmente en el peor caso.
- **Espacio $S(n)$:** cantidad de celdas utilizadas, con la convención de medición indicada para el modelo.

Un algoritmo de tiempo $O(n^2)$ tiene crecimiento polinomial; uno de tiempo $O(2^n)$ tiene crecimiento exponencial. Son cotas de algoritmos: encontrar un algoritmo lento no prueba que el problema exija ese costo.

| Clase | Definición para problemas de decisión | Idea para recordar |
|---|---|---|
| P | Decidibles por una MT determinista en tiempo polinomial | Resolución eficiente en el sentido teórico |
| NP | Decidibles por una MT no determinista en tiempo polinomial; equivalentemente, admiten certificados de tamaño polinomial verificables en tiempo polinomial | Verificación eficiente de las respuestas positivas |
| PSPACE | Decidibles por una MT determinista en espacio polinomial | Se acota memoria, sin exigir tiempo polinomial |
| EXPTIME | Decidibles por una MT determinista en tiempo $2^{p(n)}$, para algún polinomio $p$ | Cota superior de tiempo exponencial |

$$\mathrm P\subseteq\mathrm{NP}\subseteq\mathrm{PSPACE}\subseteq\mathrm{EXPTIME}.$$

**NP no significa «no polinomial».** No se sabe si P = NP. Se sabe que P es distinta de EXPTIME, pero no que todas las inclusiones consecutivas de la cadena sean estrictas. Pertenecer a EXPTIME tampoco significa que todo algoritmo necesite tiempo exponencial: P está incluida en EXPTIME.

### 4.1. Ejemplos y límites de las analogías cotidianas

**Contraseña de 16 caracteres.** Con 74 símbolos posibles hay $74^{16}$ candidatos. Si podemos comprobar cada candidato en tiempo finito, recorrer todo el conjunto decide si alguno sirve. Puede ser impracticable sin ser indecidible. Para estudiar complejidad asintótica se deja variar la longitud $n$: la búsqueda tiene $74^n$ candidatos.

**Saldo suficiente para un pago.** Con saldo, importe y reglas representados mediante datos finitos, comparar cantidades es decidible. Obtener datos actuales o coordinar operaciones concurrentes son problemas adicionales del sistema.

**Buscar un ave de una especie.** Encontrar una evidencia válida permite responder «sí»; no encontrarla todavía no demuestra que no exista. Es una analogía de reconocimiento, pero no prueba que el problema biológico sea formalmente RE o indecidible: faltan una codificación, un universo y reglas precisas de observación.

**Predecir un choque.** No disponer de información suficiente sobre el mundo no demuestra no computabilidad. Tanto la pregunta por un choque exacto como la de una probabilidad mayor al 10 % dependen de un modelo y de los datos disponibles. Para un ejemplo formal de indecidibilidad conviene usar HALT.

### Material de clase: fundamentos

> [!example]- Capturas originales de la clase
> ![[Pasted image 20261030193206.png]]
> ![[Pasted image 20261030193226.png]]
> ![[Pasted image 20261030193550.png]]
> ![[Pasted image 20261030193600.png]]
> ![[Pasted image 20261030194335.png]]
> ![[Pasted image 20261030194512.png]]
> ![[Pasted image 20261030194736.png]]
> ![[Pasted image 20261030194914.png]]
> ![[Pasted image 20261030195338.png]]

## 5. Computabilidad en Bitcoin

### 5.1. Transacciones y condiciones de gasto

Bitcoin es una red entre pares que permite verificar transacciones sin un servidor central que autorice cada pago. BTC es la unidad del activo; Bitcoin también designa la red y el protocolo.

Una transacción utiliza **entradas**, que referencian salidas anteriores, y crea **salidas**, que contienen montos y condiciones para gastarlos. Una salida no gastada se denomina **UTXO**. Quien la gasta aporta los datos necesarios para satisfacer su condición, por ejemplo una firma y una clave pública.

En esquemas tradicionales esos datos aparecen en `scriptSig`; en otros, se utiliza el campo de testigo o *witness*. Son mecanismos relacionados, pero no campos intercambiables en todos los tipos de transacción.

El script responde una pregunta acotada: **¿se cumplen las condiciones para gastar esta salida?** La validez total de una transacción incluye otras reglas, como que las entradas existan y no hayan sido gastadas. Los nodos completos que validan una transacción comprueban sus reglas de manera independiente; no todos los participantes de la red realizan necesariamente esa validación completa.

Fuente de consulta: [guía de transacciones de Bitcoin](https://developer.bitcoin.org/devguide/transactions.html).

### 5.2. Script como máquina de pila

Bitcoin Script procesa una secuencia de datos e instrucciones (*opcodes*). Los datos se apilan; las operaciones consumen elementos de la cima y colocan resultados.

Ejemplo didáctico, mostrando la pila de abajo hacia arriba:

| Instrucción | Pila resultante |
|---|---|
| `OP_2` | `[2]` |
| `OP_3` | `[2, 3]` |
| `OP_ADD` | `[5]` |
| `OP_5` | `[5, 5]` |
| `OP_EQUAL` | `[verdadero]` |

Un ejemplo clásico P2PKH usa la condición:

```text
OP_DUP OP_HASH160 <hash de la clave pública> OP_EQUALVERIFY OP_CHECKSIG
```

La prueba aporta `<firma> <clave pública>`. Se duplica la clave, se calcula su hash, se compara con el esperado y se verifica la firma respecto de la transacción según las reglas de firma. No basta con comparar números: los opcodes criptográficos realizan verificaciones especializadas.

### 5.3. Restricciones y clasificación del modelo

Script tiene condicionales, operaciones de pila y verificación criptográfica, pero **no ofrece bucles generales ni saltos hacia atrás**. El programa y sus recursos están acotados por reglas de validación. No realiza consultas arbitrarias a archivos, redes o relojes externos; algunas instrucciones sí verifican restricciones temporales a partir del contexto de la transacción.

Las capturas muestran límites como 1000 elementos de pila, 520 bytes por elemento, 10 000 bytes de script y 201 operaciones. **No deben memorizarse como una tabla universal para todas las versiones:** las reglas dependen del tipo de script y existen diferencias con Tapscript. Lo relevante para esta clase es la ejecución restringida y acotada.

**¿Por qué la clase lo asocia con tipo 3 aunque use una pila?** Un autómata de pila teórico dispone de una pila sin cota fija. Si toda la memoria de trabajo y el contexto relevante están acotados, hay una cantidad finita de configuraciones: se puede modelar mediante un autómata finito, aunque resulte enorme. Usar una pila en una implementación no le concede automáticamente la potencia de un AP teórico.

Esta es una abstracción del verificador acotado presentado en clase; no clasifica toda la red Bitcoin como un único lenguaje regular. De modo análogo, las computadoras físicas tienen memoria finita, pero los lenguajes generales se estudian con memoria idealizada sin cota fija.

La restricción reduce el riesgo de que un script provoque una ejecución interminable durante la validación. Replicar verificaciones tiene un costo: su finalidad es que los participantes puedan comprobar las reglas por su cuenta.

### Material de clase: transacciones y Script

> [!example]- Capturas originales de la clase
> ![[Pasted image 20261030201537.png]]
> ![[Pasted image 20261030201622.png]]
> ![[Pasted image 20261030201741.png]]
> ![[Pasted image 20261030201824.png]]
> ![[Pasted image 20261030201844.png]]
> ![[Pasted image 20261030201900.png]]
> ![[Pasted image 20261030201921.png]]
> ![[Pasted image 20261030201956.png]]
> ![[Pasted image 20261030202139.png]]
> ![[Pasted image 20261030202212.png]]
> ![[Pasted image 20261030202317.png]]
> ![[Pasted image 20261030202445.png]]
> ![[Pasted image 20261030202501.png]]
> ![[Pasted image 20261030202715.png]]
> ![[Pasted image 20261030202812.png]]
> ![[Pasted image 20261030202836.png]]
> ![[Pasted image 20261030202955.png]]
> ![[Pasted image 20261030203152.png]]

## 6. Cómputo fuera de Bitcoin y verificación de disputas

La clase plantea una tensión: se desea construir aplicaciones más complejas sobre una base verificable y resistente a la censura, pero su lenguaje tiene capacidades limitadas. Cambiar las reglas de consenso requiere coordinación y adopción; no es solamente una modificación de código.

Propiedades como «inmutabilidad» o «resistencia a la censura» deben entenderse bajo los supuestos de funcionamiento y seguridad de la red, no como garantías absolutas. La cifra histórica de disponibilidad de las diapositivas se conserva como dato del material, sin convertirla en una medición actual verificada.

### 6.1. Computación optimista o disputable

La idea es ejecutar el programa complejo **fuera de la cadena** (*off-chain*) y utilizar Bitcoin para resolver una disputa acotada cuando alguien impugna el resultado.

1. **Acuerdo previo:** se fijan el programa, las entradas, la máquina o entorno de ejecución, los compromisos, las garantías y los plazos.
2. **Ejecución:** el operador corre el programa fuera de la cadena y publica una afirmación sobre el resultado, junto con lo exigido por el protocolo.
3. **Verificación:** uno o más verificadores lo ejecutan por su cuenta y comparan.
4. **Sin disputa:** al vencer el plazo, se acepta la afirmación de acuerdo con el protocolo.
5. **Con disputa:** se localiza una transición de estado cuya corrección pueda comprobarse en la cadena.

Es **optimista** porque la vía normal acepta el resultado si nadie demuestra un error dentro del plazo. La seguridad requiere verificadores capaces de detectar y disputar errores, disponibilidad de datos y acceso oportuno a la cadena, además de los supuestos específicos del protocolo. «Alcanza con uno honesto» resume solo parte de esas condiciones.

### 6.2. Búsqueda del paso en desacuerdo

Si ambas partes parten del mismo estado y afirman estados finales distintos, pueden comparar compromisos de estados intermedios para reducir el tramo en disputa. En una búsqueda binaria se conserva un intervalo cuyos extremos delimitan el desacuerdo y se divide por la mitad en cada ronda.

Para una traza de $N$ pasos, localizar la transición requiere del orden de $\log_2 N$ rondas: aproximadamente 20 para un millón de pasos. Esto cuenta las rondas de búsqueda, **no todo el costo del protocolo**, las transacciones ni las verificaciones de memoria.

Al final se comprueba una transición concreta a partir del estado anterior acordado. El operador o el impugnante pierde la garantía según el resultado y las reglas establecidas. Bitcoin no necesita repetir toda la ejecución para resolver esa disputa.

### 6.3. BitVM y BitVMX

Las capturas presentan **BitVM (2023)** y **BitVMX (2024)** como ejemplos. La propuesta original de BitVM utiliza verificación de cómputos mediante circuitos; BitVMX desarrolla la verificación de una CPU de propósito general y sus trazas de ejecución.

La búsqueda binaria sirve como explicación didáctica; el diseño de BitVMX también contempla búsquedas n-arias y mecanismos adicionales para localizar errores. Los tamaños concretos de scripts y los costos de las diapositivas corresponden a sus ejemplos, no a una garantía universal.

**Estos protocolos no agregan bucles generales a Bitcoin Script:** amplían lo que se puede verificar mediante un protocolo que combina ejecución externa y resolución de disputas.

Fuente de consulta: [BitVMX: A CPU for Universal Computation on Bitcoin](https://arxiv.org/abs/2405.06842).

### Material de clase: restricciones, motivación y disputas

> [!example]- Capturas originales de la clase
> ![[Pasted image 20261030203239.png]]
> ![[Pasted image 20261030203256.png]]
> ![[Pasted image 20261030203643.png]]
> ![[Pasted image 20261030203714.png]]
> ![[Pasted image 20261030203859.png]]
> ![[Pasted image 20261030203959.png]]
> ![[Pasted image 20261030204130.png]]
> ![[Pasted image 20261030204217.png]]
> ![[Pasted image 20261030204336.png]]
> ![[Pasted image 20261030204533.png]]
> ![[Pasted image 20261030204807.png]]
> ![[Pasted image 20261030205014.png]]
> ![[Pasted image 20261030205144.png]]
> ![[Pasted image 20261030205352.png]]
> ![[Pasted image 20261030205534.png]]
> ![[Pasted image 20261030205604.png]]
> ![[Pasted image 20261030205712.png]]
> ![[Pasted image 20261030205721.png]]
> ![[Pasted image 20261030210004.png]]
> ![[Pasted image 20261030210039.png]]

## 7. Ethereum: cómputo general y gas

Ethereum adopta otro enfoque: una máquina virtual, la **EVM**, permite ejecutar contratos con control de flujo general y estado persistente. Solidity es uno de los lenguajes utilizados para escribir contratos que se compilan a código de la EVM.

La expresividad del modelo no permite predecir la parada de cualquier programa. La solución práctica es asignar costos a las operaciones y establecer un **límite de gas** para cada ejecución. El gas mide recursos; su precio se expresa en el activo nativo, ETH.

Si una ejecución agota su gas, falla y se revierten sus cambios de estado, pero se cobra el trabajo consumido. **El gas limita la ejecución; no resuelve el problema de la parada.**

Se suele llamar Turing completa a la EVM por su capacidad de programación general idealizada. Una transacción concreta dispone de gas finito, y también hay otras cotas del sistema; por eso algunas explicaciones técnicas emplean «cuasi Turing completa».

Fuentes de consulta: [gas y comisiones](https://ethereum.org/developers/docs/gas/) y [explicación técnica de la EVM](https://ethereum.org/developers/tutorials/yellow-paper-evm).

### 7.1. Comparación de los enfoques de la clase

| Aspecto | Bitcoin Script | Ethereum / EVM |
|---|---|---|
| Enfoque | Verificar condiciones de gasto con operaciones restringidas | Ejecutar contratos de propósito general |
| Control de flujo | Sin bucles generales | Permite bucles y saltos |
| Límite de ejecución | Restricciones estructurales y de recursos | Gas y otras cotas del protocolo |
| Cómputo complejo | Puede desplazarse fuera de la cadena y verificarse mediante protocolos de disputa | Puede ejecutarse en la capa base, sujeto al costo y al límite de gas |
| Modelo usado en la clase | Verificador finito acotado, asociado con tipo 3 | Modelo universal idealizado, asociado con tipo 0 |

La pregunta «¿qué tipo de lenguaje necesita la capa base de un sistema financiero global: 3, 2, 1 o 0?» queda como **discusión de diseño**, sin una respuesta única establecida en clase. Depende de qué se quiera ejecutar directamente y de qué se pueda verificar mediante capas adicionales.

La «velocidad de escape funcional» presentada en las diapositivas expresa la idea de que la base tenga suficiente capacidad de verificación para construir extensiones sobre ella sin modificarla continuamente. Es una idea de arquitectura, no una nueva clase de la jerarquía de Chomsky.

### Material de clase: Ethereum y comparación

> [!example]- Capturas originales de la clase
> ![[Pasted image 20261030210316.png]]
> ![[Pasted image 20261030210412.png]]
> ![[Pasted image 20261030210534.png]]
> ![[Pasted image 20261030210809.png]]
> ![[Pasted image 20261030210929.png]]
> ![[Pasted image 20261030211122.png]]
> ![[Pasted image 20261030211214.png]]

## 8. Máquinas y autores

El orden histórico no coincide con el orden de menor a mayor potencia usado al estudiar la materia: la MT fue formulada antes que varios modelos más restringidos.

| Modelo o aporte | Referencia histórica presentada |
|---|---|
| Máquina de Turing | Alan Turing, 1936 |
| Máquina de Mealy | George H. Mealy, 1955 |
| Máquina de Moore | Edward F. Moore, 1956 |
| Autómata linealmente acotado | Desarrollo del modelo alrededor de 1960 |
| Autómata de pila | Desarrollo del modelo a comienzos de la década de 1960 |

Mealy y Moore son modelos finitos con salida: en Mealy la salida depende del estado y de la entrada; en Moore depende del estado. Se distinguen de los aceptores finitos por la función de salida, sin convertirse en modelos universales.

La MT aporta un modelo preciso de cómputo, la idea de una **máquina universal** que simula otras máquinas a partir de su descripción y una vía para demostrar límites de los algoritmos. La **tesis de Church-Turing** relaciona la noción informal de procedimiento efectivo con la computabilidad por MT; no es un teorema sobre una definición matemática previa de «procedimiento efectivo».

### Material de clase: historia

> [!example]- Capturas originales de la clase
> ![[Pasted image 20261030212125.png]]
> ![[Pasted image 20261030212338.png]]

## 9. Algoritmo de Hopcroft y Ullman — pendiente de identificar

El apunte original termina con este título, sin pasos, consigna ni una captura asociada. **No hay información suficiente para determinar qué algoritmo se explicó.** Se conserva el tema pendiente: hace falta recuperar su objetivo, entradas, salida y procedimiento antes de desarrollarlo. Atribuirle aquí un algoritmo concreto podría mezclar contenidos diferentes.

## 10. Preguntas para repasar

1. **¿Todo lenguaje reconocible es decidible?** No. HALT es reconocible e indecidible.
2. **¿Todo lenguaje indecidible está fuera de Chomsky?** No. Los RE indecidibles son de tipo 0.
3. **¿Un algoritmo exponencial prueba que el problema es indecidible?** No. Tiempo de resolución y existencia de un decisor son cuestiones distintas.
4. **¿NP significa que no hay solución polinomial?** No. Describe una clase con certificados verificables en tiempo polinomial.
5. **¿Usar una pila vuelve a Script equivalente a un AP teórico?** No. La pila de Script tiene cotas fijas.
6. **¿BitVMX convierte Script en un lenguaje general con bucles?** No. Combina cómputo externo y verificación de disputas.
7. **¿El gas decide si un contrato terminaría con recursos ilimitados?** No. Impone un límite a su ejecución concreta.
8. **¿Turing completo implica eficiente?** No. Expresividad y costo computacional son propiedades diferentes.

### Referencias para las aclaraciones teóricas

- [UC Davis: máquinas de Turing, reconocimiento y decidibilidad](https://web.cs.ucdavis.edu/~doty/ecs120slides/08a_TuringMachines-deck.html).
- [UMass: reconocimiento, decidibilidad y clases de complejidad](https://people.cs.umass.edu/~marius/class/cs501/lec30-nup.pdf).

Relacionado: [[AG - Clase 8]] · [[AG - Clase 7]] · [[Autómatas y gramática]]
