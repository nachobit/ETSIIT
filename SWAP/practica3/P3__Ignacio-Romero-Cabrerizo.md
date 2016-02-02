#Practica 3

##Pasos iniciales:

NGINX

*Instalamos la herramienta nginx: apt-get install nginx*
- cd /tmp/
- wget http://nginx.org/keys/nginx_signing.key apt-key add /tmp/nginx_signing.key
- rm -f /tmp/nginx_signing.key

NOTA: Para poder corroborar que el balanceador funciona correctamente, modificamos el archivo index.html en ambas máquinas virtuales para identificar el balanceo de forma más sencilla.

**Pasos realizados en la máquina1:**

nano /var/www/index.html

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica3/us1.png)

**Pasos realizados en la máquina2:**

nano /var/www/index.html

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica3/us2.png)


**Pasos realizados en la máquina Balanceador:**

- Una vez instalado nginx procedemos a editar su archivo de configuración ubicado en: /etc/nginx/conf.d/default.conf

- Añadimos una lína upstream con las 2 máquinas junto con los parámetros necesarios de proxy como se muestra en la imagen.

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica3/balanceador.png)


**Comprobamos que el balanceo se realiza correctamente:**
![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica3/check.png)


HAPROXY

- Matamos el nginx: service nginx stop
- Instalamos haproxy: apt-get install haproxy
- De forma similar a nginx debemos editar el archivo de configuración por defecto de haproxy ubicado en: /etc/haproxy/haproxy.cfg
- Por último iniciamos haproxy una vez realizados los cambios: 
/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg
- Comprobamos que realiza el balanceo de carga de forma correcta.

![img](https://github.com/nachobit/ETSIIT/blob/master/swap1415/practica3/haproxy.png)







