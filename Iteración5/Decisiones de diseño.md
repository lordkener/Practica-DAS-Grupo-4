```markdown
# Decisión de diseño 008: Suscripcion RRS

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-7] <!-- when the decision was last updated -->

## Contexto del problema

¿Cómo podriamos interaccionar con los usuarios enviandoles notificaciones nuevas en base a que ellos esten suscritos
por algun medio en el sistema para que esten actualizados?

Solución:
Los usuarios se suscriben y reciben informacion cada x tiempo. Esto se hace para separar las representaciones 
internas de información de las formas en que se presenta y acepta la información del usuario. 
Desacopla los componentes y permite la reutilización eficiente del código. Seria eficiente definir una 
arquitectura para aplicaciones World Wide Web en los principales lenguajes de programación.

## Decision Drivers 

* RF19

## Opciones consideradas

* Patrón de modelo-vista-controlador
* Patrón observer
* Patron Publish-Suscribe

## Decision final [outcome]

Opción seleccionada: Patrón de modelo-vista-controlador, ya que generaliza ambas opciones de Observer y Publish-suscribe

### Consecuencias positivas 

* Se puede hacer facil el tener multiples vistas partiendo desde el mismo modelo, el cual puede estar conectado o 
desconectado en tiempo de ejecucion.

### Consecuencias negativas 

* Aumenta la complejidad.
* Puede llevar a muchas actualizaciones innecesarias para los usuarios.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
# Decisión de diseño 009: Escalabilidad

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-7] <!-- when the decision was last updated -->

## Contexto del problema

El enfoque usual de la aplicacion es que mantenga al estado actual de los datos mediante actualizacion conforme los 
usuarios trabajan con ellos. Por ejemplo, a menos que exista un mecanismo de auditoria adicional que registre los
detalles de cada operacion en un registro independiente, el historial se pierde. ¿Cómo damos una solución a esto?

Solución:
Definir un enfoque para controlar las operaciones basado en una secuencia de eventos, cada uno de los cuales se registra 
en un almacen de solo anexar. Este almacen publicara estos eventos para que los consumidorespuedan recibir notificacioes
y controlarlos si lo necesitan. Ademas, las aplicaciones pueden leer el historial de eventos en cualquier momento y 
usuario para materializar el estado actual de una entidadal reproducir y consuir todos los eventos relacionados con esa
entidad.

## Decision Drivers 

* RF20

## Opciones consideradas

* Patrón Evento-Sourcing

## Decision final [outcome]

Opción seleccionada: Event-Sourcing

### Consecuencias positivas 

* Los eventos son inmutables y pueden almacenarse mediante una operacion de solo anexar.
* Ayuda a impedir que las actualizaciones simultanteas causen conflictos, ya que evita la necesidad de actualizar 
directamente los objetos en el almacen de datos.
* No hay ninguna contencion durante el procesamiento de transacciones.
* Mejora considerablemente el rendimiento y la escalabilidad de las aplicaciones, especialmente el nivel de presentacion
o la interfaz de usuario.

### Consecuencias negativas 

* El sistema solo sera coherente al crear vistas materializadas o proyecciones de los datos mediante la reproduccion 
de eventos.
* Puede ser dificil combinar los eventos existentes en el almacen con la nueva version, cuando se quiera modificar un
formato.
* No hay ningun enfoque estandar ni mecanismos existentes como consultas SQL para leer los eventos y obtener informacion.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
