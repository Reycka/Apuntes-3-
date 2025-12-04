# Bloque de Control de Procesos

**Ejercicio 1. ps(1) permite ver los procesos del sistema y su estado. Estudiar la página de manual y determinar las opciones necesarias para:

- Mostrar todos los procesos del usuario actual en formato extendido. (Nota: usar la variable de entorno USER).
	- Accediendo al manual encontramos una parte donde nos habla de  las formas de uso de ps, utilizando ps ax y ps axu se saca el formato extendido 
	- Para acceder a user se hace -u
	
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
 
- Ejercicio3: teniendo "12345" > /proc/$ $/fd/1 ¿Cual es el output?
	-  Crea o machaca el archivo 1 escribiendo 12345 en la ruta marcada por proc $ $ fd --> donde $ $ es el argumento de la ruta que le pasamos. Si la ruta no existe debería controlar el error

# CREACIÓN Y GESTIÓN DE PROCESOS

- Ejercicio 5.  Escribir un programa que cree un proceso hijo con las siguientes características:
- El programa recibirá dos argumentos en la forma:  ./ejercicio5 <segundos_padre> <segundos_hijo>

- El hijo creará su propia sesión, imprimirá sus identificadores (como en el Ejercicio 2), esperará segundos hijo (segundo argumento) con la llamada sleep(3); y terminará.
    
- El padre imprimirá sus identificadores (Ejercicio 2), esperará segundos padre (primer argumento) con la llamada sleep; y terminará.
    

Ejemplo de salida:

$ ./eje5 2 1

[Padre] PID=1616, PPID=1362, PGID=1616, SID=1362. Durmiendo 2s

[Hijo] PID=1617, PPID=1616, PGID=1617, SID=1617. Durmiendo 1s

[Hijo] Terminado.

[Padre] Terminado.

Considera las siguientes ejecuciones, observa los procesos con la orden ps -lHu $USER y completa la siguiente tabla para los procesos relacionados con el ejercicio:

**

|   |   |   |   |
|---|---|---|---|
|Orden|Proceso PID|PPID, CMD ( padre)|Estado|
|./eje5 600 1&||||
||||
|./eje5 1 600&||||
||||



**

NOTA: no todas las filas son necesarias

Explica razonadamente el estado de los procesos en el primer caso (el hijo termina antes) y el PPID de los procesos en el segundo caso (el padre termina antes), identifica el proceso padre con la ayuda del comando ps(1).

Ejecuta el programa con un tiempo de espera largo (ej. ./eje5 60 60), antes de que terminen las llamadas a sleep(3) presiona Ctrl-C en el terminal. ¿Qué ocurre? ¿Mueren ambos procesos? ¿Por qué?


**💻Ejercicio 9 Escribir un programa que ejecute otro programa (ejecutable y argumentos) que se pasará como argumento. El programa creará un proceso hijo que ejecutará el programa dado en el argumento con la función execvp(3). El proceso padre esperará que termine el hijo e imprimirá su código de salida. Ejemplos de ejecución:**

$ ./eje9 cat /etc/passwd

root:x:0:0:root:/root:/bin/bash

daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin

…

El proceso hijo terminó con código de salida 0

$ ./eje9 cat /etc/shadow

cat: /etc/shadow: Permission denied

El proceso hijo terminó con código de salida 1

  

$ (./eje9 sleep 3600&) ; sleep 1 ; pkill -SIGKILL sleep

El proceso hijo terminó por señal 9

Nota: Considerar cómo deben pasarse los argumentos en cada caso para que sea sencilla la implementación. Por ejemplo: ¿qué diferencia hay entre: ./eje9 ps -el y ./eje9 "ps -el"?

**
- Ej 11: 
	- Se debe de abrir el archivo  
	- Se usa el comando write(int FileDoc,buffer[],bufferSize * typeSize)
	- Los ficheros siempre empiezan en el 0 en cuanto a bytes independientemente de la cantidad de bytes ya ocupadas, se usa lseek
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