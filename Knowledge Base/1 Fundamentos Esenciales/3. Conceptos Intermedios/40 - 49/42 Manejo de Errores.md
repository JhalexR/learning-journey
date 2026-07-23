# Manejo de Errores
> (Error Handling)

El manejo de errores es lo que separa el código de juguete del código de producción. 

+ Los errores van a:
    + **ocurrir**; 
    
+ la pregunta es: 
    + **cómo los manejas.**

**Error Handling**: es el conjunto de técnicas utilizadas para detectar, reportar y responder a situaciones anómalas durante el desarrollo o la ejecución de un programa.

Su objetivo principal no es evitar todos los errores **(eso es imposible)**, sino hacer que el software:

+ Sea más robusto.
+ Falle de forma controlada.
+ Informe claramente qué ocurrió.
+ Permita recuperarse cuando sea posible.

## Tipos de Errores

Podemos dividir los errores en tres grandes categorías:

```
Errores
│
├── Errores de programación (Bugs)
│
├── Errores esperados
│      (fallos operacionales)
│
└── Errores irrecuperables
```
> Cada uno requiere una estrategia distinta.

+ No todos los problemas tienen el mismo origen.
+ Algunos aparecen porque el programador escribió código incorrecto.
+ Otros ocurren porque el mundo real es impredecible.
+ Y otros indican que el programa ha llegado a un estado del que no puede recuperarse.

### Errores de programación (Bugs)

Son errores producidos por el desarrollador.

En otras palabras:

+ El programa hace algo incorrecto porque el código fue escrito incorrectamente.

    + _No son culpa del usuario ni del sistema operativo._
    + _Son defectos del software._

**Características**

+ Se originan durante el desarrollo.
+ Generalmente indican una lógica incorrecta.
+ Deben corregirse modificando el código.
+ No deberían manejarse como parte del flujo normal del programa.

**Ejemplos**

```python
# División entre cero
numero = 10
resultado = numero / 0
# El programador olvidó validar el divisor.

# Variable inexistente
print(nombre)
# Nunca se creó la variable.

# Error lógico
precio = 100
descuento = 20
total = precio + descuento
# El programa funciona.
# No produce excepción.
# Pero el cálculo es incorrecto.

# Debería ser:
total = precio - descuento

# Bucle infinito
while True:
    pass
# El programa nunca termina.
```

**¿Cómo se solucionan?**

**No con manejo de excepciones.**

Se solucionan:

+ depurando (debugging)
+ realizando pruebas
+ revisando el código
+ usando herramientas de análisis.

**¿Se deben capturar?**

Generalmente no.

Por ejemplo:

```python
try:
    resultado = numero / 0
except:
    pass
```
+ Esto oculta el problema.
+ **Es mucho mejor dejar que el error aparezca durante el desarrollo para corregirlo.**

### Errores esperados (Fallos operacionales)

+ Aquí ocurre algo muy diferente.
+ El programa está perfectamente escrito.
+ Sin embargo, el entorno produce una situación que ya sabemos que puede ocurrir.
+ No es un bug.
+ Es una condición normal del mundo real.

**Ejemplos**

+ El usuario intenta abrir un archivo que no existe.
    + El programa debe responder adecuadamente.

+ No hay conexión a Internet 
    + El programa intenta descargar información → La red falla.
    + No es culpa del código.

+ La base de datos está temporalmente apagada.
    + El programa puede intentar nuevamente.

**Características**

Estos errores:

+ son previsibles
+ ocurren frecuentemente
+ deben manejarse
+ forman parte del funcionamiento normal.

Ejemplo:
```python
try:
    archivo = open("datos.txt")
except FileNotFoundError:
    print("El archivo no existe.")
```

+ Aquí no hay un bug.
+ El programa simplemente responde correctamente.

### ¿Qué debe hacer el programa?

Normalmente alguna de estas acciones:

+ informar al usuario
+ pedir nuevos datos
+ intentar nuevamente
+ usar un valor alternativo
+ registrar el problema.

```
Servidor no disponible.

Intentando reconectar...
```

+ El software continúa funcionando.

### Errores irrecuperables

Son situaciones donde continuar ejecutando el programa sería peligroso o imposible.

**No existe una forma segura de seguir.**

**Ejemplos**

+ Memoria completamente agotada → El programa no puede crear nuevos objetos.
+ Corrupción de memoria: 
    + Los datos internos ya no son confiables.
    + Daño crítico en archivos del sistema.
    + Violaciones graves de seguridad.
+ Errores internos imposibles.
    + Si ocurre → significa que el estado interno del programa quedó inconsistente.

**Características**

+ Muy poco frecuentes.
+ No forman parte del flujo normal.
+ Generalmente obligan a detener el programa.
+ Continuar podría producir pérdida de información.

**Ejemplo conceptual**

+ Un banco detecta que una transacción dejó las cuentas con saldo negativo imposible.
+ En vez de continuar realizando operaciones,
+ el sistema decide detener el proceso.
+ Es mejor detenerse que producir datos corruptos.

**Comparación general**

| Tipo                | ¿Es culpa del programador? | ¿Es esperado? | ¿Se debe manejar?                   | ¿Debe corregirse en el código? |
| ------------------- | -------------------------- | ------------- | ----------------------------------- | ------------------------------ |
| Bug                 | Sí                         | No            | Normalmente no                      | Sí                             |
| Error operacional   | No                         | Sí            | Sí                                  | No (se maneja)                 |
| Error irrecuperable | No necesariamente          | Muy raro      | Solo para finalizar de forma segura | Depende del origen             |

**Ejemplo completo**

Imagina una aplicación bancaria

```
Usuario inicia sesión
          │
          ▼
¿Contraseña incorrecta?
          │
      Sí  ▼
 Mostrar mensaje            → (Error esperado)

Usuario solicita saldo
        │
        ▼
Base de datos caída
        │
        ▼
Intentar reconectar            → (Error esperado)

El programa calcula intereses
        │
        ▼
El desarrollador escribió mal la fórmula
        │
        ▼
Resultado incorrecto            → (Bug)

La memoria queda corrupta
        │
        ▼
Detener aplicación            → (Error irrecuperable)
```

### Conclusiones

+ Si es un bug, lo correcto es corregir el código, no ocultar el error.
+ Si es un error operacional, el programa debe anticiparlo y manejarlo como parte de su comportamiento normal.
+ Si es un error irrecuperable, la prioridad es proteger la integridad del sistema y los datos, incluso si eso implica detener la ejecución

Esta clasificación es la base de mecanismos más avanzados: 

+ las excepciones, 
+ los bloques try/catch (try/except en Python), 
+ la propagación de errores, 
+ los códigos de error, 
+ el registro (logging) 
+ las estrategias de recuperación.