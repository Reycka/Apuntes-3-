![[Pasted image 20260507091804.png]]
Ejercicio 1 (1): El administrador de red ha usado la IP privada tipo C 192.168.120.0/24 para crear tres subredes con la misma máscara 
a) ¿Qué máscara de red tiene que asignar a las subredes?
La máscara de red utilizada será de 26 bits ya que necesitaremos un total de 3 subredes como mínimo dejando siempre 1 suelta ya que no podemos crear 3 subredes sin tener como mínimo una suelta
b) Indica la dirección de subredes

| Subred | Dirección de Red CIDR |
| ------ | --------------------- |
| 1      | 192.168.120.0         |
| 2      | 192.168.120.64        |
| 3      | 192.168.120.128       |
c) Determina la dirección de broadcast y el rango útil de direcciones IP para la “Subred 3”
Dirección broadcast:  192.168.120.191 y su rango de direcciones IP es de 192.168.120.129 - 192.168.120.190

Ejercicio 2 (3 puntos): El administrador de la red, ha configurado las interfaces, direcciones IP y tablas de encaminamiento de cada una de las máquinas. Para comprobar la conectividad entre la Subred 2 y la Subred 3, ha ejecutado desde el Host A el comando: ping -c 1 IP_B

a) Rellena la siguiente tabla indicando TODAS las tramas que circularán por la red. Ponlas en el orden correcto Pon las direcciones IP y MAC de manera simbólica. Por ejemplo, IP-R1-eth0 y MAC-R1-eth0

Las tablas de ARP de A, B, Router-1 y Router-2 contienen la siguiente información, el resto de host tienen las tablas vacías
![[Pasted image 20260507093341.png]]
* NOTAS para rellenar la parte Red, Contenido y Descripción: - SubRed: indica por qué subred viaja la trama - Si la trama lleva contenido ARP: indicar MAC sender, IP sender, MAC target, IP target. Descripción mensaje ARP. - Si la trama lleva contenido IP: indicar IP src, IP dest, Protocolo. Y la descripción del mensaje que corresponda: UDP, TCP o ICMP

| CabeceraEthernet                                              . | CabeceraIP                                                    . |
| --------------------------------------------------------------- | --------------------------------------------------------------- |

| Nº  | Subred | MAC / IP SRC           | MAC / IP DST | TIPO | Contenido ARP O IP    | Descripcion                                                |
| --- | ------ | ---------------------- | ------------ | ---- | --------------------- | ---------------------------------------------------------- |
| 1   | 2      | MAC A IP A             | BroadCast    | ARP  | ARP request broadcast | Pregunta por la MAC del Router 2                           |
| 2   | 2      | MAC Router2 IP router2 | MAC A IP A   | ARP  | ARP reply             | Contesta al Host A con su mac e IP                         |
| 3   | 2      | MAC A IP A             | MAC R1 IP B  | IP   | ICMP request          | Le pasa el mensaje al router para que este se lo mande a B |
| 4   | 3      | MAC R2 IP A            | MAC B IP B   | IP   | ICMP request          | El router le manda a B el mensaje                          |
| 5   | 3      | MAC B IP B             | MAC R2 IP A  | IP   | ICMP reply            | B contesta a A mandando primero el mensaje a R2            |
| 6   | 2      | MAC R2 IP B            | MAC A IP A   | IP   | ICMP reply            | El R2 le manda el mensaje de B a A                         |

b) Tras el tráfico generado en el apartado a), ¿cómo han quedado las tablas de cada uno de los conmutadores (SW), sabiendo que en el momento en que se ha mandado ese ping las tablas los conmutadores (SW) contienen lo siguiente?: 

SWITCH 1

| Marca de Tiempo | DIR MAC | Puerto | Donde manda |
| --------------- | ------- | ------ | ----------- |
| 4               | R2-eth1 | 0      | Br          |
| 5               | B       | 1      | 0           |

SWITCH 2

| Marca de Tiempo | DIR MAC | Puerto | Donde manda |
| --------------- | ------- | ------ | ----------- |
|                 | B       | 0      |             |
|                 | C       | 1      |             |
| 4               | R2-eth1 | 0      | --------    |

SWITCH 3 

| Marca de Tiempo | DIR MAC | Puerto | Donde manda |
| --------------- | ------- | ------ | ----------- |
| 4               | R2-eth1 | 2      | Br          |
SWITCH 4

| Marca de Tiempo | DIR MAC | Puerto | Donde manda |
| --------------- | ------- | ------ | ----------- |
|                 | B       | 2      |             |
| 4               | R2-eth1 | 2      | -------     |
SWITCH 5

| Marca de Tiempo | DIR MAC | Puerto | Donde manda |
| --------------- | ------- | ------ | ----------- |
| 1 *3            | A       | 1      | Br /// 2    |
|                 | R1-eth0 | 0      |             |
| *2 *6           | R2-eth2 | 2      | 1 / 1       |

NOTA: El switch solo aprende del que se le manda no del que le llega, ya que es tu única confirmación directa, del mismo modo si el switch sabe como llegar al sitio que le preguntan y no tiene que mandar el mensaje por ningún lado NO HACE NADA

c) ¿Hay algún SW que haya tenido que hacer broadcast? Si es así, indica qué SW y con cuál/les de los mensajes ha sido
Si, el switch 1, switch 5, y el switch 3. el switch 1 ha sido en el mensaje ICMP request del router2 a B y el 5 ha sido en el ARP request Broadcast ya que A le ha pedido un broadcast y por ende el switch lo hace también y el switch 3 lo hace igual que el 1 ya que tampoco sabe como llegar

Ejercicio 3 (2 puntos): La Subred 1 es la zona wifi. En la topología mostrada en la figura, E1, E2, E3, E4 y E5 representan cada uno de los medios de comunicación.

a) En un momento dado desde el host P envía un mensaje al host K. Indica los distintos enlaces por los viaja la trama (E1, E2, E3, E4 y E5) y escribe el contenido de la cabecera de dicha trama (cabecera capa de enlace) cuando viaja por cada uno de ellos. 
NOTA: los campos de la cabecera de la capa de enlace que interesan en este problema
CABECERA TRAMA WIFI

| DIR 1 | DIR 2 | DIR 3 | DIR 4 | a DS | de DS |
| ----- | ----- | ----- | ----- | ---- | ----- |
| AP1   | P     | K     | ----  | 1    | 0     |
| K     | AP2   | P     | ----  | 0    | 1     |
CABECERA TRAMA ETHERNET

| DIR DESTINO | DIR ORIGEN |
| ----------- | ---------- |
| AP2         | AP1        |


b) Una persona entra en la zona wifi (subred 1) y su portátil realiza una configuración automática de los parámetros de la red (IP, máscara, router predeterminado…) ¿Qué servicio de la capa de aplicación está usando el portátil?
Esta utilizando el protocolo DHCP de la capa de aplicación, el cual se encarga de configurar la IP del Host que se está conectando

c) Los mensajes enviados por el servicio que hace la configuración automática de los parámetros de la red, ¿qué protocolo usa en la capa de transporte?
Utiliza el protocolo UDP ya que prioriza la velocidad

Ejercicio 4 (2.5 puntos): El administrador de la red quiere proteger las IP privadas de los hosts conectados a la red de la empresa.

a) ¿Qué servicio de la capa de aplicación y en qué router de la topología de la red debe configurarlo para lograr esta protección? Explica brevemente cómo funciona.
Utiliza el protocolo NAPT de la capa de Aplicación el cual cambia tus IPs privadas por una IP pública, como solo nos interesa proteger para internet la colocamos en el router2 para que cuando lo mande al exterior sea siempre la IP pública en lugar de la privada rellenando su tabla NAPT

b) Un empleado desde el host C se quiere conectar a www.wikipedia.org cuya dirección IP no conoce su ordenador. ¿Cómo consigue dicho host conocer la dirección IP de esa web? Explica brevemente cómo funciona. Supón que el router de ISP actúa de resolver
Lo consigue a través del protocolo DNS el cual permite la comunicación con el resto de webs a través de un rsolver el cual va preguntando por jerarquías empezando por la raíz y yendo preguntando 1 a 1 (después el TLD y finalmente los subdominios) hasta localizar la IP correspondinete con www.wikipedia.org (Si el resolver lo tiene en cache devuelve la ruta sin buscar)
Se puede explicar con la diapo 31 del Tema 5

c) ¿Qué dirección IP fuente tendrán los mensajes enviados por el host C cuando llegan el router del ISP?
Cuando lleguen al router de ISP la IP de C es la pública ya que el Router2 ya ha modificado la IP privada y le pasa la pública a este router

Ejercicio 5 (1,5 puntos): En un momento dado el Host A inicia una conexión TCP con el servidor
a) ¿Qué mensajes se envían al iniciar la conexión? añádelos en el siguiente esquema. 
SYN - SYN ACK - ACK
b) A continuación, desde el host A se envían al servidor una serie de segmentos de 1000 bytes en el orden que se muestra el esquema. Complétalo con los números de confirmación de los segmentos devueltos por el servidor.

![[Pasted image 20260507104558.png]]