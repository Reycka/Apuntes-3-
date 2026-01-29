- 1. Se ha enviado un mensaje desde el host A al host B los cuales están conectados a través de las redes que se muestran en la figura.
	- ![[Pasted image 20260129100520.png]]
	- a) Indica las capas del modelo TCP/IP por las que pasa el mensaje al atravesar cada uno de los componentes (Host, Switch, Router)
		-  El Host A y el B pasa por todas , el SW solo llega hasta enlace y finalmente el router que solo llega hasta red
	- b) Si se sustituye el SW por un HUB ¿el mensaje pasaría por las mismas capas? Razona la respuesta.
		- Es exactamente igual pero no existe la capa de enlace, ya que el HUB / BUS no tiene el filtro de enlace que si tiene el switch
-  2. Dada la siguiente topología, y suponiendo que inicialmente las memorias de los conmutadores (SW) están vacías, indicar por qué enlaces viajan las tramas correspondientes a cada uno de los siguientes eventos, y el contenido de las tablas de los conmutadores. NOTA: Cada evento sucede a continuación del anterior, los númeos alrededor del switch son los puertos
- IMPORTANTE: Si la tabla no me lo chiva (es decir no tiene la copia tal cual entonces es un broadCast)
- 
	- ![[Pasted image 20260129101601.png]]
	- a) C envía una trama a todos (Tiempo = a)
	- b) D envía una trama a C  (Tiempo = b)
	- c) F envía una trama a E (Tiempo = c)
	- d) B envía una trama a C (Tiempo = d)
	- e) D envía una trama a B (Tiempo = e)
	- Tablas de los conmutadores:
		
SWITCH 1

| MARCA<br>TIEMPO | DIR.MAC | PUERTO | Enlaces (ESTO NO SE GUARDA EN UN SWITCH) |
| --------------- | ------- | ------ | ---------------------------------------- |
| a               | C       | 1      | Todos (BroadCast)                        |
| c               | F       | 1      | Todos (BroadCast)                        |

SWITCH 2

| MARCA<br>TIEMPO | DIR.MAC | PUERTO | Enlaces           |
| --------------- | ------- | ------ | ----------------- |
| a               | C       | 1      | Todos (BroadCast) |
| c               | F       | 3      | Todos (BroadCast) |
| d               | B       | 0      | B - SW2 - SW3 - C |
| e               | D       | 1      | D - SW3 - SW2 - B |
SWITCH 3

| MARCA<br>TIEMPO | DIR.MAC | PUERTO | Enlaces                                     |
| --------------- | ------- | ------ | ------------------------------------------- |
| a               | C       | 0      | Todos (BroadCast)                           |
| b               | D       | 1      | D - SW3 - C                                 |
| c               | F       | 2      | Todos (BroadCast)                           |
| d después e*    | B       | 2      | (b) B - SW2 - SW3 - C (e) D - SW3 - SW2 - B |

SWITCH 4

| MARCA<br>TIEMPO | DIR.MAC | PUERTO | Enlaces           |
| --------------- | ------- | ------ | ----------------- |
| a               | C       | 0      | Todos (BroadCast) |
| c               | F       | 2      | Todos (BroadCast) |
