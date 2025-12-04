- Como se representan los casis:
	- Sacar los datos de dicho casos
		- PPIL, POSICIONES, DISTANCIAS, DIRECCIONES,DistPP,Level
	- La solución del caso:
		- El movimiento que se deben usar
	- Resultado:
		- FR( T ): [0 - 100] me dice como de viable es mi camino
- Organización de memoria:
	- Son varios CBR (una por grupo)
	- Hacer un árbol en el que se vaya dividiendo los casos en un arbol
		- Si es edible (rama izq) si no rama(der) 
- Resumen:
	- La base de datos almacena los datos y al pasarle un caso nuevo se hace una comparativva que devuelven un valor de similitud entre casos, posteriormente se hace una media ponderada (ya que hay atributos más importantes que otros) y al final el que más puntos tenga será mi intervalo de similitud por lo que le añado a la lista de casos más parecidos (En caso de que la similitud sea inferior a cierto ratio le dejo en random y que aprenda)
	
- IMPORTANTE LA FUNCION DE ADAPTACION:
		- Puede ocurrir que el caso más similar sea el que peor resultado da
		- FA(SOL_k, Sim_k,Result_k)
		
- FUNCION DE RECUERDO:
	- Fremember: En caso de que haya un caso muy similar pero con peor resultado es lógico insertar el caso por el que se ha parecido (En caso de ser varios, el de peor resultado es el sustituido)
- Pasos:
	- Definir los casos:
		- Pocos hace que sea tonto
		- Muchos hace que sea muy costoso
		
	- Gestor de memoria:
		- Lineal (mejor no)
		- Arboles (mejor)
		
	- Hacer la funcion resultado
		- Como saca el valor de dicho resultado
		
	- Funcion de similitud:
		- Como se hace la compartativa de casos entre el actual y los de la lista
		- se saca la media ponderada de dichos casos
		- Me quedo con las 3 más similares
		- Comparo si cumplen la similitud minima
		
	- Funcion de adaptacion
		- En caso de tener varias con el mismo resultado tomar ese resultado
		- En caso de tener resultados distintos Pillar el que mejor resultado de
		
	- Funcion de recuerdo:
		- Si el resultado obtenido es mejor que el de menor resultado de esos 3, se sustituye ese por el nuevo caso








# CHARLA DE MAXI:

#IMPORTANTE
- Si tengo caso a y caso b siendo ambos 2 casos contiguos la solución del caso a es el movimiento que tiene PacMan en el caso b!!!! 
- Al tomar un caso simulo los posibles movimientos que puede tomar PacMan en ese momento y esas simulaciones van a preguntar a la CBR los casos más similares y va a tomar el mejor de esos casos, haciendo que estos se vuelvan a comparar para asignarle el mejor movimiento posible a msPacMan. 
- Para la función de similitud de los vectores se utiliza la inversa de la funcion euclidiana




# ALGUN QUE OTRO APUNTE DE CBR EXTRA
- Cuidao Espejo!!
- Comparacion de distancias: 1- ((|Distancia de la base de datos - Distancia del caso|) / MaxDist) 
- La simulación se hace en la función de revisión que da nuestro Resultado que se usará en la función de adaptación
- Se pueden tener atributos compuestos (Las distancia a los fantasmas en un único atributo y luego hacer la media con las posiciones de los fantasmas y trabajo con ese único valor)
- Atributo numerico valorado y Simbólico jerarquico univalorado (Interesantes oara itris trabajos)
- Los casos se guardan en CSV, pueden ser uno o varios, cuanto más CSV hay menos comprobaciones por tick tengo que hacer
- Cada fila del CSV corresponde con un caso, y la columna con el atributo en cuestión.

- NO FUNCIONAN LOS PRIMITIVOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOS



- Espejo:
	- El mapa es simétrico solo en X por lo que a lo mejor podemos guardarnos los casos solo para que afecten a un lado (si ocurre un caso en el lado contrario podemos preguntar si hay alguno parecido en el caso contrario o incluso si no lo hay guardarnos ese caso pero a la inversa)
	- También podemos guardar ambos aunque no lo veo necesario
	- Esto facilita mucho el almacenamiento de casos pues se reducen a la mitad los casos sin perder información
- Recuerdo:
	- Solo tomar los casos si superan el >0.5 y solo tomar los 3 más parecdos (no quiero todos los casos, quiero los 3 primeros que superen el 0.95 o 0.92...) 
-  INPUT_
	- ID
	- EDIBLE
	- LEVEL
	- LISTANODOS --> Vector Integrer
	- TIME
	
	
	- 1,1,FALSE,1,3#5#7,2000 lo del # lo hacemos nosotros
- EVALUACION DE LOS CASOS:
	- En el Execitor test, cambiamos el executor por runCBRExperiment el cual se encuentra en una clase nueva que hay que incluir en el MsPacManEngine
	- El PacMan Controler debe extender de PacManCBRControler