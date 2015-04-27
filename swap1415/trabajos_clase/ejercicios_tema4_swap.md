#EJERCICIOS TEMA 4#

##Ejercicio T4.1: Buscar información sobre cuánto costaría en la actualidad un mainframe. Comparar precio y potencia entre esa máquina y una granja web de unas prestaciones similares.

En la actualidad se utilizan cada vez más los servicios de web, mail y cloud (nube), servicios que el usuario exige que sean rápidos, fiables e ininterrumpidos.
Los mainframe poseen súper procesadores con un gran poder de cálculo pero requieren una gran inversión y no prestan las características de los clústeres y la computación paralela (brindan múltiples peticiones a los usuarios en servicios web sin retardo y de una forma eficiente) ni su reducido coste y alto desempeño.

Las granjas web aún así, no llegan a tener los niveles de confiabilidad de los mainframes.

##Ejercicio T4.2: Buscar información sobre precio y características de balanceadores hardware específicos. Compara las prestaciones que ofrecen unos y otros.


| Balanceador                      | Precio  | Características                                     |                                                       |
|----------------------------------|---------|-----------------------------------------------------|-------------------------------------------------------|
| Cisco ACE (4710)                 | 10.000€ | Detección servicios/máquinas defectuosos            | Sticky Groups: (asociación usuario-servidor concreto) |
|                                  |         | Mejora la escalabilidad (hasta 4Gbps)               | Aceleración                                           |
| F5 Networks Big-IP 2000          | 15.000€  | Local Traffic Manager (ataques DDoS)                | Aceleración SSL                                       |
|                                  |         | Eliminación de puntos únicos de fallo               | Rastrea niveles dinámicos de servidores en grupo      |
| Nortel Alteon Load Balancer 5412 | 16.000€ | Aislamiento de fallos (vADC por aplicación)         | AppWall Web Application Firewall (WAF)                |
|                                  |         | Monitoreo en tiempo real - gestión de SLA proactiva | FastView Web Performance Optimization (WPO)           |


##Ejercicio T4.3: Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2



##Ejercicio T4.4: Instala y configura en una máquina virtual el balanceador ZenLoadBalancer. Compara con la dificultad de la instalación y configuración usando nginx o haproxy (práctica 3).


##Ejercicio T4.5: Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?



##Ejercicio T4.6: Buscar información sobre los bloques de IP para los distintos países o continentes. Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario.



##Ejercicio T4.7: Buscar información sobre métodos y herramientas para implementar GSLB.
