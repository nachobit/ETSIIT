#EJERCICIOS TEMA 5#

##Ejercicio 5.1: Buscar información sobre cómo calcular el número de conexiones por segundo.##

Habría que considerar los datos que la máquina envía. La transferencia de estos datos se calcularía como:

	`días por mes x visitas diarias x páginas por visita x volumen por página x 1,25`


Por otro lado existen herramientas (ab, siege...) que permiten simular conexiones o peticiones sobre un servicio web en el que se tiene en cuenta el tiempo de respuesta, peticiones fallidas, datos transferidos o peticiones por segundo realizadas.

##Ejercicio 5.2: Instalar wireshark y observar cómo fluye el tráfico de red en uno de los servidores web mientras se le hacen peticiones HTTP.##

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/trabajos_clase/wire.gif)


##Ejercicio 5.3: Buscar información sobre características, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.##

**NAGIOS**: sistema de monitorización de redes número uno, de código abierto.
Entre sus características figura la monitorización de servicios SMTP, POP3, HTTP... y de recursos de sistemas hardware (uso de discos, memoria, puertos, carga del procesador...).

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/trabajos_clase/nagios.png)

**ZABBIX**: sistema de monitoreo de redes diseñado para servicios de red, hardware de red y servidores. Ofrece al igual que Nagios bastantes posiblidades de análisis y puede ser intalado tanto en UNIX como en Windows para monitorizar carga de CPU, uso de memoria, discos duros, etc.

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/trabajos_clase/Zabbix.png)

**PRTG Network Monitor**: otro servicio de monitoreo de redes para Windows. Soporta dispositivos en IPv6 y se basa en interfaz web como Nagios y Zabbix.

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/trabajos_clase/PRTG.png)

**New Relic SERVERS**: uno de las soluciones más completas en el mercado, centrado en grandes empresas y con métricas de análisis avanzadas que abarcan todos los servicos que se componen en un servidor.