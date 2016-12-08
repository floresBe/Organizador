Introducción
Programación Lógica.
Campo que estudia el uso de la lógica para el planteamiento de problemas y el control sobre las reglas de inferencia 
para llegar a una solución automática.

La Programación Lógica forma parte de lo que se conoce como Programación Declarativa, es decir, consiste en indicar 
como resolver un problema mediante sentencias; se trabaja de una forma descriptiva, estableciendo relaciones entre entidades, 
indicando no como, sino que hacer, entonces se dice que la idea esencial de la Programación Lógica es:

Programa= lógica + control

Lógica (programador): hechos y reglas para representar conocimiento
Control (interprete): deducción lógica para dar respuestas (soluciones)

La programación lógica intenta resolver lo siguiente:
Dado un problema S, saber si la afirmación A es solución o no del problema o en que casos lo es. 
Además se busca que los métodos sean implantados en maquinas de forma que la resolución del problema se haga de forma automática.

La programación lógica: construye base de conocimientos mediante reglas y hechos.

Regla: implicación o inferencia lógica que deduce nuevo conocimiento, la regla permite definir nuevas relaciones apartir de otras ya existentes.

Hecho: declaración, cláusula o proposición cierta o falsa, el hecho establece una relación entre objetos y es la forma más sencilla de sentencia.

Campos de Aplicación.
Sistemas Expertos , donde un Sistema de información imita las recomendaciones de un experto sobre algún dominio de conocimiento.

Demostración automática de teoremas, donde un programa genera nuevos teoremas sobre una teoría existente.

Reconocimiento de lenguaje natural, donde un programa es capaz de comprender (con limitaciones) la información contenida 
en una expresión lingüística humana.

Inteligencia artificial


Sistemas de información

Descripcion de la problematica.
Se trata de un dispositivo capaz de recorrer una habitación y, con la ayuda de mecanismos creados para sostener y mover objetos, sensores cuya funcion es determinar el tipo de objeto y de una serie de conocimientos previos, colocar cada uno de los objetos con los que se tope en su lugar especificado.


Justificación
Hoy en dia es muy comun que la vida de las personas sea mas activa que antes, es decir, no es raro conocer a una persona que estudie y trabaje a la vez, o que tenga mas de un trabajo. Es un estilo de vida que deja a cualquier persona desorganizada con tiempo a penas para comer y dormir antes de empezar de nuevo el dia a dia. Este tipo de situaciones genera, entre otras cosas, una eterna falta de organizacion y limpieza en las habitaciones en las que generalmente se llevan a cabo las actividades del diario. 

Desarrollo.
Para el desarrollo de la logica del organizador se utilizo el siguiente codigo.

Las siguientes reglas pueden interpretarse como acciones a realiza por el Organizador.

encender inicia la secuencia de acciones a realizar mandando a llamar la accion de recorrerHabitacion. 
encender:- write('Dispositivo Encendido.. '), nl, recorrerHabitacion.

recorrerHabitacion, como su nombre lo dice, traslada al dispositivo por toda la habitacion sensando la distancia que existe entre el y los objetos a su alrededor.
recorrerHabitacion:- write('Recorriendo Habitacion.. '),
		     nl,write('Sensar Distancia (cm): '),
		     read(Distancia),sensorProximidad(Distancia).

colocarEnSuLugar toma al objeto y lo coloca en el lugar establecido en la base de datos y una vez colocado sigue recorriendo la habitacion.
colocarEnSuLugar(Objeto,Lugar):- write('Colocando  '+ Objeto +' en  '+ Lugar),
	                         nl,recorrerHabitacion.

Dentro de la base de datos del organizador se encuentran los siguientes hechos.

Se busca que al momento de comprobar los siguientes hechos, el parametro entrante sea proporcionado por un sensor de vision, quien dentro de su memoria ya tiene identificados los objetos que se pudiera encontrar en su camino.

esRopa('Pantalon').
esRopa('Camiseta').
esRopa('Calcetin').
esRopa('Calzon').
esRopa('Sosten').
esRopa('Abrigo').
esRopa('Guante').

esBasura('Papel Arrugado').
esBasura('Botella Vacia').
esBasura('Bola de Polvo').
esBasura('Restos de Comida').

esUtencilioCocina('Vaso').
esUtencilioCocina('Plato').
esUtencilioCocina('Tenedor').
esUtencilioCocina('Cuchara').
esUtencilioCocina('Botella de Salsa Catsup').
esUtencilioCocina('Botella de Salsa Amor').
