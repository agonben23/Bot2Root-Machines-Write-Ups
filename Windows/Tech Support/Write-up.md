# Tech Support

[Enlace a la máquina](https://tryhackme.com/room/techsupp0rt1)


## Enumeration

En el escaneo con NMAP aparece información sobre los puertos TCP :

- 22 : OpenSSH 7.2p2
- 80 : Apache hhttpd 2.4.18
- 139
- 445 : Microsoft DS (SMB)

![](./images/2025-03-15_14-50.png)

![](./images/2025-03-15_14-51.png)

![](./images/2025-03-15_14-51_1.png)

Usamos para ver las unidades SMB compartidas

![](./images/2025-03-15_16-34.png)

Vemos una unidad sospechosa llamada "websvr"

![](./images/2025-03-15_16-34_1.png)

Entramos en la unidad

![](./images/2025-03-15_16-38.png)

Encontramos credenciales de acceso

![](./images/2025-03-15_16-38_1.png)

![](./images/2025-03-15_16-51.png)

En el puerto 80, encontramos el login del CMS Subrion. Entramos las credenciales.

![](./images/2025-03-15_16-54.png)

![](./images/2025-03-15_16-55.png)

Buscamos en Metasploit algún exploit para esa versión de Subrion y encontramos uno que explota una vulnerabilidad relacionada con la subida de archivos.

![](./images/2025-03-15_16-57.png)

![](./images/2025-03-15_17-02.png)

Introducimos los datos 

![](./images/2025-03-15_17-02_1.png)

![](./images/2025-03-15_17-03.png)

![](./images/2025-03-15_17-03_1.png)

Y ejecutamos

![](./images/2025-03-15_17-03_2.png)

Tenemos acceso a una shell de meterpreter

![](./images/2025-03-15_18-44.png)

Ejecutamos una shell de bash dentro de la sesión y hacemos un upgrade de dicha shell usando python

![](./images/2025-03-15_18-56.png)

Buscando por la unidad encontramos la configuración de wordpress con una contraseña de acceso a la base de datos.

![](./images/2025-03-15_18-58.png)

Intentamos abrir una ventana de ssh con las credenciales encontradas.

![](./images/2025-03-15_18-58_1.png)

## Escalate

Vemos los comandos que puede correr sin necesidad de tener acceso como root.

![](./images/2025-03-15_18-59.png)

![](./images/2025-03-15_19-00.png)

