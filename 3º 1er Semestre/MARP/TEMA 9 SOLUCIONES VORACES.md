- TIEMPO EN EL SISTEMA MÍNIMO:
	Tenemos un parámetro de Ti que guarda el tiempo que tarda la tarea en ejecutarse sumándole el tiempo de las tareas que tardan en ejecutarse a su vez antes que ella.
	El objetivo es minimizar ese coste al mínimo posible

- TAREAS CON PLAZO FIJO Y BENEFICIO:
	![[Pasted image 20251109165317.png]] ![[Pasted image 20251109165515.png]]

	- En estos problemas se utiliza una estructura de Conjuntos Disjuntos donde se almacena para dicho conjunto el último día libre que tienen las cosas, de tal manera que al asignarse ese día se asigna la unión de conjuntos disjuntos con el día anterior, asi se consigue averiguar el último día libre de la tarea con una complejidad de O(N) para inicializar las cosas + O(NlogN) + O(N) para buscar soluciones 