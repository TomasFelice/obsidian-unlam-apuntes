---
tipo: clase
fecha: 2026-05-06
tema: "Desarrollo asistido por IA y revisión de concurrencia"
fecha_original: 2026-04-20
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Concurrencia en IA

## Tipos de Vibecoding

![[Pasted image 20260506192909.png]]

## Tipos de Prompt

![[Pasted image 20260506192949.png]]

## Prompt Pattern (Tecnico)

En esta cátedra, usaremos esta plantilla:
- Lenguaje de programación:
- Plataforma:
- Funcionalidades a implementar:
- Requisitos específicos:
- Restricciones:
> *Es similar a una Especificacion de Requisitos*. Utilizando esto reducimos la ambiguedad para el modelo

**Ejemplo**
![[Pasted image 20260506193335.png]]
![[Pasted image 20260506193353.png]]

### Consejos para armar un prompt

1. Hacer una parte
2. Probar
3. Refinar si es necesario
> 1 -> 3 (se hace continuamente)

## Riesgos de Vibecoding

- Problemas de concurrencia no detectados
- Mala gestión de recursos (memoria, cpu, consumo)
- Validaciones incorrectas
- Credenciales hardcodeadas
- Inyeccion de código
- Autenticación insegura
- APIs vulnerables
![[Pasted image 20260506194137.png]]
![[Pasted image 20260506194152.png]]
![[Pasted image 20260506194327.png]]
![[Pasted image 20260506194443.png]]

## Secure IA Development en vibecoding

> Desarrollar software asistido por IA incorporando revisión de seguridad, validaciones y pruebas durante el proceso.

![[Pasted image 20260506194636.png]]

### ¿Cómo lo aplicamos?

![[Pasted image 20260506194757.png]]

## Herramientas existentes

![[Pasted image 20260506195156.png]]

---

# Actividad Práctica Obligatoria (APO)

---

## Complemento de estudio

### Revisar el código generado

Un prompt debe precisar qué recursos se comparten, qué operaciones deben ser atómicas, quién cierra los canales y cómo se espera la finalización.

Ejemplo: «Dos productores envían trabajos a una cola acotada; cuatro consumidores procesan cada trabajo una sola vez dentro del proceso; al terminar la entrada, todos finalizan y el proceso espera su cierre». Aclarar excepciones y cancelaciones.

Revisar accesos compartidos, orden de adquisición de locks, tiempos límite y liberación de recursos. Probar entradas vacías, fallos de trabajadores y sobrecarga. Una prueba exitosa no demuestra ausencia de carreras.
