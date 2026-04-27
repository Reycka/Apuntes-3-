**1.** En la topología de red de la figura ejecutamos wireshark para capturar el tráfico y obtenemos los siguiente siguientes mensajes

![[Pasted image 20260416090846.png]]
a)       ¿En qué red está escuchando wireshark ?
- El wireshark está escuchando en la Red 1
b)       ¿Quién envía el mensaje y qué tipo de instrucción ha ejecutado para enviarlo?
- El que envía el mensaje es el Host 3 y la instrucción que ha mandado es ping -c 3
c)       ¿A quién va dirigido el mensaje?
- El mensaje va dirigido al Host2
d)       ¿A qué protocolo pertenecen los dos primeros mensajes? y ¿Por qué se envían?
- Los 2 primeros mensajes pertenecen al protocolo ARP
e)       ¿Cuál es la dirección destino de la cabecera de enlace  del primer mensaje? Y por qué
- La dirección destino de la cabecera de enlace del primer mensaje es un broadCast ya que la tabla del router 1 en la red 1 no tiene la IP registrada, por lo que la pide a todas las máquians de la red esperando la respuesta de alguna
f)        ¿Qué máquina responde el primer mensaje? Y por qué
- El host 2 ya que es quien tiene la IP que pedía el broadcast
2 . En la topología de red de la figura, ejecutamos Wireshark **para capturar el tráfico de la red 2**. En dicha captura observamos el siguiente mensaje ICMP 
![[Pasted image 20260416091303.png]]
![[Pasted image 20260416091313.png]]
a)       ¿Qué máquina envió este mensaje?
- El Host A
b)       ¿A qué máquina va dirigido este mensaje?
- Al Host C
c)       ¿A qué máquina e interfaz de red corresponde la dir. MAC origen de la cabecera Ethernet ?
- Al Router 1
d)       ¿A qué máquina e interfaz de red corresponde la dir. MAC destino de la cabecera Ethernet
- Al Router 2
e)       Cuando la máquina origen envió este mensaje, ¿cuál era el valor inicial del campo TTL de la cabecera IP?
- 64
3 . En la siguiente topología de red los computadores A y B tienen configurado a R como su encaminador predeterminado. En el computador A se ejecuta la siguiente orden: 
![[Pasted image 20260416091850.png]]
![[Pasted image 20260416092035.png]]

a)       ¿Qué tipo de mensaje es?
- Se trata de un mensaje echo reply del protocolo ICMP
b)       ¿Podemos conocer a través de este paquete la dirección IP del computador A?  
En caso afirmativo, especificar dicha dirección.
- Si, la dirección IP del Host A es 10.10.10.1 que es el Destination del reply
c)       ¿Podemos conocer a través de este paquete la dirección IP del Router por alguna de sus interfaces?  
En caso afirmativo, especificar dicha dirección.
- No podemos saber la Ip del router ya que este mensaje no lo indica, lo único que indica del router es la Mac, equivalente a la Mac destino

d)       ¿Podemos conocer a través de este paquete la dirección MAC del computador A?  
En caso afirmativo, especificar dicha dirección. En caso negativo explica por qué.
- No podemos saber la Mac de A ya que en este momento las Mac con las que se trabajan son las de B mac Source y Router mac dest

e)       ¿Podemos conocer a través de este paquete la dirección MAC del computador B?  
En caso afirmativo, especificar dicha dirección. En caso negativo explica por qué.
- Si, la dirección Mac de B es es la Mac Source que es 02:00:00:00:03:00

f)        ¿Podemos conocer a través de este paquete la dirección MAC del encaminador R_eth1?  
En caso afirmativo, especificar dicha dirección.
- Si, la dirección Mac del router es la Mac Destination que es 02;00:00:00:03:00

g)       ¿Podemos conocer la IP de la Red1 y de la Red2
- No, no se puede ya que no conocemos la máscara. (El length es el tamaño de la cabecera)

4 . La siguiente topología de red se ha configurado con las direcciones que se muestran en la tabla:
![[Pasted image 20260416093438.png]]
Se ha enviado un ping y mediante wireshark se ha realizado una captura del mensaje.
![[Pasted image 20260416093509.png]]
a)       ¿Qué máquina a enviado el ping y a que máquina iba dirigido?
- El HostA es el que lo envía y va dirigido al HostC
b)       ¿En qué segmento de red se ha capturado la trama?
- Está capturado en la Red2
5 . Supongamos la siguiente topología de red donde los computadores A y B tienen configurado a R como su encaminador predeterminado. En el computador A se ejecuta la siguiente orden: 
![[Pasted image 20260416093905.png]]
Responder a las siguientes cuestiones:

a) ¿Está activado el mecanismo de descubrimiento de la MTU del camino (_path MTU discovery_) en el computador A? Razonar la respuesta.
- Si, ya que el Router manda la señal a A indicando que debe fragmentar el mensaje para que pase, en caso contrario el Router debería poder fragmentar dicho paquete sin necesitar nada de A más que el propio paquete

b) En esta situación, en caso de ser necesaria la fragmentación de los paquetes que se envíen desde A hasta B, ¿quién realizará dicha fragmentación: el computador A, el router R, o el destinatario B?
- El encargado de realizar dicha fragmentación es el Host A ya que el router al no poder pasarlo manda el mensaje al HostA indicandole que o lo fragmenta o no pasa, por lo que tiene que ser el HostA quien lo fragmente ya que si no lo fragmentaría el router y no mandaría esa señal a A

c) ¿Cuál es la MTU de la red 2?
- 600 bytes

6 . Se ha encargado al administrador de red que configure la siguiente topología para que se puedan conectar todas las máquinas.
![[Pasted image 20260416095106.png]]
Al mostrar las tablas de encaminamiento podemos ver los siguiente:

**Máquina A**

192.168.3.0/24 dev eth0 proto kernel scope link src 192.168.3.10

default via 192.168.3.1 dev eth0

**Router**

192.168.1.0/24 dev eth1 proto kernel scope link src 192.168.1.1

192.168.2.0/24 dev eth2 proto kernel scope link src 192.168.2.1

192.168.3.0/24 via 192.168.3.1 dev eth0

**Máquina C**

192.168.2.0/24 dev eth0 proto kernel scope link src 192.168.2.30

192.168.3.0/24 via 192.168.2.1 dev eth0

**Máquina B**

192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.20

**a)**      ¿Se pueden conectar todas las máquinas? Justifica la respuesta
- No, ya que la red 1 se encuentra aislada
b)      Arregla lo que creas necesario para que se puedan conectar.
- Hay que introducir la IP de A al router
c)       Si añadimos las siguientes entradas permanentes a la tabla ARP de A, evitaremos que esta máquina envíe mensajes ARP cuando se comunica con B o C. ¿Verdadero o Falso?. Razona la respuesta
ip neigh add 192.168.1.20 lladdr 02:00:00:00:00:BB dev eth0
ip neigh add 192.168.2.30 lladdr 02:00:00:00:00:CC dev eth0
- Falso, el protocolo ARP es para Hosts y routers de la misma red NO DE DISTINTAS :/

7 . Se ha configurado la siguiente topología para permitir que todas las máquinas se conecten correctamente al servidor. Como parte del proceso de verificación, se han enviado solicitudes **ping** **desde cada cliente** hacia el servidor con el fin de comprobar la conectividad.
![[Pasted image 20260416101120.png]]
a)       Describe brevemente cuál crees que ha sido el problema 
- Hay una IP mal...
**b)**      Para resolverlo se ha mirado la tabla de encaminamiento del router y de la máquina que ha recibido el mensaje de error obteniendo la siguiente información. **Indica dónde está el problema**
- ![[Pasted image 20260416102200.png]]
- La tabla de encaminamiento del Host 1 no tiene el como llegar  a la Red del Servidor
c) ¿Qué instrucción añadirías para solucionar el problema de conexión anterior?
- Añadiría la HOST 1 la forma de comunicarme con la Subred del servidor, que no la tiene:
- Ip route add 192.168.1.0 via 192.168.1.126 dev eth0