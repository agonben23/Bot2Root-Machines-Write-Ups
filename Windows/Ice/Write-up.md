
# Ice

[Enlace a la máquina](https://tryhackme.com/room/ice)

# Escaneo con Nmap

En el escaneo preeliminar aparece información sobre los puertos TCP :

- 135
- 139
- 445
- 3389
- 5357
- 8000


![](./images/Pasted%20image%2020250222121413.png)

Haciendo un escaneo profundo de esos puertos obtenemos información relevante :

- En el puerto 3389 está corriendo un servicio RDP (Remote Desktop Protocol) para acceder a la máquina de forma remota
- En el puerto 8000 está corriendo un servicio HTTP, más concretamente el servicio de streaming icecast

- El nombre del equipo vulnerable es DARK-PC

![](./images/Pasted%20image%2020250222122135.png)

## Identificación de la vulnerabilidad

![](./images/Pasted%20image%2020250222123941.png)

## Explotación de la vulnerabilidad

### Gain Access

Buscamos el exploit relacionado con la vulnerabilidad en metasploit

![](./images/Pasted%20image%2020250222124220.png)

Introducimos los datos

![](./images/Pasted%20image%2020250222124735.png)

![](./images/Pasted%20image%2020250222124804.png)

![](./images/Pasted%20image%2020250222124842.png)

![](./images/Pasted%20image%2020250222124900.png)

![](./images/Pasted%20image%2020250222124931.png)

Ejecutamos el exploit

![](./images/Pasted%20image%2020250222125107.png)

Ya tendríamos acceso a la máquina. Ejecutamos ```get uid``` para obtener más información de la máquina

![](./images/Pasted%20image%2020250222125758.png)

### Escalate 

Ejecutamos un comando para ver que exploits nos pueden servir para escalar privilegios

![](./images/Pasted%20image%2020250222130052.png)

El primero de ellos nos puede valer pero vamos a necesitar primero poner en standby nuestra sesión para ello ejecutamos "background"

Podemos comprobar la lista de sesiones ejecutando "sessions"

![](./images/Pasted%20image%2020250222130252.png)

Vamos a usarlo para ello nos pide la id de sesión y la ip del equipo vulnerable

![](./images/Pasted%20image%2020250222130751.png)

Introducimos los datos

![](./images/Pasted%20image%2020250222130903.png)

Comprobamos que todo esté en orden

![](./images/Pasted%20image%2020250222131023.png)

Y ejecutamos

![](./images/Pasted%20image%2020250222131840.png)

Como podemos observar tenemos acceso a numerosos privilegios como "SeTakeOwnershipPrivilege", que nos permite tomar convertirnos en propietarios de archivos

![](./images/Pasted%20image%2020250222131942.png)

### Looting

Ejecutamos el comando ps para listar los procesos visibles para el usuario root

![](./images/Pasted%20image%2020250222132236.png)

Pivotamos al proceso del servicio de impresión con el fin de poder interactuar con el lsaas (servicio responsable de las políticas de seguridad del sistema) ya que tiene la misma arquitectura y los mismos permisos.

![](./images/Pasted%20image%2020250222133901.png)

Cargamos la herramienta "kiwi" que nos permite hacer un volcado de todas las contraseñas del sistema con el comando "creds_all"

![](./images/Pasted%20image%2020250222134059.png)

![](./images/Pasted%20image%2020250222134219.png)

## Post-explotation

Como tenemos las contraseñas y el servicio RDP está en funcionamiento podemos entrar al equipo a través de la interfaz visual como si fueramos el usuario Dark

![](./images/Pasted%20image%2020250222142825.png)

![](./images/Pasted%20image%2020250222143152.png)
