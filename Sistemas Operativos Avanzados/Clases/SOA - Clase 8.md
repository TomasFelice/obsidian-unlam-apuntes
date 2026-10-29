---
tipo: clase
fecha: 2026-10-20
tema: "Microservicios, APIs y comunicación IoT"
fecha_original: 2026-09-29
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Arquitectura de microservicios

### Arquitectura Monolitica

La arquitectura "de siempre" es **Monolitica**
- Puede tener alto acoplamiento si está mal modularizada; no es una propiedad obligatoria del monolito.
- Diferentes componentes ejecutan como uno solo
- Con alta demanda, escala toda la arquitectura
- Propagacion de errores
- Despliegue más riesgoso
![[Pasted image 20261020193012.png]]

### Microservicios

Seccionamos la aplicación en módulos.
Con cada módulo, los distribuimos  en distintos servicios
Los servicios son coordinados por un API Gateway.
El backend en realidad son múltiples backends separados (teoricamente aislados e independientes)
- Escalabilidad independiente
- Despliegues más seguros
- Flexibilidad tecnologica
- Equipos de desarrollo autonomos
- Mayor resiliencia
- Escalabilidad horizontal
Necesitamos un protocolo de comunicación que permita coordinar los microservicios.
![[Pasted image 20261020193053.png]]

### Mejores practicas

- Separar almacenamiento en distintas bases de datos por servicios
- Definir calidad y escalabilidad según necesidades de cada servicio; no exigir idéntica capacidad a todos.
- Separar el build de cada microservicio. Cada servicio se encarga de su propio build
- Unica responsabilidad por servicio
- Desplegar en containers
- Tratar los servidores como "sin estado" (stateless)
- Domain-driven design. Arquitectura "tipo hexagonal". Casos de uso.
- Micro-frontend. Se desarrollan componentes que ya resuelven la comunicación con su servicio
- Orquestar microservicios (kubernetes)

### Implementación

![[Pasted image 20261020195349.png]]

### Contenedores

Los microservicios van muy relacionados a los contenedores, ya que se espera que cada microservicio s despliegue con contenedores
![[Pasted image 20261020200852.png]]
![[Pasted image 20261020200906.png]]
> vm vs container

- Aislamiento
- Menor uso de hw
- Inicio y fin rápido
- Menor riesgo de interrupción
- Mayor seguridad
- Mayor facilidad de portabilidad

### Api Gateway

Servidor que permite gestionar las múltiples conexiones de acceso a los microservicios
Gestiona las funciones transversales a los microservicios de forma centralizada
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
- Único punto de falla
- Problemas de rendimiento (mayor latencia)
- Costo adicional en comunicación
- Una interfaz única puede volverse compleja al atender necesidades muy distintas de los clientes.
- Debe configurarse el enrutamiento a los múltiples backends; el soporte depende del producto y del diseño.

### Patron BFF (Backend For Frontend)

![[Pasted image 20261020201649.png]]
Puedo separar el api gateway según el cliente en un "backend for frontend"
En cada backend, podes tener incluso endpoints distintos. Son piezas independientes completamente.
- soluciona el problema de múltiples clientes de diferentes tipos y la posible tendencia de convertir el sistema en monolit
- Implementación de gateway independiente para cada cliente.
	- Diferentes alcances y dominios.
	- Diferentes métodos de autenticacion.
	- Modelo desacoplado

## Servicios REST

> **API**: Una interfaz que se define en nuestros programas con ciertas restricciones y recomendaciones para que otros sistemas puedan comunicarse con el
> Tipos:
> - REST: HTTP. GET, POST, PUT, DELETE. Utiliza los métodos para realizar operaciones sobre los recursos definidos x URI
> - WebSockets: Comunicación bidireccional entre cliente y backend.
> - SOAP: Mensajes estructurados, XML. Sobre HTTP, SMTP, TCP
> - RPC: Permite invocar funciones o procedimientos a un sistema remoto como si fuera un sistema local.

## Arquitectura REST

![[Pasted image 20261020202630.png]]
- Estructura estandarizada
- Identificación del recurso
- Método de acceso
- Stateless
Formato del request
![[Pasted image 20261020202853.png]]
Formato del response
![[Pasted image 20261020203008.png]]

### Estados REST

- Stateless
	- Cada solicitud contiene lo necesario para interpretarla sin depender de una sesión de interacción guardada en el servidor. El servidor sí puede persistir recursos en una base de datos.
	- Arquitectura simple
	- Facilmente escalable
	- El estado lo mantiene el cliente (ls, cache, cookies)
- Stateful
	- El servidor mantiene la información
	- Arquitectura compleja
	- Reduce la escalabilidad debido al almacenamiento de aplicaciones
	- Sesiones de clientes

## Comunicación

Al integrar microservicios, se busca **minimizar** la comunicación entre ellos.
**Menos comunicación es mejor**
- Sincrónica
	- HTTP
	- HTTPS
- Asincrónica
	- AMQP
	- MQTT

#### Sincrónica

El tipo de comunicación más común para microservicios
Basada en HTTP/HTTPS
Poco recomendable en la integracion de varios microservicios
![[Pasted image 20261020203812.png]]

#### Asincrónica

Da ventaja en la integracion de microservicios
MAyor escalabilidad  flexibilidad de implementación
Basada en protocolos asincronicos como MQTT o AMQP
![[Pasted image 20261020203938.png]]

## Estrategias de comunicación

### Event Bus

![[Pasted image 20261020204014.png]]

### API polling

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
	- En un hilo, creo el objeto, abro la conexión, hago la peticion y espero la respuesta
- Retrofit
	- Asincronico
	- Trabaja con JSON, lo transforma a objeto
	- Se crea en el hilo principal
		- Se usa un callback que maneja la lógica.

---

## Complemento de estudio

### Criterios de arquitectura

Un monolito puede ser modular y escalar horizontalmente. Los microservicios habilitan despliegues y escalado independientes cuando sus límites y contratos lo permiten, pero agregan red, fallos parciales y consistencia distribuida.

API Gateway, contenedores, Kubernetes, arquitectura hexagonal y microfrontends son decisiones posibles, no requisitos universales de los microservicios. Un gateway puede atender varios backends y tipos de cliente; BFF permite especializar la interfaz por experiencia de usuario.

En REST, stateless significa no depender de una sesión de interacción almacenada entre solicitudes; no impide usar bases de datos. GET consulta; PUT expresa reemplazo de un recurso y es idempotente; POST no lo es por definición. La idempotencia es útil ante reintentos.

Polling consulta repetidamente. Un webhook notifica al receptor mediante una llamada cuando ocurre un evento. En ambos casos definir autenticación, tiempos límite, reintentos y duplicados. Elegir comunicación síncrona o asíncrona según las necesidades del caso.
