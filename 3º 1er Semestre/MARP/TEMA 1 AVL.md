Si yo tengo un arbol 1,2,3 siendo 3 la raiz de arriba
Aplico rotación simple derecha
En caso de ser al revés, se aplica rotación simple a la izquierda

Si se va en línea (izquierda,izquierda... ROTO DERECHA ; derecha, derecha.... ROTO IZQUIERDA) se aplican rotaciones simples

Si primero bajo hacia la derecha y luego a la izquierda desde el nodo desequilibrado, aplico rotación doble primero a la derecha y luego a la izquierda, y en caso de bajar primero a la izquierda y luego a la derecha entonces aplico la rotación primero izquierda y luego derecha (ir de uno a otro depende de cual es el camino más largo entre ambos)

IMPORTANTE: Solo se comprueban los 2 nodos más próximos (Si hay 4,7,15,14,16,13) y el 4 esta desequilibrado compruebo los 2 movimientos más cortos del 4, siendo estos derecha y derecha por el 7 y el 15
Para sacar la cantidad de arboles de un bosque se hace Vertices - Aristas
La altura de un árbol binario semicompleto se hace un 2^ al número y si el valor está entre n y n+1 se escoge n+1