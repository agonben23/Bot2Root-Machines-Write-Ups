# Retro

[Enlace a la máquina](https://tryhackme.com/room/retro)

## Enumeration

En el escaneo aparece información sobre los puertos TCP :

- 80 : Microsoft IIS (Internet Information Service) 10.0
- 3389 : Microsoft Terminal Services (RDP)

![](./images/2025-03-14_18-18.png)

![](./images/2025-03-14_18-18_1.png)

![](./images/2025-03-14_18-19.png)

Realizamos un fuzzing de directorio al servidor Web alojado en el puerto 80

![](./images/2025-03-14_18-32.png)

Encontramos el path a una posible página principal

![](./images/2025-03-14_18-36.png)

Efectivamente, es la página principal de la web. Encontramos un usuario que está posteando en el blog, podría ayudarnos más adelante.

![](./images/2025-03-14_18-36_1.png)

En uno de los post una nota dejada por dicho usuario para no olvidarla, también podría sernos de utilidad.

![](./images/2025-03-14_19-22.png)

## Explotación de la vulnerabilidad

### Gain Access

Con las credenciales encontradas entramos por RDP al ordenador

![](./images/2025-03-14_18-43.png)

![](./images/2025-03-14_18-44.png)

![](./images/2025-03-14_18-44_1.png)

### Escalate

Para escalar privilegios haremos uso de un exploit que explota la vulnerabilidad CVE-2017-0213

![](./images/2025-03-14_18-47.png)

Descomprimimos el archivo

![](./images/2025-03-14_18-51.png)

Levantamos en un servidor http con el modelo de python http.server

![](./images/2025-03-14_18-51_1.png)

Descargamos el archivo

![](./images/2025-03-14_19-03.png)

![](./images/2025-03-14_19-06.png)

Lo ejecutamos y ya tendremos acceso como administrador

![](./images/2025-03-14_19-07.png)

![](./images/2025-03-14_19-10.png)