# Manejo de Ficheros y Directorios:

- **Ejercicio 1. ls(1) muestra el contenido de directorios y los atributos básicos de los ficheros. Consultar la página de manual y estudiar el uso de las opciones -a -l -d -h -i -R -1 -F.**

	- -a (-all): Hace que ls no ignore los archivos que empiezan por .
	- -l: Hace que se devuelva con una lista de formato de tipo long, devuelve el mayor y el minor
	- -d (directory):  Devuelve solo los directorios, no sus contenidos
	- -h (human, readable): con -l y -s devuelve el tamaño que ocupa el directorio entero
	- -i(inodo): devuelve el i-nodo en el que se encuentra cada archivo  
	- -R(Reverse): devuelve la lista ordenada en sentido contrario
	- -1: devuelve una lista con un archivo por linea, se puede evitar el "\n" con -q o -b
	- -F(classify): append indicator (one of */=>@|) to entries

- ** Ejercicio 2.  Considerar el directorio /run:

	- **Escribir un comando que obtenga  las características detalladas de todos los ficheros.
	    - 1º Me coloco con cd en el directorio en cuestión
	    - 2º Utilizo el comando ls -a para sacar todos los contenidos del directorio
	- **¿Cuántos tipos de ficheros (directorio, fichero regular, enlace…) diferentes hay?
		- 1º El ls se devuelve con un sistema de colores que representa un tipo de fichero u otro. 
	    - 2º Utilizo la función stat para identificar que tipo de fichero es (star "NOMBRE")
	    - 3º Tras comprobar todo y contar hay un total de 6 

	- **Escribir una línea de comandos que muestre qué  tipos diferentes hay en ese directorio. Los tipos se indicarán con el caracter (d, -, l...) usado por el comando ls. Ejemplo:**
		-  Se usa ls -F --file-type "NOMBRE"

- **Ejercicio 3.  Crear un fichero en el directorio home del usuario con la orden:**
	- ¿Cuál es el inodo del fichero?
	    - El inodo es el 256398
	- ¿Qué usuario puede leer los contenidos del fichero? ¿y modificarlo?
	    - En este caso ninguno tiene acceso ni a la lectura ni a la modificación (ni el usuario, ni el grupo ni nadie externo) 
	- ¿Cuál es el tamaño del fichero? ¿Cuántos bloques ocupa en el sistema de ficheros?
		- El tamaño del fichero es de 4 y ocupa 8 bloques
	- ¿Cuál es la ruta del disco (relativa a /dev) dónde se almacena el archivo? 
		- Su ruta es 4096

	- Determinar qué atributos del inodo del fichero cambian cuando se ejecutan los siguientes comandos:
		- touch archivo.txt
			- Modifica los tiempos de acceso y los tiempos de modificación 
		- echo “Otra línea más en el fichero” >> archivo.txt
			- cModifcia el tamaño (size) asi como sus tiempos de modificación
		- cat archivo.txt
			- Modifica los tiempos de acceso 
		
- **Ejercicio 4. Escribir un programa (mistat) que emule el comportamiento de stat(1). El programa aceptará un único argumento que será la ruta del fichero del que se quiere obtener la información. Si el fichero no existe se informará del error. La información del fichero será:**
	- El número major y minor asociado al dispositivo, ver major(3)/minor(3).
    
	- El número de inodo del fichero.
    
	- El tipo de fichero (únicamente considerar directorio, enlace simbólico o fichero ordinario).

	- La hora en la que se accedió el fichero por última vez. ¿Qué diferencia hay entre st_mtime y st_ctime?
		- st_mtime corresponde con la última modificación
		- st_ctime corresponde con el último cambio en metadatos
	
# Sistema de Ficheros:

- **Ejercicio 10.  Un dispositivo de memoria flash de 64 MB de capacidad y bloques de 1KB, contiene un sistema de ficheros FAT. Describa la estructura de la tabla y cómo se representa la asignación de bloques a un fichero. ¿Cuántos bytes son necesarios para almacenar la tabla FAT?**
	- ![[Pasted image 20251010114727.png]]
	 
-  **Ejercicio 11. En la siguiente figura se representa una tabla FAT y el contenido de cierto directorio: que incluye: el nombre del archivo, el tipo (F=archivo, D=directorio) y el número del bloque inicial. El tamaño del bloque es 512b

|     |                  |     |                  |     |             |      |        |                 |
| --- | ---------------- | --- | ---------------- | --- | ----------- | ---- | ------ | --------------- |
|     | Bloque siguiente |     | Bloque siguiente |     | Nombre      | Tipo | Bloque | Que bloques usa |
| 0   | EOF              | 10  | 11               |     | DATA.TXT    | F    | 3      | 3,15,5,6        |
| 1   | 2                | 11  | EOF              |     | DATA1.TXT   | F    | 0      | 0               |
| 2   | 4                | 12  |                  |     | DATA2.TXT   | F    | 1      | 1,2,4           |
| 3   | 15               | 13  |                  |     | LOGS        | D    | 7      | 7               |
| 4   | EOF              | 14  |                  |     | RESULTS.JPG | F    | 8      | 8,9,10,11       |
| 5   | 6                | 15  | 5                |     |             |      |        |                 |
| 6   | EOF              | 16  |                  |     |             |      |        |                 |
| 7   | EOF              | 17  |                  |     |             |      |        |                 |
| 8   | 9                | 18  |                  |     |             |      |        |                 |
| 9   | 10               | 19  |                  |     |             |      |        |                 |

El tamaño de bloque en este sistema de ficheros es de 512 bytes y que el sistema operativo siempre asigna los bloques empezando por el primer bloque libre (número inferior) disponible. Completar el estado final de las tablas tras realizar (en orden) las siguientes operaciones:

1. Creación del fichero DATA1.TXT de tamaño 10 bytes.
	- Saco el Tamaño: TF/TBLO = 1 (no puedo darle algo menos) 
	- Lo asigno al bloque y le indico cual es su siguiente (EOF en caso de no tener)
2. Creación del fichero DATA2.TXT de tamaño 1200 bytes. 
    - Saco el Tamaño: TF/TBLO = 3 ya que con 2 me quedo corto
    - Lo asigno al bloque y le indico cual es su siguiente (EOF en caso de no tener)
3. Se añaden datos al archivo DATA.TXT que requieren 2 bloques más. 
	- Como ahora necesito 2 bloques más, el 15 deja de ser EOF y pasa a referencia el bloque siguiente, pasando a ser el EOF el número 6
4. Creación del directorio LOGS. 
	- El directorio ocupa exactamente 1 bloque por lo que EOF es el 7
5. Creacion del fichero RESULTS.JPG de tamaño 2 Kbytes
    - Saco el Tamaño: TF/TBLO = 4 ya que con 3 me quedo corto
    - Lo asigno al bloque y le indico cual es su siguiente (EOF en caso de no tener)

- **Ejercicio 13. Crear un sistema de ficheros ext2 con la siguiente estructura de ficheros y directorios. Nota: los comandos mostrados a continuación se ejecutarán como root (cambiar a ejecutando sudo -i):**
	- 1º Utilizo el truncate --size tamaño del inodo  
	- 2º Puedo mirar el tamaño del fichero y ver el bloque que ocupa con el comando ls -lhs
	- 3º Utilizando el comando mkfs (make file system).ext2 (extended 2)
	- 4º Todo lo que sale lo tengo que entender (Me chiva los tamaños, lo que ocupa, localización de los bloques, las copias de seguridad)
	
	- 5º Objetico montar un sistema de ficheros en un directorio
		- Montamos el sistema de  ficheros con permisos de super usuario sudo mount -t ext2 -o loop SISTEMA DE FICHEROS para montar el sistema de ficheros sobre otro sistema de ficheros (en caso de no querer usar eso no usamos loop)
		- En caso de tener algún i-nodo sin localizar podemos recuperarlo con lost+found que se encarga de buscar los i-nodos no enlazados en el sistema de ficheros
		
	- 6º En caso de querer debugear el sistema de ficheros usamos debugfs -R "stat" el cual corresponde al stat del sistema de ficheros (entre menor que i-nodo mayor que) sistema de ficheros del cual coger.
	- 7º Lectura de los bloques:
		-  Primero indica los i-nodos que ocupa
		-  Los IND indican bloques indirectos
		-  Tercero viene el DIND que es otro tipo de bloque
		-  Finalmente tenemos un total
		
- **Ejercicio 14. Las entradas de directorio en un sistema de ficheros ext2 incluyen: el número de inodo (32 bits), la longitud del nombre  y el nombre del archivo, que puede tener un máximo de 256 caracteres. ¿Cuántas entradas de directorio se pueden almacenar en un bloque de disco de 4 KB?**
	-  La estructura del directorio sería:
	- Una vez sacados los bytes que utiliza se saca la entrada; 4 + 1 + 256 = 261
	- Entradas/bloque = (4 * 2^10 bytes) / 261bytes = 15 entrada
	
| INODO  | LONG  | NOMBRE (256 bytes)                                 |
| ------ | ----- | -------------------------------------------------- |
| 32b    | 8b    | 256bytes                                           |
| 4bytes | 1byte | El long se saca con el log en base 2 de 256 --> 8b |
 - **Ejercicio 15. Considere un sistema de ficheros con los siguientes contenidos de inodos y bloques de disco.**
	 - Los enlaces duros solo pueden ser de ficheros
	 - El número de enlaces se marca con el número de apariciones
	 - El bloque en el que se guarda es el que almacene el .
	 - El siguiente (los bloques unidos de ficheros) se marcan con .. vease El 2 empieza en el 2 y prosigue en el 0

|         |     |     |         |     |     |         |     |     |         |     |     |         |     |
| ------- | --- | --- | ------- | --- | --- | ------- | --- | --- | ------- | --- | --- | ------- | --- |
| inodo   | 2   |     | inodo   | 3   |     | inodo   | 4   |     | inodo   | 5   |     | inodo   | 9   |
| Enlaces | 2   |     | Enlaces | 1   |     | Enlaces | 2   |     | Enlaces | 3   |     | Enlaces | 2   |
| Tipo    | D   |     | Tipo    | F   |     | Tipo    | F   |     | Tipo    | D   |     | Tipo    | D   |
| Bloque  | 3   |     | Bloque  | 6   |     | Bloque  | 12  |     | Bloque  | 0   |     | Bloque  | 5   |

  
  

|        |     |     |        |     |     |        |     |
| ------ | --- | --- | ------ | --- | --- | ------ | --- |
| Bloque | 0   |     | Bloque | 3   |     | Bloque | 5   |
| .      | 5   |     | .      | 2   |     | .      | 9   |
| ..     | 2   |     | ..     |     |     | ..     | 5   |
| C      | 9   |     | A      | 3   |     |        |     |
| D      | 4   |     | B      | 5   |     |        |     |
|        |     |     | E      | 4   |     |        |     |
-  Rellene los huecos para que el sistema sea consistente.
    
-  Dibuje de forma esquemática  el árbol del directorio empleando.
	 - Comenzamos con el bloque 3 (i-nodo 2) donde tenemos 3 entradas (A(3),B(5) y E(4)) 
	 - Del bloque 3 se une el bloque 0 (B) donde tenemos 2 entradas (C (9)y D(4))
		 - Del C colgaría el .9 y el ..5 del bloque 5 
	 - Del bloque 0 se une le bloque 5 (i-nodo 9)

- ![[Pasted image 20251017113314.png]]

- **Ejercicio 16.  Un usuario desea dar formato a una partición de disco para almacenar su colección de fotografías. Cada fotografía se almacena en un fichero con un tamaño fijo de 7000 bytes. El sistema de ficheros usado tiene las siguientes características:

	- Bloques indexados con 2 enlaces directos y 1 indirecto simple por inodo. 
    
	- 4 bytes para identificar un inodo
    
	- Tamaño de puntero a bloque de 32 bits. 
    

	El sistema de ficheros se puede formatear con  tres tamaños de bloque: 1024 bytes, 2048 bytes y 4096 bytes. Analiza las ventajas de cada tamaño contestando a las siguientes preguntas:

	-  ¿Cuál de las tres opciones presenta menos fragmentación interna? Para cada tamaño de bloque, indique el porcentaje de ocupación real de cada uno de los bloques de datos asignados a un fichero. 
	
		- ![[Pasted image 20251010123741.png]] 
    
	- ¿Cuál de las tres opciones ofrece un mejor aprovechamiento de los bloques de disco disponibles? Para cada tamaño de bloque, indique qué porcentaje de bloques de disco se utilizarán para almacenar los datos de un determinado fichero.
	
		- ![[Pasted image 20251010124327.png]] 
    
	- ¿Cuántos accesos a disco requerirá una lectura secuencial completa de una fotografía en cada caso?
	
		-  Tantos accesos como bloques de datos + accesos totales
			- 1024 --> 7 + 1 //N + num i
			- 2048 --> 4 + 1 //N + num i
			- 4096 --> 2 //N + num i
    
	- ¿Cómo afectarán a la selección de un tamaño de bloque determinado al tamaño de la tabla de inodos y al mapa de bits de bloques libres?
		
		-  La densidad del tamaño no modifica la tabla de i-nodos
		- Cuantos más bloques más bits, por lo que a necesitarás tantos bits como bloque haya, es decir, a mayor tamaño de bloque menor tamaño del mapa
    
- **Ejercicio 17. Un sistema de ficheros UNIX tiene las siguientes características:**

	- Bloques de 512 bytes y direcciones de bloque de disco de 16 bits.
    
	- Bloques indexados con 10 punteros directos a bloque,  1 puntero indirecto simple y 1 puntero indirecto doble.
    

	-  **Conteste de manera razonada a las siguientes cuestiones:**

		-  ¿Cuál es el tamaño máximo de un fichero en este sistema? 
		    - ![[Pasted image 20251017113936.png]]
		- Un programa UNIX crea un fichero en este sistema e inmediatamente después escribe un byte de datos en la posición 1.000 y otro en la posición 10.000. ¿Cuántos bloques del disco  ocupa este nuevo fichero en disco?
			- Se trata de un fichero (sparse)
			- Bloques = 1
			- ¿Dónde está el bloque de datos?
			- 1000byte Empiezo en este byte por lo que TB = 1 (Estoy dentri de los directos) ya que el total de dir = 5120 bytes > 1000bytes
			- 10000 por el contrario esta en TB = 1 de datos(dir) + 1 de indirecto(dir) = 2 ya que el total de ind = 128000 > 10000


	