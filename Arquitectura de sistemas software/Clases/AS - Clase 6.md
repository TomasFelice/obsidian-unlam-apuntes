---
tipo: clase
fecha: 2026-05-04
tema: Complete el tema
---
# Contenido útil
- [Roadmaps de aprendizaje](https://roadmap.sh "https://roadmap.sh")
## Apuntes video BettaTech - Caso Netflix
[Caso Netflix - BettaTech](https://www.youtube.com/watch?v=aQVImBSxxQc "https://www.youtube.com/watch?v=aqvimbsxxqc")
Netflix se aloja en AWS
### Caso inicial
![[Pasted image 20260504193154.png]]
Una sola instancia de EC2 (un sv). En cuanto crecen los clientes, explota.
### Caso mejorado
![[Pasted image 20260504193240.png]]
Se replican los servidores en un *"Conjunto de servidores"*
El Load Balancer tiene registro de cada uno de ellos, y se encarga de lanzar peticiones a todos ellos segun un algoritmo a definir:
- Round Robin -> una peticion a cada uno.
- Por monitorizacion -> CPU, RAM, etc.
### Qué hace Netflix?
Netflix tiene **Amazon EC2 Auto-Scaling**
El escalamiento es dinamico, ya que no necesitas todos los sv prendidos todo el tiempo. Soporta picos de demanda
**OpenConnect**: Similar a CloudFront. Hace de CDN, todo pasa primero por ahi.
![[Pasted image 20260504193810.png]]
Netflix intenta preveer con algoritmos de IA cuando se van a visualizar los contenidos. Netflix pre-popula las CDN. Esto lo usan para disminuir los accesos a S3.
