
```markdown
# Decisión de diseño 001: Interfaz única

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-23] <!-- when the decision was last updated -->

Technical Story: [description | ticket/issue URL] 

## Contexto del problema

Necesitamos una interfaz unica para que puedan acceder de la misma forma diferentes dispositivos, que metodo
es el mas adecuado?

Solucion:
Para hacer más sencillo el manejo del sistema, éste debe proporcionar una única interfaz, para diferentes. 
*(Visible tanto en smartphone, como en ordeador o tablet)*

## Decision Drivers 

* RF2

## Opciones consideradas

* Patrón Facade (fachada), ya que se ajusta y se precisa a la interfaz unica para todos los usuarios.

## Decision final [outcome]

Opción seleccionada: "FACADE", ya que éste patrón se aplica cuando se necesite proporcionar una interfaz  
simple para un sistema complejo.

### Consecuencias positivas 

* Independencia, portabilidad y reutilización.
* Reducción de dependencias entre los subsistemas y los clientes.
* A la hora de modificar las clases de los subsistemas basta con realizar cambios en la interfaz (fachada) y 
que los clientes puedan quedar aislados.

### Consecuencias negativas 

* Si el acceso por parte de los clientes es masivo, podrían acabar usando solamente una pequeña parte de   
la fachada.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 

# Decisión de diseño 002: Sensores geográficos

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-23] <!-- when the decision was last updated -->

## Contexto del problema

Queremos detectar por medio de sensores, los eventos inesperados que hace que se notifique al sistema 
de emergencias para que se procesen adecuadamente, ¿Qué sistema necesitamos?

Solucion:
Para acceder al estado sensores en los distintos puntos geográficos, agregaremos en el centro de control
remoto un sistema para recoger informacion de estos en tiempo real, para luego poder enviar la   
notificacion al centro de emergencias.

## Decision Drivers 

* RF12, RF13

## Opciones consideradas

* Arquitectura dirigida por eventos

## Decision final [outcome]

Opción seleccionada: Arquitectura dirigida por eventos. Los sensores son los generadores, es decir, 
son los que se pueden activar o no; el centro de control remoto está conectado con los sensores y recibe 
la señal si se activan, es el componente de mensajería e informa a las partes interesadas, en este 
caso el sistema de emergencias.

### Consecuencias positivas 

* Detecta un cambio significativo en un estado.
* Simplicidad.
* Una sola modalidad para eventos diversos.

### Consecuencias negativas 

* Hay posibilidad de desborde.
* Potencial imprevisión de escalabilidad
* Pobre comprensibilidad: Puede ser difícil prever qué pasará en respuesta a una acción
* No hay mucho soporte de recuperación en caso de falla parcial

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 