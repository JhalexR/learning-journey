#### 27/09/2026

<details>
<summary>expandir</summary>

##### Hoy aprendí

### APIs y Comunicación entre Sistemas

**¿Qué es una API?**
+ Entre dos sistemas independientes; Acceder directamente a la base de datos **sería una mala arquitectura**
+ Una API funciona como un contrato de comunicación: 
	+ La aplicación no necesita acceder directamente a la base de datos. -> En cambio, realiza una solicitud a la API
+ La **API** establece una **interfaz controlada** entre ambos sistemas.
+ cada sistema debe **mantener su propia implementación interna**
+ **API y API HTTP** -> no son exactamente lo mismo
	+ `API` es un concepto general de una interfaz que permite que dos programas se comuniquen -> Puede estar dentro de un mismo sistema operativo, o en un software de computadora sin necesidad de internet
	+ **`API HTTP` es un tipo específico de API que funciona exclusivamente a través de internet usando el protocolo HTTP** 
	+ Naturaleza ligera:  suele ser más rápida, directa y económica de implementar que otros tipos de servicios web
+ La `API` es una parte de la arquitectura, no necesariamente un programa independiente.
+ REST, GraphQL y gRPC no son simplemente "tres versiones de HTTP". Cada uno tiene una forma diferente de diseñar la comunicación entre sistemas.
+ **Una API no es solamente un endpoint** -> Una URL o endpoint puede formar parte de una API, pero una API es mucho más amplia.

**Estilos de API**
| Estilo      | Idea principal                                                                                  |
| ----------- | ----------------------------------------------------------------------------------------------- |
| **REST**    | Trabajar con recursos mediante una interfaz uniforme                                            |
| **GraphQL** | El cliente especifica exactamente los datos que necesita                                        |
| **gRPC**    | Comunicación basada en llamadas a procedimientos/servicios, con contratos fuertemente definidos |

+ **REST** es un _estilo arquitectónico_ para diseñar sistemas que se comunican mediante una red.
	+ **RESTful API** -> una `API` que sigue los principios de **REST**

La API no debería diseñarse pensando principalmente en:
> "¿Qué funciones tiene mi programa?"
sino en:
> "¿Qué recursos estoy exponiendo y cómo se relacionan?"
Esta diferencia es fundamental.
+ **REST** no necesariamente expone directamente el objeto interno del servidor -> Expone una representación del recurso.
+ **REST** no significa que el sistema no tenga datos ni estados.
+ **Uniform Interface.** -> La idea es que los recursos se manipulen mediante una interfaz consistente y predecible.
+ **REST** también establece una separación entre Cliente y Servidor.
	+ El cliente se ocupa principalmente de la interacción con el usuario.
	+ El servidor se ocupa de proporcionar los datos y servicios.
	+ **Esto permite que diferentes clientes consuman la misma API.**

+ **REST** también permite una arquitectura organizada en capas.
+ **Idempotencia** Una operación es idempotente cuando realizarla varias veces produce el mismo efecto final que realizarla una sola vez.
	+ **Idempotencia** -> tiene importantes implicaciones en _**sistemas distribuidos**_.
+ **REST no significa CRUD** -> **REST** es un estilo arquitectónico mucho más amplio.
+ `REST` **no obliga a utilizar JSON.**
+ **HATEOAS** -> La idea es que una representación de un recurso puede incluir enlaces hacia las acciones o recursos relacionados que el cliente puede seguir.
+ ¿Qué hace que una API sea RESTful?
```
API RESTful
│
├── Recursos identificables
│
├── Representaciones
│
├── Interfaz uniforme
│
├── Cliente / servidor separados
│
├── Stateless
│
├── Cacheable
│
├── Arquitectura por capas
│
└── HATEOAS
```
</details>


#### 28/09/2026

<details>
<summary>expandir</summary>

##### Hoy aprendí

### Diseño práctico de una API RESTful

+ Diseñar primero los recursos
+ Nombrar recursos correctamente
	+ **Una buena práctica es utilizar sustantivos, no verbos.**
+ No utilizar acciones en las URLs
+ breaking change -> Es un cambio que puede hacer que un consumidor existente deje de funcionar correctamente.
+ Checklist para diseñar una API RESTful
**Recursos**

¿Cuáles son las entidades principales?
¿Están claramente identificadas?
¿Estoy utilizando sustantivos?

**URLs**
+ ¿Las rutas son consistentes?
+ ¿Distinguen colecciones y recursos individuales?
+ ¿Las relaciones están representadas de forma clara?
+ ¿Estoy evitando anidamientos innecesarios?

**Métodos**
+ ¿Estoy utilizando correctamente GET, POST, PUT, PATCH y DELETE?
+ ¿Estoy considerando la idempotencia?

**Consultas**
+ ¿Tengo filtros?
+ ¿Búsqueda?
+ ¿Ordenamiento?
+ ¿Paginación?

**Respuestas**
+ ¿Las estructuras son consistentes?
+ ¿Los códigos HTTP representan correctamente el resultado?
+ ¿Los errores tienen un formato uniforme?

**Evolución**
+ ¿Cómo manejaré breaking changes?
+ ¿Tengo una estrategia de versionado?

**Documentación**
+ ¿Otro desarrollador podría utilizar mi API sin preguntarme cómo funciona?

+ Cuando estés diseñando una API REST, piensa en este orden:

```
          1. ¿Qué recursos tengo?
                     ↓
          2. ¿Cómo los identifico?
                     ↓
          3. ¿Cómo se relacionan?
                     ↓
          4. ¿Qué operaciones necesito?
                     ↓
          5. ¿Qué datos recibe/devuelve?
                     ↓
          6. ¿Cómo filtro y pagino?
                     ↓
          7. ¿Cómo manejo errores?
                     ↓
          8. ¿Cómo evolucionará la API?
                     ↓
          9. ¿Cómo la documento?
```

**GraphQL**
+ Es un lenguaje de consulta para **APIs** y también una especificación para ejecutar esas consultas sobre los datos de un servidor.
+ La idea fundamental de **GraphQL** es diferente a la de una **API REST** tra+dicional:
	+ **En GraphQL, el cliente puede especificar exactamente qué datos necesita.**
+ `GraphQL` y `REST` son **formas diferentes de diseñar APIs.**
+ **Over-fetching** -> Significa recibir más información de la que realmente necesitas.
+ **Under-fetching** -> Significa lo opuesto a **Over-fetching**
+ **GraphQL** intenta solucionar es el **over-fetching.**

####conceptos que maneja **GraphQL** 
+ **GraphQL** maneja el concepto de **Schema** -> significa: qué datos y operaciones están disponibles en la **API** y qué tipos tienen.
+ **GraphQL** utiliza un **sistema de tipos** -> y es fuertemente tipado
+ **GraphQL** es adecuado para representar **datos relacionados**.
+ maneja **Objetos**
+ maneja **Queries** -> consultas
+ maneja **Mutations** -> modifica datos 
+ maneja **Subscriptions** -> Su objetivo es permitir recibir actualizaciones cuando ocurre determinado evento.
+ **El concepto de resolver** -> Un resolver es la lógica que determina cómo obtener el valor de un campo solicitado.
+ **GraphQL** puede combinar múltiples fuentes -> puede coordinar la obtención de información desde diferentes puntos 
	+ Esto resulta especialmente interesante en arquitecturas con múltiples servicios.
+ muchas **APIs GraphQL** utilizan `un endpoint principal para las consultas`
	+ El endpoint puede ser el mismo, pero la consulta cambia.
+ **selección explícita de campos** -> La consulta puede navegar por las relaciones definidas en el schema.
+ **Variables** -> Las consultas no tienen que contener valores directamente.
+ **Validación antes de ejecutar** -> Gracias al schema y al sistema de tipos, una consulta puede validarse.
+ **GraphQL** tiene un modelo de **errores parciales**.

### GraphQL y REST no son mutuamente excluyentes

</details>