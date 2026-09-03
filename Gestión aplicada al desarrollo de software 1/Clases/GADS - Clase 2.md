---
tipo: clase
fecha: 2026-08-20
tema: Introduccion
---
# Modelos de Ciclo de Vida y Modelos de Negocio
# Modelos de Ciclo de Vida y Modelos de Negocio

## Idea central de la clase

El **modelo de ciclo de vida** define cómo evoluciona un producto de software desde su concepción hasta su retiro. A nivel macro, determina:

- cómo se organiza el proyecto;
- en qué momentos existen entregables;
- cuándo recibe valor el usuario;
- cuánto riesgo se asume antes de validar el producto;
- cómo se estima el trabajo;
- y, en muchos casos, **cómo, cuánto y cuándo se cobra**.

> No existe un ciclo de vida perfecto: existe un ciclo de vida adecuado para un proyecto concreto.

Una mala elección puede llevar a trabajar durante meses sobre funcionalidades que nadie usa. La clase remarca que **el código que nadie usa es uno de los costos más caros de un proyecto**.

---

# 1. Producto, proceso y ciclo de vida

Es importante distinguir:

- **Producto:** el software que se construye y sus distintos estados durante el proyecto.
- **Proceso:** las actividades utilizadas para producirlo.
- **Ciclo de vida:** la forma en la que el producto evoluciona a lo largo del tiempo.

Algunas actividades típicas del proceso son:

1. obtención de requisitos;
2. diseño del sistema;
3. programación;
4. pruebas;
5. instalación;
6. mantenimiento;
7. ampliación.

Los estados del producto evolucionan desde una **necesidad** hasta una **especificación de requisitos**, un **diseño**, un **programa** y finalmente un **sistema software**.

---

# 2. Unidad mínima de proceso

La **unidad mínima de proceso** es el conjunto básico de actividades necesarias para producir una parte funcional del software.

Normalmente incluye:

1. **Análisis de requisitos**
2. **Diseño**
3. **Construcción**
4. **Pruebas**
5. **Gestión**

La gran diferencia entre los modelos de ciclo de vida está en **cuántas veces se ejecuta esta unidad mínima** y **qué se conoce antes de comenzar cada ejecución**.

---

# 3. Niveles de abstracción según Davis y Alexander

Davis y Alexander distinguen tres niveles de abstracción para analizar los modelos de proceso.

## Nivel 3 - Desarrollo

Describe cómo evoluciona globalmente el producto y cómo se subdividen las necesidades del usuario.

Modelos principales:

- **Convencional / Tradicional**
- **Incremental**
- **Evolutivo**

## Nivel 2 - Actividades

Refina el modelo anterior especificando qué actividades se realizan y cómo se relacionan.

Ejemplos vistos:

- Cascada
- Refinamiento sucesivo
- Iterativo incremental
- Espiral
- Espiral Win-Win
- Métodos ágiles

## Nivel 1 - Herramientas

Es el nivel más concreto. Define herramientas, métodos y técnicas para ejecutar las actividades.

Ejemplo visto:

- RUP

> Importante: en la exposición de clase se usa muchas veces **“Tradicional (Cascada)”** como simplificación. En la clasificación más formal del material, **Convencional** corresponde al nivel de desarrollo y **Cascada** a un modelo de actividades.

---

# 4. Los tres modelos principales de ciclo de vida

## 4.1. Modelo Tradicional / Convencional

### Idea

La necesidad del usuario **no se subdivide**. El producto se desarrolla completamente y se entrega una sola vez.

La unidad mínima de proceso se ejecuta una única vez:

**Análisis → Diseño → Construcción → Pruebas → Entrega**

### Características

- alcance conocido desde el inicio;
- requisitos definidos y prácticamente congelados;
- una única entrega final;
- poca tolerancia al cambio;
- fuerte planificación inicial;
- útil cuando el problema no puede dividirse de manera valiosa.

### Cuándo tiene sentido

Cuando:

- el alcance está claramente definido;
- los cambios son costosos o imposibles;
- existe alta criticidad;
- existen restricciones regulatorias;
- el sistema no puede entregarse parcialmente.

### Ejemplos vistos

- control de tráfico aéreo;
- software embebido de marcapasos;
- sistemas sujetos a normativa, como liquidaciones impositivas;
- software embebido o regulado.

### Riesgo principal

Se puede trabajar durante mucho tiempo sin validación real de usuarios.

---

## 4.2. Modelo Incremental

### Idea

Se entiende **todo el problema al inicio**, pero se decide dividirlo en partes.

El sistema completo se descompone antes de comenzar en un número conocido de incrementos.

Cada incremento ejecuta una unidad mínima de proceso completa.

### Flujo conceptual

1. estudiar el problema completo;
2. dividirlo en subproblemas;
3. planificar las etapas;
4. desarrollar cada incremento;
5. entregar funcionalidad real en cada etapa;
6. completar progresivamente el producto.

### Características

- alcance total conocido;
- problema divisible;
- cantidad de incrementos planificada;
- entregas parciales con valor;
- menor riesgo que una única entrega final;
- feedback temprano.

### Cuándo tiene sentido

Cuando el sistema es grande o complejo, pero puede dividirse en módulos independientes.

### Ejemplos vistos

- e-commerce;
- home banking;
- ERP corporativo;
- sistemas empresariales grandes.

---

## 4.3. Modelo Evolutivo

### Idea

Al comenzar el proyecto **solo se conoce una parte del alcance**.

Se desarrolla una primera versión y las próximas etapas se definen a partir del uso real, el feedback de usuarios o cambios en el mercado.

A diferencia del incremental, **las evoluciones futuras no están completamente previstas desde el inicio**.

### Características

- alcance parcial al comenzar;
- alta incertidumbre;
- requisitos cambiantes;
- entregas frecuentes;
- feedback continuo;
- producto adaptable;
- cada versión ayuda a decidir qué construir después.

### Cuándo tiene sentido

En:

- productos innovadores;
- startups;
- productos digitales nuevos;
- mercados cambiantes;
- situaciones donde no se conoce con precisión el producto final.

### Ejemplos vistos

- Instagram;
- Twitter/X;
- Slack;
- MercadoLibre.

Estos casos comenzaron resolviendo un problema o con una propuesta diferente y evolucionaron según el comportamiento de usuarios o el mercado.

---

# 5. Comparación rápida

| Criterio | Tradicional | Incremental | Evolutivo |
|---|---|---|---|
| Alcance inicial | Conocido | Conocido | Parcial |
| Problema | No divisible | Divisible | Divisible |
| Cantidad de entregas | Una | Varias definidas | Varias, no totalmente definidas |
| Requisitos futuros | Conocidos | Conocidos | Se descubren |
| Feedback | Tardío | En cada incremento | Continuo |
| Cambio esperado | Bajo | Moderado | Alto |
| Ejemplos | Software regulado | ERP, e-commerce | Startups, marketplaces |

La pregunta clave para diferenciar **incremental** de **evolutivo** es:

> **¿Sé desde el principio cuáles van a ser los próximos incrementos?**

- Si **sí** → Incremental.
- Si **no**, y se definirán según el feedback → Evolutivo.

---

# 6. Variables a considerar antes de elegir un ciclo

La clase plantea varias preguntas iniciales:

- ¿Cuánto presupuesto hay?
- ¿El presupuesto es fijo o flexible?
- ¿Qué tipo de cliente es?
- ¿Qué tan urgente es salir al mercado?
- ¿Qué tan claro está el alcance?
- ¿El problema puede dividirse?
- ¿Cada división entrega valor real?
- ¿Qué tan crítico es el sistema?
- ¿Cuánto puede cambiar el problema?
- ¿Qué disponibilidad tiene el cliente para dar feedback?

La elección del ciclo no debería realizarse por preferencia personal del equipo, sino por las características concretas del proyecto.

---

# 7. Prototipos

Un **prototipo** es una herramienta para entender y validar requisitos.

No es un modelo de ciclo de vida en sí mismo y puede utilizarse dentro de distintos ciclos.

Su objetivo es evitar congelar requisitos que fueron mal comprendidos.

El usuario interactúa con el prototipo y puede descubrir necesidades que no habían sido identificadas inicialmente.

## Tipos de prototipos

### 7.1. Maqueta

Representación principalmente visual.

Características:

- muestra entradas, salidas y pantallas;
- utiliza datos simples o estáticos;
- permite discutir interacción y apariencia;
- normalmente no contiene lógica funcional.

Útil para validar interfaces y necesidades básicas.

---

### 7.2. Prototipo desechable

Se construye rápidamente para probar aspectos inciertos del sistema.

Características:

- es funcional;
- puede utilizar datos reales;
- se concentra en partes mal entendidas;
- se utiliza para obtener feedback;
- posteriormente se descarta.

No necesita cumplir los estándares técnicos del producto final porque su código no será reutilizado.

---

### 7.3. Prototipo evolutivo

Se construye una primera versión funcional y luego se la mejora hasta convertirla en el producto definitivo.

Características:

- parte de aspectos bien comprendidos;
- cada versión agrega o refina funcionalidades;
- el prototipo no se descarta;
- debe respetar desde el inicio una calidad compatible con el producto final.

### Diferencia principal

| Desechable | Evolutivo |
|---|---|
| Sirve para aprender | Sirve para aprender y construir |
| Se descarta | Evoluciona al producto final |
| Puede hacerse rápidamente sin cuidar arquitectura final | Debe construirse con estándares sostenibles |
| Menor costo inicial | Mayor inversión inicial |

---

# 8. Método de Davis / Davids y Alexander

El método propone seleccionar el ciclo de vida utilizando criterios objetivos en lugar de decidir intuitivamente.

Se analizan **20 criterios** relacionados con el proyecto y se determina cuál de los tres modelos se adapta mejor.

## Procedimiento general

1. **Identificar / analizar los criterios**
2. **Evaluar cada criterio**
3. **Asignar valores**
4. **Transformar los valores según las matrices de selección**
5. **Sumar los resultados**
6. **Seleccionar el modelo con mayor puntaje**

En el material de clase también se presenta una versión conceptual en cuatro etapas:

1. Identificación
2. Evaluación
3. Ponderación
4. Selección

La idea central es la misma:

> La elección del modelo debe estar respaldada por características concretas del proyecto.

---

# 9. Los 20 criterios de Davis y Alexander

## A. Personal / Usuarios y equipo

### C1. Experiencia de los usuarios en el dominio

Cuánto conocen los usuarios el negocio o problema.

### C2. Habilidad del usuario para expresar necesidades

Qué tan bien pueden comunicar sus requerimientos.

### C3. Experiencia de los desarrolladores en el dominio

Cuánto entiende el equipo sobre el negocio.

### C4. Experiencia de los desarrolladores en Ingeniería de Software

Conocimiento de:

- tecnologías;
- herramientas;
- métodos;
- técnicas;
- lenguajes.

---

## B. Problema

### C5. Madurez de la aplicación

Determina si se trata de un dominio bien conocido o de un área nueva.

### C6. Complejidad del problema

Dificultad intrínseca del problema a resolver.

### C7. Necesidad de funcionalidad parcial

Evalúa si resulta útil o necesario entregar partes funcionales antes del producto completo.

### C8. Frecuencia de cambios

Qué tan seguido cambia el problema o los requisitos.

### C9. Magnitud de cambios

Qué tan grandes son los cambios esperados.

---

## C. Producto

### C10. Tamaño del producto

Tamaño estimado del software final.

### C11. Complejidad del producto

Complejidad técnica del software.

### C12. Requisitos no funcionales

Incluye aspectos como:

- fiabilidad;
- adaptabilidad;
- usabilidad;
- reutilización;
- mantenimiento.

### C13. Requisitos de interfaz humano-computadora

Importancia y criticidad de la interfaz de usuario.

---

## D. Recursos

### C14. Perfil de financiación

Estabilidad o variabilidad de los fondos durante el proyecto.

### C15. Disponibilidad de fondos

Si el presupuesto disponible resulta suficiente.

### C16. Perfil del personal

Cómo varía la cantidad de personas disponibles durante el proyecto.

### C17. Disponibilidad del personal

Disponibilidad real de los miembros del equipo.

### C18. Accesibilidad a usuarios

Qué tan fácil es que el equipo interactúe con usuarios o stakeholders.

---

## E. Organización

### C19. Compatibilidad con la dirección

Qué tan compatible es el modelo de proceso con la forma de trabajar de la organización.

### C20. Compatibilidad con gestión y control de calidad/configuración

Evalúa la compatibilidad del proceso con:

- garantía de calidad;
- gestión de configuración;
- procedimientos internos.

---

# 10. Lectura práctica de los criterios

Algunos patrones importantes:

- **Requisitos claros y estables** → favorecen Tradicional o Incremental.
- **Requisitos inciertos o cambiantes** → favorecen Evolutivo.
- **Necesidad de entregas parciales** → favorece Incremental o Evolutivo.
- **Alta criticidad** → favorece procesos más formales.
- **Cliente disponible para feedback** → posibilita Evolutivo.
- **Cliente poco disponible** → dificulta ciclos altamente iterativos.
- **Equipo con poca experiencia en el dominio** → conviene aprender mediante ciclos cortos.
- **Presupuesto rígido** → favorece un alcance más definido.
- **Mercado cambiante** → favorece Evolutivo.

---

# 11. Modelo de negocio

Un **modelo de negocio** define cómo una empresa:

- crea valor;
- entrega valor;
- captura valor;
- genera ingresos.

En términos simples, responde preguntas como:

- ¿A quién le cobro?
- ¿Por qué me paga?
- ¿Cuánto le cobro?
- ¿Cuándo le cobro?
- ¿Cómo distribuyo el producto o servicio?
- ¿Qué recursos necesito?
- ¿Qué costos tengo?

---

# 12. Las dos grandes familias: Producto vs. Servicio

## Producto

Existe un activo tangible o digital que puede venderse, licenciarse o replicarse.

Ejemplos:

- software empaquetado;
- videojuegos;
- hardware;
- plataformas propias.

### Ventaja clave

En software, el costo de producir una copia adicional puede ser muy bajo, por lo que el producto puede escalar.

---

## Servicio

Se vende tiempo, conocimiento o una acción.

Ejemplos:

- desarrollo a medida;
- consultoría;
- soporte;
- agencias;
- servicios IT.

El tiempo no puede almacenarse: una hora no utilizada se pierde.

La tecnología permite escalar servicios mediante plataformas, como ocurre en modelos similares a Uber, Airbnb, Rappi o Globant.

---

# 13. Modelos de negocio tecnológicos vistos en clase

## 13.1. Freemium

Una parte del producto es gratuita y las funciones avanzadas requieren pago.

### Lógica

**Muchos usuarios gratuitos → una minoría paga → los premium financian el sistema**

Ejemplos vistos:

- Spotify
- Notion
- Canva
- Dropbox
- Duolingo
- Zoom

### Ventaja

Facilita la adopción masiva.

### Riesgo

Se necesita suficiente escala y una buena conversión de usuarios gratuitos a pagos.

---

## 13.2. Suscripción / SaaS

El usuario paga periódicamente para acceder al software.

Puede ser:

- mensual;
- anual;
- por plan;
- por usuario.

Ejemplos:

- Microsoft 365
- Adobe Creative Cloud
- Netflix

### Ventaja principal

Ingresos **recurrentes y predecibles**.

El foco deja de ser solamente vender y pasa a ser **retener al cliente**.

---

## 13.3. Licencia / Pago único

El cliente paga una vez por el derecho a utilizar el software.

Ejemplos históricos:

- AutoCAD clásico;
- Photoshop pre-Creative Cloud;
- software corporativo instalado localmente;
- videojuegos tradicionales.

### Ventaja

Cobro inmediato.

### Desventaja

Los ingresos futuros dependen de nuevas ventas, soporte o nuevas versiones.

---

## 13.4. Cobro por hora o paquete de horas

Muy utilizado en:

- consultoría;
- desarrollo a medida;
- soporte.

### Por hora

Se factura el tiempo efectivamente utilizado.

### Paquete de horas

El cliente compra anticipadamente un bloque de horas.

Esto da mayor previsibilidad al proveedor y mantiene cierta flexibilidad para el cliente.

---

## 13.5. Publicidad

El usuario utiliza el producto gratuitamente.

La empresa monetiza vendiendo la atención de los usuarios a anunciantes.

Ejemplos:

- Google;
- Meta;
- TikTok;
- X;
- Spotify Free.

### Requisito central

Escala masiva de usuarios.

---

## 13.6. Marketplace / Comisión

La plataforma conecta oferta y demanda y cobra una comisión sobre las transacciones.

Ejemplos:

- MercadoLibre;
- Airbnb;
- Uber;
- Rappi;
- Workana.

### Concepto clave: efecto red

Cuantos más usuarios existen de un lado del mercado, más atractiva se vuelve la plataforma para el otro lado.

Esto genera un círculo:

**más compradores → más vendedores → más oferta → más compradores**

---

# 14. Ejemplos de empresas tecnológicas

La clase muestra que las empresas tecnológicas exitosas suelen combinar modelos.

Patrones frecuentes:

## Cloud Computing

Ejemplos:

- AWS;
- Azure;
- Google Cloud.

Infraestructura ofrecida como servicio mediante ingresos recurrentes.

## Hardware + Software

Ejemplos:

- Apple;
- Nvidia;
- Tesla.

El hardware genera la entrada del usuario al ecosistema y el software aumenta retención, diferenciación y margen.

## Publicidad digital

Ejemplos:

- Google;
- Meta.

Servicios gratuitos permiten generar atención masiva que luego se monetiza mediante anunciantes.

---

# 15. Casos argentinos vistos

## Globant

Modelo principal:

- servicios de software / consultoría IT.

## MercadoLibre

Combina:

- marketplace;
- fintech;
- pagos;
- logística;
- crédito.

Es un buen ejemplo de producto que evolucionó según las necesidades del mercado latinoamericano.

## Otros casos mencionados

- Satellogic
- Ualá
- Despegar
- Workana
- Pomelo
- Mural

---

# 16. Patrones de equipos pequeños que funcionan

La clase destaca tres ideas.

## 1. Resolver un dolor real

Los fundadores suelen conocer el problema porque ellos mismos lo sufrieron.

## 2. Usar la red inicial

Los primeros clientes suelen provenir de:

- contactos;
- universidad;
- LinkedIn;
- comunidades;
- meetups;
- network profesional.

## 3. Validar con clientes reales

Un cliente dispuesto a pagar valida mejor el problema que una idea teórica.

> Antes de escalar o buscar inversión, conviene comprobar que alguien realmente pagaría por la solución.

---

# 17. Relación entre ciclo de vida y modelo de negocio

Una de las ideas más importantes de la clase es que ambos conceptos están relacionados.

| Ciclo de vida | Negocios típicos | Monetización frecuente |
|---|---|---|
| Tradicional | Software regulado, embebido, defensa | Licencia / pago único |
| Incremental | ERP, home banking, Enterprise SaaS | Suscripción / licencia |
| Evolutivo | Startups, apps de consumo, marketplaces | Freemium / publicidad / comisión |

Estas combinaciones **no son obligatorias**. Una empresa madura puede utilizar múltiples modelos simultáneamente.

Sin embargo, al comenzar un proyecto, elegir de forma coherente el ciclo de vida y el modelo de negocio ayuda a reducir riesgo.

---

# 18. Ciclo de vida, forma de cobro y valor hora

El ciclo de vida afecta directamente la economía del proyecto.

Puede condicionar:

## Cómo cobrás

- por proyecto;
- por entrega;
- por sprint;
- por hora;
- por suscripción;
- por comisión.

## Cuándo cobrás

- anticipado;
- durante el desarrollo;
- al finalizar;
- periódicamente.

## Cuánto cobrás

Una mala estimación puede hacer que una tarifa aparentemente alta termine siendo muy baja cuando se consideran las horas reales.

Ejemplo conceptual de la clase:

Si se facturan pocas horas pero se trabajan muchas horas adicionales no registradas, el **valor hora real** cae significativamente.

Por eso:

> **Sin medir las horas reales, no puede evaluarse correctamente la rentabilidad del proyecto.**

---

# 19. Ideas clave para examen o repaso

## Diferencia Tradicional vs. Incremental

En ambos puede conocerse todo el alcance.

La diferencia es:

- Tradicional → una única entrega.
- Incremental → varias entregas planificadas.

## Diferencia Incremental vs. Evolutivo

- Incremental → sé desde el inicio qué incrementos voy a construir.
- Evolutivo → las próximas funcionalidades se definen durante el proyecto.

## Prototipo vs. ciclo de vida

- Ciclo de vida → estructura general del proyecto.
- Prototipo → herramienta para comprender o validar requisitos.

## Prototipo desechable vs. evolutivo

- Desechable → se usa para aprender y luego se elimina.
- Evolutivo → se transforma gradualmente en el producto final.

## Producto vs. servicio

- Producto → se vende o licencia algo replicable.
- Servicio → se vende tiempo, conocimiento o ejecución.

## Modelo de negocio

Define cómo la empresa captura valor económico del software.

---

# 20. Checklist para elegir ciclo de vida

Antes de empezar un proyecto, preguntarse:

- [ ] ¿Conozco todo el alcance?
- [ ] ¿Los requisitos son estables?
- [ ] ¿El problema puede dividirse?
- [ ] ¿Cada entrega parcial genera valor?
- [ ] ¿Necesito feedback frecuente?
- [ ] ¿El cliente estará disponible?
- [ ] ¿El producto es innovador?
- [ ] ¿Hay regulación o alta criticidad?
- [ ] ¿El presupuesto es fijo?
- [ ] ¿El mercado puede cambiar rápidamente?
- [ ] ¿El equipo conoce el dominio?
- [ ] ¿El equipo domina la tecnología?
- [ ] ¿Necesito salir rápido al mercado?

### Regla rápida

```text
¿Conozco todo el alcance?
│
├── NO → Evolutivo
│
└── SÍ
    │
    ├── ¿Puedo dividir el producto en entregas con valor?
    │   ├── SÍ → Incremental
    │   └── NO → Tradicional
```

---

# 21. Conclusiones

La clase conecta tres dimensiones:

## Ciclo de vida

Define:

- fases;
- entregas;
- estimación;
- riesgo.

## Modelo de negocio

Define:

- cómo se cobra;
- cuándo se cobra;
- quién paga;
- escalabilidad.

## Valor hora

Depende de:

- medir correctamente;
- estimar correctamente;
- evitar trabajo no contemplado;
- elegir un modelo coherente con el proyecto.

La principal conclusión es:

> **Elegir cómo construir software también es elegir cómo generar valor y cómo capturarlo económicamente.**

Antes de escribir la primera línea de código conviene definir conscientemente:

1. qué problema se está resolviendo;
2. qué ciclo de vida se adapta al proyecto;
3. cómo se validará el producto con usuarios;
4. cuál será el modelo de negocio;
5. cómo se medirá el trabajo real.
