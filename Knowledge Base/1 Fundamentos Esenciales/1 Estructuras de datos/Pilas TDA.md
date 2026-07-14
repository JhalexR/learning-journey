# ¿Qué es una pila (Stack)?

Una pila es un Tipo de Dato Abstracto (TDA) que almacena una colección ordenada de elementos, donde todas las inserciones y eliminaciones se realizan por un único extremo, llamado tope (top).

Su funcionamiento sigue el principio LIFO (Last In, First Out):

> El último elemento que entra es el primero que sale.

#### Analogía

Imagina una pila de platos.

```
     ┌───────┐
Top→ │ Plato │
     ├───────┤
     │ Plato │
     ├───────┤
     │ Plato │
     └───────┘
```
> La Pila (Stack) introduce una regla de acceso específica a los datos.

+ Solo puedes colocar un plato encima.
+ Solo puedes retirar el plato de arriba.

> _**No puedes sacar uno que esté en medio sin quitar antes los superiores.**_
>> _**Esa es exactamente la regla de una pila.**_

Supongamos que la pila contiene:

```
Top
 │
 ▼
┌────┐
│ 40 │
├────┤
│ 30 │
├────┤
│ 20 │
├────┤
│ 10 │
└────┘
```
El 40 fue el último en entrar, por lo tanto será el primero en salir.

#### Operaciones básicas

Un TDA Pila suele definir las siguientes operaciones.

| Operación      | Descripción                                    |
| -------------- | ---------------------------------------------- |
| Crear          | Construir una pila vacía.                      |
| Push(x)        | Insertar un elemento en el tope.               |
| Pop()          | Eliminar y devolver el elemento del tope.      |
| Top() o Peek() | Consultar el elemento del tope sin eliminarlo. |
| isEmpty()      | Verificar si la pila está vacía.               |
| Size()         | Obtener el número de elementos.                |

#### Push (Agregar un elemento.)

```
Antes:
Top -> 30, 20, 10

> Push(40)

Después:
Top -> 40, 30, 20, 10
```

#### Pop (Eliminar el elemento superior.)

```
Antes:
Top -> 40, 30, 20, 10

> pop()

Después:
Top -> 30, 20, 10
```

#### Peek o Top (Consulta el elemento superior sin eliminarlo.)

```
> Peek() Top -> 40, 30, 20, 10  

> 40
```
> La pila no cambia.

## Implementaciones

Una pila puede implementarse mediante:

+ un arreglo (pila secuencial)
+ una lista simplemente enlazada
+ una lista doblemente enlazada

> Todas ofrecen las mismas operaciones (push, pop, peek), aunque internamente funcionen de forma distinta.

#### 1. Implementación mediante arreglos (pila secuencial)

```
Índice

0   1   2
┌───┬───┬───┐
│10 │20 │30 │
└───┴───┴───┘
            ▲
           Top
```
El tope suele almacenarse como un índice.

#### Ventajas:

+ Acceso muy rápido.
+ Implementación sencilla.

#### Desventajas:

+ Si el arreglo es de tamaño fijo, puede llenarse.
+ Si es dinámico, ocasionalmente requiere redimensionarse.

#### 2. Implementación mediante listas enlazadas

```
Top
 │
 ▼
┌─────────┐
│30 | •───┼──►
└─────────┘
           ▼
     ┌─────────┐
     │20 | •───┼──►
     └─────────┘
                ▼
          ┌──────────┐
          │10 | NULL │
          └──────────┘
```
El tope corresponde a la cabeza de la lista.

Hacer push y pop solo implica modificar esa referencia, por lo que ambas operaciones son muy eficientes.

#### Complejidad temporal

| Operación | Arreglo | Lista enlazada |
| --------- | :-----: | :------------: |
| Push      |  O(1)*  |      O(1)      |
| Pop       |   O(1)  |      O(1)      |
| Peek      |   O(1)  |      O(1)      |
| isEmpty   |   O(1)  |      O(1)      |

#### Aplicaciones comunes

Las pilas aparecen con frecuencia en programación:

+ Deshacer/Rehacer en editores de texto.
+ Historial de navegación (botón "Atrás").
+ Llamadas a funciones (la pila de llamadas o call stack).
+ Evaluación de expresiones matemáticas.
+ Verificación de paréntesis y otras estructuras balanceadas.
+ Recorridos de árboles y grafos (como la búsqueda en profundidad, DFS).

#### Idea clave

**A diferencia del TDA Lista, donde puedes acceder o modificar elementos en distintas posiciones, una pila restringe el acceso al tope. Esa restricción simplifica muchas operaciones y la hace ideal para problemas donde el orden de procesamiento debe ser LIFO (Last In, First Out).**