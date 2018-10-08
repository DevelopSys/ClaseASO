# Quita semana

## TEMA 2 INSTALACIONES RED / LOCALES
### LUNES 
**Servidor TFTP Ubuntu Server**
***
1. Configuración de la tarjeta de red con una tajeta estática
````
sudo nano /etc/network/interfaces
auto enp0s3
iface enp0s3 inet auto
auto enp0s8
iface enp0s8 inet static
address 10.0.0.2
netmask 255.255.255.0
broadcast 10.0.0.255
gateway 10.0.0.253
````
2. Instalación de los paquetes correspondientes
''''
sudo apt-get install apache2 tftpd-hpa inetutils-inetd
''''
3. Configuración del demonio TFTP para que se ejecute automáticamente el servicio correpondiente
````
sudo nano /etc/default/tftpd-hpa
RUN_DAEMON="yes"
OPTIONS="-l -s /var/lib/tftpboot"
````
4. Configurar el servicio inet para que trate las peticiones de forma efectiva
````
sudo nano /etc/inetd.conf
tftp    dgram   udp    wait    root    /usr/sbin/in.tftpd /usr/sbin/in.tftpd -s /var/lib/tftpboot
# puerto tipoDato protocolo ejecucion usuarios comando
````
5. Agregar imagen de red al servidor a la carpeta correspondiente
````
sudo cp -fr /montaje/install/netboot/* /var/lib/tftpboot/
````
6. Agregar la imagen completa al servidor
````
sudo cp -fr /montaje/* /var/www/html/ubuntu/
````
7. Modificar el fichero de arranque y agregar la opción correspondiente
````
sudo nano /var/lib/tftpboot/pxelinux.cfg/
# agregar el kernel correspondiente
label linux
        kernel ubuntu-installer/amd64/linux
        append ks=http://192.168.10.2/ks.cfg vga=normal initrd=ubuntu-installer/amd64/initrd.gz
ramdisk_size=16432 root=/dev/rd/0 rw  --
````
8. Configurar dhcp para que pase pxelinux.0
````
allow booting;
allow bootp;
option option-128 code 128 = string;
option option-129 code 129 = text;
next-server 192.168.1.105;
filename "pxelinux.0";
````
