## REST — Representational State Transfer

### 1. ¿Qué es REST?

**REST** significa _Representational State Transfer_.

**REST** es un _estilo arquitectónico_ para diseñar sistemas que se comunican mediante una red.

Esto es importante:

Es un conjunto de **principios y restricciones arquitectónicas** que permiten diseñar `APIs` de manera consistente.

**RESTful API**

+ Se usa para referirnos a una `API` que sigue los principios de **REST**.

### 2. La idea fundamental de REST

La idea central de REST es que un sistema expone **recursos** que pueden ser identificados y manipulados mediante una interfaz uniforme.

Por ejemplo, una aplicación de una tienda:

**Recursos"
```
Usuarios
Productos
Pedidos
Categorías
Reseñas
```

Cada recurso puede tener una representación accesible mediante la API.

```
/users
/products
/orders
/reviews
```

Podemos imaginarlo así:

```mermaid

flowchart 

A((API 
REST
))
B((Users))
C((Products))
D((Orders))
E((/users))
F((/products))
G((/orders))
 
A --> C
A --> B
A --> D 
B --> E
C --> F
D --> G

style A fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style B fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style C fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style D fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style E fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style F fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style G fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
```

La API no debería diseñarse pensando principalmente en:

**"¿Qué funciones tiene mi programa?"**

sino en:

**"¿Qué recursos estoy exponiendo y cómo se relacionan?"**

Esta diferencia es fundamental.

### 3. Recursos

Un recurso es cualquier entidad que el sistema puede identificar y gestionar.

```
Usuario
Producto
Pedido
Factura
Comentario
Categoría
```

+ Supongamos que tenemos: `Producto #25` -> Podríamos identificarlo mediante: `/products/25`

+ Mientras que todos los productos podrían estar representados por: `/products` Por tanto: `/products` representa la colección de productos. -> Y `/products/25` representa un producto específico.

**Ejemplo**

```
/products
/products/10
/products/25
/products/80
```

Conceptualmente:

```
/products
    │
    ├── 10
    ├── 25
    └── 80
```

### 4. Recursos vs. acciones

Esta es una de las diferencias más importantes al diseñar REST.

Una **API** tradicional podría diseñarse así:

```
/getUsers
/createUser
/deleteUser
/updateUser
```

Aquí los endpoints están expresando acciones.

`REST` propone representar principalmente recursos:

```
/users
/users/25
```

Y utilizar el método HTTP para indicar la operación.

Por ejemplo:

| Operación            | Recurso     |
| -------------------- | ----------- |
| Obtener usuarios     | `/users`    |
| Obtener usuario 25   | `/users/25` |
| Crear usuario        | `/users`    |
| Modificar usuario 25 | `/users/25` |
| Eliminar usuario 25  | `/users/25` |

El verbo ya está expresado mediante HTTP.

Por eso normalmente evitamos:

```
/createUser
/deleteUser
/updateUser
```

y preferimos:

```
POST   /users
DELETE /users/25
PUT    /users/25
```

### 5. Identificación de recursos

Cada recurso debería poder identificarse de manera clara.

Por ejemplo:

```
/users
/users/15

/products
/products/827

/orders
/orders/5001
```

También podemos tener relaciones entre recursos:

`/users/15/orders`

que conceptualmente significa:
> Los pedidos asociados al usuario 15.

O:

`/orders/5001/items`
> Los elementos que pertenecen al pedido 5001.

Esto permite expresar relaciones entre recursos mediante la estructura de la `API`.

### 6. Representaciones

Aquí aparece una palabra muy importante de **REST**:

**Representation — Representación**

**REST** no necesariamente expone directamente el objeto interno del servidor.

Expone una representación del recurso.

Por ejemplo, internamente el servidor podría tener:

```
User
├── id
├── name
├── email
├── passwordHash
├── createdAt
└── internalMetadata
```

Pero la API podría representar ese usuario así:

```JSON
{
  "id": 15,
  "name": "Juan",
  "email": "juan@example.com"
}
```

Esta es una representación del recurso.

El recurso real existe dentro del sistema, mientras que el cliente recibe una representación de él.

### 7. ¿Por qué se llama Representational State Transfer?

El nombre puede parecer complicado, pero podemos dividirlo:

**Representational**

El cliente recibe una representación del recurso

```JSON
{
  "id": 15,
  "name": "Juan"
}
```

**State**

La representación refleja un determinado estado del recurso.

```
Usuario 15
Nombre: Juan
Estado: activo
```

Si posteriormente el usuario cambia su nombre:

```
Usuario 15
Nombre: Carlos
Estado: activo
```

la representación cambia.

**Transfer**

Esa representación se **transfiere entre cliente y servidor**.

```
Servidor
   │
   │ representación
   ▼
Cliente
```

Por eso:
> Representational State Transfer = transferencia de representaciones del estado de recursos.

### 8. La restricción Stateless

Esta es una de las características fundamentales de `REST`.

**Stateless** significa que cada solicitud debe contener la información necesaria para que el servidor pueda procesarla.

El servidor no debería depender de un estado de sesión almacenado entre solicitudes para interpretar qué significa una nueva solicitud.

Por ejemplo:

```mermaid 

flowchart LR

A((Cliente))
B[Request 1 
+ 
información necesaria]
C((Servidor))
D[Después:]
 
A --> B --> C

D

E((Cliente))
F[Request 2 
+ 
información necesaria]
G((Servidor))

E --> F --> G

style A fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style B fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style C fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style E fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
style F fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
style G fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
```

El servidor no debería necesitar recordar:
> "Este cliente hizo anteriormente la solicitud X, por lo tanto ahora debo interpretar Y."

**Cada solicitud debe poder entenderse por sí misma.**

### 9. Stateless no significa "sin estado"

Esta confusión es muy común.

**REST** no significa que el sistema no tenga datos ni estados.

Un servidor puede tener perfectamente:

```
Usuarios
Pedidos
Productos
Sesiones
Configuraciones
```

Lo que significa Stateless es que:
> **el servidor no debe depender del estado de una conversación previa entre cliente y servidor para comprender una solicitud.**

Por ejemplo:

```
Servidor
│
├── Base de datos
│   ├── usuarios
│   ├── productos
│   └── pedidos
│
└── No depende de una sesión conversacional
    para interpretar cada request
```

### 10. Ejemplo de Stateless

Imaginemos una API protegida mediante un token.

El cliente realiza:

```
GET /orders/500
Authorization: Bearer TOKEN
```

El servidor puede utilizar la información de esa solicitud para determinar:

```
¿Quién realiza la solicitud?
        ↓
¿Qué recurso solicita?
        ↓
¿Tiene permiso?
        ↓
¿Qué debe devolver?
```

No necesita depender de que el cliente haya realizado previamente:

`POST /login`

en esa misma conexión o conversación para saber quién es.

El token permite transportar la información necesaria para procesar la solicitud.

### 11. Interfaz uniforme

Otra restricción fundamental de REST es la **Uniform Interface.**

La idea es que los recursos se manipulen mediante una interfaz consistente y predecible.

GET    /products
GET    /products/25
POST   /products
PUT    /products/25
DELETE /products/25

Una persona que conoce REST puede comprender rápidamente qué hace cada operación.

No necesita aprender una función completamente diferente para cada recurso.

Por ejemplo, 

```
GET    /products
GET    /products/25
POST   /products
PUT    /products/25
DELETE /products/25
```

Una persona que conoce REST puede comprender rápidamente qué hace cada operación.

No necesita aprender una función completamente diferente para cada recurso.

sería menos consistente tener:

```
GET /getAllProducts
POST /makeNewProduct
POST /removeProduct
GET /fetchSingleProduct
```

La uniformidad facilita:

+ aprendizaje
+ mantenimiento
+ documentación
+ integración
+ reutilización
+ evolución de la API

### 12. Separación Cliente-Servidor

REST también establece una separación entre Cliente y Servidor.

```mermaid
flowchart TB

    Client["👤 CLIENTE<br/><br/>React / Android<br/>iOS / Desktop"]

    subgraph Server["🖥️ SERVIDOR"]
        direction TB

        Backend["⚙️ Backend"]
        Logic["🧠 Lógica de negocio"]
        DB[("🗄️ Base de datos")]

        Backend --> Logic
        Logic --> DB
    end

    Client -->|"🔌 API"| Server

    classDef client fill:#D9EAD3,stroke:#6AA84F,stroke-width:2px,color:#000;
    classDef backend fill:#D0E0FF,stroke:#3D85C6,stroke-width:2px,color:#000;
    classDef database fill:#EADCF8,stroke:#8E7CC3,stroke-width:2px,color:#000;

    class Client client;
    class Backend,Logic backend;
    class DB database;
```

+ El cliente se ocupa principalmente de la interacción con el usuario.

+ El servidor se ocupa de proporcionar los datos y servicios.

+ **Esto permite que diferentes clientes consuman la misma API.**

```
              API REST
             /    |    \
            /     |     \
           ▼      ▼      ▼
        Web     Android   iOS
```

Los tres clientes pueden utilizar el mismo backend.

### 13. Cacheable

**REST** también establece que las respuestas deberían indicar si pueden ser almacenadas temporalmente en caché.

Esto puede mejorar:

+ rendimiento
+ latencia
+ consumo de red
+ carga del servidor

Por ejemplo

`GET /products/25`

Si el producto cambia muy pocas veces, una respuesta podría ser reutilizada durante determinado período.

```mermaid 

flowchart LR

A((Cliente))
B[GET /products/25]
C((Servidor))
D((Caché))
 
A --> B --> C --> D

style A fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style B fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style C fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style D fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
```

La siguiente solicitud puede evitar una nueva operación contra el servidor dependiendo de las reglas de caché.

Esto es especialmente útil para recursos relativamente estáticos.

### 14. Sistema por capas

**REST** también permite una arquitectura organizada en capas.

Por ejemplo:

```mermaid 

flowchart LR

A((Cliente))
B((API Gateway))
C((Servicio))
D((Base 
de 
datos))
 
A --> B --> C --> D

style A fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style B fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style C fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style D fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
```

El cliente no necesariamente sabe cuántas capas existen detrás de la API.

Puede existir:

```mermaid 

flowchart LR

A((Cliente))
B((Load 
Balancer))
C((API 
Gateway))
D((Servicio 
de 
usuarios))
E((Base 
de 
datos))
 
A --> B --> C --> D --> E

F[o incluso:]

G((Cliente))
H((API))
I((Servicio A))
J((Servicio B))
K((Servicio C))

G --> H --> I --> J --> K

style A fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style B fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style C fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style D fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style E fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;

style G fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
style H fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
style I fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
style J fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
style K fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#10e8c0;
```

Cada capa puede encargarse de una responsabilidad diferente.

### 15. Idempotencia

Este concepto es muy importante en APIs REST.

Una operación es idempotente cuando realizarla varias veces produce el mismo efecto final que realizarla una sola vez.

Por ejemplo:

`PUT /users/25`

con:

```JSON
{
  "name": "Juan"
}
```

Si ejecutamos la misma operación:

+ 1 vez
+ 2 veces
+ 10 veces
+ 100 veces

el estado final debería seguir siendo:

```
Usuario 25
Nombre: Juan
```

No debería convertirse en:

`Juan Juan Juan...`

**Métodos y la idempotencia**

De forma general:

| Método | Idempotente      |
| -------| -----------------|
| GET    | Sí               |
| PUT    | Sí               |
| DELETE | Sí               |
| POST   | No necesariamente| 

Esto tiene importantes implicaciones en _**sistemas distribuidos**_.

Por ejemplo, si una solicitud falla debido a un problema de red, un cliente puede necesitar decidir si es seguro repetirla.

### 16. REST no significa CRUD

**CRUD** significa:

+ Create
+ Read
+ Update
+ Delete

**REST** es un estilo arquitectónico mucho más amplio.

**CRUD** puede encajar muy bien con REST:

```
Create → POST
Read   → GET
Update → PUT/PATCH
Delete → DELETE
```

**REST** también involucra:

+ recursos
+ representaciones
+ interfaz uniforme
+ statelessness
+ separación cliente-servidor
+ cacheabilidad
+ sistema por capas
+ hipermedia/HATEOAS

### 17. REST y JSON

`REST` **no obliga a utilizar JSON.**

Una **API REST** puede utilizar diferentes formatos de representación:

```
JSON
XML
HTML
texto
otros formatos
```

Sin embargo, **JSON es extremadamente común en APIs REST modernas.**

Por ejemplo:

```JSON
{
  "id": 25,
  "name": "Laptop",
  "price": 2500000
}
```

**JSON es un formato de representación frecuente en REST, pero JSON y REST no son sinónimos.**

### 18. HATEOAS

Este es uno de los conceptos más avanzados de **REST**.

Significa:

**Hypermedia As The Engine Of Application State**

La idea es que una representación de un recurso puede incluir enlaces hacia las acciones o recursos relacionados que el cliente puede seguir.

Por ejemplo:

```JSON
{
  "id": 25,
  "name": "Laptop",
  "links": {
    "self": "/products/25",
    "reviews": "/products/25/reviews",
    "category": "/categories/10"
  }
}
```

El cliente obtiene información no solamente sobre el recurso, sino también sobre **qué puede hacer o consultar a continuación**.

Conceptualmente:

```
Producto
   │
   ├── self
   ├── reviews
   └── category
```

**HATEOAS** es parte de la visión original de `REST`, aunque muchas APIs llamadas _"REST"_ en la práctica **no implementan HATEOAS completamente.**

Esto es importante porque en el mundo real encontrarás muchas **APIs** descritas como `RESTful` que siguen solamente una parte de las restricciones `REST`.

### 19. ¿Qué hace que una API sea RESTful?

Ideas principales:

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

**No todas las APIs que utilizan HTTP y JSON cumplen todas estas características.**

Por eso hay una diferencia entre:

+ `API HTTP` y `API RESTful`

Una API puede utilizar HTTP pero no seguir completamente los principios REST.

### 20. Ejemplo completo

Imaginemos una API para una tienda.

**Colección**

`/products`

**Producto individual**

`/products/25`

**Obtener productos**

`GET /products`

**Obtener un producto**

`GET /products/25`

**Crear producto**

`POST /products`

**Actualizar producto**

`PUT /products/25`

**Eliminar producto**

`DELETE /products/25`

Y una respuesta podría ser:

```JSON
{
  "id": 25,
  "name": "Laptop",
  "price": 2500000
}
```

Podemos representar la arquitectura así:

```mermaid 
flowchart 

A((API REST))
B[Products]
C[Orders]
D[Users]
E["/Products"]
F["/Orders"]
G["/Users"]
H["/products/25"]
I["/products/26"]
J["/products/27"]
 
A --> B 
A --> C 
A --> D

B --> E
C --> F
D --> G

E --> H
E --> I
E --> J

style A fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style B fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style C fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style D fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style E fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style F fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style G fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style H fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style I fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
style J fill:#07284d,stroke:#0d2847,stroke-width:1px,color:#00fc0d;
```

### 21. REST vs. API HTTP tradicional

|Característica	                     |API HTTP genérica	|	API RESTful	                |
|------------------------------------|------------------|-------------------------------|
|Utiliza HTTP	                     |Puede       	    |Sí, normalmente                |
|Recursos	                         |No necesariamente	|Sí	                            |
|Interfaz uniforme                   |No necesariamente	|Sí	                            |
|Stateless	                         |No necesariamente	|Sí     	                    |
|JSON                                |Puede	            |Frecuente, pero no obligatorio	|
|Endpoints orientados a recursos     |No necesariamente	|Sí	                            |
|HATEOAS	                         |No	            |Forma parte de REST	        |
|Arquitectura por capas	             |Puede	            |Permitida por REST	            |

### 22. Lo más importante para recordar

### 1. REST es un estilo arquitectónico

No es:

+ ❌ lenguaje
+ ❌ protocolo
+ ❌ framework
+ ❌ librería

Es: ✅ conjunto de restricciones/principios arquitectónicos

### 2. REST piensa en recursos

En lugar de:

```
/createUser
/deleteUser
/updateUser
```

pensamos:

```
/users
/users/25
```

### 3. HTTP proporciona la interfaz de comunicación

+ REST aprovecha mecanismos de HTTP, pero REST no es HTTP.

### 4. Stateless es fundamental

+ Cada solicitud debe contener la información necesaria para ser procesada independientemente de solicitudes anteriores.

### 5. JSON no es REST

+ JSON es simplemente uno de los formatos de representación más utilizados.

### 6. No toda API HTTP es RESTful

+ Puede existir:

`API HTTP ≠ API RESTful`

### Mapa mental

```
                        REST
                          │
           ┌──────────────┼──────────────┐
           │              │              │
       Recursos       Representación   HTTP
           │              │              │
       /users          JSON/XML      GET/POST/...
           │
     ┌─────┴─────┐
     │           │
  Colección    Recurso
  /users       /users/25
     │
     └───────────────┐
                     │
              Restricciones
                     │
       ┌─────────────┼──────────────┐
       │             │              │
   Stateless    Uniform Interface  Cache
       │             │
       └─────────────┼──────────────┘
                     │
              Cliente/Servidor
                     │
                 Capas
                     │
                  HATEOAS
```