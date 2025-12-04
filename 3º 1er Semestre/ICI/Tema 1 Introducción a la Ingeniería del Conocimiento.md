- 1.1 Sistemas basados en reglas
	- Sigue un bucle constante: 
		1) Reconocimiento: que reglas son aplicables
		2) Selección: que regla se dispara
		3) Actuación: Ejecución de la acción correspondiente 
	- Esto no funciona para problemas complejos ya que una regla puede modificar a otra generando en situaciones demasiado complejas
- 1.2 Pensamiento Heurístico
	-  Otra forma de IA, busca ejemplos de algo que se parezca y luego lo modifica dependiendo de sus variaciones con respecto al ejemplo
- 1.3 Tipos de Conocimientos:
	- Factual o declarativo
	- Procedimental (operativo)
	- Metaconocimiento o conocimiento de control
- 1.4 Reglas vs CBR
	- 1.4.1 Razonamiento basado en casos:
		- Resolver un problema en base a las experiencias, PROBLEMAS SIMILARES TIENEN SOLUCIONES SIMILARES
		- EL CBR facilita la adquisición de conocimiento
		- Con un conjunto de problemas resueltos nos vale
		- Casos + Recuperación + Adaptación < Sistema de reglas/algorítmico
		- Ciclo CBR:
			1) Base de Caso previa
			2) Entra caso nuevo
			3) Agarro los 3-5 casos más parecidos
			4) Pillo la mejor de esas
			5) Reviso que la solución vaya a funcionar
			6) Si funciona guardo este caso en la base de datos de casos previos