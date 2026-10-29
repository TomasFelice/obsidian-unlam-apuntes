---
tipo: examen
fecha: 2026-09-11
tema: "Repaso: Thompson, Rabin–Scott, Moore y regularidad de lenguajes"
fecha_original: 2026-04-20
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Práctica Unidad 2B

![[Pasted image 20260911191618.png]]

## 1. Thompson

> 3 reglas

![[Pasted image 20260911191830.png]]
![[Pasted image 20260911191920.png]]
![[Pasted image 20260911191938.png]]
![[Pasted image 20260911191954.png]]
> En la construcción clásica, cada fragmento tiene un estado inicial y un estado final.

> **Caso especial: clausura positiva r+**
> *En la presentación de la cátedra se deriva la clausura positiva a partir de las operaciones básicas: r+ = r · r*. También existen variantes con una construcción directa.*
> **Las reglas fijan un procedimiento reproducible. El autómata resultante puede variar en nombres de estados y convenciones de construcción sin cambiar su lenguaje.**
> ![[Pasted image 20260911192519.png]]


### Ejercicio 2a

![[Pasted image 20260911192706.png]]
![[Pasted image 20260911193040.png]]

### Ejercicio 2c

![[Pasted image 20260911193149.png]]
![[Pasted image 20260911193413.png]]
![[Pasted image 20260911193525.png]]
![[Pasted image 20260911194018.png]]
![[Pasted image 20260911194649.png]]![[Pasted image 20260911194705.png]]
![[Pasted image 20260911195031.png]]

### Método Rabin-Scott

![[Pasted image 20260911200902.png]]
![[Pasted image 20260911201242.png]]
![[Pasted image 20260911201420.png]]
![[Pasted image 20260911201713.png]]
![[Pasted image 20260911201919.png]]
![[Pasted image 20260911202309.png]]
> Como no aparecio ningún subconjunto nuevo, cerramos la tabla

![[Pasted image 20260911202752.png]]
> Luego se completa el AFD con un estado sumidero si falta alguna transición y se aplica Moore para minimizarlo. Son pasos distintos.

### Ejercicio de Moore (simplificacion)

![[Pasted image 20260911203027.png]]
![[Pasted image 20260911210632.png]]
![[Pasted image 20260911210750.png]]
> Este autómata ya era mínimo.

![[Pasted image 20260911211130.png]]
![[Pasted image 20260911211356.png]]
> Siempre conviene primero dibujar el grafo para detectar estados inalcanzables

![[Pasted image 20260911211534.png]]


---

# Parte 3

Recordemos que hay que verificar si los lenguajes son regulares
![[Pasted image 20260911212447.png]]
![[Pasted image 20260911212516.png]]
![[Pasted image 20260911212527.png]]
![[Pasted image 20260911212618.png]]
![[Pasted image 20260911212826.png]]
> [!todo] Revisar la grabación para completar este ejercicio.
![[Pasted image 20260911212918.png]]

---

## Complemento de estudio

### Guía de resolución

Para convertir una ER en AFD mínimo, usar la secuencia de [[AG - Clase 4]] y conservar tablas intermedias. Verificar la cadena vacía y al menos un caso aceptado y rechazado por cada restricción.

Para demostrar que un lenguaje no es regular, puede usarse el lema de bombeo. Su orden lógico importa: suponer regularidad, tomar una longitud p, elegir una palabra suficientemente larga y considerar **todas** las descomposiciones permitidas. Elegir un bombeo que contradiga la pertenencia.

El lema da una condición necesaria de regularidad: encontrar una descomposición que funciona para una palabra no demuestra que el lenguaje sea regular. Si se pretende demostrar regularidad, construir un autómata, una ER o aplicar propiedades de clausura.
