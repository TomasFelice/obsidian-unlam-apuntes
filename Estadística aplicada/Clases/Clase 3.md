---
tipo: clase
fecha: 2026-04-23
tema: "Inferencia bayesiana: modelo geométrico y proceso de Poisson"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Inferencia bayesiana

Las copias [[Estadística aplicada/Clases/Clase 3(1)|Clase 3(1)]] y [[Estadística aplicada/Clases/Clase 4|Clase 4]] repiten el comienzo de esta nota; se conservan para no romper enlaces.

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

![[Pasted image 20260423202317.png]]
![[Pasted image 20260423203304.png]]
![[Pasted image 20260423203804.png]]
![[Pasted image 20260423204004.png]]
![[Pasted image 20260423204505.png]]
![[Pasted image 20260423205605.png]]
![[Pasted image 20260423210227.png]]
![[Pasted image 20260423210342.png]]

---

## Complemento de estudio

### Ejemplo resuelto: intentos hasta el primer clic

Se supone una muestra independiente de una geométrica que cuenta **intentos**, con soporte {1,2,…}:

$$P(X=x\mid p)=p(1-p)^{x-1}.$$

Para x = {3,5,2,4}, n = 4 y suma de observaciones = 14. La verosimilitud es proporcional a p⁴(1−p)¹⁰. Por máxima verosimilitud, p̂ = n/Σxᵢ = 4/14 ≈ **0,2857**.

Con prior Beta(α,β), la posterior es Beta(α+n, β+Σxᵢ−n). La prior uniforme en (0,1) de la captura equivale a Beta(1,1), por lo que:

$$p\mid x\sim\operatorname{Beta}(5,11).$$

La media posterior es **5/16 = 0,3125** y el MAP es **4/14 ≈ 0,2857**. Son estimadores distintos. Un intervalo de credibilidad central del 95 % es aproximadamente **[0,1182; 0,5510]**, obtenido con los cuantiles 0,025 y 0,975. El 95 % se usa como ejemplo explícito, porque el porcentaje no es legible en la captura.

Si la geométrica contara fallos antes del éxito, el soporte comenzaría en 0 y cambiarían la verosimilitud y las fórmulas.

### Proceso de Poisson y tiempos de espera

Para tasa constante λ: N(t) ~ Poisson(λt), el tiempo al primer evento es Exponencial(tasa λ) y al k-ésimo evento es Gamma(forma k, tasa λ). La media del primer tiempo es 1/λ. No confundir tasa con escala, que es su inversa.

En el ejemplo de tiempos {45,60,52} minutos: Σxᵢ = 157 y la estimación clásica de λ es **3/157 ≈ 0,0191 min⁻¹**.

**Corrección de la diapositiva:** si la prior es Uniforme(0,1), la posterior tiene densidad proporcional a λ³e^(−157λ) **solo en 0 < λ < 1**: es una Gamma(4, tasa 157) truncada a ese intervalo. Con la prior impropia constante para λ > 0 sí se obtiene la Gamma no truncada. La diferencia numérica aquí es despreciable, pero los modelos no son idénticos. Una prior uniforme no es una elección automática ante falta de información.

Para una prior Gamma(a,b), con b como tasa, la actualización exponencial es Gamma(a+n,b+Σxᵢ).

**Repaso:** distinguir verosimilitud, prior y posterior; indicar soporte y unidades antes de calcular. Referencia para la familia beta: [NIST](https://www.itl.nist.gov/div898/handbook/eda/section3/eda366h.htm).
