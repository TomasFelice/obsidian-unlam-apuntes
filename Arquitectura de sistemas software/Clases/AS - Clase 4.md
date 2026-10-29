---
tipo: clase
fecha: 2026-04-20
tema: "Estilos arquitectónicos y comparación de arquitecturas"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Generos arquitectonicos

![[Pasted image 20260420194930.png]]![[Pasted image 20260420194943.png]]![[Pasted image 20260420194950.png]]
![[Pasted image 20260420194930.png]]![[Pasted image 20260420194943.png]]![[Pasted image 20260420194950.png]]
![[Pasted image 20260420195039.png]]

## Diferencias entre generos y estilos

![[Pasted image 20260420195059.png]]

## Estilos

### Monolitica

![[Pasted image 20260420195120.png]]
![[Pasted image 20260420195133.png]]

![[Pasted image 20260420195144.png]]
![[Pasted image 20260420195152.png]]
![[Pasted image 20260420195159.png]]
![[Pasted image 20260420195208.png]]

### Arquitectura Orientada a Servicios (SOA)

![[Pasted image 20260420195216.png]]
![[Pasted image 20260420195227.png]]
![[Pasted image 20260420195234.png]]
![[Pasted image 20260420195241.png]]

### Microservicios

![[Pasted image 20260420195450.png]]
![[Pasted image 20260420195939.png]]
![[Pasted image 20260420200034.png]]
![[Pasted image 20260420200416.png]]

### Diferencias entre SOA y Microservicios

![[Pasted image 20260420200800.png]]
Entre otras...

## Desacoplamiento de componentes Monoliticos en Microservicios

![[Pasted image 20260420200837.png]]

### Arquitectura en capas

![[Pasted image 20260420200906.png]]
![[Pasted image 20260420201209.png]]
![[Pasted image 20260420201215.png]]
![[Pasted image 20260420201303.png]]
![[Pasted image 20260420201327.png]]

### Arquitectura orientada a objetos

![[Pasted image 20260420201620.png]]
![[Pasted image 20260420201627.png]]

### Arquitectura Pipeline

![[Pasted image 20260420201732.png]]

### Arquitectura cliente-servidor

![[Pasted image 20260420202241.png]]
![[Pasted image 20260420202248.png]]

### Diseño de arquitectura mixta

![[Pasted image 20260420202305.png]]
**La mayoría de arquitecturas son mixtas**
[[Trabajo Practico N2]]

---

## Complemento de estudio

### Cómo comparar estilos

Un estilo arquitectónico define tipos de elementos, relaciones y restricciones. La palabra «género» puede usarse en el material para categorías de aplicación; su significado debe fijarse antes de compararla con «estilo».

| Estilo | Ventaja posible | Costo o límite |
|---|---|---|
| Capas | Separar responsabilidades | Cambios que atraviesan varias capas |
| Pipeline | Transformaciones componibles | Latencia, buffers y errores entre etapas |
| Cliente-servidor | Centralizar servicios | Dependencia de red y disponibilidad |
| Microservicios | Despliegue y escalado por servicio | Operación distribuida y consistencia |

SOA y microservicios comparten orientación a servicios, pero difieren según tamaño, gobierno, integración y autonomía. No existe una frontera basada solo en cantidad de líneas.

Para elegir, formular escenarios medibles: quién solicita qué cambio o carga, bajo qué condiciones y con qué respuesta esperada. Ejemplo: soportar el doble de consultas manteniendo un objetivo de latencia definido.
