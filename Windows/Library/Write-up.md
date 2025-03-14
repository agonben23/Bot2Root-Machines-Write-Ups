# Library

[Enlace a la máquina](https://tryhackme.com/room/bsidesgtlibrary)

## Escaneo con Nmap

En el escaneo aparece información sobre los puertos TCP :

- 22 : OpenSSH 7.2p2
- 80 : Apache httpd 2.4.18

![](./images/2025-03-14_15-23.png)

Entramos por el puerto 80 en el navegador y nos encontramos un blog. Donde vemos un post escrito por el usuario del blog "meliodas".

![](./images/2025-03-14_15-30_1.png)

## Identificación de la vulnerabilidad

Buscando posibles vulnerabilidades en los servicios encontrados encontramos [una vulnerabilidad](https://www.cvedetails.com/cve/CVE-2016-6210/) con un exploit publicado.

![](./images/2025-03-14_15-25.png)

![](./images/2025-03-14_17-10.png)

## Explotación de la vulnerabilidad

### Gain Access

Procedemos a explotar la vulnerabilidad, para ello buscamos en metasploit por el CVE de dicha vulnerabilidad.

Este exploit verifica si los usuarios introducidos en la lista existen en el servicio SSH. Vamos a probar con el usuario que encontramos antes en el blog.

![](./images/2025-03-14_15-26.png)

Abrimos las opciones e introducimos los datos necesarios.

![](./images/2025-03-14_15-27.png)

![](./images/2025-03-14_15-28.png)

![](./images/2025-03-14_15-28_1.png)

![](./images/2025-03-14_15-29.png)

Ejecutamos el exploit y observamos que el usuario "meliodas" existe.

![](./images/2025-03-14_15-29_1.png)

![](./images/2025-03-14_15-30.png)

Utilizamos la herramienta "hydra" para atacar con fuerza bruta al servicio SSH con dicho usuario y el diccionario de contraseñas [*rockyou.txt*](https://github.com/brannondorsey/naive-hashcat/releases).

![](./images/2025-03-14_15-34.png)

Obtenemos la contraseña, así que podemos entrar por SSH con : 

- usuario : meliodas
- contraseña : iloveyou1

![](./images/2025-03-14_15-34_1.png)