# Errores en Código Asíncrono

En un programa asíncrono, una operación puede tardar segundos en completarse y el error aparecer mucho después de que la función original haya terminado de ejecutarse.

El manejo de errores en código asíncrono consiste en detectar, comunicar y responder a errores que ocurren durante operaciones que no se ejecutan de forma inmediata, sino que continúan en otro momento o incluso en otro hilo o proceso.

Estas operaciones incluyen, por ejemplo:

+ Peticiones HTTP.
+ Acceso a bases de datos.
+ Lectura y escritura de archivos.
+ Comunicación con APIs.
+ Operaciones de red.
+ Tareas en segundo plano.

### ¿Por qué son diferentes?

En código síncrono el flujo es lineal.

```
Inicio
   │
   ▼
Operación
   │
   ▼
¿Error?
   │
 ┌─┴─────┐
 │        │
No       Sí
 │        │
 ▼        ▼
Continúa  Excepción
```

Todo ocurre en la misma secuencia.

En código asíncrono ocurre algo diferente.

```
Inicio
   │
   ▼
Se inicia operación
   │
   ▼
El programa continúa
haciendo otras tareas
   │
   ▼
Tiempo después...
   │
   ▼
La operación termina
   │
   ▼
Puede aparecer un error
```

+ El error aparece más tarde.

+ Incluso puede ocurrir cuando la función que inició la operación ya terminó.

### Ejemplo conceptual

Supongamos que una aplicación descarga información de Internet.

```
Solicitar datos
↓
Esperar respuesta del servidor
↓
Servidor responde
```
El problema es que la respuesta puede tardar:
+ 10 milisegundos,
+ 2 segundos,
+ 30 segundos,
+ o nunca llegar.

Mientras tanto, el programa sigue funcionando.

### El principal desafío

+ En programación `síncrona`: si ocurre un error, aparece inmediatamente.

+ En programación `asíncrona`: 

```
Solicitar lectura
↓
El programa sigue ejecutándose
↓
Más tarde ocurre el error
```

+ Ya no basta con colocar un `try`/`catch` alrededor de la llamada inicial.
+ Hay que capturar el error cuando la operación realmente termina.

### Fuentes comunes de errores asíncronos

**Problemas de red**

```
Servidor inaccesible
↓
Timeout
↓
Conexión perdida
```
+ Son probablemente los errores más frecuentes.

**Servicios externos**

Una API puede responder:

+ `500 Internal Server Error`
+ `503 Service Unavailable`

La aplicación debe manejar esas respuestas correctamente.

**Operaciones canceladas**

+ El usuario puede cancelar una operación antes de que termine.
+ La tarea termina con una cancelación, no necesariamente con un fallo técnico.

**Recursos compartidos**

Dos procesos intentan modificar el mismo dato simultáneamente.

Puede producirse:

+ bloqueo
+ conflicto
+ pérdida de información

### ¿Por qué un `try`/`catch` tradicional no siempre funciona?

Supongamos:

```
try
    iniciar descarga
catch
    mostrar error

try termina
↓
La descarga sigue ejecutándose
↓
Cinco segundos después
↓
Aparece el error
```

El problema es que:

+ Cuando el error ocurre,
+ el bloque `try` ya terminó.
+ Por eso muchos lenguajes incorporan mecanismos especiales para el código asíncrono.

### Manejo de errores con Promesas (Promises)

En lenguajes como `JavaScript`, una **Promesa** (`Promise`) representa el resultado futuro de una operación asíncrona.

Una promesa puede terminar en tres estados:

+ pendiente
+ Cumplida (éxito)
+ Rechazada (error)

Cuando ocurre un error, la promesa se **rechaza** (`rejected`).

Ese rechazo puede capturarse con mecanismos como:
+ .`catch()` 
+ `try`/`catch` cuando se usa `async`/`await`.

**Ejemplo en JavaScript:**
```javascript
fetch("/usuarios")
    .then(respuesta => respuesta.json())
    .catch(error => {
        console.log("No fue posible obtener los datos.");
    });
```

### Manejo con async/await

Muchos lenguajes modernos permiten escribir código asíncrono con una sintaxis muy similar al código síncrono.

Por ejemplo:

```javascript
// javascript
async function cargarUsuarios() {
    try {
        const respuesta = await fetch("/usuarios");
        const datos = await respuesta.json();
    }
    catch(error) {
        console.log("Error al cargar usuarios.");
    }
}
```

+ Aunque el código parece secuencial, `await` suspende temporalmente la función hasta que la operación finaliza.
+ Si durante esa espera ocurre un error, el flujo salta al bloque `catch`, igual que en el código síncrono.

### Manejo en otros lenguajes

| Lenguaje   | Mecanismo habitual                                            |
| ---------- | ------------------------------------------------------------- |
| JavaScript | `Promise`, `async/await`, `.catch()`                          |
| Python     | `async` / `await` junto con `try/except`                      |
| C#         | `Task`, `async/await`, `try/catch`                            |
| Java       | `CompletableFuture`, `Future`, programación reactiva          |
| Kotlin     | Coroutines y `try/catch`                                      |
| Go         | Goroutines, canales (`channels`) y valores de error (`error`) |

+ Cada lenguaje tiene su propio modelo para gestionar errores asíncronos

+ Aunque la sintaxis cambia, el objetivo siempre es el mismo: 
    + **capturar el error cuando la operación asíncrona realmente finaliza.**

### Errores no manejados

Uno de los problemas más comunes es iniciar una operación asíncrona y olvidarse de manejar un posible error.

**Ejemplo conceptual:**

```
Iniciar operación
↓
Nadie espera el resultado
↓
Ocurre un error
↓
El error queda sin manejar
```

Las consecuencias pueden ser:

+ Finalización inesperada del programa.
+ Mensajes de error en la consola.
+ Recursos sin liberar.
+ Datos inconsistentes.

En JavaScript, por ejemplo, esto suele aparecer como una **Unhandled Promise Rejection**.

### Cancelación vs. Error

Un aspecto importante del código asíncrono es distinguir entre una operación que **falló** y una que fue **cancelada**.

```
Operación iniciada
        │
        ▼
¿Terminó?
        │
 ┌──────┼────────────┐
 │      │            │
 ▼      ▼            ▼
Éxito  Error     Cancelación
```
La cancelación no siempre representa un fallo.

Ejemplo:

+ El usuario cierra la aplicación mientras se descarga un archivo.
+ Se cancela una petición `HTTP` porque ya no es necesaria.
+ Se detiene una tarea porque el usuario inició otra equivalente.

En estos casos, el programa debe reconocer la cancelación como un resultado esperado y no tratarla como un error inesperado.

### Buenas prácticas

Cuando trabajes con código asíncrono, es recomendable seguir estas prácticas:

+ Manejar siempre los posibles errores de las operaciones asíncronas.
+ No ignorar promesas o tareas pendientes.
+ Diferenciar entre errores reales y cancelaciones.
+ Liberar correctamente recursos incluso cuando la operación falle.
+ Registrar los errores para facilitar su diagnóstico.
+ Aplicar los principios: 
    + Fail Fast
    + No Atrapar Todo
    + Mensajes de Error Útiles 
    + Propagar vs. Manejar.

**El hecho de que el problema ocurra mucho después de hacer el pedido ilustra por qué el manejo de errores en sistemas asíncronos requiere mecanismos distintos a los del código síncrono.**

### Relación con los principios de manejo de errores

+ Los principios de manejo de errores siguen siendo válidos
+ **pero adquieren aún más importancia en entornos asíncronos:**

| Principio                    | Aplicación en código asíncrono                                                                                                                                 |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Fail Fast**                | Validar parámetros antes de iniciar una tarea asíncrona para evitar ejecutar operaciones que ya se sabe que fallarán.                                          |
| **No Atrapar Todo**          | Capturar únicamente los errores que puedan resolverse y permitir que los demás se propaguen al componente adecuado.                                            |
| **Mensajes de Error Útiles** | Incluir información sobre qué operación asíncrona falló (por ejemplo, una URL, un identificador de tarea o el recurso afectado).                               |
| **Propagar vs. Manejar**     | Decidir si la tarea asíncrona puede recuperarse por sí misma (por ejemplo, reintentando una conexión) o si debe informar el fallo a quien inició la operación. |

### Resumen

| Concepto                  | Descripción                                                                                                                               |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Error asíncrono**       | Error que ocurre durante una operación cuyo resultado se obtiene en el futuro, no inmediatamente.                                         |
| **Principal desafío**     | El error puede aparecer después de que el flujo original haya continuado o incluso haya terminado.                                        |
| **Fuentes comunes**       | Fallos de red, APIs externas, operaciones canceladas, conflictos entre tareas y recursos compartidos.                                     |
| **Mecanismos habituales** | Promesas (`Promise`), `async/await`, tareas (`Task`), futuros (`Future`), corrutinas (`Coroutine`) y valores de error, según el lenguaje. |
| **Buenas prácticas**      | Manejar siempre los errores de las tareas asíncronas, distinguir cancelaciones de fallos y no dejar operaciones sin supervisión.          |

### Ideas clave

+ La diferencia fundamental entre el manejo de errores en código síncrono y asíncrono no está en qué errores pueden ocurrir, sino en cuándo ocurren
+ En programación asíncrona, el error puede manifestarse mucho tiempo después de iniciar una operación, por lo que el diseño del programa debe contemplar mecanismos para recibir, propagar y manejar esos errores cuando finalmente aparezcan
+ Esto es esencial para construir aplicaciones modernas que interactúan con **redes**, **bases de datos**, **interfaces de usuario** y **servicios distribuidos**.