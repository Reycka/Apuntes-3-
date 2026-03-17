1) Los que son seguros para intercambiar son los asimétricos, la integridad se consigue gracias a los algoritmos HMAC
2) MD5 y SHA Hashing per MD5 obsoleto (BUSCAMOS HASHING PARA CONTRASEÑAS)
3) Lo que protege la confidencialdad es el HTTPS
4) Medidas de Prevención, no de detección
5) Certificado valido (firmado por autoridad reconocida, no caducado y no revocado)
6) Un programa no guarda código ejecutable en la pila, eso es la base del buffer overflow que busca introducir código ejecutable en la pila donde nunca hay código ejecutable
7) El cifrado es más costoso que el hash y un algoritmo de hash es suficiente para poder defender las contraseñas (no los user names) de nuestros usuarios
8) En la detección el cliente no es el que tiene el detector, es el servidor por tanto es el servidor donde