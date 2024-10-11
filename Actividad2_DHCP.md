#  Actividad
### Realizando la instalación y configuración de un servidor DHCP en Debian, junto con la configuración de dos clientes, uno con Windows y otro con Ubuntu, en la misma subred. Configurando el servidor para que asigne automáticamente direcciones IP y parámetros de red a los clientes. Verificando que los clientes reciban correctamente la configuración y tengan conectividad con la red e Internet, y documentando todo el proceso y resultados obtenidos con las capturas necesarias:
--- 
## El diagrama :
   
   ![awgf](./images/Captura%20de%20pantalla%202024-10-07%20110921.jpg)

 ## Preparación del entorno:
   
   ### Instalación :
   1. La máquina virtual del rooter Pfsence `Pfsense_Hafsa`:
   ![jsdgh](./images/1.jpg)
   2. La máquina virtual del cliente Windows `W_Hafsa` :
   ![uh](./images/2.jpg)
   3. La máquina virtual del cliente Ubuntu `U_Hafsa`:
   ![sekkuh](./images/3.jpg)
   4. La máquina virtual del servidor Debian `D_Hafsa`:
   ![seukrh](./images/4.jpg)
   ### configuración de la red
   
   > **Router**

   La máquina tiene dos tarjetas de red una conectada con internet usando Adaptador puente , la segunda conectada con red interna que se llama SRI215 para ser como puerta d'enlace para los clientes y el servidor para poder dar internet a las demás máquinas :
      Para la ip de la red LAN le damos: **10.0.215.1**, es **el gateway** con mascara de 24 bits, luego la interfaz wan la configuramos con DHCP :
   ![jsdgh](./images/5.jpg)
   > **W_Hafsa**

   La maquina virtual de windows esta en la misma red interna SRI215, al principio le damos ip estatica: 10.0.215.7 , y como gateway la ip del router :
   ![jsdgh](./images/6.jpg)

   > **D_Hafsa**

el servidor tambien esta en la misma red interna SRI215, deberiamos darle la ip estatica fija :10.0.215.2 :
   ![jsdgh](./images/7.jpg)
   > **U_Hafsa**

   el cliente ubuntu tambien en la misma red interna SRI215, en el inicio le dimos la ip estatica: 10.0.215.9:

   ![jsdgh](./images/10.jpg)
   > **Deshabilitar DHCP en el enrutador para que el servidor sea el único !**

   ![jsdgh](./images/GetImage.png)



### Comprobamos si el servidor Debian navega por internet

![jsdgh](./images/8.jpg)
![jsdgh](./images/9.jpg)

## Instalación del servidor DHCP en Debian
![jsdgh](./images/11.jpg)

configuracion de dhcp:

![jsdgh](./images/14.jpg)
copia de seguridad :
![jsdgh](./images/15.jpg)

configuracion 1 dhcp :
![jsdgh](./images/16.jpg)

copia de seguridad:
![jsdgh](./images/17.jpg)


configuracion  rango start by 3 because the debian have the 2:
![jsdgh](./images/25.jpg)

ubuntu reservacion :
![jsdgh](./images/19.jpg)

dhcp configuracion restart :
![jsdgh](./images/20.jpg)

dhcp satuts:
![jsdgh](./images/21.jpg)










ex2 :

equipo windows as dhhcp :
![jsdgh](./images/12.jpg)

. equipo ubuntu as dhcp :
![jsdgh](./images/13.jpg)

gateway

![jsdgh](./images/24.jpg)

nombre del dominio :
![jsdgh](./images/26.jpg)
dns por defecto :

![jsdgh](./images/27.jpg)

mac :

![jsdgh](./images/28.jpg)

. windows :
![jsdgh](./images/29.jpg)



ver el fichero rn debian :
cat /var/lib/dhcp/dhcpd.leases:
![jsdgh](./images/30.jpg)


conection de ubuntu a windows :

![jsdgh](./images/31.jpg)

de windows a ubuntu :

![jsdgh](./images/32.jpg)

ping from ubuntu a internet :
![jsdgh](./images/33.jpg)

ping from windows a internet :
![jsdgh](./images/34.jpg)

ping from windows to the rooter:
![jsdgh](./images/35.jpg)

ping from ubuntu to rooter :

![jsdgh](./images/36.jpg)


ha registrado en los logs del sistema por la herramienta 
Journalctl:

![jsdgh](./images/37.jpg)


sudo journalctl -u isc-dhcp-server --since "2024-10-10 12:00" --until "2024-10-10 13:00"



Preparación del entorno: Instalación y configuración de la red
Instalación del servidor DHCP en Debian
Configuración del servidor DHCP: Rango de IPs, puerta de enlace, DNS y reservas
Configuración de los clientes DHCP: Windows y Linux
Verificación de conectividad y acceso a internet en los equipos
Monitoreo de logs y actividad del servidor DHCP con journalctl
Documentación del proceso en GitHub y entrega en Teams

