```markdown
# Decisión de diseño 007: Comunicación y conexion internacional

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-7] <!-- when the decision was last updated -->

## Contexto del problema

¿Cómo podriamos coordinar las emergencias en base a las unidades activas dependiendo de la zona, que se puedan traducir
a otro idioma si fuese necesario, y que la comunicación sea cifrada?

Solución:
Todos los componentes tienen acceso al sistema. Los usuarios que monitorizan las llamadas en curso 
pueden producir nuevos objetos de datos que se agregan a las emergencias. Los componentes buscan tipos particulares 
de datos en el sistema, y pueden encontrarlos por coincidencia de patrones con la fuente de conocimiento existente.

## Decision Drivers 

* RF15, RF16, RF17, R18

## Opciones consideradas

* Patrón de pizarra(blackboard)

## Decision final [outcome]

Opción seleccionada: Patrón de pizarra

### Consecuencias positivas 

* Reconocimiento de voz e identificación única.
* Identificación y seguimiento del vehículo.
* Identificación de la estructura proteica.
* Sonar señala la interpretación.
* Facil de añadir nuevas aplicaciones.
* Tambien es facil extender la estructura del espacio de datos.

### Consecuencias negativas 

* Modificar el espacio de la estructura de datos puede ser costoso, ya que todas las aplicaciones pueden ser afectadas.
* Puede necesitar sincronizacion y control de acceso.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
