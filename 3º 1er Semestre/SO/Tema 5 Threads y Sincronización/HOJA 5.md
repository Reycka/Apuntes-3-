 **Ejercicio 1.  Escribir un programa que cree un número de threads indicado por el primer argumento, de forma que:**
-  1º Se incluyen las lib y h necesarias para trabajar con el proyecto
	- #include <stdio.h> #include <sched.h> #include <stdlib.h> #include <unistd.h> #include <pthread.h> 
- 2º Creamos el struct thread_info que almacena toda la información relevante del thread
	- Almacena la id, el número del thread y el valor que este 
- 3º Creamos un main(int arg, char* argas[]) que será el thread padre de esta secuencia

	- Cada thread se le asignará un identificador 0,1,2…  que imprimirá por la salida estándar y usará para hacer un sleep(3) de los mismos segundos.
		- int num_threads = atoi(args[1]); utilizamos atoi para parsear el argumento a entero,pthread_attr_t attr; struct thread_info * tinfo;
		- Creamos un bucle que vaya creando un thread por cantidad indicada en el args[1], el método de create_thread viene dado por la lib y solo le debes de pasar el id del thread en cuestión, el attr, nuestro método al que llamaremos cuando el thread termine y el info de ese thread
		- El método que creamos nosotros imprime el id del thread terminado en cuestión y lo manda a dormir por 3 segundos
    
	- El thread principal esperará a que terminen todos los threads, mostrando el identificador del thread que termina.**
		- Cuando quiero devolver algo en un * void CUIDADO ya que no puedo devolver nada que no este almacenado en la pila puesto que se pierde