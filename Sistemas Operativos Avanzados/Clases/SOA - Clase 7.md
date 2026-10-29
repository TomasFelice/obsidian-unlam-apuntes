---
tipo: clase
fecha: 2026-09-29
tema: Android
---
> **Temario**
> ![[Pasted image 20261013192302.png]]

---
# Sensores en Android
> Para que se usan?

![[Pasted image 20261013192400.png]]

### Clases necesarias para usar sensores
- **SensorManager**
- **Sensor**
- **SensorEvent**
- **SensorEventListener**
![[Pasted image 20261013192734.png]]
![[Pasted image 20261013192822.png]]
Estos metodos (onAccuracyChanged, onSensorChanged), hay que sobreescribirlos en la clase de nuestro sensor

> Comentario al pasar: Recordatorio de estados de Activities
> ![[Pasted image 20261013193212.png]]

### Acelerometro
![[Pasted image 20261013193743.png]]
![[Pasted image 20261013193833.png]]
![[Pasted image 20261013194905.png]]

### Giroscopio
![[Pasted image 20261013195443.png]]
> es importante tener en cuenta que el giroscopio va acumulando error

![[Pasted image 20261013203657.png]]
Para la entrega 2, usaremos MyMqtt
Las otras aplicaciones, tambien ayudan a testear la comunicacion con el embebido.

## Estrategias para programas la comunicacion con Android
![[Pasted image 20261013204048.png]]

![[Pasted image 20261013204316.png]]
Threads, Services o WorkManager

![[Pasted image 20261013204516.png]]

JSON
![[Pasted image 20261013204604.png]]

---
![[Pasted image 20261013205843.png]]

![[Pasted image 20261013205935.png]]

Directa
![[Pasted image 20261013205956.png]]
![[Pasted image 20261013210159.png]]

MQTT
![[Pasted image 20261013210314.png]]
![[Pasted image 20261013210417.png]]
![[Pasted image 20261013210604.png]]
![[Pasted image 20261013210805.png]]
Servidor nube
![[Pasted image 20261013210819.png]]
![[Pasted image 20261013210831.png]]
![[Pasted image 20261013211259.png]]
![[Pasted image 20261013211411.png]]
![[Pasted image 20261013211424.png]]
![[Pasted image 20261013211557.png]]
> Ver ejemplo de gitlab

ubidots
![[Pasted image 20261013212013.png]]

> Ver nodered en video de miel

![[Pasted image 20261013214828.png]]
![[Pasted image 20261013214915.png]]
![[Pasted image 20261013215046.png]]
![[Pasted image 20261013215129.png]]
![[Pasted image 20261013215959.png]]
![[Pasted image 20261013220518.png]]
![[Pasted image 20261013220555.png]]
![[Pasted image 20261013220623.png]]
Publish esta mal. es la BD MYSQL.
![[Pasted image 20261013220719.png]]
![[Pasted image 20261013221128.png]]

---
Web Service
