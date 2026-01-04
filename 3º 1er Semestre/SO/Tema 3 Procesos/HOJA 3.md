# Bloque de Control de Procesos

**Ejercicio 1. ps(1) permite ver los procesos del sistema y su estado. Estudiar la página de manual y determinar las opciones necesarias para:

- Mostrar todos los procesos del usuario actual en formato extendido. (Nota: usar la variable de entorno USER).
	- Accediendo al manual encontramos una parte donde nos habla de  las formas de uso de ps, utilizando ps ax y ps axu se saca el formato extendido 
	- Para acceder a user se hace -u
	- Se usa la opción -l -a -u $USER -f da toda la informacion de USER en formato extendido
	
- Mostrar los procesos del sistema, incluyendo el identificador del proceso, el identificador del grupo de procesos, el identificador de sesión, el estado y el comando con todos sus argumentos.
	-  El odemtificador de grupo el PID del proceso mientras que el identificador del proceso igual ya que la terminal lo asocia por defecto, el identificador de sesión es el start y el del estado es stat
    
- Observar el identificador de proceso, grupo de procesos y sesión de los procesos. ¿Qué identificadores comparten la shell y los programas que se ejecutan en ella (usar la opción -H para identificar fácilmente la relación entre procesos)? 
	- Comparten la pid con la PID , el TTY, el Stat y el START 
    
- ¿Cuál es el identificador de grupo de procesos cuando se crea un nuevo proceso? Usar el comando sleep para poder verlo fácilmente en la salida del comando ps.
    - El identificador del proceso es el identificador del proceso del padre
    
- **Ejercicio 2. Escribir un programa que muestre los identificadores del proceso (PID, PPID, PGID y SID), el identificador del usuario y grupo, y su directorio de trabajo actual.
	- Creamos el archivo de c
	- Incluimos las librerías necesarias en la cabecera
		- stdio.h 
		- stdlib.h
		- unistd.h
	- Agregamos un main sin argumentos ya que no debemos pasarle ninguno
	- Hacemos un printf de los distintos casos que nos piden:
		-  getpid
		- getppid
		- getpgid
		- getsid(getpid())
		- getuid()
		- getcwd(NULL,0)
		- ![[Pasted image 20251231192345.png]]
 
- Ejercicio3: teniendo "12345" > /proc/$ $/fd/1 ¿Cual es el output?
	-  Crea o machaca el archivo 1 escribiendo 12345 en la ruta marcada por proc $ $ fd --> donde $ $ es el argumento de la ruta que le pasamos. Si la ruta no existe debería controlar el error


- **Ejercicio 4. Consulta el tipo de fichero y contenido de los siguientes ficheros del proceso de la shell actual (/proc/ $ $) completa la siguiente tabla:**
	- Para acceder al sistema de ficheros que es proc basta con estar en la raiz y hacer cd proc/$ $ --> El cual apunta al proceso actual
	- ALGUNAS DE LAS DESCRIPCIONES SE ENCUENTRAN EN EL MAN

|         |                             |                                                                     |
| ------- | --------------------------- | ------------------------------------------------------------------- |
| Fichero | Tipo<br><br>enlace, dir,... | Descripción<br><br>contenido/propósito                              |
| cmdline | fichero regular vacío       | Como se inicializa el proceso                                       |
| cwd     | enlace simbólico            | Apunta al directorio de trabajo actual del proceso.                 |
| environ | fichero regular vacío       | Contiene las variables de entorno del proceso.                      |
| exe     | enlace simbólico            | Apunta al archivo ejecutable del proceso                            |
| fd      | directorio                  | Contiene enlaces simbólicos a los descriptores de archivo abiertos. |
| limits  | Fichero regular vacío       | Muestra los límites del proceso                                     |
| maps    | fichero regular vacío       | Distribución de la memoria del proceso actual                       |
| root    | Enlace simbólico            | Da acceso a la raíz del sistema de archivos                         |



# CREACIÓN Y GESTIÓN DE PROCESOS

- Ejercicio 5.  Escribir un programa que cree un proceso hijo con las siguientes características:
- El programa recibirá dos argumentos en la forma:  ./ejercicio5 <segundos_padre> <segundos_hijo>
	- Se gestiona el error con args averiguando si es que estos son el número adecuado (2 por lo que args tiene que ser 3)
	- Se usa atoi para parsear el tiempo a int

- El hijo creará su propia sesión, imprimirá sus identificadores (como en el Ejercicio 2), esperará segundos hijo (segundo argumento) con la llamada sleep(3); y terminará.
    - IMPORTANTE: El padre ya existe, es el proceso que se crea al iniciar el programa, por eso el fork hace un hijo de este proceso
    - Para los parámetros del hijo no se usa el pid que genera el fork, se usan los métodos getpid,getpgid... PORQUE TOMAN EL PROCESO ACTUAL QUE EN EL CASO DE CREAR EL HIJO ES EL HIJO
- El padre imprimirá sus identificadores (Ejercicio 2), esperará segundos padre (primer argumento) con la llamada sleep; y terminará.
	- ![[Pasted image 20251231201414.png]]
	    

Ejemplo de salida:

$ ./eje5 2 1

[Padre] PID=1616, PPID=1362, PGID=1616, SID=1362. Durmiendo 2s

[Hijo] PID=1617, PPID=1616, PGID=1617, SID=1617. Durmiendo 1s

[Hijo] Terminado.

[Padre] Terminado.

Considera las siguientes ejecuciones, observa los procesos con la orden ps -lHu $USER y completa la siguiente tabla para los procesos relacionados con el ejercicio:

**

|               |             |                    |                                                            |
| ------------- | ----------- | ------------------ | ---------------------------------------------------------- |
| Orden         | Proceso PID | PPID, CMD ( padre) | Estado                                                     |
| ./eje5 600 1& | 5934        | 5933               | Z                                                          |
|               | 5933        | 5012               | S                                                          |
| ./eje5 1 600& | 5812        | 5811               | S (se queda huerfano y es adoptado por el padre del padre) |
|               | 5811        | 5309               | Z                                                          |



**

NOTA: no todas las filas son necesarias

Explica razonadamente el estado de los procesos en el primer caso (el hijo termina antes) y el PPID de los procesos en el segundo caso (el padre termina antes), identifica el proceso padre con la ayuda del comando ps(1).

Ejecuta el programa con un tiempo de espera largo (ej. ./eje5 60 60), antes de que terminen las llamadas a sleep(3) presiona Ctrl-C en el terminal. ¿Qué ocurre? ¿Mueren ambos procesos? ¿Por qué?
	- Los procesos terminan su ejecución y la llamada a sleep se cancela

- **💻Ejercicio 6. kill(1) permite enviar señales a un proceso o grupo de procesos por su identificador (pkill(1) permite hacerlo por nombre de proceso). Estudiar la página de manual y las señales que se pueden enviar a un proceso.**
	- Se pasa el comando la señal y el PID  kill -signal pid
	- Si le agrego un - al pid es para indcar el gripo del proceso	
- **💻Ejercicio 7. En un terminal, arrancar un proceso de larga duración (ej. sleep 600). En otra terminal, enviar diferentes señales al proceso (terminar, interrumpir, parar, continuar) y comprobar el comportamiento.** 
	- ![[Pasted image 20260102180000.png]]
- **Ejercicio 8. Determina las opciones adecuadas para el comando kill(1) para terminar (SIGINT) los dos procesos que se crean en la ejecución del programa del ejercicio 5.**
	- En una terminal ejecuto el proceso, esa terminal está trabajando ese proceso por lo que necesito otra terminal distinta para parar el otro proceso
	- En la otra terminal ejecuto el comando kill -SIGINT -PGID para forzar la detención del programa (como si de un ctrl  C se tratase)
	
- **💻Ejercicio 9 Escribir un programa que ejecute otro programa (ejecutable y argumentos) que se pasará como argumento. El programa creará un proceso hijo que ejecutará el programa dado en el argumento con la función execvp(3). El proceso padre esperará que termine el hijo e imprimirá su código de salida. Ejemplos de ejecución:**
	- ![[Pasted image 20260102185741.png]]
	- ![[Pasted image 20260102185828.png]]

	- Nota: Considerar cómo deben pasarse los argumentos en cada caso para que sea sencilla la implementación. Por ejemplo: ¿qué diferencia hay entre: ./eje9 ps -el y ./eje9 "ps -el"?
		- Uno lo trata como toda la pila de procesos de ps y el otro como el texto ps -el

- **Ejercicio 10  Dibuja el esquema jerárquico de los procesos creados en la ejecución del siguiente programa con argc=3:

void main(int argc, char *argv[])

{

    int i;

    for(i=1; i<=argc; i++)

    {

        pid_t pid = fork();

        ...

    }

    return 0;

}

- Respuesta:
	- El esquema es: 
		- 1ª iteracion: Padre -> Hijo1; Hijo1 -> Hijo2; Hijo2->Hijo3
		- 2ª iteración el padre sigue: Padre-> Hijo2; Hijo2 -> Hijo3
		- 3ª iteración el padre sigue: Padre -> Hijo3
	
- Ej 11: 
	- Se debe de abrir el archivo  
	- Se usa el comando write(int FileDoc,buffer[],bufferSize * typeSize)
	- Los ficheros siempre empiezan en el 0 en cuanto a bytes independientemente de la cantidad de bytes ya ocupadas, se usa lseek
	- IMPORTANTE: Siempre que un hijo tiene que hacer algo se debe hacer un wait al padre con el do while que esta en el man de wait porque si no eso empieza a ir por libre (sin el wait el padre se puede ejecutar más de una vez y es liada), del mismo modo si un hijo termina se le hace un exit para que pase a estado zombie
	- ![[Pasted image 20260102200630.png]]
	- ![[Pasted image 20260102200718.png]]
	- **Ejercicio 12 Considera el programa descrito en el Ejercicio 11. Dado que la tabla de descriptores se hereda ¿Es posible usar el descriptor de fichero abierto por el padre en los hijos?
		- La respuesta es que sí ya que la tabla de descriptores almacena todos los archivos que tuviera el padre almacenados y si el padre abrió/desplazó algún byte eso se ve reflejado en la tabla de descriptores del hijo que es un puntero a la del padre
	- **Ejercicio 13 Considere el código que se muestra a continuación:

int global;

void main() {

    int   local=3;

    pid_t pid;

  

    global=10;

    pid = fork();

    if (pid == 0 ) {

        global = global + 5;

        local  = local + 5;

    }

    else {

        wait(NULL);

        global += 10;

        local  += 10;

    }

    printf(“global:%d local:%d\n”, global, local);

} 

- Determine qué mensajes se imprimirán en la terminal. ¿Es posible que el resultado de la ejecución del programa cambie según el orden en que se ejecuten los procesos padre e hijo?. Nota: suponer que todas las llamadas al sistema se ejecutan exitosamente.
	- 1º El proceso padre espera al hijo (global = 10 local = 3)
	- 2º El proceso hijo suma 5 a global y a local (global = 15 y local = 8), como no hago exit el proceso sigue hasta llegar al printf por lo que imprime los valores que son 15 y 8
	- 3º Al terminar el hijo le toca al padre que suma 10 a global y local que pasan de valer 10 y 3 a 20 y 13 respectivamente siendo estos los valores que imprime
	- Los valores no cambian ya que el wait obliga al padre a esperar al hijo y tanto el global como el local no cambian
- **Ejercicio 14 Considere el código que se muestra a continuación:

int a = 3;

void main() {

    int b=2;

    for (i=0;i<4;i++) {

        pid_t p=fork();

        if (p==0) {

            b++;

            execlp("/usr/bin/sleep", “/usr/bin/sleep”, “2”, NULL);

            a++;

        }

        else {

           wait(NULL);

           a++;

           b--;

        }

    }

    printf(“variables - a:%d b:%d\n”, a, b);

}

- Determine qué mensajes se imprimirán en la terminal. ¿Cuántos procesos se crean en total? ¿Cuántos coexisten en el sistema como máximo?. Nota: suponer que todas las llamadas al sistema se ejecutan exitosamente.
	- Se crean 4 procesos hijo, en total son 5 procesos si contamos al padre
	- El exelcp hace que el código del hijo se modifique por completo por lo que deja de ejecutarse y se pierde todo lo del print de abaji
	- Por tanto y como esta dentro de un for el resultado esperado es a= 7 y b=-2
		- a = 7 porque sale de hacer el a++ de cada wait y b = -2 pq sale de hacer el b-- de cada wait
# Planificación Procesos

- Ejercicio 16. En un sistema monoprocesador se ejecutan los procesos mostrados a continuación (todos los tiempos son en segundos): (EXAMEN)

|         |         |     |     |     |     |
| ------- | ------- | --- | --- | --- | --- |
| Proceso | Llegada | CPU | E/S | CPU | E/S |
| P1      | 0       | 1   | 5   | 1   | -   |
| P2      | 1       | 3   | 1   | 1   | 1   |
| P3      | 0       | 5   | 4   | 1   | -   |
| P4      | 3       | 3   | 2   | 1   | 1   |

  

Determina los tiempos de retorno (turnaround) y de espera para cada proceso y la productividad (throughput) del sistema para las siguientes políticas de planificación:

- First Come First Serve (FCFS)
		
| tiempo | P1     | P2     | P3             | P4     | Cola preparados |
| ------ | ------ | ------ | -------------- | ------ | --------------- |
| 0      | w      |        | R,5(dnd acaba) |        | P3,P1           |
| 1      | w      | w      | R              |        | P1,P2           |
| 3      | w      | w      | R              | w      | P1,P2,P4        |
| 5      | R,6    | w      | E/S,9          | w      | P2,P4           |
| 6      | E/S,11 | R,9    | E/S            | w      | P4              |
| 9      | E/S    | E/S,10 | E/S            | R,12   |                 |
| 10     | E/S    | w      | w              | R      | P3,P2           |
| 11     | w      | w      | w              | R      | P3,P2,P1        |
| 12     | w      | w      | R, 13          | E/S,14 | P2,P1           |
| 13     | w      | R,14   | -              | E/S    | P1              |
| 14     | R,15   | E/S,15 | -              | w      | P4              |
| 15     | -      | -      | -              | R,16   | P1              |
| 16     | -      | -      | -              | E/S,17 |                 |
| 17     | -      | -      | -              | -      |                 |
- Tiempo de TurnAround:
	- TwP1 =  (5-0) + (14-11) = 8 //Tiempo que esta en waiting
	- TtaP1 = (15 - 0) = 15//Tiempo de que entra hasta que acaba
	- TwP2 = (6-1) + (10-13) = 8
	- TtaP2 = 15 - 1 = 14
	- IGUAL PA P3
	- IGUAL PA P4
	- Productividad = 1 trabajo cada 4.2 segundos (TOTAL TRABAJOS/TIEMPO FINAL)

- Shortest Job First (SJF)
    
- Round Robin (RR) con cuanto de **3s ESTO ES LO QUE ME PERMITE HACER UNA TAREA HASTA ESPERAR**
    

| tiempo | P1    | P2      | P3                                     | P4      | Cola Preparados |
| ------ | ----- | ------- | -------------------------------------- | ------- | --------------- |
| 0      | R,1   |         | W                                      |         | P3              |
| 1      | E/S,6 | w       | R,4 (2(tiempo restante al llegar a 4)) |         | P2              |
| 3      | E/S   | w       | R                                      | w       | P2,P4           |
| 4      | E/S   | R,7(0)  | w                                      | w       | P4,P3           |
| 6      | w     | R       | w                                      | w       | P4,P3,P1        |
| 7      | w     | E/S,8   | w                                      | R,10(0) | P3,P1           |
| 8      | w     | w       | w                                      | R       | P3,P1,P2        |
| 10     | w     | w       | R,12                                   | E/S 12  | P1,P2           |
| 12     | R,13  | w       | E/S.,16                                | w       | P2,P4           |
| 13     | -     | R,14    | E/S                                    | w       | P4              |
| 14     | -     | E/S, 15 | E/S                                    | R,15    |                 |
| 15     | -     | -       | E/S                                    | E/S,16  |                 |
| 16     | -     | -       | R,17                                   | -       |                 |
| 17     | -     | -       | -                                      | -       |                 |
- Sacar los tiempos y la productividad

Round Robin (RR) con cuanto de 1s**

- Ejercicio 17. Considere un sistema monoprocesador con una política de planificación de procesos de 3 niveles con realimentación. Los procesos que agotan el cuanto bajan de nivel y los que ceden la CPU antes de agotarlo son promocionados. Además cuando un proceso acaba una operación de E/S se añade a la cola de espera de mayor prioridad. Cada nivel usa una política round robin cuyos cuantos de tiempo son 2, 4 y 8, respectivamente para cada nivel.

Al principio hay 3 procesos en la cola del nivel 1 (máxima prioridad) y el resto de colas están vacías. Los procesos tiene el siguiente patrón de ejecución que se repite indefinidamente:

|   |   |   |
|---|---|---|
|Proceso|CPU|E/S|
|P1|3|5|
|P2|8|5|
|P3|5|5|

Dibuja un diagrama de gantt para la ejecución para los primeros 30s que muestre además el estado de las colas de espera de cada nivel.  Calcula los tiempos de espera de cada proceso.

**