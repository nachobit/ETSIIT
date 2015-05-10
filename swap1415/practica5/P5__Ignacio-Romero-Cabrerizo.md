#Practica 5#

## REPLICAR BASES DE DATOS MySQL (MAESTRO/ESCLAVO) ##

### Pasos iniciales: ###

- Para conseguir una copia de nuestra base de datos cuando ésta contiene gran cantidad de información y datos, vamos a hacer uso de **mysqldump**, configurando 2 máquinas como *Maestro-Esclavo*.

- En nuestro caso la máquina 1 será el maestro y la máquina 2 el esclavo.

- Para realizar las consultas accederemos a mysql de la siguiente forma:
***mysql -u root –p***

- En el caso de no tener una, comenzamos creando una base de datos "contactos" por ejemplo, en la máquina 1 y una tabla "datos" con 2 campos (nombre y teléfono):

	mysql> CREATE database contactos;
	mysql> use contactos;
	mysql> CREATE table datos(nombre varchar(100),tlf int);

- Procedemos a insertar una fila nueva:

	-mysql> INSERT INTO datos(nombre,tlf) VALUES ("pepe",95834987);

Como resultado obtendremos lo siguiente:
![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/maestro0.png)

###COPIA DE BASE DE DATOS###
- Antes de pasar a realizar el backup con mysqldump debemos bloquear las tablas para evitar que se acceda a la base de datos si ésta se estáactualizando en el servidor, para ello:

	-mysql> FLUSH tables WITH READ LOCK;

- Pasamos a realizar, ahora sí, la copia de nuestra base de datos:
***mysqldump contactos -u root -p > /root/contacto.sql***

- Desbloqueamos las tablas:

	-mysql> UNLOCK TABLES; 
	-mysql> quit

- En la **máquina 2** mediante el protocolo de transferencia SCP, obtenemos el archivo creado por mysqldump en la máquina 1:

***scp root@maquina1:/root/contacto.sql /root/***

- Debemos crear la base de datos en la **máquina 2** antes de realizar la restauración o copia desde el archivo sql creado:

	-mysql> CREATE database contactos;
	-mysql> quit

###CONFIGURACION MAESTRO/ESCLAVO PARTE 1###
##MAESTRO##

- En la **máquina 1** (Maestro) debemos realizar la siguiente modificación en el archivo de configuración **my.cnf**: 
***/etc/mysql/my.cnf***

* Comentar el parámetro de escucha de servidor:
![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/maestro1.png)

* Establecer el identificador del servidor (Maestro será el 1 y Esclavo será el 2) y el registro binario (contiene toda la información del registro de actualizaciones):
![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/maestro2.png)

* Guardar el archivo sobreescribiendo y reiniciar el servicio:
***/etc/init.d/mysql restart***

##ESCLAVO##
- En la **máquina 2** (Esclavo) debemos realizar la siguiente modificación en el archivo de configuración **my.cnf**: 
***/etc/mysql/my.cnf***
* Comentar el parámetro de escucha de servidor
* Establecer el identificador del servidor:
![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/esclavo1.png)

* Guardar el archivo sobreescribiendo y reiniciar el servicio:
***/etc/init.d/mysql restart***

###CONFIGURACION MAESTRO/ESCLAVO PARTE 2###
##MAESTRO##

* Si no hemos obtenido ningún error en la configuración del archivo **my.cnf** de ambas máquinas, pasamos a crear un usuario y darle permisos de acceso para la replicación de la base de datos:

	-mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
	-mysql> GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%' IDENTIFIED BY 'esclavo';
	-mysql> FLUSH PRIVILEGES;
	-mysql> FLUSH TABLES;
	-mysql> FLUSH TABLES WITH READ LOCK;
	-mysql> SHOW MASTER STATUS;

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/maestro3.png)

La última sentencia nos permite obtener los datos de la base de datos a replicar para usarlos en la configuración del esclavo.

##ESCLAVO##

- Pasamos los datos del maestro al esclavo:

	-mysql> CHANGE MASTER TO MASTER_HOST='IP_MAESTRO', 
	MASTER_USER='esclavo', MASTER_PASSWORD='esclavo', 
	MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=501, MASTER_PORT=3306;

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/esclavo2.png)

- Finalmente arrancamos el esclavo:

	-mysql> START SLAVE;

- En el **Maestro** activamos de nuevo las tablas bloqueadas:

	-mysql> UNLOCK TABLES;

- Para comprobar que el esclavo no se ha creado con errores y que todo funciona correctamente, ejectucamos la siguiente orden:

	-mysql> SHOW SLAVE STATUS\G

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/esclavo3.png)

y verificamos que el valor de la variable *Seconds_Behind_Master* es 0.


Para acabar, insertamos una nueva fila en nuestra tabla "contactos" de la máquina *Maestro* para corroborar que los cambios se realizan por igual en nuestra máquina *Esclavo*:

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica5/final.png)
