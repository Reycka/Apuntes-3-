- Fuerza = -k * X (en vectores)
- Ley de Hooke:
	- F = -k(|d| - l_o) * (d/|d|)
	- d => Vector que une los extremos del muelle
	- l_o Longitud del muelle en reposo
- Implementación:
	- La idea es tener 2 generadores de fuerza, una para el pinto A y otra para el punto B
		- Se necesitará la K
		- El L_o
		- La otra partícula para saber la distancia de una a otra
		- Este generador recibe otra partícual (A) para saber como colisiona con ella


# FLOTACIÓN:
- Destacamos 2 fuerzas en caso de que no haya fricción, una fuerza en el eje -y que es la Fg y otra fuerza en el eje y que es el Empuje (E) donde el Empuje = (Volumen sumergido * densidad del líquido) * gravedad, la fuerza de la gravedad es Mo * g
- Si la Fg > E el objeto se hunde, si ambas fuerzas son iguales, el objeto se queda quieto
- Importante cambiar el damping, trabajar con volumenes proporcionales al tamaño de la partícula 1m^3 ES UNA BARBARIDAD