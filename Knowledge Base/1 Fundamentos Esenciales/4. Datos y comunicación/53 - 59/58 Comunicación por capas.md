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