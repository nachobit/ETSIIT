#Practica 4#

## COMPROBAR EL RENDIMIENTO DE SERVIDORES WEB ##

### Pasos iniciales: ###

- Para realizar las pruebas, de acuerdo al guión práctico, tanto dichas pruebas como los resultados mostrados, han sido generados desde la terminal de la máquina anfitriona.

- Para poder sacar una conclusión "más cercana a la realidad" los test se han realizado 10 veces sobre la máquina 1 y la granja web con ambas herramientas.

- Para forzar una carga mayor en los servidores, incorporamos un script PHP en /var/www/ en ambas máquinas servidoras con el fin de generar dicha carga superior en el servidor y la granja web:
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/granja1.png)


*Herramientas usadas:*

- **ab (Apache Benchmark):** programa monoproceso para medir el rendimiento de los servidores web HTTP. Originalmente diseñado para probar Apache HTTP Server, permite realizar pruebas genéricas con cualquier servidor web.

- **Siege:** programa de carga HTTP y utilidad benchmarking. Fue diseñado para permitir a los desarrolladores medir el código bajo una carga forzada. De igual forma, permite medir el rendimiento en servidores web.


### Batería de pruebas ###
**Servidor Solo**

La ejecución de ab ha sido la siguiente:

***ab -n 500 -c 200 http://10.211.55.26/f.php***

	-n 500: solicita 500 veces el script
	-c 200: realiza las peticiones de 200 en 200 (concurrencia)

Benchmarking usando la herramienta ab:
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/ab1_mac.png)

Los valores a tener en cuenta con la herramienta ab por su interés han sido:
* Time taken for test
* Failed requests
* Requests per second
* Time per request

La ejecución de Siege ha sido la siguiente:
 ***siege -b -t60S -v http://10.211.55.26/f.php***

	-b: realiza el test sin pausas
	-t60S: 60 segundos en ejecución
	-concurrencia por defecto: 15

Benchmarking usando la herramienta Siege:
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/siege1.png)

Los valores a tener en cuenta con la herramienta ab por su interés han sido:
* Elapsed Time
* Response Time
* Transaction Rate
* Longest Transaction

Por tanto, usando una concurrencia de 15 usuarios(valor por defecto) tras la ejecución durante 60 segundos como se muestra en la anterior captura, obtenemos los siguientes resultados:
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/siege2.png)


En la siguiente tabla se muestran los resultados obtenidos tras realizar la batería de pruebas en el servidor 10 veces:
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/ssolo.png)


### Batería de pruebas ###
**Granja WEB con NGINX**

La ejecución de ab ha sido la siguiente:
***ab -n 500 -c 200 http://10.211.55.28/f.php***

La ejecución de siege ha sido la siguiente:
***siege -b -t60S -v http://10.211.55.28/f.php***

En la siguiente tabla se muestran los resultados obtenidos tras realizar la batería de pruebas en la granja web 10 veces:
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/nginx.png)

### Batería de pruebas ###
**Granja WEB con HAPROXY**

La ejecución de ab ha sido la siguiente:

***ab -n 500 -c 200 http://10.211.55.28/f.php***

La ejecución de siege ha sido la siguiente:

***siege -b -t60S -v http://10.211.55.28/f.php***

En la siguiente tabla se muestran los resultados obtenidos tras realizar la batería de pruebas en la granja web 10 veces:
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/haproxy.png)


###Aquí se muestran los gráficos resultantes con la MEDIA para los atributos seleccionados (antes mencionados) a analizar: ###

*Para ab:*
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/barra1.png)

*Para SIEGE*
![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica4/barra2.png)

En resumen, como se puede observar en los gráficos, la granja web balanceada es capaz de realizar ***más peticiones por segundo y en un tiempo menor***.