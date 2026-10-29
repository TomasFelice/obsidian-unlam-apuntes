---
tipo: clase
fecha: 2026-10-13
tema: "Sensores Android y comunicación IoT"
fecha_original: 2026-09-29
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Sensores y comunicación en Android

## Clases e interfaz

- **SensorManager:** descubre sensores y registra o elimina escuchas.
- **Sensor:** describe un sensor disponible.
- **SensorEvent:** contiene una muestra, su tiempo y precisión.
- **SensorEventListener:** interfaz con onSensorChanged() y onAccuracyChanged().

Los callbacks se implementan en el listener, no necesariamente en una clase que represente el sensor físico. Comprobar disponibilidad y registrar o retirar la escucha según el ciclo de vida para evitar gasto innecesario.

## Acelerómetro y giroscopio

El acelerómetro mide aceleración incluyendo gravedad. El giroscopio mide velocidad angular; el error se acumula al integrar sus muestras para estimar orientación. El procesamiento debe considerar unidades, frecuencia y marcas temporales.

## Comunicación del proyecto IoT

La clase presenta alternativas de conexión directa, MQTT, servidor en la nube y servicios web. Threads, Services y WorkManager tienen funciones distintas; elegir según duración, persistencia y ciclo de vida, como se explica en [[SOA - Clase 6]]. JSON es un formato de intercambio, no un protocolo de transporte.

En MQTT, los clientes publican y se suscriben a topics mediante un **broker**. Una base MySQL puede persistir datos del sistema, pero no equivale a la operación publish. El original señala una etiqueta «Publish» incorrecta en una diapositiva: contrastar el gráfico antes de reutilizarla.

Para la segunda entrega se anotó el uso de MyMQTT; también se mencionan Ubidots, el ejemplo de GitLab y el video de Node-RED en MIEL. No se registraron enlaces específicos para esos ejemplos.

## Complemento de estudio

Definir por mensaje identificador del dispositivo, medida, unidades y momento de medición. Para órdenes, especificar valores válidos y respuesta observable. Ejemplo: publicar temperatura en °C y confirmar si se aplicó una orden al ventilador.

Decidir qué ocurre al perder conexión y cómo se manejan reintentos. Una orden repetida no debería producir acciones adicionales indebidas. **Repaso:** dibujar qué papel cumplen embebido, broker, Node-RED, almacenamiento y aplicación, distinguiendo transporte de persistencia.

---

## Material visual de la clase

![[Pasted image 20261013192302.png]]

![[Pasted image 20261013192400.png]]

![[Pasted image 20261013192734.png]]

![[Pasted image 20261013192822.png]]

![[Pasted image 20261013193212.png]]

![[Pasted image 20261013193743.png]]

![[Pasted image 20261013193833.png]]

![[Pasted image 20261013194905.png]]

![[Pasted image 20261013195443.png]]

![[Pasted image 20261013203657.png]]

![[Pasted image 20261013204048.png]]

![[Pasted image 20261013204316.png]]

![[Pasted image 20261013204516.png]]

![[Pasted image 20261013204604.png]]

![[Pasted image 20261013205843.png]]

![[Pasted image 20261013205935.png]]

![[Pasted image 20261013205956.png]]

![[Pasted image 20261013210159.png]]

![[Pasted image 20261013210314.png]]

![[Pasted image 20261013210417.png]]

![[Pasted image 20261013210604.png]]

![[Pasted image 20261013210805.png]]

![[Pasted image 20261013210819.png]]

![[Pasted image 20261013210831.png]]

![[Pasted image 20261013211259.png]]

![[Pasted image 20261013211411.png]]

![[Pasted image 20261013211424.png]]

![[Pasted image 20261013211557.png]]

![[Pasted image 20261013212013.png]]

![[Pasted image 20261013214828.png]]

![[Pasted image 20261013214915.png]]

![[Pasted image 20261013215046.png]]

![[Pasted image 20261013215129.png]]

![[Pasted image 20261013215959.png]]

![[Pasted image 20261013220518.png]]

![[Pasted image 20261013220555.png]]

![[Pasted image 20261013220623.png]]

![[Pasted image 20261013220719.png]]

![[Pasted image 20261013221128.png]]
