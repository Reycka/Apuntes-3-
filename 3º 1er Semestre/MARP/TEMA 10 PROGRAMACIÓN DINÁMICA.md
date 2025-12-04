Se almacenan todas las soluciones en una tabla
El tamaño de la matriz depende del número de argumentos
La tabla tiene un valor que representa si el dato ya habia sido registrado previamente, por lo que en la funcion recursiva si no se trata de un caso base se  pregunta si el valor ubicado en la tabla i j en el caso de tener 2 argumentos es equivalente al valor por defecto, entonces el valor no habia sido registrado
- Tenemos 2 tipos de programación dinámica:
	- Descendente: 
		- Mantiene la recursion
		- Se le pasa la tabla con los problemas ya resueltos
		- Antes de resolver el problema se comprueba si 
		- ![[Pasted image 20251114194018.png]]
	- Ascendente:
		- Cambia el orden en el que se resuelve los subproblemas
		- Se resuelven los subproblemas pequeños para luego combinarlos hasta llegar al problema original
		- Se resuelven los subproblemas de menor a mayor
		- Todos los pequeños se deben resolver antes que el mayor
		- ![[Pasted image 20251114193857.png]]
		
- # Problema del cambio de monedas
	- ![[Pasted image 20251115000118.png]]
	- La respuesta al número se saca con el valor en la posicion nC 
	- Se va avanzando en la tabla hasta llegar al valor de equivalencia de la moneda:
		-  En m1 de la fila 1 comenzamos a preguntar que valor es mejor (menor en este caso)  entre la posicion actual - 1  (ese valor + 1) y la que se encuentra una fila por encima 
		- En m2 de la fila 2 es igual pero se empieza a preguntar en la posicion 4 y se hace actual - 4 en lugar de -1
		- En m3 de la fila 3 pasa lo mismo pero empezando en el 6 y haciendo actual - 6 pero nos quedamos siempre con el menor de arriba o el posterior izquierda
	- Que monedas se saca se aplica haciendo la inversa 
		- 1º En nC pregunto de donde viene el valor, ese 2 proviene de la posicion n-1C por lo que la fila n no me vale para nada y ahora me ubico en n-1 C
		- 2º Desde n - 1 C vuelvo a preguntar de donde proviene el valor que es 2, como ahora proviene de la posicion n - 1 C - 4 me desplazo hasta allí
		- 3º Desde n - 1 C - 4 vuelvo a preguntar de donde viene el valor, como proviene de n - 1 C - 8 me desplazo alli
		- 4º Como estoy en un punto donde el valor es 0 significa que he llegado y por tanto necesito dos monedas de 4 para pillar ese valor
	- A nivel de tiempo y espacio es todo del tipo O(nC) aunque se puede reducir el espacio a O(C) ya que solo nos importa los valores menores de cada fila por lo que no hace falta guardarse todo (SOLO FUNCIONA EN LAS MONEDAS) 