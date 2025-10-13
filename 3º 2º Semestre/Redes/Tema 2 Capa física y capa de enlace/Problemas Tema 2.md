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

| MARCA<br>TIEMPO | DIR.MAC | PUERTO | Enlaces                           |
| --------------- | ------- | ------ | --------------------------------- |
| a               | C       | 0      | Todos (BroadCast)                 |
| b después e*    | D       | 1      | D - SW3 - C (e) D - SW3 - SW2 - B |
| c               | F       | 2      | Todos (BroadCast)                 |
| d               | B       | 2      |  B - SW2 - SW3 - C                |

SWITCH 4

| MARCA<br>TIEMPO | DIR.MAC | PUERTO | Enlaces           |
| --------------- | ------- | ------ | ----------------- |
| a               | C       | 0      | Todos (BroadCast) |
| c               | F       | 2      | Todos (BroadCast) |

- 3. Dada la siguiente topología, y suponiendo que inicialmente las memorias de los conmutadores (SW) están vacías, indicar por qué enlaces viajan las tramas correspondientes a cada uno de los siguientes eventos, y el contenido de las tablas de los conmutadores. NOTA: Cada evento sucede a continuación del anterior 1. A envía una trama a C. 2. D envía una trama a A. 3. F envía una trama a D. 4. B envía una trama a F. 5. E envía una trama de difusión
- ![[Pasted image 20260205090703.png]]
- a) A envía una trama a C. 
- b) D envía una trama a A. 
- c) F envía una trama a D. 
- d) B envía una trama a F. 
- e) E envía una trama de difusión.

SWITCH 1

| MARCA DE TIEMPO | DIR MAC | PUERTO | ENLACES                                |
| --------------- | ------- | ------ | -------------------------------------- |
| a               | A       | 0      | BroadCast                              |
| b               | D       | 1      | D-HUB2-SW2 --- D-HUB2-HUB1-SW1 y C - A |
| c               | F       | 1      | BroadCast                              |
| d               | B       | 2      | B-SW1-HUB1-HUB2                        |
| e               | E       | 1      | BroadCast                              |
SWITCH 2

| MARCA DE TIEMPO | DIR MAC | PUERTO | ENLACES                                  |
| --------------- | ------- | ------ | ---------------------------------------- |
| a               | A       | 1      | BroadCast                                |
| b               | D       | 1      | -                                        |
| c               | F       | 0      | F-SW2-Hub2-D (Apuntar todos los enlaces) |
| d               | B       | 1      | BroadCast                                |
| e               | E       | 2      | BroadCast                                |

- 4. Dada la siguiente topología, y suponiendo que inicialmente las memorias de los conmutadores (SW) están vacías, indica por qué enlaces viajan las tramas correspondientes a cada uno de los siguientes eventos, y cómo queda la memoria de los conmutadores tras cada uno:
- ![[Pasted image 20260205093742.png]]
- a) C envía una trama de difusión. 
- b) E envía una trama a C 
- c) A envía una trama a C 
- d) C envía una trama a A 
- e) F envía una trama a B

SWITCH1

| MARCA DE TIEMPO | DIR MAC | PUERTO | ENLACES                       |
| --------------- | ------- | ------ | ----------------------------- |
| a/d*            | C       | 0      | BroadCast (C-HUB-SW3 y SW1-A) |
| b               | E       | 0      | -                             |
| c               | A       | 2      | A-SW1-HUB-C                   |
| e               | F       | 3      | BroadCast                     |
SWITCH2

| MARCA DE TIEMPO | DIR MAC | PUERTO | ENLACES   |
| --------------- | ------- | ------ | --------- |
| a               | C       | 0      | BroadCast |
| e               | F       | 2      | BroadCast |

SWITCH3

| MARCA DE TIEMPO | DIR MAC | PUERTO | ENLACES     |
| --------------- | ------- | ------ | ----------- |
| a/d*            | C       | 1      | BroadCast   |
| b               | E       | 2      | E-SW3-HUB-C |
| c               | A       | 1      | -           |
| e               | F       | 1      | BroadCast   |
- 5. Supongamos que tenemos 5 estaciones de trabajo, A, B, C, D y F, conectadas tal y como se muestra en la figura. AP1 y AP2 están conectados mediante un sistema de distribución cableado de tipo Ethernet. 
- ![[Pasted image 20260206114536.png]]
- Describir qué sucede cuando se observan las siguientes tramas en la red, indicando, para cada caso, si la combinación de direcciones es válida para esta topología y, en caso afirmativo, especificando el tipo de trama (Ethernet o WiFi), el segmento de red por el que circula cada trama (E1, E2, E3, ó E4), así como la estación origen y destino. 
- a) Dir1=MAC_AP1, Dir2=MAC_A, Dir3=MAC_D, a DS=1, de DS=0 
	- Correcto, trama WIFI que circula por E1 cuyo destino es AP1 y su origen es A y el destino final es D
- b) Dir. Destino=MAC_B, Dir. Origen=MAC_F 
	- **Correcto, trama Ethernet que circula por E2 y E3 cuyo destino es B y el origen es F
- c) Dir1=MAC_D, Dir2=MAC_AP2, Dir3=MAC_B, a DS=0, de DS=1 
	- Correcto, trama WIFI  que circula por E4 cuyo destino es D, el origen es AP2 y su origen inicial es B
- d) Dir1=MAC_AP1, Dir2=MAC_AP2, Dir3=MAC_A, Dir4=MAC_D, a DS=1, de DS=1
	- Falso, pq como están enganchados por cable no puede haber un 1 a 1 ya que esto solo ocurre si ambops APs están conectados por wifi, no por cable
	
- 6. Supongamos una topología de red compuesta por cuatro computadores (A, B, C y D), dos puntos de acceso WiFi (AP1 y AP2) y un sistema de distribución cableado por Ethernet. Supongamos que observamos los siguientes grupos de tramas WiFi y Ethernet en dicha red: NOTA: la colocación de las tramas en cada apartado puede NO ESTAR EN ORDEN  LOS APARTADOS SON UNA ÚNICA TRAMA POR LO QUE DENTRO DEL APARTADO SI VAN EN ORDEN

- a) E2: Dir1=MAC_AP1, Dir2=MAC_B, Dir3=MAC_D, a DS=1, de DS=0 E3: Dir. Destino=MAC_D, Dir. Origen=MAC_B                                         E4: Dir1=MAC_D, Dir2=MAC_AP2, Dir3=MAC_B, a DS=0, de DS=1

- b) E1: Dir1=MAC_A, Dir2=MAC_AP1, Dir3=MAC_C, a DS=0, de DS=1 E3: Dir. Destino=MAC_A, Dir. Origen=MAC_C

- c) E2: Dir1=MAC_AP1, Dir2=MAC_B, Dir3=MAC_A, a DS=1, de DS=0  E1: Dir1=MAC_A, Dir2=MAC_AP1, Dir3=MAC_B, a DS=0, de DS=1

- donde E1, E2, E3 y E4 identifican a los distintos segmentos de la red, Dibujar y justificar una topología de red capaz de realizar TODAS las comunicaciones anteriores e identificar los BSSs existentes en dicha topología.
- ![[Pasted image 20260206124234.png]]