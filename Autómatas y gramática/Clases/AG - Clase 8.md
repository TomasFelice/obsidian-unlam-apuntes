---
tipo: clase
fecha: 2026-10-23
tema: "Diseño y prueba de máquinas de Turing"
fecha_original: 2026-10-02
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Máquina de Turing

![[Pasted image 20261023193707.png]]
Realizar con el siguiente orden:
1. Análisis (Que recibe, que produce, casos, que entradas se rechazan)
2. Estrategia (En palabras, antes del diagrama, cuantas cintas y para que, que tiene que recordar el estado, que pasos)
3. Desarrollo (JFLAP 8, estados, transiciones, símbolos, movimientos)
4. Pruebas (lote con entradas que tienen que funcionar y entradas que tienen que rechazarse)

---

## Complemento de estudio

### Plantilla para diseñar una MT

**Análisis:** definir alfabeto, lenguaje o transformación, palabra vacía y salida esperada. **Estrategia:** describir qué representa cada marca y qué invariante se mantiene. **Desarrollo:** traducir fases a estados y transiciones. **Pruebas:** contrastar resultados esperados con los obtenidos.

Para {aⁿbⁿcⁿ : n ≥ 0}, una estrategia unicinta consiste en marcar una a, buscar y marcar una b y una c y volver al comienzo; repetir y comprobar al final que no haya símbolos sin marcar ni desordenados. Aceptar ε si n = 0 está permitido.

Probar ε, abc y aabbcc; rechazar ab, aabbc, acb y abcabc. Son pruebas propuestas, no ejecuciones verificadas en JFLAP.

Si la máquina reconoce un lenguaje, distinguir rechazo de bucle infinito; si transforma una entrada, especificar también contenido final de la cinta y posición de cabezales cuando lo exija la consigna.
