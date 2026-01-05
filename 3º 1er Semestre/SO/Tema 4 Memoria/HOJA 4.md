- EJERCICIO 1
	- Consulta los segmentos definidos en el ejecutable generado con el comando readelf -l  y completa la siguiente tabla.

	- Los segmentos de la tabla corresponden a las secciones de tipo LOAD. La primera de ellas PHDR es la 00, INTERP la 01 y así sucesivamente.
		- Los LOAD están entonces en el 02 03 y 04 respectivamente
	- Algunas secciones del programa pueden estar asignadas al mismo segmento del ejecutable.
		- Como es el caso del .data y el .bss
	- IMPORTANTE:
		- Este comando tiene la chuleta en la parte de arriba indicando tanto el tamaño como las direcciones virtuales del mismo
		- ![[Pasted image 20260104210814.png]]
	
|          |                                            |        |             |       |
| -------- | ------------------------------------------ | ------ | ----------- | ----- |
| Segmento | Código C correspondiente                   | Offset | Dir.virtual | Flags |
| .text    | printf y sleep return 0 mul = num * factor | 0x1000 | Ox1000      | R E   |
| .rodata  | const char msg                             | Ox2000 | Ox2000      | R     |
| .bss     | mul                                        | Ox2dc0 | Ox3dc0      | RW    |
| .data    | num y factor                               | Ox2dc0 | Ox3dc0      | RW    |

- Ejecutar ahora el programa y obtener los segmentos de memoria virtual accediendo al fichero maps del directorio del proceso en /proc. Nota: Se puede identificar la correspondencia de los segmentos del ejecutable y los segmentos de memoria virtual comparando el camp offset y los flags:

- Si el resultado esperado es anon, significa que esa memoria es privada, mientras que si sale cualquier otra cosa, esa memoria es compartida con la cosa que salga
	- ![[Pasted image 20260104210839.png]]

|          |                                     |                                   |       |                  |                  |
| -------- | ----------------------------------- | --------------------------------- | ----- | ---------------- | ---------------- |
| Segmento | Rango de direcciones virtuales      | Offset del fichero                | Flags | Tipo map/anónimo | Ruta del fichero |
| .text    | 00005579433f7000 - 00005579433f7FFF | Ox1000 (Restar el 7FFF - el 7000) | r x   | map              | Ejercicio1       |
| .rodata  | 00005579433f8000 - 00005579433f9FFF | Ox2000                            | r     | map              | Ejercicio1       |
| .bss     | 00005579433fa000-000055794fa56FFF   | Ox2dc0                            | rw    | map              | Ejercicio1       |
| .data    | 00005579433fa000-000055794fa56FFF   | Ox2dc0                            | rw    | map              | Ejercicio1       |
| [heap]   | 000055794fa57000-00007ff87403EFFF   | Ox8000                            | rw    | anonmio          | anon             |
| [stack]  | 00007ff87403f000-00007ff874041FFF   | Ox2000                            | rw    | anonimo          | anon             |

- Nota: Alternativamente, el programa pmap(1) puede utilizarse para consultar la información sobre los segmentos de memoria (misma información que proc/pid>/maps)

	- Cuestiones:

	- En qué segmento(s) de memoria virtual está la cadena "El resultado es:\n". Los contenido del segmento de memoria virtual se puede acceder en el directorio del proceso /proc/pid proceso>/map_files/rango del segmento>. Comprobar que la respuesta es correcta con el comando strings(1).
		- La respuesta está marcada en el rango de direcciones virtuales, con el comando en cuestión se puede sacar la posición concreta dentro de ese rango que es el entry point + el inicio del rango
		- ![[Pasted image 20260104212554.png]]
    
	- En la salida del comando readelf se muestra el inicio del programa (entry point). ¿En qué segmento del fichero está ubicado? ¿Y en qué segmento de memoria virtual?
		- Se encuentra ubicado en el segmento Ox1060 y en memoria está en el segmento Ox10a0 (1060 + Ox0040)
    
	- Dibuja esquemáticamente (como en las transparencias de teoría) el espacio de direcciones del proceso con las regiones correspondientes.
		- Esquema de pagina virtual que apunta a la física que apunta a la cache donde está el archivo
    
	- Investiga cuál es el contenido y propósito de las áreas de memoria marcadas como [vdso] y [vvar].
		- vdso hace referencia al códgo del kernel accesible al usuario
		- vvar hace referencia a las variables virtuales 
- **Ejercicio 2.  Considera el siguiente programa y completa la siguiente tabla. 

|                    |                               |          |
| ------------------ | ----------------------------- | -------- |
| Símbolo            | Espacio en ejecutable (Sí/No) | Segmento |
| CONSTANT           | No                            | ----     |
| i                  | No                            | stack    |
| num1               | Si                            | data     |
| num2               | Si                            | bss      |
| “%s: %d, argc: %d” | Si                            | roadata  |
- IMPORTANTE:

	- Las **macros no ocupan memoria**
    
	- Las **variables globales** sí están en el ejecutable
    
	- Las **locales** viven en la pila
    
	- Las **cadenas literales** van a `.rodata`
    
	- `malloc` reserva memoria en el **heap**, no en el ejecutable
	
- **Ejercicio 3. Escribe un programa que cree una región de memoria (mmap(2)) con las siguientes características:

	- Tamaño 1024 bytes
    
	- Acceso privado
    
	- Modo lectura y escritura
    

- Una vez creada la región de memoria el proceso la inicializará con ‘\0’ (usar un bucle o la llamada memset(3)), mostrará la dirección del segmento (modificador de formato %p) y el PID del proceso. Finalmente el proceso  hará un sleep de 600s. Ejemplo de ejecución:
- Usando el PID consultar el fichero maps e identificar el segmento creado en el espacio de memoria del proceso:
	- No lo carga

| Dirección Inicial | Dirección FInal | Offset | Flags |
| ----------------- | --------------- | ------ | ----- |
|                   |                 |        |       |
- **💻 Ejercicio 4. Re-escribir el ejercicio 11 de la Hoja 3 proyectando el fichero de salida (output.txt) en la memoria virtual:
- El esquema es el siguiente:
	
	- Preparación del segmento de memoria. Cuando se proyecta un fichero debe tener al menos el tamaño de la región que se quiere crear, y se debe abrir con el mismo modo que se quiere crear la región (lectura, escritura,...). Las acciones que realizará el proceso padre son:
    

	- Crear el fichero de salida con la llamada open(2) y las opciones O_TRUNC y lectura/escritura.
		- Esto se hace como siempre, se llama a open(pathname,flags,permisos)
    
	- Para fijar el tamaño de la región usaremos la llamada al sistema ftruncate(2) (fichero sparse)
		- Se "reserva" la memoria que va a utilizar el archivo en cuestión usando ftruncate(fd,tamaño)
    
	- Proyectará en la memoria virtual del proceso con (mmap(2)). Nota: convertir el puntero retornado por map() a char *
		- Se crea el espacio de memoria char* addr = mmap(NULL,tam,PROT,flags,fd,0)
    
	- Cerrar el descriptor (close(2)), esto no afecta al segmento de memoria proyectado.
		- Una vez hecho todo se cierra el archivo;
    

- Inicialización del segmento de memoria. Se crearán los hijos que usarán su identificador como base del desplazamiento a la zona de memoria y fijará en cada posición el caracter correspondiente. Truco: se puede usar el operador + en variables de tipo char para movernos por la tabla de caracteres, por ejemplo: (char) ‘5’ = (char) ‘0’ + (int) 5
	- En la creación de procesos se pregunta si es un hijo, si lo es se hace el addr[offset + j] para colocar el puntero en la posición en concreto y escribir el número en cuestión
	- Si es un padre se hace lo mismo pero addr[j] escribe 0 (siendo j un índice = 0 de for < 5), después se hace un do while para que espere a todos los hijos
    
- Finalización. El proceso padre esperará la finalización de todos los hijos y eliminará la región con las llamadas msync(2) y munmap(2).
	- Una vez terminados los hijos se hacen las llamdas a msync(addr,tam,MS_SYNC) y a munmap(addr,tam) para liberar la memoria
	- ![[Pasted image 20260105000129.png]]
	- ![[Pasted image 20260105000146.png]]
- **Ejercicio 5. Compara la implementación del Ejercicio 4 y la realizada en el Ejercicio 11 de la Hoja 3:

	- Respecto a E/S, describe qué acciones realiza el sistema. ¿Hay alguna diferencia entre ambas alternativas (e.g. número de escrituras en disco…)?. Nota: considera todos los componentes del VFS y memoria virtual.
		- Sí hay diferencias, usando write se hacen llamdas de escritura constantemente por no hablar de que cada vez que se hace se debe de asignar nueva memoria en disco lo que puede provocar a fallos de almacenamiento (frag interna por ejemplo) 
		- Por el contrario con la forma de memoria solo se hace la llamada a las escrituras ya que la asignación de memoria se hace antes de todo
    
	- Respecto al SO, ¿cuál de las dos alternativas es preferible? ¿Y desde el punto de vista del programador?
		- Para el SO la segunda para el programador la primera
- **Ejercicio 6.  Considera un sistema operativo con una memoria virtual paginada de un nivel y tamaño de página de 512 palabras. El espacio de direcciones virtuales tiene 512 páginas y la memoria física tiene 10 marcos de página.

	- Describe la estructura del espacio de direcciones virtuales y física, y de la tabla de páginas que usaría el sistema operativo. Indica el tamaño de todos los campos.
		- 512 páginas implica a 2⁹ que son 9 bits, lo cual se aplica también al espacio de direcciones virtuales, para las físicas se necesitan 10 marcos de página (que requiere 4 bits para representarse)
			- Solución:
				- Dir Virtual --> 18 bits --> 9 Dir 9 tam
				- Dir física --> 12 bits --> 4 Dir 9 tam
    
	- Si el contenido de la memoria física es el que se muestra a continuación, determina el contenido de la tabla de páginas del proceso. ¿Qué dirección física corresponde con las direcciones virtuales 0x13FF y 0x1403?
		- Importante: Calcular la página en la que me encuentro: pasar la dirección virtual a binario
			- Ox13FF --> Página virtual 9 y un offset de  1 1111 1111 por la tabla sabemos que la dirección física es la 4 (traducido de Ox0800) SOL Ox09FF
			- Ox1403 --> Página virtual 10 y un offset de 0 0000 0011, por la tabla sabemos que la dirección física es la 9 (traducido de Ox1200) SOL Ox1203

|                         |                   |
| ----------------------- | ----------------- |
| 0x0000                  |                   |
| 0x0200                  |                   |
| 0x0400                  |                   |
| 0x0600                  | Página virtual 34 |
| 0x0800                  | Página virtual 9  |
| 0x0a00                  |                   |
| 0x0c00                  |                   |
| 0x0e00                  | Página virtual 65 |
| 0x1000                  |                   |
| 0x1200                  | Página virtual 10 |
| Contenido de la memoria |                   |

- ¿Qué ocurre si un proceso intenta acceder a la posición 0x80E8?
	- La página virtual es la 64, como no está en la página ocurre un fallo de página, lo que provoca que se traiga el bloque a la tabla asociandolo a nuevo bloque físico, (Aquí el proceso se interrumpe hasta que el SO resuelva el fallo de páginas)
    
- Supongamos que el marco de página en las direcciones 0x0800-0x09ff se quiere compartir con otro proceso. ¿Debería asignarse al mismo segmento virtual?** 
	- Al segmento virtual no es necesario al físico sí ya que ambos utilizan memoria similar
	
- **💻Ejercicio 7. Considera el siguiente programa:
	- Realiza dos ejecuciones con el comando strace para identificar cómo se reserva la memoria del array ptr. Consulta el mapa de memoria del proceso en /proc para completar la siguiente tabla para la región de memoria dónde está la memoria del array. Nota: lee la sección NOTES de la página de manual de malloc(3).

		- Caso A. strace ./ejercicio7 1
    
		- Caso B. strace ./ejercicio7 1024
    
|      |                      |                               |       |               |                            |
| ---- | -------------------- | ----------------------------- | ----- | ------------- | -------------------------- |
| Caso | Dirección<br><br>ptr | Rango irecciones              | Flags | Tipo Segmento | Mecanismo Memoria Dinámica |
| A    | 557a45319000         | 0x557a45319000 -557a4533a000  | rw p  | 00000         | heap                       |
| B    | 0x5563a2395000       | 0x5563a2395000-0x5563a23b6000 | rw p  | anom          | mmap                       |
|      |                      |                               |       |               |                            |

- **Ejercicio 8.  Un sistema tiene un uso medio de la CPU del 15% (usuario) y 3% (sistema), el área de swap está ocupada al 92%. La salida del comando ps muestra 50 procesos en estado “D” (espera no interrumpible) . ¿Cuál de estas acciones aumentará más la utilización de la CPU?:

	- Ampliar la memoria principal
		- Respuesta correcta, el área de swap solo impide que el sistema no se caiga y si damos más memoria al sistema reducirá el consumo de la CPU sin duda provocando un aumento del uso de la CPU
    
	- Ejecutar más programas para aumentar el grado de multiprogramación 
		- Esto solo sobrecargará al sistema
    
	- Aumentar el área de swap
		- No cambia el rendimiento de la CPU solo da más margen al sistema
    
	- Añadir más CPU’s
		- Igual que swap, da más capacidad
    
- **Ejercicio 9.  En un sistema con memoria virtual paginada indicar las acciones son realizadas por el sistema operativo (especificando a qué estructuras de datos accede y como las modifica) en los siguiente casos: 

	- Un proceso intenta escribir en una página de solo lectura
		- Se comprueba que el fichero este en memoria, si está se comprueba su bit de escritura, como este está a 0 se manda una violación de segmento que impide escribir en el archivo
    
	- Un proceso intenta acceder a una dirección correspondiente a una página que no está en memoria.
		- Busca en la TLB si la página se encuentra disponible, como no es el caso el SO manda una señal al proceso para dejarlo en espera (lo interrumpe), mientras eso ocurre se va memoria virtual a traer la página referenciada y la trae a la TLB, si esta está llena sustiuira dependiendo del modelo de memoria que este utilice. Una vez este la dirección disponible el SO reanudará el proceso mandandole la señal correspondiente

- **Ejercicio 10. Considera el siguiente código e indique razonadamente si cada una de las afirmaciones posteriores son ciertas o falsas. Asuma que todos los segmentos de memoria del proceso asociado (texto, datos, pila,...) ocupa  una página de 4 Kb.

- int main() {

    int i;

    int M[128]; --> Ocupa 512 Pq un entero son 4bytes 2⁷ * 2² = 2⁹ = 512B

    int x,y;

    x = M[0];

    y = 0;

    for (i=1; i < 200; i++) {

        y = x + M[i];

        M[i] = y;

    }

    return 0;

	}
- CUESTIONES:
	
	- El proceso provocará una excepción por violación de segmento (SIGSEV) al ejecutarlo porque accede a elementos de M no reservados.
	    - Falso, al no tratarse de memoria dinámica no hace falta reservarlo con malloc, por el contrario generará error de asignar valores no inicializados VA A LA PILA
	    
	- La ejecución del proceso  corromperá los datos de la pila.
	    -  Verdadero ya que M ocupa hasta 512 mientras que el bucle llega hasta 199 por lo que la pila se corrompe
	    
	- La ejecución del proceso puede corromper el segmento de código del programa. 
	    - Falso ya que las variables de text están en posiciones diferentes  
	    
	- Si se modifica el bucle para que recorra 4096 posiciones del array M se producirá una excepción.
		- Verdadero ya que se recorren más páginas de las disponibles
 