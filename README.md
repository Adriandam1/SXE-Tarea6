# SXE-Tarea6

Utiliza docker para poner en marcha Prestashop según esta [imagen](https://hub.docker.com/r/prestashop/prestashop/).

Crear un repositorio en github y enlazarlo aquí.

Describe el proceso en un documento Readme. Utiliza capturas para demostrar el funcionamiento en el navegador.

Se valorará:

El uso de docker-compose. 
Claridad en la explicación
<!--
## 1. Descargar la imagen "Prestashop" y comprobar que está en tu equipo.
```bash
docker pull prestashop/prestashop
docker images
```
![presta1](https://github.com/user-attachments/assets/54b1ecec-d529-46c1-b1da-ba36ae44f976)
-->
## 1. Crear la carpeta con el archivo docker-compose.
```bash
#Creamos una carpeta donde vamos a almacenar el docker compose
mkdir compose_prestashop
```

## 2. Configuramos nuestro archivo docker-compose.
```bash
nano compose_prestashop/docker-compose.yml
```
En mi caso:
```bash
# Configuracion servicio mysql para prestashop
version: '3.8'  # Especifica la versión de Docker Compose

services:
  db:
    image: mariadb:10.11.2
    ports:
      - "3307:3306"
    volumes:
      - db_data_prestashop:/var/lib/mysql
    restart: no
    environment:
      MYSQL_ROOT_PASSWORD: admin
      MYSQL_DATABASE: prestashop
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin

  # Configuracion prestashop
  prestashop:
    depends_on:
      - db
    image: prestashop/prestashop:latest
    ports:
      - "8800:80"
    restart: no
    environment:
      PS_DEV_MODE: 0
      PS_HOST_MODE: 0
      PS_DEMO_MODE: 0
      DB_SERVER: db
      DB_USER: admin
      DB_PASSWD: admin
      DB_PREFIX: ps_
      DB_NAME: prestashop
      PS_LANGUAGE: en
      PS_SHOP_NAME: mi_super_tienda
      PS_DOMAIN: "localhost:8800"
    networks:
      - prestashop_network

volumes:
  db_data_prestashop:

networks:
  prestashop_network:

```
Imagen del archivo(conectado por ssh por el CMD de Windows):

![presta2](https://github.com/user-attachments/assets/f484ba4c-828e-45f9-8683-3e335cf1cd20)


## 3. Arrancar Prestashop:
```bash
sudo docker-compose up -d
```

![presta3](https://github.com/user-attachments/assets/a4ef536b-b9a1-439e-9566-2d2f37a35c08)

## 4. Acceder a Prestashop:
Utilizando nuestra ip y el puerto que hemos elegido:
```bash
http://192.168.1.131:8800/
```
![presta4](https://github.com/user-attachments/assets/429fd755-e16c-4c00-be27-8c83db0d306e)


### Introducimos nuestro credenciales:
<!-- Para el ejemplo la contraseña es ejemplo123 -->
![presta5](https://github.com/user-attachments/assets/aed04d9e-4180-49a6-bf4f-50dd8d13bbc4)


### Configuramos la conexión de la base de datos con nuestros credenciales, el puerto ponemos el por defecto:

![prestarreglado1](https://github.com/user-attachments/assets/ec7f5b04-0de2-4257-a113-0ccfc85566f9)


### Se instala

![pretsaaaaaaaaaaaaa](https://github.com/user-attachments/assets/44893a06-f8f3-4599-b85f-28e216929d0d)


### Queda correcto:

![ptressssssss222222222222222](https://github.com/user-attachments/assets/6ed9b6e9-b07e-4bca-8467-196f4715db76)

### Comprobamos la tienda:

![prestatienda](https://github.com/user-attachments/assets/938f07e9-57de-424c-a8ce-9dc54f67ac6f)





### Eliminar la carpeta install y renombrar la carpeta admin dentro del contenedor del prestashop:
<!--
docker exec -it <nombre_o_id_del_contenedor_prestashop> rm -rf /var/www/html/install
docker exec -it <nombre_o_id_del_contenedor_prestashop> mv /var/www/html/admin /var/www/html/admin
-->
```bash
docker exec -it compose_prestashop-prestashop-1 rm -rf /var/www/html/install
docker exec -it compose_prestashop-prestashop-1 mv /var/www/html/admin /var/www/html/admin123
```
Podriamos acceder con nuestras credenciales a: 
http://192.168.1.131:8800/admin123

![prestaAdmin](https://github.com/user-attachments/assets/5e8f51aa-ec15-45e3-ab4a-9845b3f5a9ee)

### Vemos la vista de admin:

![prestaAdmin2](https://github.com/user-attachments/assets/c46d9782-8016-458a-b31f-d80a84dc49e2)
















