Número de Aristas = V  * (V-1) / 2
Complejidades:
Matrices:
- Añadir cosas y comprobar O(1)
- Buscar aristas del vertice  O(V^2)
- Buscar un vertice O(V)
Adyacentes:
- Añadir O(1)
- Comprobar O(V)
- Buscar aristas del vertice O(V + A)
- Buscar un vertice O(V)

DEFINICIONES:
- Grafo Bipartito: Aquel que cumple la regla de los 2 colores (Si eres color 1 todos tus adyacentes han de ser color 2 y asi sucesivamente)
- Arbol libre: Aquel grafo que cumple que es conexo y sin ciclos
- Grafo Euleriano: Grafo Conexo cuyo grado en V es siempre par
- Grafo SemiEuleriano: Grafo conexo cuyo grado en V es siempre par salvo 2 vertices que es grado Impar
- Grafo Hamiltoniano: Grafo que posee un ciclo hamiltoniano: 
	- El ciclo hamiltoniano es un ciclo que se recorre todos los vertices del grafo exactamente 1 vez y el último vertice en el que acaba es siempre el vértice de origen 
- Grafo Isomorfo: Aquellos grafos que cumplen que sus hijos están conectados de la misma forma y tienen el mismo número de A y de V (Son el mismo grafo pero ordenado de forma diferente)
- Los grafos no dirigidos dan lugar a un equivalente de 2 aristas en la lista de adyacentes en lugar de 1, cosa que en la dirgida no ocurre
- En un recorrido de anchura el mínimo de veces que se incluye un vertice es 0 (el no conectado al origen)
- La operación para calcular los adyacentes a un vértice tiene coste en O(V) (aunque después de la lista solamente queramos saber su longitud). Y esta operación se repite para cada vértice. El coste total está en O(V2).



![[Pasted image 20260112135649.png]]
![[Pasted image 20260112135718.png]]![[Pasted image 20260112135737.png]]