atoi(argv[1]) parsear el argumento a entero.
- LA LÍNEA DE COMANDOS

	- **Ejercicio 1. Arrancar un terminal y comprobar el prompt de la shell. Cada usuario tiene un prompt distinto configurable. Para cambiar de usuario podemos usar el programa su. Ejecutar sudo -i  y comprobar si cambia el prompt, regresar al usuario inicial con la orden exit. El comando exit termina la ejecución de la shell y devuelve opcionalmente un código de retorno.**
		

- PÁGINAS DE MANUAL

	- **Ejercicio 1. Consultar la página de manual de man (man man) . Especialmente las secciones de una página de manual (NAME, SYNOPSIS, DESCRIPTION...).**
		- 1º Accedo al manual con man man
		- 2º Busco la sección de Name, synopsis y description como si de un diccionario se tratase
	- **Ejercicio 2. Para buscar en una sección determinada simplemente se puede especificar antes del nombre de la página. Por ejemplo, ver la diferencia entre man 1 time y man 2 time**
		- Básicamente me permite seccionar las páginas del manual del comando que busco en cuestión
	- **Ejercicio 3. Para buscar páginas de manual sobre un tema en particular se puede usar la opción -k, o las órdenes whatis o apropos. Buscar las órdenes relacionadas con la “hora” (time). Nota: Este comando accede a una base de datos sencilla para cada página de manual. La base de datos se gestiona con el comando mandb**
		- Similar a la sección anterior pero en lugar de ser una página es una parte concreta de una función
		
- COMANDOS Y SECUENCIAS DE COMANDOS
	- **Ejercicio 1. Estudiar el funcionamiento del comando echo (man echo). ¿Qué hacen las opciones -n y -e? Imprimir la frase “Curso de Sistemas Operativos” con un tabulador al principio.**
		- 1º El comando echo funciona para escribir caracteres, ya sea en la terminal únicamente o para crear o modificar algún fichero.
		- 2º -n permite la utilización de saltos de línea mientras que -e permite el uso del tabulador al principio para separar las palabras
		- 3º Utilizamos el comando echo -e " Curso de Sistemas Operativos " para escribir lo pedido en pantalla
	- **Ejercicio 2. Los comandos se pueden partir en varias líneas terminando cada una con ‘\’. Imprimir la frase del ejemplo anterior, escribiendo cada palabra en una línea. Comprobar que el prompt  de la shell cambia en el modo multi-línea.** 
		- 1º Utilizo el comando echo y voy separando cada palabra con \ y un enter 
		- 2º Finalemente le doy al enter y si no queda ningun \ detrás escribe la frase completa
	- **Ejercicio 3. La shell dispone de una serie de meta-caracteres que permiten controlar su comportamiento. En especial: || && ; ( ) | &, sirven para generar secuencias o listas de comandos. Estudiar el funcionamiento de las siguientes secuencias:**
		- 1º ; --> Permite escribir varios comandos y hace que se ejecuten de manera consecutiva
		- 2º && --> Similar al ; con la diferencia que solo lo hace si todos los comandos se pueden ejecutar correctamente
		- 3º || --> Escribe el comando de la izquierda y en caso de no poder realizarse escribe el de la derecha
		- 4º () --> Dan prioridad al comando que tiene que ejecutarse
	
- VARIABLES DE ENTORNO 
	
	-  **Ejercicio 1. Consultar el entorno de la shell mediante env.**
		- Muestra una descripción de la shell actual de trabajo
	
	- **Ejercicio 2. El valor de las variables se puede acceder con el prefijo $. Consultar el valor, y determinar el significado de: USER, UID, HOME, PWD, SHELL, $, PPID, ?,  PATH.**
		- 1º El $ permite acceder y declarar variables
		- 2º USER: Usuario que está usando la terminal
		- 3º UID: Determina la ID del usuario
		- 4º HOME: Devuelve la dirección del directorio HOME
		- 5º PWD:  Devuelve el directorio actual
		- 6º SHELL: Devuelve la shell actual
		- 7º PPID: Devuelve la ID de la ruta donde estamos
		- 8º PATH: Devuelve la ruta actual
		
	- **Ejercicio 3. Fijar el valor de las variables VARIABLE1, VARIABLE2 y VARIABLE3 a “Curso”, “de” y “Sistemas Operativos”, respectivamente. Imprimir la frase “Curso de Sistemas Operativos” accediendo a las variables**
		- 1º  Creo las 3 variables, para ello escribo: VAR1="CURSO", VAR2="DE",VAR3="SO"
		- 2º Usando echo escribo las 3 variables: echo "$VAR1 $VAR2 $VAR3"
		
	- **Ejercicio 4. Las colisiones entre variables se pueden evitar poniendo el nombre de la variable entre llaves {}. Fijar la variable VAR1 a “1+1=” y VAR12 a “error”. ¿Qué imprime echo $VAR12? ¿Cómo se imprimiría “1+1=2” (sin espacios) usando el valor de VAR1?** 
		- 1º  Este caso se utiliza en el caso de querer hacer algo similar al ejemplo del ejercicio, ya que en el otro caso solo se escribiría error en lugar del 1+1=2
	
	- **Ejercicio 5. La variable PS1 guarda la estructura del prompt. Consultar la sección PROMPTING en la página de manual de bash y cambiar el prompt a ”12:39|~% ” (hora | directorio %). **

	 - **Ejercicio 6. PATH es una de las variables más importantes del entorno de la shell. Consultar su valor y añadir el directorio actual al PATH. ¿Qué diferencia hay entre añadir ./ y $PWD?**
		 - ./ Confirma si estoy en un directorio
		 - $PWD Indica el direcotrio en el que me encuentro
		
- MANEJO DE CADENAS Y FLUJOS DE CARACTERES

	- **Ejercicio 1 y 2. Estudiar el comando sort (man sort). Ordenar las palabras: zorro, pájaro, vaca, caballo y abeja,  imprimiendo cada una en una línea (\n) con el comando echo y encadenando su salida (tubería ‘|’) con el comando sort.**
		- 1º Creamos el archivo Animales.txt
			- Para ello utilizamos echo -e ("texto") > "Nombre de archivo" el cual crea el archivo con el nombre de archivo en el que dentro se encuenetra texto (-e se usa para permitir el salto de linea con "\n" , > indica que borre el interior de ese archivo entero o lo cree)
		- 2º Utilizamos sort para ordenar texto
			- sort "Animales.txt" el cual devuelve los valores ordenados 
		- 3º Inserto tubería en animales.txt
			- Para ello utilizo echo -e ("texto")  >> "Nombre de archivo" el cual agrega la palabra texto al archivo cuyo nombre es "Nombre de archivo"
		- 4º Vuelvo a utilizar Sort 
		
	-  **Ejercicio 3. El comando cat muestra el contenido de un fichero, probar con texto1. Además, si no se especifica un fichero (o se usa ‘-’, ver man cat), recoge la entrada estándar que puede redirigirse a un fichero. Escribir las palabras:  pera, manzana, plátano y ciruela, cada una en una línea, en el fichero texto2. Nota: el flujo de entrada estándar se cierra con Ctrl+d. Comprobar el contenido de texto2 con cat.**
		- 1º  Creo el fichero texto2.txt
		- 2º Utilizo cat "texto2.txt" para que me lea el archivo en cuestión
		- (si escribes cat - o cat a secas puedes agregar valores a un txt hasta que salgas con ctrlD)
		
	-  **Ejercicio 4. cat se puede usar para concatenar ficheros si se especifican como argumentos. Unir los ficheros texto1 y texto2 en texto3 usando la redirección (‘>’).**
		- 1º Concateno los 2 txt creados a un nuevo txt
			- Para ello utilizo cat "txt1" "txt2" > "Nuevo archivo txt", esto hará que el nuevo archivo de txt tenga ambos txt1 y txt2 uno detrás de otro
		- 2º Compruebo el Nuevo archivo txt con el comando cat "Nuevo archivo txt"
		
	- **Ejercicio 5. wc sirve para contar palabras, caracteres y líneas de un fichero de texto. Comprobar el tamaño de los ficheros texto1, texto2 y texto3 con wc, y compararlo con la salida de ls -l *. Consultar la página de manual para ver como controlar la salida del comando.** 
		- 1º Utilizo el comando wc "Archivo de texto" para comprobar el tamaño de cada txt
			- Este devuelve Lineas -  Palabras - Caracteres en ese orden 
		- 2º Uso el comando ls -l el cual devolverá las caracteristicas del propio archivo en lugar del contenido
		
	-  ** Ejercicio 6. Los comandos head y tail permiten ver el principio y el final de un fichero. Vamos a usar dmesg (mensajes del sistema) para probar el funcionamiento de estos comandos:**	
	
		- **En primer lugar determinar el número de líneas que produce el comando.**
		- **Usar tail para quedarse con la última parte (ej. últimas 15 líneas)
		- **Usar head para quedarse con las primeras líneas (ej. primeras 3 líneas)**
		- **Una opción importante de tail es -f que permite mostrar de forma continua las últimas líneas del fichero. Comparar con la opción -F.**
	
	- **Ejercicio 7. El comando tr sirve para cambiar caracteres (translate) o eliminarlos. Poner todas las palabras del fichero texto1 en una línea sustituyendo el carácter fin de línea por un tabulador.** 
		- 1º Utilizo el comando tr x, y < "Archivo.txt" el cual funciona de forma que sustituye todos los valores x que encuentras en Archivo.txt por el valor de y

- EL SISTEMA DE FICHEROS
	- **Ejercicio 1. Para cambiar de directorio se usa la orden cd.**
		- **Cambiar al directorio de usuario (cd sin argumentos).**
			- Para ello escribes cd la ruta a la que vas 
		- **Averiguar la ruta (path) del directorio (comando pwd, o variable PWD).**
			- Una vez en la ruta usas pwd 
		- **Pasar al directorio /usr/bin, y comprobarlo con pwd.**
			- Repetir los 2 primeros pasos 
		- **Volver al directorio anterior (cd -).**
		- **Cambiar ahora de nuevo al directorio /usr/bin pero de forma relativa desde el directorio de usuario.**
		- **Volver finalmente al  directorio de usuario** 
		
	- **Ejercicio 2. La orden mkdir sirve para crear directorios. Hacer el directorio ‘mis_archivos’ en el directorio de trabajo. Comprobar su creación con el comando ls (list).**
		- 1º Utilizas mkdir "Nombre del directorio" para crear el nuevo directorio
		- 2º Utilizo el comando ls para observar los elementos de dicho directorio
		
	- **Ejercicio 3. La opción -p de mkdir sirve para crear un directorio y todos aquellos que sean necesarios en la ruta. Crear el directorio mis_archivos/prueba/texto/tmp, probar con la opción -p y sin ella (man mkdir).**
		-  Crea una carpeta dentro de una carpeta dentro de una carpeta...
		
	- **Ejercicio 4. Un directorio se puede borrar con rmdir, pero debe estar vacío. Eliminar el directorio prueba (y todos sus contenidos con rmdir).** 
	
	- **Ejercicio 5. Copiar el fichero texto1 a copia1 con cp. Los ficheros y directorios se pueden renombrar con el comando mv,  renombrar copia1 a fichero1.**
		- 1º Copio el fichero de directorio 1 a directorio 2 usando el comando cp
			- Para ello me coloco en el directorio 1 con cd y una vez hecho eso escribo cp "Nombre del archivo a copiar " "Directorio donde se va a copiar"
		- 2º  Finalmente utilizando el comando mv "Fichero a renombrar" "Nuevo nombre" le modifico su valor
	- **Ejercicio 6. Crear un directorio llamado ‘copia’ y copiar en él los archivos texto1, texto2 y fichero1 con la orden cp en una única línea. **
		- 1º  Utilizas mkdir "Nombre del directorio" para crear el nuevo directorio  
		- 2º Copiar los ficheros de directorio 1 a directorio 2 con cp
	- **Ejercicio 7.  Los directorios se pueden copiar usando la opción -r. Copiar el directorio copia al directorio otra_copia. Consultar el propósito de las opciones -f y -i en la página de manual de cp.
		-  1º Me coloco en el directorio donde se encuentra copia con cd
		-  2º Usando cp -r "Directorio a copiar" "Nombre del nuevo directorio copiado" creo la copia
	- **Ejercicio 8. Para borrar usar el comando rm. Borrar los ficheros del directorio copia con rm, y finalmente el propio directorio copia con rmdir. Los comandos cp y rm aceptan opciones recursivas (-r) para copiar y borrar directorios respectivamente. Borrar los directorios otra_copia con rm -r.**
		-  1º Me coloco dentro del directorio usando cd
		-  2º Utilizando rm -r puedo eliminar todos los archivos del directorio
		-  3º Nos pasamos un nivel por fuera con cd -
		-  4º Elimino el directorio con rmdir "Nombre del directorio" ¡TIENE QUE ESTAR VACÍO!
		
- BUSQUEDA DE FICHEROS:
	-  **Ejercicio 1. La forma básica de uso de find es find <ruta_de_búsqueda> -name <patrón_nombre>. Por ejemplo buscar todos los ficheros que empiezan por texto en /home.**
		- 1º Se usa find /home -name  palabraClave y esto devuelve todos los archivos con dicho nombre que encuentre
	- **Ejercicio 2. Se puede además buscar por tipo usando la opción type. Consultar la página de manual de find para buscar todos los directorios en $HOME.
		- ![[Pasted image 20251008201651.png]]
		- 2º Escribimos find /home -type d y devuelve todos los directorios
	- **Ejercicio 3. La opción size permite buscar por tamaño con los modificadores c, b, k, M y G. Si se antepone + al tamaño se seleccionen ficheros mayores, con - se seleccionan ficheros más pequeños Buscar ficheros mayores de 10M en el sistema.**
		- 1º Se escrube sudo find /home -type f  -size +10M
			- Las letras corresponden al tamaño de los archivos en bytes

- REDIRECCIONES, TUBERÍAS Y EXPRESIONES REGULARES
	- **Ejercicio 1. Ejecutar en el directorio $HOME el comando ls -l text* nada* > salida. ¿Qué sucede?, ¿cuáles son los contenidos del fichero salida?. Con el comando anterior redirigir la salida estándar a salida.out y la salida estándar de error a salida.error.**
		- 1º 
	- **Ejercicio 2. El operador de redirección (>) ‘trunca’ el contenido del fichero. Se puede añadir al contenido ya existente mediante (>>) . Repetir el comando anterior pero sin borrar el contenido de los ficheros.**
		- 
	- **Ejercicio 3.  Se pueden duplicar los descriptores con >& y >>&, en la forma: comando > salida 2>&1. Redirigir la salida estándar y de error del comando ls anterior al fichero salida.txt. Comprobar que el comportamiento es distinto a comando 2>&1 > salida (las “duplicaciones” se hacen secuencialmente)**
		- 
	- **Ejercicio 4. Muchas veces no resulta interesante la salida del comando, sólo su resultado ($?); esto se consigue redirigiendo las salidas a /dev/null. Probar el funcionamiento con las órdenes anteriores.**
		- 
	- **Ejercicio 5** "no muy importante"
		-  
	- **Ejercicio 6. Usando el comando grep y la una expresión regular adecuada, buscar en el fichero texto1 las siguientes palabras:**
		- 1º El comando grep se usa para buscar patrones en los archivos
		- 2º Para buscar en grep se hace: grep 'patron' archivo a buscar
		- 3º Si en concreto tienen que ser la última se hace = pero se escribe 'patron$'
		- 4º Si en lugar de eso buscamos algo entre 2 letras (a a) en 'patron' escribimos 'a.a'
		- 5º Si buscamos algo que tenga de x a y caracteres necesitamos usar grep -E 'al{1,2}o' texto1.txt siendo 1 el valor de x y 2 el valor de y, en este caso busca de 1 a 2 l (todo lo que acabe en alo o allo)
		
- PROGRAMACIÓN EN LENGUAJE SHELL 
	- **Ejercicio 1.  Argumentos de un programa. Escribir un script que muestre el nombre del fichero del script ($0), el primer ($1) y segundo ($2) argumento, cada uno en una línea. Además la variable $# contiene el número de argumentos y $@ sirve para referirse a todos.** 
		- 1º Creo el script que acaba en .sh (para que se muestre lo escrito uso echo variable)
		- 2º # Contiene el número de argumentos y @los tiene a todos (esto es automatico)
		- 3º Ya creado el script nos ubicamos en su directorio con cd
		- 4º Damos permisos de ejecución con chmod +x Nombre del sh
		- 5º Abrimos el sh con ./Nombre del sh ARGUMENTO1 ARGUMENTO2....
		
	- **Ejercicio 2. Sentencias Condicionales. Escribir un programa que acepte exactamente un argumento. Si no es así debe terminar con código 1 y mostrar el mensaje correspondiente. El argumento se interpretará como una ruta. Si la ruta es un fichero regular (ver man bash, sección CONDITIONAL EXPRESSIONS), el script mostrará el número de líneas que tiene.  Nota: La ejecución de un programa se puede asignar a una variable que guardará la salida estándar. Además el comando cut puede ser útil para separar una cadena y seleccionar un campo.** 
	
		-  1º Se crea el script
		-  2º Se asigna las variables agregando un echo tambien pq si no peta :D
		-  3º Se crea el condicional (DIOS MIO BENDITO EL CONDICIONAL)
			- if [#2 -gt 1] then 
				- QUE HAGO
			- else 
				- QUE HAGO
			- fi 
		
	- **Ejercicio 3. Bucles. Escribir un script shell que itere por cada fichero de un directorio dado (argumento del script) y  si es un fichero regular muestre en un línea el nombre y el  número de palabras. Nota: Para realizar un número de iteraciones dado se puede usar la forma C (ver manual de bash) o el comando seq.**
		-  1º Creo un script de bash que recibe un argumetno que es el directorio IMPORTANTE ES EL $1, $0 corresponde al nombre del script
		-  2º Creo un bucle for que recorra para cada fichero de dir
		-  3º Comrpuebo con un if si cumple la condición para escribir, en caso de hacerlo uso el echo
		- 4º Ejecuto en consola, le paso un directorio . si es el actual ../ etc etc
		
	- **Ejercicio 4. Funciones. Para escribir una función en bash se usa la siguiente sintaxis. Probar la ejecución del siguiente script. ¿Qué valor se almacena en la variable A?** 
		- 1º Creo un script de bash que almacena la función:
			- Para crear funciones utilizo la palabra clave function NOMBRE() { codigo }
			- Si dentro utilizo algún argumento, puedo pasarle argumentos luego al llamar al método en cuestión
		- 2º Dentro del script llamo a la FUNCIÓN VALOR QUE QUIERO QUE TENGA EL ARGUMENTO
		- 3º Asigno un argumento A=lo escrito en el paso 2
		- 4º Pido que imprima el valor de A (ahora si con $ delante)
		- 5º Ejecuto el programa en bash
		
- PRÁCTICA AGENDA