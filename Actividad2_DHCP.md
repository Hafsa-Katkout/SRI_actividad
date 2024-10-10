#  Actividad
### Realizando la instalación y configuración de un servidor DHCP en Debian, junto con la configuración de dos clientes, uno con Windows y otro con Ubuntu, en la misma subred. Configurando el servidor para que asigne automáticamente direcciones IP y parámetros de red a los clientes. Verificando que los clientes reciban correctamente la configuración y tengan conectividad con la red e Internet, y documentando todo el proceso y resultados obtenidos con las capturas necesarias:
--- 
1. ## El diagrama :
   
   ![awgf](./images/Captura%20de%20pantalla%202024-10-07%20110921.jpg)

2. ## Instalación y configuración de la red. 
   1. ### la máquina virtual del rooter Pfsence:
   ![jsdgh](./images/1.jpg)
   ![uh](./images/2.jpg)
   ![sekkuh](./images/3.jpg)
   ![seukrh](./images/4.jpg)

   la red :
   ![jsdgh](./images/5.jpg)
   ![jsdgh](./images/6.jpg)
   ![jsdgh](./images/7.jpg)
   ![jsdgh](./images/10.jpg)
   dhcp no  en router :
   ![jsdgh](./images/GetImage.png)



debian navega por internet :

![jsdgh](./images/8.jpg)
![jsdgh](./images/9.jpg)

instalation of dhcp :
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

