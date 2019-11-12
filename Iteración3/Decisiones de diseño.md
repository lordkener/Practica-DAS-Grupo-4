```markdown
# Decisión de diseño 005: Algoritmo de optimización

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-3] <!-- when the decision was last updated -->

## Contexto del problema

Necesitamos un algoritmo que calcule las rutas más óptimas para que las unidades lleguen al punto de emergencia   
lo más rápido posible.

Solución:
Existe una interfaz que tendrá todos los algoritmos necesarios para el funcionamiento del programa. En el   
momento en el que una emergencia ocurra y se vaya a notificar a las unidades activas, se debe acceder a   
esta interfaz y seleccionar el método que calcule la ruta más óptima a la emergencia.

## Decision Drivers 

* RF5

## Opciones consideradas

* Patrón Strategy

## Decision final [outcome]

Opción seleccionada: Patrón Strategy

### Consecuencias positivas 

* Permite que el algoritmo pueda variar sin importar los clientes que lo utilicen.
* Es el patron mas adecuado para situar y acceder a las unidades que contienen los nodos.

### Consecuencias negativas 

* Al ser un recorrido de nodos, cuantos mas nodos hay, la complejidad de recorrer el arbol de estos, puede dificultarse.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
# Decisión de diseño 006: Asignacion de roles, recursos y llamadas

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-5] <!-- when the decision was last updated -->

## Contexto del problema

¿Cuál es el principio general para asignar responsabilidades a los roles existentes, los recursos necesarios para cada emergencia y la asignación de llamadas tanto al sistema de emergencias como al centro de operaciones?

Solución:
Asignar una responsabilidad al experto en información y la responsabilidad a un objeto que medie entre los elementos.

## Decision Drivers 

* RF5, RF7, RF8, RF9, RF10, RF14

## Opciones consideradas

* GRASP (object-oriented design General Responsibility Assignment Software Patterns)

## Decision final [outcome]

Opción seleccionada: GRASP

### Consecuencias positivas 

* Se mantiene el encapsulamiento, los objetos utilizan su propia información para llevar a cabo sus tareas. 
* Se distribuye el comportamiento entre las clases que contienen la información requerida. 
* Son más fáciles de entender y mantener.
* Si se asignan bien, el diseño puede soportar un bajo acoplamiento, mayor claridad, encapsulación y reutilización.

### Consecuencias negativas 

* Evitar/reducir el acoplamiento directo entre elementos y mejorar la reutilización suele contener bugs en el sistema.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
