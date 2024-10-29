# SXE-Tarea6

Utiliza docker para poner en marcha Prestashop según esta [imagen](https://hub.docker.com/r/prestashop/prestashop/).

Crear un repositorio en github y enlazarlo aquí.

Describe el proceso en un documento Readme. Utiliza capturas para demostrar el funcionamiento en el navegador.

Se valorará:

El uso de docker-compose. 
Claridad en la explicación

## 1. Descargar la imagen "Prestashop" y comprobar que está en tu equipo.
```bash
docker pull prestashop/prestashop
docker images
```
![presta1](https://github.com/user-attachments/assets/54b1ecec-d529-46c1-b1da-ba36ae44f976)

## 2. Crear la carpeta con el archivo docker-compose.
```bash
#Creamos una carpeta donde vamos a almacenar el docker compose
mkdir compose_prestashop
```

## 3. Configuramos nuestro archivo docker-compose.
```bash
nano compose_prestashop/docker-compose.yml
```
En mi caso:
```bash
#Configuracion servicio mysql para prestashop
services:
  db:
    image: mariadb:10.11.2
    volumes:
    - db_data_prestashop:/var/lib/mysql
    restart: no
    environment:
      MYSQL_ROOT_PASSWORD: admin
      MYSQL_DATABASE: prestashop
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin

#Configuracion prestashop
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

![presta2](https://github.com/user-attachments/assets/8faded6d-cf1f-41ed-a113-6432763bcef5)

## 4. Arrancar Prestashop:
```bash
sudo docker-compose up -d
```

![presta3](https://github.com/user-attachments/assets/a4ef536b-b9a1-439e-9566-2d2f37a35c08)

## 5. Acceder a Prestasgop:
Utilizando nuestra ip y el puerto que hemos elegido:
```bash
http://192.168.1.131:8800/
```
![presta4](https://github.com/user-attachments/assets/429fd755-e16c-4c00-be27-8c83db0d306e)









