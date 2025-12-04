- Los digrafos valorados son grafos valorados dirigidos
- Todas las complejidades son las mismas que las que hay en los grafos valorados no dirigidos
- ALGORITMO DE Dijkstra: Es un algoritmo voraz
	- ![[Pasted image 20251026211521.png]] 
	- ![[Pasted image 20251026211937.png]]
	- ![[Pasted image 20251026212354.png]]
	- En resumen: Vas preguntando al que tenga el coste menor de todos los hijos y pasando por las aristas de menor valor, por lo que si se encuentra un camino más óptimo este se actualiza, para ello se utiliza una INDEX PQ
	- ![[Pasted image 20251026212632.png]]
	- ![[Pasted image 20251026212734.png]] ![[Pasted image 20251026212953.png]]
	- Dijkstra lo usaremos siempre que queramos calcular la distancia más corta en un grafo valorado de cualquier tipo
	- Kruskal por el contario solo lo usaremos si queremos el árbol de recubrimiento mínimo (es decir el más pequeño de todos, pero no el que indica esa distancia)
	- El BSF por el contario no se puede usar con colas de prioridad para este caso ya que es menos eficiente que Dijkstra

- CUESTIONARIOS:
	- ![[Pasted image 20251028091648.png]] Es 1
 
	- ![[Pasted image 20251028091717.png]]
	
	- ![[Pasted image 20251028091746.png]]

	- INSERTAR EN LA COLA NO SE CUENTA COMO MODIFICACIÓN 