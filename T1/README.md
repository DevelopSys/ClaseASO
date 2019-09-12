
<a name="indice"></a>
## ASO - Administración de Sistemas Operativos
 - [Configuración e información del sistema](#tema1)
	 - Windows
		 - Información
		 - Roles y características
		 - DHCP
		 - WDS, MDT
		 - RAIDs
	 - Linux
		 - Información
		 - DHCP
		 - TFPT
		 - RAIDs

**Windows Server 2019**

- <a href="https://www.microsoft.com/es-es/cloud-platform/windows-server-pricing">Precio de licencias</a>
- <a href="https://docs.microsoft.com/es-es/windows-server/get-started-19/whats-new-19">Novedades WServer2019</a>
- <a href="https://social.technet.microsoft.com/wiki/contents/articles/15720.instalacion-y-configuracion-basica-de-windows-deployment-services-en-server-2012-es-es.aspx">Documentación oficial WDS</a>
- <a href="https://docs.microsoft.com/es-es/windows/deployment/deploy-windows-mdt/deploy-a-windows-10-image-using-mdt">Implementación por WDS + MDT</a>

**Ubuntu Server 18.04 LTS**



**Enlaces interesantes**

- https://www.geekboots.com/story/ntfs-vs-ext4-vs-fat32

==

### Windows

<a href="https://docs.microsoft.com/es-es/windows-server/manage/windows-admin-center/understand/what-is">WAS - Administración remota de equipos en una red</a>

<a href="- http://www.developandsys.es/informacion-del-sistema-wserver/">Información del sistema</a>

<a href="http://www.developandsys.es/dhcp-windows-server/">Instalación y configuración DHCP</a>

<a href="http://www.developandsys.es/servicio-implementacion-wds">Instalación y configuraciones WDS</a>

<a href="http://www.developandsys.es/mdt-imagenes-personalizadas/">Instalación y configuraciones MDT</a>

<a href=" http://www.developandsys.es/aseguramiento-la-informacion/">Instalación y configuración de RAIDS</a>





### Linux

<a href="http://www.developandsys.es/configuraciones-basicas-linux/">Configuraciones básicas</a>

<a href="http://www.developandsys.es/informacion-del-sistema-userver/">Información del sistema</a>

<a href="http://www.developandsys.es/dhcp-ubuntu-server/">Instalación y configuraciones DHCP</a>

<a href=" http://www.developandsys.es/aseguramiento-la-informacion/">Intsalación y configuración de RAIDS</a>

<a href="http://www.developandsys.es/servidor-tfpt-ubuntu/">Instalación y configuración TFTP</a>

****

**Prácticas a entregar**

1. Realiza el montaje de RAID 5 tanto en Windows como en Linux donde el raid original deberá tener 4 discos (dos reserva en Ubuntu). Las tareas que se deben realizar son
	- provocar fallo en uno de los discos y arreglarlo
	- hacer crecer el raid de 4 discos a 5 discos (en Ubuntu)
	- hacer decrecer el raid de 5 discos a 4 discos (en Ubuntu)
2. Realiza una instalación desatendida mediante WDS + MDT de una imagen que tenga al menos dos programas incluidos
3. Realiza las modificaciones necesarias en WDS para que se puedan hacer instalaciones de distribuciones Linux (necesitas utilizar SysLinux<a href="https://wiki.syslinux.org/wiki/index.php?title=WDSLINUX"></a>)
4. Instalaciones y configuraciones básicas de UbuntuServer subidas a la carpeta de Drive

Todas las prácticas se entregarán en formato pdf con capturas de pantalla mínimamente explicadas. La fecha de entrega de las prácticas será el **6 de octubre** en la carpeta de Drive