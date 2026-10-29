---
tipo: clase
fecha: 2026-10-16
tema: "Repaso de pila, lenguajes tipo 1 y 0 y máquinas de Turing"
fecha_original: 2026-10-02
fecha_fuente: nombre de capturas
fecha_inferida: true
fechas_contenido:
  - 2026-10-16
  - 2026-10-23
---

> [!note] Material de varias fechas
> Las capturas corresponden a 2026-10-16 y 2026-10-23. El campo `fecha` usa la primera; `fechas_contenido` registra todas.

# Repaso unidad 3a

![[Pasted image 20261016191850.png]]
![[Pasted image 20261016191858.png]]
![[Pasted image 20261016192222.png]]
![[Pasted image 20261016192457.png]]![[Pasted image 20261016193046.png]]
![[Pasted image 20261016193352.png]]
![[Pasted image 20261016194217.png]]![[Pasted image 20261016194619.png]]![[Pasted image 20261016195142.png]]

![[Pasted image 20261016200048.png]]![[Pasted image 20261016200239.png]]
![[Pasted image 20261016200521.png]]
![[Pasted image 20261016201141.png]]
![[Pasted image 20261016201512.png]]

---

# Unidad 4: Lenguajes Tipo 1 y Tipo 0

![[Pasted image 20261016202348.png]]
![[Pasted image 20261016202934.png]]
Forma Normal Kuroda
![[Pasted image 20261016203743.png]]
![[Pasted image 20261016203802.png]]
![[Pasted image 20261016204632.png]]

![[Pasted image 20261016205251.png]]
![[Pasted image 20261016205340.png]]
![[Pasted image 20261016205641.png]]
![[Pasted image 20261016210029.png]]
![[Pasted image 20261016210109.png]]

### Máquina de turing

![[Pasted image 20261016210501.png]]
![[Pasted image 20261023194350.png]]![[Pasted image 20261023194416.png]]


![[Pasted image 20261016212326.png]]
![[Pasted image 20261016212611.png]]

![[Pasted image 20261016212622.png]]

### Esquemas: Una sola cinta o Multicinta

- Modelo clásico: Una sola cinta
	- Contiene la entrada inicialmente escrita en la parte izquierda
	- Sirve como memoria de trabajo: puede leer, escribir y mover el cabezal sobre esa misma cinta
	- Puede tener la salida: al finalizar, la cinta queda con el resultado
	- Entonces, no es solo una "cinta de entrada", sino que una cinta universal: entrada, procesamiento y salida ocurren en el mismo espacio
- Modelo multicinta:
	- Una puede contener la entrada original; la restricción de solo lectura pertenece a algunas variantes, no al modelo multicinta general.
	- Las otras cintas se usan como espacio de trabajo adicional, lo que facilita ciertas operaciones (copiar símbolos, comparar extremos, etc)
	- Esto mejora la eficiencia, pero no aumenta la potencia computacional. Todo lo que hace una multicinta, puede simularse en una sola cinta, pero más lento.

## Ejercicios Lenguajes

![[Pasted image 20261023202110.png]]

### Notación JFLAP

**Caracter que leo; Caracter que escribo, movimiento**
- Si leo y escribo el mismo símbolo, se interpreta como que deje lo que estaba
- Si el carácter que leo o escribo es blanco, se usa un cuadrado
- Movimientos posibles:
	- S: No se mueve
	- R: Derecha
	- L: Izquierda
Se usan los pipes para dividir las cintas. Empiezan a contar desde 1
![[Pasted image 20261023202515.png]]

Ejercicio 1
![[Pasted image 20261023205303.png]]
![[Pasted image 20261023205510.png]]

![[Pasted image 20261023211958.png]]
![[Pasted image 20261023212227.png]]![[Pasted image 20261023212332.png]]

---

## Complemento de estudio

### Pila, tipos de lenguaje y decisión

El lenguaje {aⁿb³ᵐcᵐdⁿ : n,m ≥ 1} permite anidamiento: guardar marcas de a, contar cada terna de b con una marca adicional, quitar esas marcas con c y luego las de a con d. Probar especialmente ternas incompletas y orden incorrecto.

En gramáticas tipo 1 se usa la condición no contractiva |izquierda| ≤ |derecha|, con las convenciones sobre ε correspondientes. En tipo 0 no se impone esa restricción, pero el lado izquierdo debe contener un no terminal.

Un **reconocedor** de un lenguaje tipo 0 puede no terminar ante entradas que no pertenecen. Un **decisor** termina tanto si acepta como si rechaza. Por eso «reconocible» no equivale a «decidible».

Una MT multicinta no aumenta la clase de funciones computables respecto de una unicinta, aunque puede mejorar tiempos de ejecución. El autómata linealmente acotado restringe su espacio de trabajo proporcionalmente al tamaño de la entrada.
