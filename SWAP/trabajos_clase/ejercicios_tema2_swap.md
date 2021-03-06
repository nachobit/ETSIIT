#EJERCICIOS TEMA 2#

##Ejercicio T2.1: Calcular la disponibilidad del sistema descrito en edgeblog.net si tenemos dos réplicas de cada elemento salvo para el centro de datos (en total 3 elementos en cada subsistema).

As = Ac(n-1) + ((1 – Ac(n-1)) * Acn)

Disponibilidad(mínimo n-1) = Dn + nD(n-1)(1-D)


##Ejercicio T2.2: Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. Como ejemplo, examina PM2: https://github.com/Unitech/pm2 que sirve para administrar clústeres de NodeJS.

* StrongNode (Strongloop): paquete de soporte de Node.js. Depuración avanzada, agrupación y soporte a registros privados npm.

* Sails.js: facilita la construcción a nivel empresarial de aplicaciones Node.js. Emula el patrón MVC dando soporte a requisitos actuales como APIs basadas en datos con una arquitectura orientada a servicios escalables.

* Koa: framework de desarrollo web rápida con un gran control de errores.

* Locomotive: framework que integra motores de bases de datos fácilmente. 

* webControl CMS: framework para sitios web y entornos de alta disponibilidad con elevados volúmenes de tráfico y concurrencia

* Squid: servidor proxy para web con caché. Mejora el rendimiento de las conexiones guardando en caché peticiones recurrentes a servidores web/DNS y acelera el acceso a un servidor web determinado.


##Ejercicio T2.3: ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor? Buscar herramientas y aprender a usarlas.

Mediante el uso de software específico capaz de analizar y medir el uso de los componentes del servidor en este caso.

* ApacheBench (ab): la utilidad más usada. Programa mediante línea de comandos para medir el rendimiento de servidores web http.

**Ejemplo de uso:**

ab -n 100 -c 10 http://www.google.com/

* Siege: utilidad de testeo y benchmarking de carga http.
Ejemplo de uso:

siege -t 60s -c 100 -b -q http://localhost:8888/loadTesting/test

*n: cantidad de peticiones a enviar	-c: cantidad conexiones concurrentes*


##Ejercicio T2.4: En este ejercicio debemos buscar diferentes tipos de productos: (1) Buscar ejemplos de balanceadores software y hardware (productos comerciales). (2) Buscar productos comerciales para servidores de aplicaciones. (3) Buscar productos comerciales para servidores de almacenamiento.

**1.Balanceadores:**
- Barracuda (prevención intrusiones)
- Coyote Point (solución comercial económica)
- CISCO (referente en la red)
- ZEN Load (software) - NGINX (software) – HAProxy(software)

**2.Servidores de aplicaciones:**
- IBM WebSphere
- BEA WbLogic
- Sun ONE
- Oracle IAS
- Borland AppServer

**3.Servidores de almacenamiento:**
- Servidores PowerEdge DELL
- Servidores HP (3PAR,MSA, BURA)
