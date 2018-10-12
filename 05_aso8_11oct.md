# Quinta semana

## TEMA 2 INSTALACIONES RED / LOCALES
### LUNES 
**Servidor TFTP Ubuntu Server** - http://www.developandsys.es/servidor-tfpt-ubuntu/
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
9. Reseteo y comprobación de todos los servicios. Creacion regla en firewall para peticiones tftp
````
sudo systemctl restart isc-dhcp-server
sudo systemctl restart tftpd-hpa
// comprobación de los servicios
sudo systemctl status isc-dhcp-server
sudo systemctl status tftpd-hpa
sudo ufw allow tftp
````

## JUEVES
**Resolución del examen**
***
1. 
a. Un dhcp autoritativo es aquel servicio principal dentro de una red de asignaciones. Se utiliza para asignar automáticamente IPs sobre clientes o DHCPs secundarios de forma automática
b. El archivo de configuración es /etc/dhcp/dhcpd.conf. Para poder asignar una dirección ip se asocia la dirección a una dirección MAC mediante el siguiente código
````
sudo nano /etc/dhcp/dhcpd.conf
host nombre_equipo{
hardware ethernet AA:AA:AA:AA:AA:AA
fixed-address 10.0.0.3
}
````
2.
a. Para poder montar discos en Ubuntu existen dos posibilidades: 
- montaje temporal utilizando el comando mount: la restricción de este método es que cuando la máquina se apaga el montaje deja de efectivo
- montaje definitivo utilizando el fichero /etc/fstab
b. En el fichero /etc/fstab se lee cada vez que la máquina se inicia por lo que los montajes siempre serán realizados. En este fichero encontramos: elemento_a_montar punto_montaje sistema_ficheros opciones dumpl backup. El comando para poder saber el UUID de un disco es blkid -o UUID -e /dev/sdb
3. 
a. Para poder saber todos los raid montados en el sistema se utiliza el comando mdadm --datail --scan. Para poder mostrar el detalle de un dispositivo en concreto se utiliza el comando mdadm --detail /dev/md1
b. Los raid utilizan discos dinámicos porque son aquellos que permiten que su estructura interna cambie sin tener que formatearlos. La diferencia con un básico es que este puede contener un sistema operativo ya que los bloques siempres osn los mismos
4.
a. Para hacer funcionar el servicio WDS es obligatorio el servicio WDS (pxe y tftp) y DHCP. Como optativos están el DNS y AD
b. Se necesitan 2xml para poder automatizar las instalaciones. El primer xml automatiza la parte del arranque y el segundo automatiza la instalación de la imagen
5. 
a. El fichero /etc/inetd.conf se utiliza para configurar el funcionamiento de los servicios que realizan peticiones por puertos específicos
b. El comando muestra: puerto_peticion datos_pasar protocolo funcionamiento usuarios_privilegios comando (opciones del comando)


### PRÁCTICAS A ENTREGAR

Realizar una aplicación que simule el funcionamiento de una calculadora:
1. Instalación desatendida de una imagen generada por MDT
- https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732280%28v%3dws.10%29
- https://docs.microsoft.com/es-es/windows/deployment/windows-adk-scenarios-for-it-pros
2. Instalación de una imagen linux en onfraestructura WDS (Syslinux)
3. Instalación y funcionamiento de un servidor DHCOP ubuntu
4. Montaje, error y recuperación de RAIDs en Windows (diskpart) y Ubunto (mdadm)