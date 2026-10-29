---
tipo: clase
fecha: 2026-04-29
tema: "GIL, async/await, corutinas, futures y pools"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# GIL - Async/Await - Coroutines - Futures - Thread Pools

## Concurrencia y paralelismo

![[Pasted image 20260429193325.png]]
![[Pasted image 20260429193501.png]]
![[Pasted image 20260429193631.png]]

## GIL en Python

![[Pasted image 20260429193718.png]]

## threads vs procesos

![[Pasted image 20260429194406.png]]

## Async / Await: Concurrencia sin bloquear

![[Pasted image 20260429194536.png]]

## Corutinas: Funciones que pueden pausarse

![[Pasted image 20260429194821.png]]

## Futures: Promesas de resultado

![[Pasted image 20260429194924.png]]

## Thread Pool: reutilizar hilos

![[Pasted image 20260429195125.png]]

## Cuando usar cada uno?

![[Pasted image 20260429195641.png]]
![[Pasted image 20260429195945.png]]
![[Pasted image 20260429200343.png]]
![[Pasted image 20260429200443.png]]
![[Pasted image 20260429200707.png]]

---

## Complemento de estudio

### Elegir el mecanismo según la carga

| Trabajo | Alternativa | Precaución |
|---|---|---|
| Muchas esperas de red | async/await | La E/S debe ceder el control |
| E/S con biblioteca bloqueante | Pool de hilos | Limitar trabajos simultáneos |
| Cálculo intensivo en Python | Procesos o biblioteca nativa | Medir transferencias y serialización |

En CPython con GIL habilitado, un solo hilo ejecuta bytecode Python a la vez. Esto no impide concurrencia de E/S; ciertas extensiones liberan el GIL. Existen compilaciones sin GIL: la conclusión depende del intérprete y su configuración.

Una corutina puede suspenderse en un await; escribir async no vuelve no bloqueante una función bloqueante. Un **future** representa un resultado pendiente: también puede fallar o cancelarse. Un pool reutiliza trabajadores.

Fuente: [threading y GIL](https://docs.python.org/3/library/threading.html).
