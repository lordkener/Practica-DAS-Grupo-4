```markdown
# Decisión de diseño 003: Llamadas distribuidas

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-30] <!-- when the decision was last updated -->

## Contexto del problema

Las llamadas en cola se tienen que asignar a los operadores dependiendo de la disponibilidad de   
estas, ¿Cómo se podrian asignar uniformemente?

Solucion:
Un módulo que permita acceder y supervisar el estado de la cola de las llamadas, y que al mismo  
tiempo, asignarlos y priorizarlos a los diferentes operadores inactivos o en pausa.

## Decision Drivers 

* RF11

## Opciones consideradas

* Supervisor Module

## Decision final [outcome]

Opción seleccionada: Supervisor Module

### Consecuencias positivas 

* Acceso en tiempo real a la cola de llamadas
* Priorizacion de tareas
* Se podria ocupar de grabar la conversacion

### Consecuencias negativas 

* El tiempo de espera puede ser exponencial si la cola no va desapareciendo

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
# Decisión de diseño 004: Video-vigilancia

* Estado: [Decidida]
* Responsables de la decisión: [Hamsa Aldrobi, Raquel Alonso]
* Fecha: [2019-10-31] <!-- when the decision was last updated -->

## Contexto del problema

Queremos que existan unas cámaras transmitan en tiempo real vídeo y además, que estos vídeos se guarden  
durante un cierto tiempo para luego borrarse y así no saturar la memoria dinámica. ¿Cómo lo hacemos?

Solución:
Las cámaras remotas están en contacto con el sistema de emergencias, transmitiéndoles en tiempo   
real el vídeo. El sistema tendrá una base de datos que guarde el vídeo durante x tiempo.

## Decision Drivers 

* RF3, RF4

## Opciones consideradas

* SOA Event-Driver
* Modelo Vista-Controlador

## Decision final [outcome]

Opción seleccionada: SOA Event-Driver

### Consecuencias positivas 

* Control y acceso total al modulo de video-camaras en tiempo real.
* Al ser parecido de la decision de diseño de los sensores, se puede agrupar y tener aprovechar la relacion.

### Consecuencias negativas 

* El tiempo real puede retardarse.

## Pros and Cons of the Options
### [Opción 1: Modelo Vista-Controlador]
Buena, ya que se separa la lógica de la aplicación de la lógica de la vista.
Buena por la implementación se realiza de forma modular.
Mala ya que es necesario una mayor dedicación en los tiempos iniciales del desarrollo y el desarrollador   
debe crear un mayor número de clases que pueden ser no necesarias en otros tipos de entorno.
Mala ya que es un patrón de diseño orientado a objetos, es decir, su implementación es sumamente costosa y difícil en lenguajes que no siguen este paradigma.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
