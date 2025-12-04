- EJERCICIO 1
	- Consulta los segmentos definidos en el ejecutable generado con el comando readelf -l  y completa la siguiente tabla.

	- Los segmentos de la tabla corresponden a las secciones de tipo LOAD. La primera de ellas PHDR es la 00, INTERP la 01 y así sucesivamente.
    
	- Algunas secciones del programa pueden estar asignadas al mismo segmento del ejecutable.

	- EXPLICACION: Los números que salen en las asignaciones de sección a Segmento equivalen al valor del índice imaginario de la seccion de Encabezados de Programa
		-  0 es el PHDR
		- 1 es el INTERP...
		- Esos números a su vez contienen información de suma importancia como el segmento de código al que se asocian asi como el lugar en memoria donde se ha guardado ese código (por ejemplo en el ordenador del lab el msg se me ha guardado en el 03 que equivale a un LOAD y los .data y .bss se me han guardado en 04, cosa que varía en función del dispositivo OBVIAMENTE)
    
	
|          |                          |                 |                 |       |
| -------- | ------------------------ | --------------- | --------------- | ----- |
| Segmento | Código C correspondiente | Offset          | Dir.virtual     | Flags |
| .text    | mul *= factor printf()   | 0x0000000001000 | 0x0000000001000 | R E   |
| .rodata  | msg                      | 0x0000000002000 | 0x0000000002000 | R     |
| .bss     | mul                      | 0x0000000002db0 | 0x0000000003db0 | R W   |
| .data    | num, factor              | 0x0000000002db0 | 0x0000000003db0 | R W   |

- Ejecutar ahora el programa y obtener los segmentos de memoria virtual accediendo al fichero maps del directorio del proceso en /proc. Nota: Se puede identificar la correspondencia de los segmentos del ejecutable y los segmentos de memoria virtual comparando el camp offset y los flags:

- NOTA IMPORTANTE: POR ALGUN MOTIVO DESCONOCIDO ALGÚN NOTAS DECIDIÓ QUE ERA BUENA IDEA HACER QUE CTRL C TERMINASE PROCESOS EN TERMINAL POR LO QUE SI EL PROCESO TERMINA ENTONCES NO HAY PROCESO A COMPROBAR
- Si el resultado esperado es anon, significa que esa memoria es privada, mientras que si sale cualquier otra cosa, esa memoria es compartida con la cosa que salga
- Heap es el lugar donde se almacena la memoria dinámica (todo lo que ponga en Dynamic)
	- NOTA: LAS DIRECCIONES NO COINCIDEN YA QUE AL REHACER EL PROGRAMA POR EL REINCIO DEL PC LAS DIRECCIOENES SE HAN MODIFICADO

|          |                                      |                    |       |                           |                                       |
| -------- | ------------------------------------ | ------------------ | ----- | ------------------------- | ------------------------------------- |
| Segmento | Rango de direcciones virtuales       | Offset del fichero | Flags | Tipo map/anónimo          | Ruta del fichero                      |
| .text    | 00005555555555000-00005555555555FFF  | 4K                 | r x   | Compartida con Ejercicio1 | /home/hlcoal/workspace-jee/Ejercicio1 |
| .rodata  | 00005555555556000-00005555555556FFF  | 4K                 | r     | Compartida con Ejercicio1 | /home/hlcoal/workspace-jee/Ejercicio1 |
| .bss     | 00005555555558000-00005555555558FFF  | 4K                 | rw    | Compartida con Ejercicio1 | /home/hlcoal/workspace-jee/Ejercicio1 |
| .data    | 00005555555558000-00005555555558FFF  | 4K                 | rw    | Compartida con Ejercicio1 | /home/hlcoal/workspace-jee/Ejercicio1 |
| [heap]   |                                      |                    |       |                           |                                       |
| [stack]  | 00007ffff7ffdd000-00007ffff7ffeffff- | 136K               | x     | Compartida con pila       | pila                                  |

- Nota: Alternativamente, el programa pmap(1) puede utilizarse para consultar la información sobre los segmentos de memoria (misma información que proc/pid>/maps)

- Cuestiones:

	- En qué segmento(s) de memoria virtual está la cadena "El resultado es:\n". Los contenido del segmento de memoria virtual se puede acceder en el directorio del proceso /proc/pid proceso>/map_files/rango del segmento>. Comprobar que la respuesta es correcta con el comando strings(1).
    
	- En la salida del comando readelf se muestra el inicio del programa (entry point). ¿En qué segmento del fichero está ubicado? ¿Y en qué segmento de memoria virtual?
    
	- Dibuja esquemáticamente (como en las transparencias de teoría) el espacio de direcciones del proceso con las regiones correspondientes.
    
	- Investiga cuál es el contenido y propósito de las áreas de memoria marcadas como [vdso] y [vvar].

- Ejercicio 6 
	- Datos: 
		- 512 páginas memoria virtual
		- Tamaño de 512 palabras --> 9 bits referenciados por palabra
		- 4 bits <= Mem física 10 marcos
		- Dir virtual [9bits]  [9bits]
		- Dir f´ísica  [4bits]  [9 bits]
	- Tabla de páginas:
		-  

| nº Virt | M fisica | V   | RWD |
| ------- | -------- | --- | --- |
| 0       |          |     |     |
| 1       |          |     |     |
| 2       |          |     |     |
| 3       |          |     |     |
| 4       | 0100     | 1   |     |
|         |          |     |     |
- Ejercicio 8
- Ejercicio 9
- Ejercicio 10
	- 128 * 4 bytes = 2^7 * 2^2 bytes = 512 