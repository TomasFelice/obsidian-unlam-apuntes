---
tipo: clase
fecha: 2026-04-23
tema: "Inferencia bayesiana: modelo geométrico y proceso de Poisson"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Inferencia bayesiana

## Ejercicios

### Ejercicio del anuncio (n.º 4 en la captura)

![[Pasted image 20260423191807.png]]
> **Recordar**:
> 1. Anotar los datos
> 2. Valores de la muestra

**Datos**
X = # de intentos hasta obtener el primer clic en el anuncio
X ~ Geométrica(p)
![[Pasted image 20260423192110.png]]
**Valores de la muestra**: {3, 5, 2, 4}
***Inferencia clásica***
> p es una cte

El estimador p̂ es una variable aleatoria antes de observar los datos; su valor calculado para la muestra es una estimación.
![[Pasted image 20260423192504.png]]

***Inferencia bayesiana***
El parámetro p se modela mediante una distribución a priori f(p), que se actualiza con los datos.
Vamos a usar la posteriori f(p/datos)
a priori + muestra => a posteriori
![[Pasted image 20260423193028.png]]
![[Pasted image 20260423194122.png]]
![[Pasted image 20260423194141.png]]
![[Pasted image 20260423194328.png]]
![[Pasted image 20260423194836.png]]
![[Pasted image 20260423195653.png]]

---

# Revisión de Proceso Poisson

---

## Complemento de estudio

### Relación con la versión completa

Esta nota reproduce el ejemplo y las capturas iniciales de [[Estadística aplicada/Clases/Clase 3|Clase 3]]. Se conserva para mantener los enlaces existentes; no hay evidencia de que documente una clase distinta.

La versión completa incluye la derivación de Beta(5,11), media posterior, MAP, intervalo de credibilidad y el repaso de Poisson. Consultarla para estudiar y evitar mantener respuestas divergentes.

**Pendiente:** confirmar si este archivo corresponde a una copia accidental o si debería contener otro tema. La fecha del contenido coincide con la de las capturas; eso no confirma que esta copia corresponda a una clase distinta.
