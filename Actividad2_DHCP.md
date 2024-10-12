#  Servidor DHCP en Debian

## Índice

- [Servidor DHCP en Debian](#servidor-dhcp-en-debian)
  - [Índice](#índice)
    - [Realizando la instalación y configuración de un servidor DHCP en Debian, junto con la configuración de dos clientes, uno con Windows y otro con Ubuntu, en la misma subred. Configurando el servidor para que asigne automáticamente direcciones IP y parámetros de red a los clientes. Verificando que los clientes reciban correctamente la configuración y tengan conectividad con la red e Internet, y documentando todo el proceso y resultados obtenidos con las capturas necesarias:](#realizando-la-instalación-y-configuración-de-un-servidor-dhcp-en-debian-junto-con-la-configuración-de-dos-clientes-uno-con-windows-y-otro-con-ubuntu-en-la-misma-subred-configurando-el-servidor-para-que-asigne-automáticamente-direcciones-ip-y-parámetros-de-red-a-los-clientes-verificando-que-los-clientes-reciban-correctamente-la-configuración-y-tengan-conectividad-con-la-red-e-internet-y-documentando-todo-el-proceso-y-resultados-obtenidos-con-las-capturas-necesarias)
  - [El diagrama :](#el-diagrama-)
  - [Preparación del entorno:](#preparación-del-entorno)
    - [Instalación :](#instalación-)
    - [configuración de la red](#configuración-de-la-red)
    - [Comprobamos si el servidor Debian navega por internet](#comprobamos-si-el-servidor-debian-navega-por-internet)
  - [Instalación del servidor DHCP en Debian](#instalación-del-servidor-dhcp-en-debian)
  - [Configuración del servidor DHCP: Rango de IPs, puerta de enlace, DNS y reservas](#configuración-del-servidor-dhcp-rango-de-ips-puerta-de-enlace-dns-y-reservas)
  - [Configuración de los clientes DHCP: Windows y Linux](#configuración-de-los-clientes-dhcp-windows-y-linux)
    - [Configuramos el cliente Windows como cliente DHCP :](#configuramos-el-cliente-windows-como-cliente-dhcp-)
    - [Configuramos el cliente Ubuntu como cliente DHCP :](#configuramos-el-cliente-ubuntu-como-cliente-dhcp-)
    - [comprobamos que todo está bien :](#comprobamos-que-todo-está-bien-)
  - [Verificación de conectividad y acceso a internet en los equipos](#verificación-de-conectividad-y-acceso-a-internet-en-los-equipos)
    - [Conectividad entre los clientes:](#conectividad-entre-los-clientes)
    - [Acceco a internet:](#acceco-a-internet)
    - [Conectividad con el router :](#conectividad-con-el-router-)
  - [Monitoreo de logs y actividad del servidor DHCP con journalctl](#monitoreo-de-logs-y-actividad-del-servidor-dhcp-con-journalctl)
    - [Explicacion :](#explicacion-)
---

### Realizando la instalación y configuración de un servidor DHCP en Debian, junto con la configuración de dos clientes, uno con Windows y otro con Ubuntu, en la misma subred. Configurando el servidor para que asigne automáticamente direcciones IP y parámetros de red a los clientes. Verificando que los clientes reciban correctamente la configuración y tengan conectividad con la red e Internet, y documentando todo el proceso y resultados obtenidos con las capturas necesarias:
--- 
## El diagrama :
   
   ![awgf](./images/Captura%20de%20pantalla%202024-10-07%20110921.jpg)

 ## Preparación del entorno:
   
   ### Instalación :
   > 1. La máquina virtual del **rooter Pfsence** `Pfsense_Hafsa`:

   ![jsdgh](./images/1.jpg)
   
   > 2. La máquina virtual del **cliente Windows** `W_Hafsa` :
   
   ![uh](./images/2.jpg)
   
   > 3. La máquina virtual del **cliente Ubuntu** `U_Hafsa`:
   
   ![sekkuh](./images/3.jpg)
   
   > 4. La máquina virtual del **servidor Debian** `D_Hafsa`:
   
   ![seukrh](./images/4.jpg)
   
   ### configuración de la red
   
   > **Router**

La máquina tiene dos tarjetas de red una conectada con internet usando **Adaptador puente** , la segunda conectada con **red interna** que se llama **SRI215** para ser como **puerta d'enlace** para los clientes y el servidor para poder dar internet a las demás máquinas :
 Para la ip de la red LAN le damos: **10.0.215.1**, es **el gateway** con **mascara de 24 bits**, luego la interfaz wan la configuramos con **DHCP** :

   ![jsdgh](./images/5.jpg)
   
 > **W_Hafsa**

   La maquina virtual de windows esta en la misma **red interna SRI215**, al principio le damos ip estatica: **10.0.215.7** , y como **gateway la ip del router** :

   ![jsdgh](./images/6.jpg)

   > **D_Hafsa**

   El servidor tambien esta en la misma **red interna SRI215**, deberiamos darle la ip estatica fija :**10.0.215.2** :
   ![jsdgh](./images/7.jpg)

   > **U_Hafsa**

   el cliente ubuntu tambien en la misma red interna **SRI215**, en el inicio le dimos la ip estatica: **10.0.215.9**:

   ![jsdgh](./images/10.jpg)

   > **Deshabilitar DHCP en el enrutador para que el servidor sea el único !**

   ![jsdgh](./images/GetImage.png)



### Comprobamos si el servidor Debian navega por internet
Para comprobar que el servidor navega por internet hacemos :
1. ping a **8.8.8.8**:
   
![jsdgh](./images/8.jpg)

2. ping a **www.google.es**:

![jsdgh](./images/9.jpg)

## Instalación del servidor DHCP en Debian

`apt-get install isc-dhcp-server`:

![jsdgh](./images/11.jpg)

## Configuración del servidor DHCP: Rango de IPs, puerta de enlace, DNS y reservas
1. Añadir el nombre de la interfaz corresondiente `enp0s3` en el fichero`/etc/default/isc-dhcp-server` y ponemos `INTERFACES='enp0s3'`:
   
   ![jsdgh](./images/14.jpg)

2. Hacemos una copia de seguridad del fichero de la onfiguracion:

   ![jsdgh](./images/17.jpg)

3. Cambiamos el fichero con nuestra configuracion :

   En el fichero `/etc/dhcp/dhcpd.conf` en el partado que empieza con `A slightly diffrent configuration for an internal subnet ` ponemos :

   > Direcciones IP en el rango 10.0.215.3 – 10.0.215.100 
   
         ¡Ponemos un rango de ips que empieza con 3 porque la ip 1 es del router y 2 es del servidor! 

   > La máscara `255.255.255.0`

   > Puerta de enlace : `10.0.215.1`

   > DNS : `8.8.8.8`

   > El sufijo DNS `SRI215.local` 

   >  El tiempo de alquiler por defecto será de 15 días para todos los 
   > equipos =`1296000 s `
   > Nunca será superior a 30 días= `2592000 s ` 
   > Nunca será inferior a 1 semana = `604800 s `

   ![jsdgh](./images/25.jpg)

   > La reserve del cliente > Ubuntu :`10.0.215.60`:

   ![jsdgh](./images/19.jpg)

4. reiniciar el serviciio y verificar que eestá activo y en ejecución :
   
   . Reiniciar :
![jsdgh](./images/20.jpg)

   . La verificacion :
![jsdgh](./images/21.jpg)




## Configuración de los clientes DHCP: Windows y Linux

   ### Configuramos el cliente Windows como cliente DHCP :
   ![jsdgh](./images/12.jpg)

   ### Configuramos el cliente Ubuntu como cliente DHCP :
   ![jsdgh](./images/13.jpg)

   ### comprobamos que todo está bien :
   > En Ubuntu :
      
         Podemos ver que como cliente del servidor DHCP Debian el cliente tiene como puerta d'enlace la 1 :

   ![jsdgh](./images/24.jpg)

         como Nombre del dominio tiene SRI215.local:

   ![jsdgh](./images/26.jpg)

         El DNS viene en Ubuntu por defecto:

   ![jsdgh](./images/27.jpg)

         La mac :

   ![jsdgh](./images/28.jpg)

   >  windows :
   
         En el cliente Windows toda la configuracion esta clara con el comando `IPCONFIG /ALL`:

   ![jsdgh](./images/29.jpg)



1. Comprobamos que las ips han sido asignadas dentro del servidor en el fichero : 
`cat /var/lib/dhcp/dhcpd.leases`:
![jsdgh](./images/30.jpg)

## Verificación de conectividad y acceso a internet en los equipos

### Conectividad entre los clientes:
1. de Ubuntu a Windows :
   ![jsdgh](./images/31.jpg)

2. de windows a ubuntu :

   ![jsdgh](./images/32.jpg)

### Acceco a internet:

   1. Ubuntu:
   ![jsdgh](./images/33.jpg)

 2. Windows :
   ![jsdgh](./images/34.jpg)

### Conectividad con el router :

1. Windows:
   ![jsdgh](./images/35.jpg)

   1. Ubuntu :

   ![jsdgh](./images/36.jpg)

## Monitoreo de logs y actividad del servidor DHCP con journalctl
### Explicacion :

El funcionamiento del servidor **DHCP** en Debian con **isc-dhcp-server** se basa en la gestión automática de direcciones IP mediante un ciclo de cuatro pasos: descubrimiento, oferta, solicitud y confirmación. El servidor asigna IPs, máscara de subred, puerta de enlace y DNS a los clientes, además de gestionar las renovaciones de leases. Toda esta actividad queda registrada en los logs del sistema, y con **journalctl** (`journalctl -u isc-dhcp-server`), podemos monitorizar solicitudes, asignaciones y errores. Esto nos permite verificar que el servidor opera correctamente y que las configuraciones de red se aplican sin problemas.

![jsdgh](./images/37.jpg)

> Para filtrar por el tiempo ejecutamos en el servidor :

`sudo journalctl -u isc-dhcp-server --since "2024-10-10 12:00" --until "2024-10-10 13:00"`


