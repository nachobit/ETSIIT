#EJERCICIOS TEMA 3#

##Ejercicio T3.1: Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.

Podemos crear reglas a través de IPtables de la forma:
- iptables -t nat -A PREROUTING -p tcp --dport 2222 -j DNAT --to-destination 7.7.7.7:2222

Enmascarado de la dirección IP:
- iptables -t nat -A POSTROUTING -j MASQUERADE

Podemos redireccionar el tráfiico de un parte de la red de la forma:
- iptables -t nat -A PREROUTING -s 10.1.1.0/24 -p tcp --dport 2222 -j DNAT --to-destination 7.7.7.7:2222

##Ejercicio T3.2: Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

**Para el filtrado de paquetes en Windows podemos usar la herramienta IPSec**

IPSec sigue una estructura similar a la siguiente:
- IPSeccmd.exe -w REG -p "Filtro de bloqueo ProtocolPortNumber - r "Block entrante ProtocolPortNumber regla" -f * = 0:PortNumber:Protocol - n BLOCK-x

Ejemplo de aplicación para bloquear el acceso al puerto 80 de entrada permitiendo el acceso saliente TCP 80:
- IPSeccmd.exe -w REG -p "Bloquear TCP 80 filtro" - r "bloquear entrada TCP 80 regla" -f * = 0:80:TCP - n BLOCK - x

Ejemplo de regla de filtrado en el acceso entrante al puerto TCP 80 para otro filtro UDP existente:
- IPSeccmd.exe -p "Filtro de bloque UDP 1434" -w REG - r "bloquear entrante TCP 80 Rule" -f * = 0:80:TCP - n BLOCK

**Para el filtrado de paquetes en linux usamos el comando iptables:**

*iptables usa la siguiente estructura:*

iptables [-t nombre-tabla] <comando> <nombre-cadena> <parametro 1> \ <opcion1>

Ejemplo de aplicación de un filtrado a un puerto determinado (2222):
- iptables -A INPUT -p tcp –sport 2222

Ejemplo de bloqueo de tráfico procedente de un rango IP:
- iptables -A INPUT -p tcp -m iprange –src-range 192.168.1.13-192.168.2.19

Ejemplo de bloqueo de MAC:
- iptables -A INPUT -m mac –mac-source 00:00:00:00:00:01

Si queremos permitir conexiones entrantes dede páginas web:
- iptables -A INPUT -i eth0 -p tcp –dport 80 -m state –state NEW,ESTABLISHED -j ACCEPT

Igual que la anterior pero para conexiones salientes:
- iptables -A OUTPUT -o eth0 -p tcp –sport 80 -m state –state ESTABLISHED -j ACCEPT

*-A agregamos una nueva regla*

*-sport: selecciona/excluye puertos de un puerto origen determinado*

*-dport: selecciona/excluye puertos de un puerto destino determinado*