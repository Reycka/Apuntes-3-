- 1.Dibujar un esquema que muestre los segmentos/datagramas que intercambian el cliente y el servidor en las siguientes situaciones: 
	- a) Establecimiento de una conexión TCP, suponiendo que el puerto servidor está ABIERTO (mostrar en este caso los números de secuencia y confirmación intercambiados).
![[Pasted image 20260409103241.png]]

| SEQ   | NAck  | FIN | SYN | ACK | RST |          |
| ----- | ----- | --- | --- | --- | --- | -------- |
| x     | ---   | 0   | 1   | 0   | 0   | Cliente  |
| y     | x + 1 | 0   | 1   | 1   | 0   | Servidor |
| x + 1 | y + 1 | 0   | 0   | 1   | 0   | Cliente  |
	- b) Establecimiento de una conexión TCP, suponiendo que el puerto servidor está CERRADO.

| SEQ   | NAck  | FIN | SYN | ACK | RST |          |
| ----- | ----- | --- | --- | --- | --- | -------- |
| x     | ---   | 0   | 1   | 0   | 0   | Cliente  |
| y     | x + 1 | 0   | 0   | 1   | 1   | Servidor |


	- c) Envío de un datagrama UDP, suponiendo que el puerto servidor está CERRADO.

 El cliente manda el Datagrama y el servidor el ICMP, las flags están vacías 
![[Pasted image 20260409103200.png]]

| Puerto fuente | Puerto destino  |
| ------------- | --------------- |
| Puerto Emisor | Puerto Receptor |

	- d) El cliente realiza fin de conexión, pero al servidor le quedan datos por enviar
 
![[Pasted image 20260410113135.png]]

| SEQ       | NAck      | FIN | SYN | ACK | RST |          |
| --------- | --------- | --- | --- | --- | --- | -------- |
| x + n     | y + n     | 1   | 0   | 1   | 0   | Cliente  |
| y + n     | x + n + 1 | 0   | 0   | 1   | 0   | Servidor |
| y + n     | x + n + 1 | 1   | 0   | 1   | 0   | Servidor |
| x + n + 1 | y +n +1   | 0   | 0   | 1   | 0   | Cliente  |
	- e) El cliente realiza fin de conexión, y al servidor NO le quedan datos por enviar
 
![[Pasted image 20260409103520.png]]

| SEQ       | NAck      | FIN | SYN | ACK | RST |          |
| --------- | --------- | --- | --- | --- | --- | -------- |
| x + n     | y + n     | 1   | 0   | 1   | 0   | Cliente  |
| y + n     | x + n + 1 | 1   | 0   | 1   | 0   | Servidor |
| x + n + 1 | y + n + 1 | 0   | 0   | 1   | 0   | Cliente  |
- 2. Supongamos la siguiente topología de red. Las direcciones IP y MAC de cada máquina están representadas de forma simbólica. Como encaminador predeterminado, las máquinas A y B tienen configurado a IP_R0 y la máquina C a IP_R1, respectivamente. Las tablas ARP de todas las máquinas están inicialmente vacías.
	![[Pasted image 20260410111124.png]]
Desde la máquina A se establece una conexión TCP entre el puerto cliente 15001 de la máquina A y el puerto servidor 80 de la máquina C Completa la siguiente tabla con todas las tramas que se observarán en la Red 1 cuando se realizan las acciones anteriormente indicadas (sigue las notas al pie de la tabla, puedes añadir tantas filas como sean necesarias).

* NOTAS para rellenar la parte "Contenido y Descripción": - Si la trama lleva contenido ARP: indicar MAC sender, IP sender, MAC target, IP target.. Descripción: indicar el mensaje ARP que corresponda - Si la trama lleva contenido IP: indicar IP src, IP dest, Protocolo. Descripción: indicar el mensaje UDP, TCP o ICMP que corresponda

| Nº  | MAC src | MAC dst | TIPO | Contenido ARP,IP o TCP | DESCRIPCION |
| --- | ------- | ------- | ---- | ---------------------- | ----------- |
| 1   | A       | R0      |      | IP A IP R0             | ARP request |
| 2   | R0      | A       |      | IP R0 IP A             | ARP reply   |
| 3   | A       | R0      |      | IP A IP C TCM          | SYN         |
| 4   | R0      | A       |      | IP C IP A TCP          | SYN + ACK   |
| 5   | A       | R0      |      | IP A IP C TCP          | ACK         |
- 3. Suponiendo que se envían segmentos TCP de 100 bytes cada uno, rellenar los números de secuencia (SEQ) y confirmación (ACK) para los casos siguientes:
	NOTA: por comodidad vamos a suponer que se empieza por el byte 0 en vez de byte 1 por lo que en vez de x+1 vamos a poner x (representa que envía el byte 0)
	- ![[Pasted image 20260410122627.png]]
	- ![[Pasted image 20260410122644.png]]
	- ![[Pasted image 20260410122704.png]]
	- ![[Pasted image 20260410122720.png]]
	- ![[Pasted image 20260410123249.png]]


