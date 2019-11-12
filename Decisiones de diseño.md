# Decisiones de diseño
A la hora de la toma de decisiones cogeremos aproximadamente unos tres requisitos y trabajaremos sobre ellos. 
Cuando se hayan tomado las decisiones sobre éstos, volveremos a coger otros requisitos y así sucesivamente. 
Hemos decidido esoger el estilo arquitectonico dirigido por eventos, o Event-driven architecture.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 

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
