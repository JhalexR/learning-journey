# Comunicación por capas

Para organizar una red grande se utilizan modelos por capas.

Cada capa:

+ Tiene responsabilidades específicas.
+ Utiliza los servicios de la capa inferior.
+ Ofrece servicios a la capa superior.

Esto hace que las redes sean:

+ Modulares
+ Más fáciles de mantener
+ Más fáciles de actualizar.

### Encapsulamiento

+ Cuando los datos bajan por las capas
    + Cada capa agrega un encabezado con información propia del protocolo.
        + Este proceso recibe el nombre de → **Encapsulamiento**

## Modelo OSI

El modelo OSI divide la comunicación en 7 capas.

### 7. Aplicación
+ Permite que las aplicaciones utilicen la red.

### 6. Presentación
Se encarga de:
+ Traducción de formatos
+ Codificación
+ Cifrado
+ Compresión

### 5. Sesión

Administra la comunicación entre aplicaciones.

Controla:

+ Inicio
+ Mantenimiento
+ Finalización de la comunicación

### 4. Transporte

Garantiza una transferencia confiable.

Funciones:

+ Segmentación
+ Reensamblado
+ Control de errores
+ Control del flujo

Aquí trabajan protocolos como **TCP** y **UDP**.

### 3. Red

Se encarga del:

+ Direccionamiento
+ Enrutamiento

Hace posible la comunicación entre redes diferentes.

### 2. Enlace de datos

Realiza:

+ Detección de errores
+ Corrección de errores
+ Comunicación entre dispositivos de la misma red

### 1. Física

Es la capa que transmite realmente los bits utilizando:

+ Cables
+ Señales eléctricas
+ Señales ópticas
+ Ondas electromagnéticas.

## Modelo TCP/IP

Es el modelo utilizado realmente en Internet.

Tiene solo 4 capas:

1. Aplicación
2. Transporte
3. Internet
4. Acceso a la red

Este modelo agrupa varias capas del modelo OSI.

### TCP/IP estándar práctico usado en Internet

### Capa Aplicación

Esta compuesta por los protocolos y servicios que interactúan directamente con el usuario o las aplicaciones finales.

+ Protocolos de aplicación (categoría general)
+ HTTP, FTP, SMTP
+ POP3 e IMAP (correo electrónico)
+ TELNET (acceso remoto)
+ SNMP (gestión y monitoreo de red)
+ DNS (Domain Name System) y Nombres de Dominio
+ URL (Localizador Uniforme de Recursos)

### Capa 5 y 6 OSI - Sesión y Presentación -> En el modelo TCP/IP

estas capas suelen integrarse dentro de la capa de **aplicación**, pero conceptualmente actúan como puente entre la aplicación y el transporte.

+ Sockets: La interfaz/puerta de enlace entre la capa de transporte (puertos) y las aplicaciones.

### Capa Transporte

Aquí van los temas enfocados en la comunicación de extremo a extremo (host a host), confiabilidad, control de flujo y multiplexación.

+ El protocolo de control de transferencia (TCP)
+ UDP (User Datagram Protocol)
+ Puertos (de la dupla "IP y puertos")
+ Apertura de la conexión TCP (HandShake)
+ Número de secuencia y ACK
+ Ventana (TCP)
+ Métodos de retransmisión:
+ Go Back - N
+ Selective Repeat
+ Transferencia de datos (mecanismos de confiabilidad y control de flujo)

### Capa - Red

+ **IP** (_IPv4_ e _IPv6_) (de la dupla "_IP y puertos_")
+ **VLSM** (_Variable Length Subnet Mask_) / Máscaras de subred de tamaño variable
+ **Los enrutadores** (dispositivos principales de Capa 3)
+ Conceptualización de los protocolos de enrutamiento **IPv4** e **IPv6**:
    + **RIP** (_Routing Information Protocol_)
    + **OSPF** (_Open Shortest Path First_)
    + **BGP** (_Border Gateway Protocol_)

### Correspondencia OSI – TCP/IP

| Modelo OSI                         | Modelo TCP/IP   |
| ---------------------------------- | --------------- |
| Aplicación + Presentación + Sesión | Aplicación      |
| Transporte                         | Transporte      |
| Red                                | Internet        |
| Enlace + Física                    | Acceso a la red |

## RFC e IETF

+ Los protocolos TCP/IP son abiertos.
+ Sus especificaciones se publican en documentos llamados RFC (Request for Comments).
+ Estos documentos son administrados por la IETF (Internet Engineering Task Force)