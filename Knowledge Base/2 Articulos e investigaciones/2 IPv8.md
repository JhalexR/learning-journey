# IPv8 

### 1. El problema: el agotamiento de IPv4

El espacio de direcciones `IPv4` (`32 bits`) se agotó hace años. Desde entonces:

+ Ya no existen bloques IPv4 nuevos para asignar.
+ Las direcciones IPv4 se compran y venden en un mercado secundario.
+ Muchos proveedores utilizan CGNAT (Carrier-Grade NAT) para que varios usuarios compartan una misma dirección IPv4 pública.

Esto provoca problemas como:

+ dificultades para aplicaciones P2P
+ Geolocalización menos precisa
+ Mayor complejidad en la administración de redes
+ aumento de la complejidad operativa.

### 2. ¿Por qué IPv6 no ha reemplazado completamente a IPv4?

+ Aunque **IPv6** fue diseñado para resolver la escasez de direcciones, su adopción ha sido más lenta de lo esperado.
+ El argumento principal es que **IPv6** requiere una transición mediante doble pila (`dual stack`), donde equipos y redes deben soportar simultáneamente **IPv4** e **IPv6** durante muchos años, lo que _incrementa los costos y la complejidad operativa._

### 3. ¿Qué propone IPv8?

La propuesta consiste en crear un protocolo con direcciones de 64 bits, escritas como:
+ r.r.r.r.n.n.n.n

donde:
+ los primeros 32 bits representarían el **ASN** (_Autonomous System Number_),
+ los últimos 32 bits serían la dirección **IPv4** tradicional.
+ La idea central es que IPv4 sea un subconjunto de IPv8
+ Según la propuesta, esto permitiría mantener compatibilidad con la infraestructura IPv4 existente.

### 4. Compatibilidad con IPv4

La transición sería más sencilla que con **IPv6** porque:

+ no sería necesario reemplazar inmediatamente todos los routers
+ no habría una migración obligatoria de toda la red
+ IPv4 seguiría funcionando como parte del nuevo protocolo.

Esta retrocompatibilidad es presentada como la principal ventaja de **IPv8** frente a **IPv6**.

### 5. Más espacio de direcciones

+ Al utilizar 64 bits, el espacio de direcciones aumentaría enormemente respecto a **IPv4**.
+ Esto eliminaría el problema del agotamiento de direcciones y reduciría la necesidad de mecanismos como **CGNAT**.

### 6. Cambios en el enrutamiento

La propuesta también plantea modificar la forma en que funciona el enrutamiento en Internet.

+ las rutas se organizarían alrededor de los ASN
+ las tablas BGP serían más pequeñas y fáciles de administrar
+ se reduciría la cantidad de prefijos anunciados globalmente.

Todo esto buscaría simplificar la operación de Internet a gran escala.

### 7. Mecanismo de transición

+ Los dispositivos intentarían determinar automáticamente si el equipo remoto entiende **IPv8** o solo **IPv4**.
+ Es un mecanismo denominado **ARP8**

Dependiendo de la respuesta:

+ Si ambos soportan **IPv8** -> se comunicarían usando **IPv8**
+ Si el destino solo soporta **IPv4** -> continuarían utilizando **IPv4**.

El objetivo es evitar interrupciones durante una transición gradual.

### 8. Plataforma de gestión integrada

Además del direccionamiento, la propuesta incorpora otros componentes para la administración de redes, entre ellos:

+ WHOIS8
+ Zone Server
+ DNS8
+ mecanismos de autenticación
+ telemetría
+ validación de rutas

La idea es integrar varias funciones de operación y seguridad en una única plataforma de gestión.

### 9. Limitaciones reconocidas por el propio artículo

El sitio también dedica una sección a explicar algunos desafíos importantes de **IPv8**:

+ depende de nuevos componentes como **WHOIS8** y **Zone Server**
+ aún no existen implementaciones comerciales ampliamente disponibles
+ puede generar cambios importantes en la forma de administrar redes
+ tendría que competir con un ecosistema **IPv6** ya desplegado en muchos entornos
+ actualmente es solo un borrador individual del **IETF**, sin respaldo de un grupo de trabajo oficial.

### Estado actual

**IPv8** no está implementado en Internet.

Actualmente:

+ no es un estándar **RFC**
+ no está soportado por routers comerciales
+ no lo utilizan los **ISP**
+ no reemplaza a **IPv4** ni a **IPv6**.

+ Se trata de una `propuesta técnica` que necesitaría:
    + Revisión
    + Consenso 
    + Implementación 
        + Antes de poder convertirse en un estándar.

### Ideas clave

+ **IPv8** como una propuesta para solucionar el agotamiento de **IPv4** mediante un protocolo de `64` bits que mantiene compatibilidad con **IPv4**
+ Sus objetivos son: 
    + Ampliar el espacio de direcciones, simplificar la transición respecto a **IPv6**
    + Reducir la complejidad del enrutamiento
    + Integrar funciones de gestión y seguridad

+ Pero sigue siendo un **Internet-Draft** individual del **IETF**, _sin adopción oficial_ ni despliegue en la Internet actual

> Rojano, E. (no date) El protocolo que resuelve el agotamiento de IPv4, IPv8. Available at: https://ipv8.es/ (Accessed: 30 July 2026). 