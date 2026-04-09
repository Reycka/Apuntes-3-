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
 
![[Pasted image 20260409103324.png]]

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
