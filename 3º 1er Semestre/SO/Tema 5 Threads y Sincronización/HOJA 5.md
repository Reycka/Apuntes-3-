 **Ejercicio 1.  Escribir un programa que cree un número de threads indicado por el primer argumento, de forma que:**
-  1º Se incluyen las lib y h necesarias para trabajar con el proyecto
	- #include <stdio.h> #include <sched.h> #include <stdlib.h> #include <unistd.h> #include <pthread.h> 
- 2º Creamos el struct thread_info que almacena toda la información relevante del thread
	- Almacena la id, el número del thread y el valor que este 
- 3º Creamos un main(int arg, char* argas[]) que será el thread padre de esta secuencia

	- Cada thread se le asignará un identificador 0,1,2…  que imprimirá por la salida estándar y usará para hacer un sleep(3) de los mismos segundos.
		- int num_threads = atoi(args[1]); utilizamos atoi para parsear el argumento a entero,pthread_attr_t attr; struct thread_info * tinfo;
		- Creamos un bucle que vaya creando un thread por cantidad indicada en el args[1], el método de create_thread viene dado por la lib y solo le debes de pasar el id del thread en cuestión, el attr --> que es NULL, nuestro método al que llamaremos cuando el thread termine y el info de ese thread
		- El método que creamos nosotros imprime el id del thread  en cuestión y lo manda a dormir por thread->num segundos
    
	- El thread principal esperará a que terminen todos los threads, mostrando el identificador del thread que termina.**
		- Cuando quiero devolver algo en un * void CUIDADO ya que no puedo devolver nada que no este almacenado en la pila puesto que se pierde
		- Para hacer esto hace falta hacer un join para asignar el thread principal
		
- **Ejercicio 2. Modificar el programa anterior para que todos los threads esperen el tiempo suficiente para consultar sus identificadores en el sistema. Ejecutar el programa con 4 threads y completar la siguiente tabla con el comando ps, usar las opciones -L (mostrar threads) y la opción de formato -o con los campos adecuados. Identificar el thread principal en la tabla.**￼￼
	- Se requiere la ejecución en segundo plano, para ello se pone & detrás del comando de ejecución
	- Se utiliza el comando ps -L para consultar los procesos de los threads (-L pilla el thread)
	- Se utiliza el comando ps -o tgid para pillar el Grupo del thread que debe coincidir con el PGID ya que ambos son lo mismo
	- Se utiliza el comando ps -o tid para pillar el id del thread que debe coincidir con el pid
	 ![[Pasted image 20260106173106.png]]
	- El thread principal es el 4855 que corresponde con el primer thread creado

| PID  | TID  | TGID | PGID | CMD            |
| ---- | ---- | ---- | ---- | -------------- |
| 4855 | 4855 | 4855 | 4855 | ./Ejercicio1 4 |
| 4855 | 4856 | 4855 | 4855 | ./Ejercicio1 4 |
| 4855 | 4857 | 4855 | 4855 | ./Ejercicio1 4 |
| 4855 | 4858 | 4855 | 4855 | ./Ejercicio1 4 |

- 💻 **Ejercicio 3. Escribir un programa que realice la suma paralela de los N primeros números naturales. Los argumentos del programa fijarán:

	- Primer argumento, el número de threads (Nt).
		- Se aplica la comprobación de argumentos y se asigna con atoi el primer argumento que es el número de threads    
	- Segundo argumento, el tamaño de bloque (Tb) que determina cuántos números sumará cada thread.
	    - Se asigna con atoi el segundo argumento que es el Tb
	- Cada thread se le asignará un identificador (i = 0,1,2…) y sumará los enteros en el rango [Tb⋅i - (i+1)⋅Tb - 1] que agregará en una variable compartida, suma. El thread principal sincronizará todos los threads y mostrará la suma.**
		- Dentro de mi método sumathread(void* arg) creo las variables init y fin que son estos límites
	- SOLUCION:
		- Creamos los threads y hacemos el join con el principal
		- Por fuera creamos las variables globales del proceso:
			- Tbloque --> El Tb del enunciadi
			- sol --> Donde vamos guardando la suma
			- mutex --> Región crítica para el trabajo multithread
		- En el sumathread realizamos las operaciones de suma que indica el enunciado no sin antes hacer un bloqueo de la suma para evitar que los datos se sobrescriban unos sobre otros
		- Finalmente escribimos la solución y liberamos tanto la memoria como el mutex (destruyendolo) una vez todos los threads hayan finalizado
		- ![[Pasted image 20260106201313.png]]
			![[Pasted image 20260106201337.png]]
-  **💻Ejercicio 4. Escribir un programa con P threads productores (primer argumento) y C threads consumidores (segundo argumento) con las siguientes características:

	- El productor escribirá en el buffer el elemento producido y el consumidor simplemente lo imprimirá en el terminal junto con las estadísticas del buffer (in, out y count). Los tiempos de producción y consumición serán de 1 y 2 segundos respectivamente.
		- Se necesita una condición de thread como variable global, un mutex y una referencia al buffer
    
	- El buffer compartido será un array circular de tamaño fijo que estará representado por una estructura similar a la siguiente:
		

	- Implementar el sistema con dos variables de condición que estarán asociadas a los siguientes  predicados: 
		- Thread consumidor: “puedo consumir”, count > 0
		- Thread producir: “puedo producir”,  count < BUFFER_SIZE 
    
	- Cada productor producirá un número fijo de elementos (NUM_ELEMENTS).
	- SOLUCION:
		- Se trabaja con las variables condicionales y el mutex, tener en cuenta que hay que mandar señales una vez se cumpla una cosa para despertar a los consumidores / productores dependiendo de una u otra
		- ![[Pasted image 20260106221712.png]]
			![[Pasted image 20260106221737.png]]
			![[Pasted image 20260106221805.png]]
			![[Pasted image 20260106221825.png]]
- **💻 Ejercicio 5. Añadir una condición de finalización al ejercicio 4 usando el patŕon centinela o píldora envenenada, de la siguiente forma:

	- El thread principal sincronizará la ejecución de todos los productores para asegurarse de que todos los elementos se han producido.
    
	- A continuación escribirá los elementos (píldoras envenenadas, por ejemplo valor -1) en el buffer, tantos como consumidores se hayan creado. Nota: Debe preservar el acceso concurrente al búfer, igual que el thread productor.
    
	- Cuando un consumidor lea la píldora envenenada del búfer terminará después de ajustar los índices y señalizar la variable de condición.
	- Sol:
		- Tan sencillo como poner una flag de if(-1) indica que he terminado y haz un break en la función del consumidor
		- Tras eso creamos un bucle para todo el numConsumidores, con el mutex y las condiciones de espera adecuadas se accede al data[in] y se le asigna el valor de -1, tras eso se manda la señal y se reactiva el mutex IMPORTANTE ANTES DE LOS JOINS
		- ![[Pasted image 20260106223104.png]]
		- ![[Pasted image 20260106223030.png]]
- **💻 Ejercicio 6.  Escribir un programa que cree L lectores (primer argumento) y E escritores (segundo argumento), de forma que:

	- Los threads de tipo Lector imprimirán por pantalla un entero compartido y esperarán 0.1s con la llamada usleep(3). Este acceso lo repetirán 5 veces.
    
	- Los threads de tipo Escritor incrementarán en 1 la variable y esperarán 0.25s. Este acceso lo repetirán 3 veces.
    
	- El thread principal arrancará primero los thread de tipo Escritor y sincronizará la finalización de todos los threads lectores y escritores.
