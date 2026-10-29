---
tipo: clase
fecha: 2026-09-29
tema: Android
---
# Arquitectura de Microservicios
# Arquitectura de Microservicios
### Arquitectura Monolitica
La arquitectura "de siempre" es **Monolitica**
- Altamente acoplada
- Diferentes componentes ejecutan como uno solo
- Con alta demanda, escala toda la arquitectura
- Propagacion de errores
- Despliegue mas riesgoso
![[Pasted image 20261020193012.png]]
### Microservicios
Seccionamos la aplicacion en modulos.
Con cada modulo, los distribuimos  en distintos servicios
Los servicios son coordinados por un API Gateway.
El backend en realidad son multiples backends separados (teoricamente aislados e independientes)
- Escalabilidad independiente
- Despliegues mas seguros
- Flexibilidad tecnologica
- Equipos de desarrollo autonomos
- Mayor resiliencia
- Escalabilidad horizontal
Necesitamos un protocolo de comunicacion que permita coordinar los microservicios.
![[Pasted image 20261020193053.png]]
### Mejores practicas
- Separar almacenamiento en distintas bases de datos por servicios
- Mantener el codigo en un mismo nivel de madurez. Todo con la misma capacidad de escalabilidad
- Separar el build de cada microservicio. Cada servicio se encarga de su propio build
- Unica responsabilidad por servicio
- Desplegar en containers
- Tratar los servidores como "sin estado" (stateless)
- Domain-driven design. Arquitectura "tipo hexagonal". Casos de uso.
- Micro-frontend. Se desarrollan componentes que ya resuelven la comunicacion con su servicio
- Orquestar microservicios (kubernetes)
### Implementacion
![[Pasted image 20261020195349.png]]

### Contendores
Los microservicios van muy relacionados a los contenedores, ya que se espera que cada microservicio s despliegue con contenedores
![[Pasted image 20261020200852.png]]
![[Pasted image 20261020200906.png]]
> vm vs container

- Aislamiento
- Menor uso de hw
- Inicio y fin rapido
- Menor riesgo de interrupcion
- Mayor seguridad
- Mayor facilidad de portabilidad

### Api Gateway
Servidor que permite gestionar las multiples conexiones de acceso a los microservicios
Gestiona las funciones transversales a los microservicios de forma centraluzasa
![[Pasted image 20261020201412.png]]
**Ventajas**
- Abstraccion de complejidad
- Autenticacion y autorizacion
- Transformacion de requests y responses
- Balanceo y reduccion de cargas (memoria cache)
- Control de vulnerabilidades
- Diferentes protocolos
- Manejo de errores.
**Desventajas**
- Unico punto de falla
- Problemas de rendimiento (mayor latencia)
- Costo adicional en comunicacion
- No es escalable para diferentes tipos de cliente
- Sin soporte para multiples backends

### Patron BFF (Backend For Frontend)
![[Pasted image 20261020201649.png]]
Puedo separar el api gateway segun el cliente en un "backend for frontend"
En cada backend, podes tener incluso endpoints distintos. Son piezas independientes completamente.
- soluciona el problema de multiples clientes de diferentes tipos y la psoible tendencia de convertir el sistema en monolit
- Implementacion de gateway independiente para cada cliente.
	- Diferentes alcances y dominios.
	- Diferentes metodos de autenticacion.
	- Modelo desacoplado

## Servicios REST
> **API**: Una interfaz que se define en nuestros programas con ciertas restricciones y recomendaciones para que otros sistemas puedan comunicarse con el
> Tipos:
> - REST: HTTP. GET, POST, PUT, DELETE. Utiliza los metodos para realizar operaciones sobre los recursos definidos x URI
> - WebSockets: Comunicacion bidireccional entre cliente y backend.
> - SOAP: Mensajes estructurados, XML. Sobre HTTP, SMTP, TCP
> - RPC: Permite invocar funciones o procedimientos a un sistema remoto como si fuera un sistema local.

## Arquitectura REST
![[Pasted image 20261020202630.png]]
- Estructura estandarizada
- Identificacion del recurso
- Metodo de acceso
- Stateless
Formato del request
![[Pasted image 20261020202853.png]]
Formato del response
![[Pasted image 20261020203008.png]]

### Estados REST
- Stateless
	- Servidor no retiene informacion
	- Arquitectura simple
	- Facilmente escalable
	- El estado lo mantiene el cliente (ls, cache, cookies)
- Stateful
	- El servidor mantiene la infromacion
	- Arquitectura compleja
	- Reduce la escalabilidad debido al almacenamiento de aplicaciones
	- Sesiones de clientes

## Comunicacion
Al integrar microservicios, se busca **minimizar** la comunicacion entre ellos.
**Menos comunicacion es mejor**
- Sincronica
	- HTTP
	- HTTPS
- Asincronica
	- AMQP
	- MQTT

#### Sincronica
El tipo de comunicacion mas comun para microservicios
Basada en HTTP/HTTPS
Poco recomendable en la integracion de varios microservicios
![[Pasted image 20261020203812.png]]
#### Asincronica
Da ventaja en la integracion de microservicios
MAyor escalabilidad  flexibilidad de implementacion
Basada en protocolos asincronicos como MQTT o AMQP
![[Pasted image 20261020203938.png]]
## Estrategias de comunicacion
### Event Bus
![[Pasted image 20261020204014.png]]
### API Pooling
Llamo constantemente haste que recibo la respuesta deseada
![[Pasted image 20261020204156.png]]
### Webhook
![[Pasted image 20261020204308.png]]
### RPC - Remote Procedure Call
![[Pasted image 20261020204453.png]]

---
# NodeRed ESP32
En esp32 hay diferentes bibliotecas que nos permiten usar MQTT/HTTP

Android
Se puede usar:
- HttpURLConnection
	- Bloqueante
	- En un hilo, creo el objeto, abro la conexion, hago la peticion y espero la respuesta
- Retrofit
	- Asincronico
	- Trabaja con JSON, lo transforma a objeto
	- Se crea en el hilo principal
		- Se usa un callback que maneja la logica.

