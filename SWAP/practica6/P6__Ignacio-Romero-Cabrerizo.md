#Practica 6#

## DISCOS EN RAID ##

### Pasos iniciales: ###

- En este caso, se trata como sabemos de máquinas virtualizadas por lo que desde el software de virtualización (Parallels) debemos crear para la máquina 1, otros 2 discos duros para poder realizar el RAID (estando apagada la máquina 1).

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica6/discos.png)

- Una vez creados los discos adicionales procedemos a crear y configurar el RAID.


###CONFIGURACION DEL RAID###

- Tras arrancar la máquina 1 lo primero es instalar el software necesario para configurar el RAID, en este caso será mediante la utilidad **mdadm**.

	`sudo apt-get install mdadm`

- Procedemos a crear el RAID 1 a través de /dev/md0 e indicando el nº de dispositivos (2 en este caso) y la ubicación:

	`sudo mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc`

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica6/mdadm.png)

- Durante el proceso nos preguntará si deseamos continuar creando el array, contestamos y (yes).

- Damos formato al RAID:

	`sudo mkfs /dev/md0`

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica6/mkfs.png)

- Creamos el directorio donde se montará la unidad de RAID:

	`sudo mkdir /datos`

	`sudo mount /dev/md0 /datos`

- Comprobamos el estado del RAID:

	`sudo mdadm --detail /dev/md0`

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica6/res.png)

- Por último configuramos el sistema para que monte el RAID al arrancar el sistema mediante la edición del archivo **/etc/fstab**:

1. Obtenemos el UUID del RAID con blkid:

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica6/uuid.png)

2. Editamos el archivo /etc/fstab y añadimos el UUID anterior:

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica6/fstab.png)

3. Comprobamos que el RAID está correctamente montado y particionado:

![img](https://github.com/nachobit/ETSIIT/blob/master/SWAP/practica6/fdisk.png)
