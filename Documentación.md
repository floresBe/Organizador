# Introducción
## Programación Lógica.
Campo que estudia el uso de la lógica para el planteamiento de problemas y el control sobre las reglas de inferencia 
para llegar a una solución automática.

La Programación Lógica forma parte de lo que se conoce como Programación Declarativa, es decir, consiste en indicar 
como resolver un problema mediante sentencias; se trabaja de una forma descriptiva, estableciendo relaciones entre entidades, 
indicando no como, sino que hacer, entonces se dice que la idea esencial de la Programación Lógica es:

_Programa= lógica + control_

Lógica (programador): hechos y reglas para representar conocimiento
Control (interprete): deducción lógica para dar respuestas (soluciones)

La programación lógica intenta resolver lo siguiente:
Dado un problema S, saber si la afirmación A es solución o no del problema o en que casos lo es. 
Además se busca que los métodos sean implantados en maquinas de forma que la resolución del problema se haga de forma automática.

_La programación lógica: construye base de conocimientos mediante reglas y hechos. _

_ Regla: _ implicación o inferencia lógica que deduce nuevo conocimiento, la regla permite definir nuevas relaciones apartir de otras ya existentes.

_ Hecho: _ declaración, cláusula o proposición cierta o falsa, el hecho establece una relación entre objetos y es la forma más sencilla de sentencia.

## Campos de Aplicación.
1. Sistemas Expertos , donde un Sistema de información imita las recomendaciones de un experto sobre algún dominio de conocimiento.

2. Demostración automática de teoremas, donde un programa genera nuevos teoremas sobre una teoría existente.

3. Reconocimiento de lenguaje natural, donde un programa es capaz de comprender (con limitaciones) la información contenida 
en una expresión lingüística humana.

4. Inteligencia artificial


5. Sistemas de información

# Descripcion de la problematica.
Se trata de un dispositivo capaz de recorrer una habitación y, con la ayuda de mecanismos creados para sostener y mover objetos, sensores cuya funcion es determinar el tipo de objeto y de una serie de conocimientos previos, colocar cada uno de los objetos con los que se tope en su lugar especificado.


# Justificación
Hoy en dia es muy comun que la vida de las personas sea mas activa que antes, es decir, no es raro conocer a una persona que estudie y trabaje a la vez, o que tenga mas de un trabajo. Es un estilo de vida que deja a cualquier persona desorganizada con tiempo a penas para comer y dormir antes de empezar de nuevo el dia a dia. Este tipo de situaciones genera, entre otras cosas, una eterna falta de organizacion y limpieza en las habitaciones en las que generalmente se llevan a cabo las actividades del diario. 

# Desarrollo.
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

La deteccion de objetos se rige por las siguientes reglas.
Donde segun la distancia a comprobar, se sabe si hay un objeto cerca o no; dicha distancia es proporcionada por un sensor de proximidad entregada en cm.

Una distancia de 10 cm o menos implica un objeto cerca. 
objetoEncontrado(Distancia):-Distancia=<10.

Una distancia mayor a 10 y menor a mil implica que no hay ningun objeto cerca.
objetoNoEncontrado(Distancia):-Distancia>10, Distancia < 1000.

Una distancia igual o mayor a mil significa que el dispositivo esta fuera de rango.
fueraDeRango(Distancia):- Distancia >= 1000.

En base a los conocimientos recien establecidos, se sabe si hay objeto o no, segun la respuesta, el sensor de proximidad actua.

Encontrar un objeto implica utilizar el sensor de vision para saber que tipo de objeto es.
sensorProximidad(Distancia):- objetoEncontrado(Distancia),write('Un Objeto Encontrado..'),
			      nl, write(' Sensar Objeto: '),read(Objeto),sensorVision(Objeto).
			      
No encontrar ningun objeto cerca implica seguir recorriendo la habitacion.
sensorProximidad(Distancia):- objetoNoEncontrado(Distancia), write('Nngun Objeto Encontrado..'), 
			      nl,recorrerHabitacion.

Si el objeto mas cercano se encuentra a 1000 o cm, significa que el dispositivo salio de rango y se apagara.
sensorProximidad(Distancia):- fueraDeRango(Distancia), write('Fuera de rango, Apagando..').

Para detectar el tipo de objeto, se utilizaron las siguientes reglas.
Una vez detectado un objeto, se dispara la accion de sensar el objeto para saber de que tipo es, como anteriormente se explico, esta informacion es obtenida por un sensor de vision.

En la base de datos actual se encuentran 3 tipos de objetos registrados, para los cuales se desata una accion diferente para cada uno al momento de encontrarlos.

Si el objeto encontrado es ropa, habra que verificar si esta esta limpia o sucia.
sensorVision(Objeto):-esRopa(Objeto),write('El objeto encontrado es Ropa '),
		      nl,write('Sensar Suciedad (0% - 100%): '), read(Nivel),sensorSuciedad(Objeto,Nivel).
		      
Si el objeto es basura, se busca identificar si se encuentra fuera de su lugar.	
sensorVision(Objeto):-esBasura(Objeto),write('El objeto encontrado es basura'),
		      nl,write('Sensar Lugar: '), read(Lugar), estaEnSuLugar(Objeto,Lugar).
		      
Si el objeto es un utencilio de cocina, se envia directamente a la cocina.
sensorVision(Objeto):-esUtencilioCocina(Objeto),write('El objeto Pertencece a la cocina.'),
		      colocarEnSuLugar(Objeto,'Cocina').

Existen reglas con las que se puede inferir si un objeto esta limpio o sucio.

Un nivel de suciedad igual o mayor al %50 implica que el objeto esta sucio.
estaSucio(Nivel):- Nivel>=50.

Un nivel de suciedad menor al %50 implica que el objeto aun esta limpio.
estaLimpio(Nivel):-Nivel<50.

Segun la suciedad y el objeto encontrado, revisar .
sensorSuciedad(Objeto,Nivel):-estaSucio(Nivel),write('El '+ Objeto +' esta sucio..'),
			      nl,write('Sensar Lugar: '), read(Lugar), estaEnSuLugar(Objeto,Lugar,Nivel).
sensorSuciedad(Objeto,Nivel):-estaLimpio(Nivel),write('El '+ Objeto +' esta limpio..'),
	                      nl,write('Sensar Lugar: '), read(Lugar), estaEnSuLugar(Objeto,Lugar,Nivel).
			      
Los lugares de los objetos estan registrados dentro de las siguientes reglas.

cuando el objeto es ropa, puede estar limpia o sucia, dependiendo de esto, cambia su lugar ..

Si el objeto esta en su lugar, se vuelve a recorrer la habiatacion en busca de mas objetos.
estaEnSuLugar(Objeto,'Armario',NivelSuciedad):- esRopa(Objeto),estaLimpio(NivelSuciedad),
	                                        nl,write('El '+ Objeto +' se encuentra en su lugar.'),
						nl, recorrerHabitacion.
estaEnSuLugar(Objeto,'Cesto',NivelSuciedad):- esRopa(Objeto),estaSucio(NivelSuciedad),
					      nl,write('El '+ Objeto +' se encuentra en su lugar'),
					      nl, recorrerHabitacion.
Si el objeto no esta en su lugar, lo lleva directo a el.						
estaEnSuLugar(Objeto,Lugar,NivelSuciedad):- esRopa(Objeto),estaLimpio(NivelSuciedad),\+(Lugar = 'Armario'),
					    nl,write('El '+ Objeto +' No se encuentra en su lugar'),
					    nl,colocarEnSuLugar(Objeto,'Armario').
estaEnSuLugar(Objeto,Lugar,NivelSuciedad):- esRopa(Objeto),estaSucio(NivelSuciedad),\+(Lugar = 'Cesto'),
					    nl,write('El '+ Objeto +' No se encuentra en su lugar'),
					    nl,colocarEnSuLugar(Objeto,'Cesto').
Cuando el objeto es basura, su lugar es el cesto.
misma logica, que en la regla anterior.
estaEnSuLugar(Objeto,'Cesto'):- esBasura(Objeto),
				write(Objeto +' se encuentra en su lugar'),
				nl, recorrerHabitacion.
estaEnSuLugar(Objeto,Lugar):- esBasura(Objeto),\+( Lugar = 'Cesto'),
                              nl,write(Objeto +'No se encuentra en su lugar'),
                              nl,colocarEnSuLugar(Objeto,'Cesto').
			      
# Resultados.

Encender dispositivo:

1 ?- encender.
Dispositivo Encendido.. 
Recorriendo Habitacion.. 
Sensar Distancia (cm): 20.
Nngun Objeto Encontrado..Recorriendo Habitacion.. 
Sensar Distancia (cm): |: 15.
Nngun Objeto Encontrado..Recorriendo Habitacion.. 
Sensar Distancia (cm): |: 13.
Nngun Objeto Encontrado..Recorriendo Habitacion.. 
Sensar Distancia (cm): |: 10.
Un Objeto Encontrado..
 Sensar tipo de Objeto: |: 'Pantalon'.
El objeto encontrado es Ropa 
Sensar Suciedad (0% - 100%): |: 25.
El +Pantalon+ esta limpio..
Sensar Lugar: |: 'Piso'.

El +Pantalon+ No se encuentra en su lugar
Colocando  +Pantalon+ en  +Armario
Recorriendo Habitacion.. 
Sensar Distancia (cm): |: 10.
Un Objeto Encontrado..
 Sensar tipo de Objeto: |: 'Papel Arrugado'.
El objeto encontrado es basura
Sensar Lugar: |: 'Piso'.

Papel Arrugado+No se encuentra en su lugar
Colocando  +Papel Arrugado+ en  +Cesto
Recorriendo Habitacion.. 
Sensar Distancia (cm): |: 10.
Un Objeto Encontrado..
 Sensar tipo de Objeto: |: 'Calzon'.
El objeto encontrado es Ropa 
Sensar Suciedad (0% - 100%): |: 95.
El +Calzon+ esta sucio..
Sensar Lugar: |: 'Cama'.

El +Calzon+ No se encuentra en su lugar
Colocando  +Calzon+ en  +Cesto
Recorriendo Habitacion.. 
Sensar Distancia (cm): 1000.
Sensor Fuera de Rango, Apagando..
true.

# Conclusion.
Con este ejemplo lo que podemos concluir es que cualquier tipo de conocimientos que un humano pueda tener, es posible transmitirselo a una maquina o cosa. Es importante destacar que la inteligencia artificial esta inspirada por el hecho de que cualquier persona busca facilitar su vida, ese es presisamente el trabajo de la programacion logica, darle a un objeto la capacidad de decidir cual es la mejor opcion a realizar segun los parametros recibidos, para asi poder encargarle una tarea de la cual el ser humano busca deshacerse.
