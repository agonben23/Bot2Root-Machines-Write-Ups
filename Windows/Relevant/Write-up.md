# Relevant

[Enlace a la máquina](https://tryhackme.com/room/relevant)

## Enumeration

En el escaneo aparece información sobre los puertos TCP :

- 80: Microsoft Internet Information Services (IIS) httpd 10.0
- 135
- 139
- 445 : Microsoft DS (SMB)
- 3389
- 49663
- 49667
- 49668

![](./images/2025-03-16_12-34.png)

![](./images/2025-03-16_12-54.png)

## Gain Access

Probamos a listar las unidades compartidas de SMB

![](./images/2025-03-16_13-13.png)

Tenemos una red de disco que parece sospechosa. Vamos a intentar entrar.

![](./images/2025-03-16_13-15.png)

Ni siquiera tiene contraseña así que ya tenemos acceso, así que tenemos abierta la posibilidad de subirle algún tipo exploit que nos ayude a entrar en el sistema. 

La forma más sencilla de obtener acceso podría ser una "shell reversa", así que vamos a generar un exploit con msfvenom que nos ayude a ese cometido.

![](./images/2025-03-16_13-28.png)

Cargamos el exploit

![](./images/2025-03-16_13-36.png)

Ponemos en escucha un netcat en el puerto que hayamos indicado en el exploit.

![](./images/2025-03-16_13-37.png)

Hacemos una petición curl a la dirección del ejecutable

![](./images/2025-03-16_13-42.png)

Ya tendríamos nuestra shell reversa con acceso al usuario del sistema.

![](./images/2025-03-16_13-42_1.png)

![](./images/2025-03-16_13-44.png)

## Escalate

Observando los privilegios del usuario vemos que tiene habilitado "SeImpersonatePrivilege" que permite impersonar un usuario una vez estás dentro del sistema. 

![](./images/2025-03-16_13-46.png)

Pero no están facil como abrir la shell como administrador, así quenecesitamos otro vector de ataque. 

Existe una vulnerabilidad en el servicio de Print Spoofer, vamos a probar por ahí.

![](./images/2025-03-17_14-10.png)

Cargamos el [ejecutable de Print Spoofer](https://github.com/dievus/printspoofer) por SMB.

![](./images/2025-03-16_13-52.png)

![](./images/2025-03-16_13-56.png)

Ejecutamos el archivo de forma que nos abra una powershell como administrador.

![](./images/2025-03-16_14-11.png)

![](./images/2025-03-16_14-17.png)