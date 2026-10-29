---
tipo: clase
fecha: 2026-05-04
tema: "Escalabilidad, balanceo y CDN: caso Netflix"
fecha_fuente: nombre de capturas
fecha_inferida: true
---

# Contenido útil

- [Roadmaps de aprendizaje](https://roadmap.sh "https://roadmap.sh")

## Apuntes video BettaTech - Caso Netflix

[Caso Netflix - BettaTech](https://www.youtube.com/watch?v=aQVImBSxxQc "https://www.youtube.com/watch?v=aqvimbsxxqc")
El video introduce un modelo simplificado para discutir escalabilidad; no tomar su secuencia como una cronología comprobada de Netflix.

### Caso inicial

![[Pasted image 20260504193154.png]]
Una sola instancia de EC2 (un servidor). En cuanto crecen los clientes, explota.

### Caso mejorado

![[Pasted image 20260504193240.png]]
Se replican los servidores en un *"Conjunto de servidores"*
El Load Balancer tiene registro de cada uno de ellos, y distribuye las solicitudes entre instancias saludables según una política:
- Round Robin -> una peticion a cada uno.
- Por monitorizacion -> CPU, RAM, etc.

### Qué hace Netflix?

**Auto Scaling** ajusta capacidad según políticas y métricas. Es distinto de balancear solicitudes.
El escalamiento es dinámico, ya que no necesitas todos los servidor prendidos todo el tiempo. Soporta picos de demanda
**Open Connect** es la CDN de Netflix, con appliances y acuerdos con proveedores de Internet para acercar contenido al usuario. No significa que todas las solicitudes de la aplicación pasen por ella.

![[Pasted image 20260504193810.png]]

---

## Complemento de estudio

### Balanceo, escalado y distribución

**Escalar verticalmente** aumenta recursos de una instancia; **horizontalmente** agrega instancias. Un balanceador distribuye tráfico, mientras que un mecanismo de autoescalado modifica capacidad. Una CDN acerca contenido cacheable a los usuarios.

Replicar un servidor no alcanza si las sesiones o archivos permanecen solo en su memoria o disco local. Revisar almacenamiento, estado compartido y salud de instancias. También puede aparecer un cuello de botella en la base de datos.

Fuente del caso real: [Netflix Open Connect](https://openconnect.netflix.com/en/). Las arquitecturas «inicial» y «mejorada» del apunte se usan como ejemplos didácticos.
