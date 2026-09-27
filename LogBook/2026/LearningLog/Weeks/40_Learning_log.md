#### 27/09/2026

<details>
<summary>expandir</summary>

##### Hoy aprendí

### APIs y Comunicación entre Sistemas

**¿Qué es una API?
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