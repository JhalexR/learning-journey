# Mecanismos de Manejo
> (Error Handling Mechanisms)

Un mecanismo de manejo de errores es una estrategia que permite a un programa detectar un problema y decidir qué hacer con él sin comportarse de manera inesperada.

Dependiendo del lenguaje de programación, existen distintos mecanismos, pero los dos más importantes y universales son:

+ **Excepciones** _(Exceptions)_
+ **Valores de retorno** _(Return Values)_

Cada uno tiene ventajas, desventajas y casos de uso específicos.

```
                   Ocurre un problema
                           │
                           ▼
                ¿Cómo lo comunica el programa?
                           │
          ┌────────────────┴────────────────┐
          │                                 │
          ▼                                 ▼
    Excepciones                     Valores de retorno
 (try/catch/finally)             (null, false, códigos,
                                    objetos Result, etc.)
```

## Excepciones (try/catch/finally)

Las excepciones son un mecanismo mediante el cual un programa interrumpe temporalmente el flujo normal de ejecución para informar que ocurrió un problema.

_En lugar de devolver un valor especial, el programa "lanza" (throw) un objeto que representa el error._

Ese objeto puede ser capturado por otro bloque de código preparado para manejarlo.

### Idea principal

Imagina que una función realiza una operación, todo va bien hasta que ocurre algo inesperado.

En ese momento:
```
Función
   │
   ▼
Realiza trabajo
   │
   ▼
¿Todo salió bien?
   │
 ┌─┴───────────────┐
 │                 │
Sí                 No
 │                 │
 ▼                 ▼
Continúa      Lanza excepción
```

La ejecución "salta" automáticamente hasta encontrar un lugar donde esa excepción pueda ser manejada.

### ¿Por qué existen?

Antes de las excepciones, los programas tenían que comprobar manualmente el resultado de prácticamente todas las operaciones.

+ Cuando un programa tiene miles de operaciones, este estilo produce código repetitivo y difícil de mantener.

Las excepciones permiten separar:

+ el código que realiza el trabajo
+ del código que maneja los errores.

### Flujo de una excepción

Una excepción sigue normalmente este recorrido:

```
Ocurre un error
       │
       ▼
Se lanza una excepción
       │
       ▼
Se busca un manejador (catch)
       │
       ▼
Si existe
       │
       ▼
Se ejecuta
```

Si nadie la captura, normalmente el programa termina mostrando el error.

### Estructura general

**Aunque la sintaxis cambia entre lenguajes, la estructura conceptual es la misma:**

```mermaid
flowchart LR

A[Intentar realizar una operación]
B[Si ocurre una excepción]
C[Manejar la excepción]
D[Ejecutar tareas finales]

A --> B
B --> C
C --> D
```

### El bloque `try`

+ El bloque try contiene el código que puede producir una excepción.
+ Por ejemplo, abrir un archivo, acceder a una base de datos o realizar una petición de red.

```python
# en python
try:
    archivo = open("datos.txt")
```
```java
// en java
try {
    FileReader archivo = new FileReader("datos.txt");
}
```
```C#
// En C#:
try
{
    File.Open("datos.txt");
}
```

**La idea es exactamente la misma en todos los lenguajes.**

### El bloque `catch` (o `except`)

Si dentro del `try` ocurre un problema, el flujo salta al bloque encargado de manejarlo.

```Python
# Python utiliza except:
try:
    archivo = open("datos.txt")
except FileNotFoundError:
    print("Archivo inexistente.")
```
```Java
// Java utiliza catch:
try {
    FileReader archivo = new FileReader("datos.txt");
}
catch(FileNotFoundException e) {
    System.out.println("Archivo inexistente.");
}
```

El propósito es el mismo:
+ Capturar la excepción y decidir cómo responder.

### El bloque `finally`

Hay tareas que deben ejecutarse siempre, haya ocurrido un error o no.

Por ejemplo:

+ cerrar archivos
+ liberar memoria
+ cerrar conexiones
+ desbloquear recursos.

Para eso existe `finally`.

```python
try:
    archivo = open("datos.txt")
except FileNotFoundError:
    print("No existe.")
finally:
    print("Fin del proceso.")
```

Aunque ocurra una excepción, el bloque `finally`  se ejecutará.

**Analogía**

Piensa en un laboratorio.

1. Entras al laboratorio (`try`).
2. Realizas un experimento.
3. Si algo falla, aplicas el protocolo de emergencia (`catch`/`except`).
4. Antes de salir, siempre limpias y cierras el laboratorio (`finally`).

```
Entrar
   │
   ▼
Intentar experimento
   │
 ┌─┴───────────────┐
 │                 │
Éxito             Error
 │                 │
 ▼                 ▼
Continuar      Aplicar protocolo
        \       /
         ▼     ▼
        Limpiar laboratorio
          (finally)
```

### Ventajas de las excepciones

Las excepciones ofrecen varias ventajas importantes:

+ Separan la lógica del negocio del manejo de errores.
+ Evitan comprobar errores después de cada operación.
+ Permiten propagar un error hasta quien realmente pueda resolverlo.
+ Facilitan escribir código más limpio y legible.
+ Son el mecanismo estándar en la mayoría de los lenguajes modernos.

### Desventajas

También tienen algunas desventajas si se usan incorrectamente:

+ Un uso excesivo puede dificultar seguir el flujo del programa.
+ Capturar todas las excepciones indiscriminadamente puede ocultar bugs.
+ Lanzar excepciones suele tener un costo mayor que devolver un valor.

Por eso se recomienda utilizarlas para situaciones excepcionales, no como mecanismo habitual para controlar el flujo del programa.

## Valores de retorno

Antes de que existieran las excepciones _(y todavía hoy en muchos lenguajes)_, los errores se comunican mediante valores de retorno especiales.

La idea es sencilla:

**En lugar de lanzar una excepción, la función devuelve un valor que indica si la operación tuvo éxito o no**

### Idea principal

La función realiza un trabajo y devuelve un resultado.

El programa que la llamó debe comprobar si ese resultado representa un éxito o un error.

```
Función
   │
   ▼
Realiza operación
   │
   ▼
Devuelve resultado
   │
 ┌─┴──────────────┐
 │                │
Éxito          Error
```

**Ejemplo con un valor booleano**

+ guardarArchivo() → `true`

    + Significa que todo salió bien.

+ guardarArchivo() → `false`

    + Significa que ocurrió un problema.

### Ejemplo en código

```python
# en python
def autenticar(usuario, contraseña):
    if usuario == "admin" and contraseña == "1234":
        return True
    return False

    ↓

if autenticar("admin", "1234"):
    print("Acceso permitido")
else:
    print("Credenciales incorrectas")
```

**No hay excepciones. Todo se comunica mediante un valor de retorno.**

### Códigos de error

Muchos sistemas utilizan números para representar distintos errores.

Por ejemplo:

+ `0` = éxito
+ `1` = archivo inexistente
+ `2` = permiso denegado
+ `3` = memoria insuficiente

Una función puede devolver uno de estos códigos.

+ resultado = abrirArchivo() → `0`

El programa interpreta que la operación fue correcta.

### Valores especiales

En algunos lenguajes se utilizan valores como:

+ `null`
+ `None`
+ `nil`
+ `nullptr`

para indicar que no fue posible obtener un resultado.

Por ejemplo:

```python
# en python
def buscar(nombre):
    if nombre == "Ana":
        return "Ana"

    return None

    ↓

persona = buscar("Luis")

if persona is None:
    print("No encontrada")
```

### Objetos de resultado

En lenguajes modernos es frecuente devolver un objeto que contiene tanto el resultado como información sobre el error.

Por ejemplo:

```
Resultado

├── éxito = True
├── dato = Usuario
└── error = Ninguno

O bien:

Resultado

├── éxito = False
├── dato = Ninguno
└── error = "Usuario inexistente"
```

Este enfoque evita lanzar excepciones para errores esperados y proporciona información estructurada sobre el resultado.

### Ventajas de los valores de retorno

+ Son simples y fáciles de entender.
+ El flujo del programa es completamente explícito.
+ Suelen ser más eficientes que lanzar excepciones.
+ Son ideales para operaciones donde el error es parte del comportamiento esperado.

### Desventajas

+ Obligan al programador a comprobar el resultado después de cada llamada.
+ Es fácil olvidar verificar el valor devuelto.
+ El código puede llenarse de comprobaciones repetitivas.
+ En operaciones complejas, el manejo de errores puede mezclarse con la lógica principal.

### Comparación entre excepciones y valores de retorno

| Característica         | Excepciones                                            | Valores de retorno                 |
| ---------------------- | ------------------------------------------------------ | ---------------------------------- |
| Comunicación del error | Se lanza una excepción                                 | Se devuelve un valor especial      |
| Flujo del programa     | Puede interrumpirse y propagarse                       | Continúa normalmente               |
| Legibilidad            | Separa la lógica principal del manejo de errores       | Requiere comprobaciones frecuentes |
| Rendimiento            | Generalmente más costoso cuando se lanza una excepción | Generalmente más eficiente         |
| Uso recomendado        | Errores inesperados o excepcionales                    | Errores esperados y frecuentes     |

### ¿Cuándo usar cada uno?

Una regla práctica utilizada en muchos proyectos es la siguiente:

| Situación                                                                                  | Mecanismo recomendado | Ejemplo                                                                                                                           |
| ------------------------------------------------------------------------------------------ | --------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| El error forma parte del funcionamiento normal                                             | Valores de retorno    | Buscar un usuario que puede no existir, validar una contraseña, comprobar si un archivo está presente antes de abrirlo.           |
| El error representa una condición excepcional que impide continuar con la operación actual | Excepciones           | Fallo al conectar con una base de datos, corrupción de datos, acceso a un recurso inexistente cuando se asumía que debía existir. |

### Resumen

| Mecanismo                             | ¿Cómo comunica el error?                                                                     | Ventajas                                                                                                  | Desventajas                                                                                  | Casos de uso típicos                                                                         |
| ------------------------------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Excepciones (`try/catch/finally`)** | Lanza un objeto de excepción que puede ser capturado y propagado.                            | Código más limpio, separa la lógica del manejo de errores y permite centralizar el tratamiento de fallos. | Mayor coste cuando se lanzan y un uso inadecuado puede ocultar errores o complicar el flujo. | Errores excepcionales, fallos inesperados o situaciones que impiden completar una operación. |
| **Valores de retorno**                | Devuelve un valor especial (booleano, código de error, `null`/`None` o un objeto resultado). | Simples, explícitos y eficientes; ideales para condiciones previstas.                                     | Requieren verificar el resultado tras cada llamada y pueden generar código repetitivo.       | Validaciones, búsquedas, operaciones donde el error es una posibilidad normal del negocio.   |

### Relación con los tipos de errores

+ **Los bugs deben corregirse en el código**; normalmente no se intenta ocultarlos con excepciones o valores de retorno.

+ **Los errores esperados (fallos operacionales)** suelen manejarse mediante valores de retorno o excepciones controladas, según el lenguaje y el diseño de la aplicación.

+ **Los errores irrecuperables** pueden detectarse mediante excepciones, pero habitualmente terminan provocando la finalización controlada del programa porque no existe una forma segura de continuar