![[Pasted image 20251012203812.png]]
El coste de la operación inversa es de V + A siendo V el número de vertices y A el número de aristas

Para las ordenaciones Topológicas es imprescindible que el grafo se DAF (Grafo dirigido aciclico)
se hacen llamadas dfs
En los grafos hay 2 tipos de ordenacion:

- PreOrden: Añade al grafo los vertices según vayan siendo alcanzados al marcados como visitados
- PostOrden: Añade al grafo los vertices tras haberse realizado las llamadas recursivas con sus hijos 
- ![[Pasted image 20251013195506.png]]
- Comienza en el 0 y recorre los adyacentes, primero el 1, luego el 4, como el 4 no tiene pues se inserta en el postOrden, luego lo mismo con el 1, luego se va al 2 y asi hasta visitar el grafo entero
- LA ORDENACIÓN TOPOLÓGICA ES EL POSTORDEN INVERSO (PostOrden dao la vuelta)
- La complejidad de todo esto es de V + A

- DETECCIÓN DE CICLOS: 
	- Se usa un recorrido en profundidad, si volvemos a un vertice apilado (NO VISITADO) entonces hay ciclo, es decir, que siga dentro de nuestra queue
	- Para esto se utiliza un vector auxiliar de apilados para saber que vertices están apilados y no
	- Complejidad del orden O(V + A)
	- ![[Pasted image 20251013200718.png]]

- PREGUNTAS CUESTIONARIO:
- Las componentes fuertemente conexas de un grafo dirigido de V vertices es V, ya que si no hay aristas cada vertice es una componente fuertemente conexas
- Añadir una Arsita tiene coste O(1)
- Para el recorrido en anchura NO SE USA UNA PILA
- Recorrido de Altura y anchura
- Calcular el grado de un Entrada de un grafo es de O(V + A) mientras que el de salida es O(1)
- Calcular el grafo inverso tiene un coste de O(V+A)
- Un grafo complementario es un grafo cuyas aristas son las contrarias a las que tienen y su coste es de O(V^2)
- SIEMPRE QUE EL GRAFO SEA ACICLICO EL POSTORDEN INVERSO ES UNA ORDENACIÓN TOPOLÓGICA