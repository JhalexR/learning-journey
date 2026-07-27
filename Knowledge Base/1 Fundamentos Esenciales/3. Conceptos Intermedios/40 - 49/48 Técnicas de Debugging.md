# Técnicas de Debugging

### Print Debugging (el básico)

Añadir prints/logs para ver valores en puntos específicos:

+ ¿Qué valor tiene esta variable aquí?
+ ¿Se está ejecutando esta línea?
+ ¿Cuántas veces entra a este bucle?

### Binary Search Debugging

Cuando no sabes dónde está el bug:

1. Pon un log a la mitad del código sospechoso.
2. ¿El bug ocurre antes o después?
3. Repite en la mitad relevante.
4. Reduce hasta encontrar la línea exacta.

### Rubber Duck Debugging

+ Explica el código línea por línea a ti mismo en voz alta.
+ Frecuentemente encuentras el error al verbalizarlo.

### Debugging con el Debugger

Usa **breakpoints** para:

+ Pausar en una línea específica
+ Inspeccionar todas las variables en ese momento
+ Ejecutar paso a paso
+ Ver el call stack completo

## Proceso Sistemático

1. Reproduce el bug de forma consistente.
2. Aísla el problema - ¿cuál es el input mínimo que lo causa?
3. Formula hipótesis - ¿qué crees que está mal?
4. Verifica la hipótesis - con logs, debugger, o tests.
5. Arregla y verifica - asegúrate de que realmente está arreglado.
6. Escribe un test - para que no vuelva a pasar.

## Cómo Buscar Soluciones Efectivamente

**Antes de buscar**

+ Lee el error completo.
+ Intenta entenderlo tú primero.
+ Simplifica el problema.

**Cómo buscar**

+ Copia el mensaje de error exacto (sin datos específicos de tu código).
+ Incluye el lenguaje/framework.
+ Busca en: IA > documentación oficial > Stack Overflow > GitHub Issues.

**Cómo evaluar respuestas**

+ ¿Es reciente? Las soluciones viejas pueden no aplicar.
+ ¿Tiene votos/aceptada? Pero no confíes ciegamente.
+ ¿Entiendes la solución? No copies código que no entiendas.
+ ¿Hay efectos secundarios? Lee los comentarios.

## Errores Comunes por Categoría

**Errores de sintaxis**
+ Paréntesis/llaves sin cerrar.
+ Punto y coma faltante (en lenguajes que lo requieren).
+ Typos en nombres de variables.

**Errores de tipos**
+ `Null`/`undefined` donde se esperaba un valor.
+ `String` donde se esperaba número (o viceversa).
+ Índice fuera de rango.

**Errores de lógica** 
+ Condición invertida (< en vez de >).
+ Off-by-one (empezar en 1 en vez de 0).
+ Variables con el valor de la iteración anterior.

**Errores de estado**
+ Variable no inicializada.
+ Estado modificado en lugar inesperado.
+ Race condition en código asíncrono.