#Practica 2

##Pasos iniciales:

sudo passwd root (en ambas máquinas)
sudo chown nachorc:nachorc -R /var/www/


**Pasos realizados en la máquina2:**

rsync -avz -e ssh root@10.211.55.26:/var/www/ /var/www/ 

**Creamos clave para poder enlazar las 2 máquinas sin necesidad de contraseña:**

ssh-keygen -t dsa
Directorio creación: /root/.ssh/id_dsa

**Copiamos la clave a la máquina1:**

ssh-copy-id -i .ssh/id_dsa.pub root@10.211.55.26

**Nos conectamos por ssh (sin necesidad de contraseña) a la máquina1 desde la máquina2:**

ssh 10.211.55.26 -l root

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica2/ssh1.png)

**Estando conectados a la máquina1 desde la máquina2, comprobamos que se han copiado las claves en (/root/.ssh):**

root@ubuntu:~/.ssh# ls

authorized_keys

**Uso crontab con tarea: ejecute cada hora para manteneractualizado el contenido del directorio /var/www entre las dos máquinas (/etc/crontab):**

0 * * * * root rsync -avz -e ssh root@10.211.55.26:/var/www/ /var/www/