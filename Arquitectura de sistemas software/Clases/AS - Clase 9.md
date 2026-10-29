---
tipo: clase
fecha: 2026-06-01
tema: "Modelo C4"
fecha_original: 2026-05-18
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Representación de Arq con C4

> Propone una **forma progresiva de visualizar un sistema en 4 niveles**:
> 1. Contexto: *visión global del sistema y actores*
> 2. Contenedores: *como se divide el sistema en aplicaciones o servicios ejecutables*
> 3. Componentes: *módulos internos de cada contenedor*
> 4. Código: *clases, scripts o estructuras a bajo nivel (opcional)*

![[Pasted image 20260601192403.png]]
> También esta draw.io

![[Pasted image 20260601192902.png]]
![[Pasted image 20260601192929.png]]
![[Pasted image 20260601193155.png]]
![[Pasted image 20260601193200.png]]
![[Pasted image 20260601193345.png]]
![[Pasted image 20260601193351.png]]
Diagrama de clases
> [!todo] Desarrollo pendiente
> El registro original no contiene una explicación en este punto. Consultar la captura o la grabación.
![[Pasted image 20260601193605.png]]
![[Pasted image 20260601193752.png]]

### Arquitectura como código

> Apunta a la creacion de los diagramas a partir de código
> ![[Pasted image 20260601193828.png]]


---

## Nivel 1 - D. de Contexto

![[Pasted image 20260601194029.png]]

## Nivel 2 - D. de Contenedores

![[Pasted image 20260601194302.png]]
![[Pasted image 20260601194519.png]]

## Nivel 3 - Diagrama de componentes

![[Pasted image 20260601194631.png]]
![[Pasted image 20260601194759.png]]

## Nivel 4 - Diagrama de código (opcional)

![[Pasted image 20260601194930.png]]

# Ventajas de C4

![[Pasted image 20260601195124.png]]
![[Pasted image 20260601195138.png]]

---
Ejemplos
![[Pasted image 20260601195233.png]]
![[Pasted image 20260601195227.png]]
![[Pasted image 20260601195336.png]]
![[Pasted image 20260601195725.png]]
![[Pasted image 20260601195846.png]]
![[Pasted image 20260601195927.png]]

---

## Complemento de estudio

### Los cuatro niveles de C4

1. **Contexto:** sistema de interés, personas y sistemas externos.
2. **Contenedores:** aplicaciones y almacenes de datos, responsabilidades y comunicación.
3. **Componentes:** partes internas relevantes de un contenedor.
4. **Código:** detalle de implementación cuando aporta valor.

Un contenedor C4 no implica un contenedor Docker. Cada vista debe indicar su alcance, responsabilidades y relaciones; rotular las flechas con su propósito y, cuando corresponda, el protocolo.

Usar solo los niveles útiles para la audiencia. Un diagrama de despliegue complementa estas vistas para mostrar dónde corre el software. Mantener diagramas como código facilita versionarlos, pero igual requiere revisar su correspondencia con el sistema.

Fuente: [C4 model: diagramas](https://c4model.com/diagrams).
