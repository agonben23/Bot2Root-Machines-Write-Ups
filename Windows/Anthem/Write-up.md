# Anthem

[Enlace a la máquina](https://tryhackme.com/room/anthem)

## Enumeration

En el escaneo aparece información sobre los puertos TCP :

- 80 : Microsoft HTTPAPI hhttd 2.0
- 3389 : Microsoft Terminal Services (RDP)

![](./images/2025-03-16_18-46.png)

![](./images/2025-03-16_18-48.png)

![](./images/2025-03-16_18-50.png)

Entramos por el puerto 80 en el navegador y nos encontramos un blog donde vemos un post escrito por el usuario del blog "Jane Doe". También aparece un correo de contacto y nos dicen que posiblemente el usuario de la máquina pueda tener uno con la misma estructura.

![](./images/2025-03-16_19-35.png)

Buscando en el robots.txt aparece un texto al principio que parece relevante.

![](./images/2025-03-16_19-35_1.png)

En el blog encontramos otro post con lo que parece un poema incompleto en inglés.

![](./images/2025-03-16_19-54.png)

Buscando en wikipedia encontramos el poema completo en el cual se menciona en el último verso que faltaba el nombre del poema "Solomon Grundy". Si atendemos a lo anterior la abreviación de Solomon Grundy es SG, lo cual encaja con el formato mencionado.

![](./images/2025-03-16_19-57.png)

## Gain Access

Como hemos visto anteriormente, el puerto 3389 está abierto así que podemos conectarnos por RDP.

![](./images/2025-03-16_20-09.png)

Probamos con el usuario SG y el texto del robots.txt y conseguimos entrar en la máquina.

![](./images/2025-03-16_20-09_1.png)

![](./images/2025-03-16_20-10.png)

![](./images/2025-03-16_20-10_1.png)

## Escalate

Examinamos el disco en busca de alguna pista y en una de las carpetas ocultas encontramos lo que parece un archivo de restauración en txt.

![](./images/2025-03-16_20-13.png)

Intentamos entrar pero no tenemos permisos, tendremos que intentar modificarlos.

![](./images/2025-03-16_20-14.png)

![](./images/2025-03-16_20-16.png)

Parece una contraseña, vamos a intentar probar a entrar a la Powershell como administrador.

![](./images/2025-03-16_20-17.png)

Efectivamente, era la contraseña de administrador.

![](./images/2025-03-16_20-21.png)

![](./images/2025-03-16_20-23.png)