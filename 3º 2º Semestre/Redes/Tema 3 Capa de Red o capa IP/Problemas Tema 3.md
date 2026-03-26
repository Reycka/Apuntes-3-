- 3. Un computador tiene la siguiente dirección IP en notación CIDR: 150.26.193.66/21. Determinar: 
	- a) La máscara de red en notación decimal de punto. 
		- 255.255.248.0
	- b) La dirección de la red donde está conectado el computador. 
		- 150.26.192.0
	- c) La dirección de difusión (broadcast) de dicha red. 
		- 150.26.199.255
	- d) El número máximo de máquinas que pueden conectarse a esa red. 
		- 2^11 -2
	- e) El rango de direcciones IP que pueden asignarse a las máquinas de dicha red.
		- 150.26.192.1 - 150.26.192.254
	
- 4. Repite el ejercicio 3 pero con la CIDR  150.26.193.66/26
	- a) La máscara de red en notación decimal de punto. 
		- 255.255.255.192
	- b) La dirección de la red donde está conectado el computador. 
		- 150.26.193.64
	- c) La dirección de difusión (broadcast) de dicha red. 
		- 150.26.193.127
	- d) El número máximo de máquinas que pueden conectarse a esa red. 
		- 2^6 -2
	- e) El rango de direcciones IP que pueden asignarse a las máquinas de dicha red.
		- 150.26.193.65 - 150.26.193.126
- 5. Supongamos una red con dirección 147.96.0.0/16 en la que se quieren hacer 8 subredes. Determinar: 
	- a) La nueva máscara de subred. 
		- 255.255.224.0
	- b) La dirección de red, dirección de difusión y rango de direcciones IP de cada subred. 
		- SubRed1
			- Direccion de Red: 147.96.0.0
			- Direccion de difusion: 147.96.31.255 (0 + 31)
			- Rango de direcciones: 147.96.0.1 - 147.96.31.254
		- SubRed2
			- Direccion de Red: 147.96.32.0
			- Direccion de difusion: 147.96.63.255 (32 + 31)
			- Rango de direcciones:147.96.32.1 - 147.96.63.254
		- SubRed3
			- Direccion de Red: 147.96.64.0
			- Direccion de difusion: 147.96.95.255 (64 + 31)
			- Rango de direcciones: 147.96.64.1 - 147.96.95.254
		- SubRed4
			- Direccion de Red: 147.96.96.0
			- Direccion de difusion: 147.96.127.255
			- Rango de direcciones: 147.96.96.1 - 147.96.127.254
		- SubRed5
			- Direccion de Red: 147.96.128.0
			- Direccion de difusion: 147.96.159.255
			- Rango de direcciones: 147.96.128.1 - 147.96.159.254
		- SubRed6
			- Direccion de Red: 147.96.160.0
			- Direccion de difusion: 147.96.191.255
			- Rango de direcciones: 147.96.128.1 - 147.96.191.254
		- SubRed7
			- Direccion de Red: 147.96.192.0
			- Direccion de difusion: 147.96.223.255
			- Rango de direcciones: 147.96.192.1 - 147.96.223.254
		- SubRed8
			- Direccion de Red: 147.96.224.0
			- Direccion de difusion: 147.96.255.255
			- Rango de direcciones: 147.96.224.1 - 147.96.255.254
- 6. Supongamos una red con dirección 147.96.80.0/24 en la que se quieren crear redes de 20 hosts. Determinar:
- a) La máscara de subred más apropiada. 
	- 255.255.255.224
- b) El número máximo de máquinas en cada subred. 
	- 2^5 máquinas = 32 dispositivos
- c) El número máximo de subredes. 
	- 2^3 subredes = 8 Subredes
- d) La dirección red, dirección de difusión y rango de direcciones IP de cada subred. 
	- SubRed1
		- Direccion de Red: 147.96.80.0
		- Direccion de difusion: 147.96.80.31
		- Rango de direcciones: 147.96.80.1 - 147.96.80.30
	- SubRed2
		- Direccion de Red: 147.96.80.32
		- Direccion de difusion: 147.96.80.63 
		- Rango de direcciones:147.96.80.33 - 147.96.80.62
	- SubRed3
		- Direccion de Red: 147.96.80.64
		- Direccion de difusion: 147.96.80.95 
		- Rango de direcciones: 147.96.80.66 -  147.96.80.94 
	- SubRed4
		- Direccion de Red: 147.96.80.96
		- Direccion de difusion: 147.96.80.127
		- Rango de direcciones: 147.96.80.97-  147.96.80.126
	- SubRed5
		- Direccion de Red: 147.96.80.128
		- Direccion de difusion: 147.96.80.159
		- Rango de direcciones: 147.96.80.129 - 147.96.80.158
	- SubRed6
		- Direccion de Red: 147.96.80.160
		- Direccion de difusion: 147.96.80.191
		- Rango de direcciones: 147.96.80.161 - 147.96.80.190
	- SubRed7
		- Direccion de Red: 147.96.80.192
		- Direccion de difusion: 147.96.80.223
		- Rango de direcciones: 147.96.80.193 - 147.96.80.222
	- SubRed8
		- Direccion de Red: 147.96.80.224
		- Direccion de difusion: 147.96.80.255
		- Rango de direcciones: 147.96.80.223 - 147.96.80.254


- 7. Supongamos una red con dirección 147.96.80.0/24. Usando VLSM, se quieren crear las siguientes subredes: 
- • 1 subred de 126 máquinas. 
- • 1 subred de 62 máquinas. 
- • 1 subred de 30 máquinas. 
- • 2 subredes de 14 máquinas. 
- Determinar una posible división en subredes para dicha red, especificando la dirección de red, la de difusión, y la máscara de cada una de las subredes.

	- SubRed1 147.96.80.0 - 147.96.80.127 (126 HOSTS)
		- Máscara 255.255.255.128
	- SubRed2 147.96.80.128 - 147.96.80.191 (62 HOSTS)
		- Máscara 255.255.255.192
	- SubRed3 147.96.80.192 - 147.96.80.223 (30 HOST)
		- Máscara 255.255.255.224
	- SubRed4 147.96.80.224 - 147.96.80.239 (14 HOSTS)
		- Máscara 255.255.255.240
	- SubRed45147.96.80.240 - 147.96.80.255 (14 HOSTS)
		- Máscara 255.255.255.240
- 8. Una determinada organización ha contratado la dirección de red 128.24.0.0/16 y pretende implantar un esquema de direccionamiento VLSM del siguiente modo:
- ![[Pasted image 20260326101335.png]]
	a) Determinar la dirección de red y la máscara de las 8 subredes de primer nivel. 
	
	- SubRed1: 128.24.0.0  --  Máscara 255.255.32.0
	- SubRed2: 128.24.32.0 --  Máscara 255.255.64.0
	- SubRed3: 128.24.64.0 --  Máscara 255.255.96.0
	- SubRed4: 128.24.96.0 --  Máscara 255.255.128.0
	- SubRed5: 128.24.128.0 --  Máscara 255.255.160.0
	- SubRed6: 128.24.160.0 --  Máscara 255.255.192.0
	- SubRed7: 128.24.192.0 --  Máscara 255.255.224.0
	- SubRed8: 128.24.224.0 --  Máscara 255.255.255.0
	
	b) Determinar el rango de IPs y dirección de difusión para la “Red 3”. 
	- 128.24.64.1 - 128.24.94.255
	
	c) Determinar la dirección de red y la máscara de las 16 subredes de la “Red 6”.  POR HACER

	- SubRed1: 128.24.160.0   --  Máscara 255.255.31.0
	- SubRed2: 128.24.160.0  --  Máscara 255.255.63.0
	- SubRed3: 128.24.160.0  --  Máscara 255.255.95.0
	- SubRed4: 128.24.160.0  --  Máscara 255.255.127.0
	- SubRed5: 128.24.160.0  --  Máscara 255.255.159.0
	- SubRed6: 128.24.160.0 --  Máscara 255.255.191.0
	- SubRed7: 128.24.160.0  --  Máscara 255.255.223.0
	- SubRed8: 128.24.160.0  --  Máscara 255.255.255.0
	- SubRed9: 128.24.160.0 --  Máscara 255.255.31.0
	- SubRed10: 128.24.160.0  --  Máscara 255.255.63.0
	- SubRed11: 128.24.160.0 --  Máscara 255.255.95.0
	- SubRed12: 128.24.160.0  --  Máscara 255.255.127.0
	- SubRed13: 128.24.160.0  --  Máscara 255.255.159.0
	- SubRed14: 128.24.160.0 --  Máscara 255.255.191.0
	- SubRed15: 128.24.160.0  --  Máscara 255.255.223.0
	- SubRed16: 128.24.160.0 --  Máscara 255.255.255.0
	
	d) Determinar el rango de IPs y dirección de difusión para la “Red 6.3”. 
	e) Determinar la dirección de red y la máscara de las 8 subredes de la “Red 6.14”. f) Determinar el rango de IPs y dirección de difusión para la “Red 6.14.2”.

- 9. Supongamos la siguiente topología de red. Las direcciones IP y MAC de cada máquina están representadas de forma simbólica. Como encaminador predeterminado (por defecto), las máquinas A y B tienen configurado a IP_R0 y la máquina C a IP_R1. Las tablas ARP de todas las máquinas están inicialmente vacías. 
- ![[Pasted image 20260326091250.png]]
	- a) Mostrar el contenido de las tablas de encaminamiento de cada Host y del router tras ejecutar la orden ip route show
	- b) Desde la máquina A - Primero se ejecuta el comando $ ping -c 2 IP_B - Luego se ejecuta el comando $ ping -c 1 IP_C
	- 
- RED 1

| CAB | ECE     | RA      | ETH                   | CABECERA                      | ARP o IP                                       |
| --- | ------- | ------- | --------------------- | ----------------------------- | ---------------------------------------------- |
| Nº  | MAC src | MAC dst | TIPO                  | Contenido ARP o IP            | DESCRICIÓN                                     |
| 1   | MAC A   | BR      | ARP Request-BroadCast | MAC A - MAC BR - IP A- IP B   | Pregunta quien tiene esta IP                   |
| 2   | MAC B   | MAC A   | ARP Reply             | MAC B - MAC A - IP B - IP A   | Dice a A quien es y donde esta                 |
| 3   | MAC A   | MAC B   | IP REQUEST            | IP A - IP B                   | Ping de A - B ICMP                             |
| 4   | MAC B   | MAC A   | IP Reply              | IP B - IP A                   | B Contesta al ping de A                        |
| 5   | MAC A   | MAC B   | IP Request            | IP A - IP B                   | Ping de A - B ICMP                             |
| 6   | MAC B   | MAC A   | IP Reply              | IP B - IP A                   | B Contesta al ping de A                        |
| 7   | MAC A   | BR      | ARP Request           | MAC A - MAC BR - IP A - IP R0 | A pregunta quien tiene la IP de R0             |
| 8   | MAC R0  | MAC BR  | ARP Reply             | MAC R0 - MAC BR- IP R0 - IP A | R0 responde a A                                |
| 9   | MAC R0  | MAC A   | IP Reply              | IP R0 - IP A                  | R0 devuelve el echo de C a A                   |
| 10  | MAC A   | MAC R0  | IP request            | IP A - IP R0                  | A pregunta quien tiene la IP de su encaminador |


- RED 2

| CAB | ECE     | RA      | ETH         | CABECERA                     | ARP o IP                                               |
| --- | ------- | ------- | ----------- | ---------------------------- | ------------------------------------------------------ |
| Nº  | MAC src | MAC dst | TIPO        | Contenido ARP o IP           | DESCRICIÓN                                             |
| 1   | MAC R0  | MAC BR  | ARP Request | MAC R0 - MAC BR IP R0 - IP C | R0 pregunta quient tiene la IP C                       |
| 2   | MAC R0  | MAC C   | IP Request  | IP A - IP C                  | R0 manda el ping de A a C                              |
| 3   | MAC C   | MAC R0  | ARP reply   | MAC C - MAC R0               | C contesta a R0 con donde está                         |
| 4   | MAC C   | MAC R'  | IP reply    | IP C - IP A                  | C contesta al ping de A y se lo manda a su encaminador |
c) Indica cuál será el contenido final de las tablas ARP de A, B y C:

A

| DIR IP | DIR MAC |
| ------ | ------- |
| IP B   | MAC B   |
| IP R0  | MAC R0  |

B

| DIR IP | DIR MAC |
| ------ | ------- |
| IP A   | MAC A   |

C

| DIR IP | DIR MAC |
| ------ | ------- |
| IP R0  | MAC R0  |
