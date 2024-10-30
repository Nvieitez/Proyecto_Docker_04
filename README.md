# Proyecto_Docker_04
En este proyecto trataremos el uso de los archivos "Docker-Compose" y la instalación de PrestaShop através de los siguientes pasos:

    1. Configuración de un Docker-Compose
    2. Inicio de los contenedores
    3. Acceso a PrestaShop

## 1. Configuración de un Docker-Compose
Para crear un Docker-Compose primero debemos hacer un archivo .yml, en este caso le llamaremos "Docker-Compose.yml", dentro de este mismo introduciremos todos los ajustes necesarios para la base de datos de PrestaShop
    
    version: '3.8'

    services:
      db:
        image: mysql:5.7
        command: --default-authentication-plugin=mysql_native_password
        environment:
          MYSQL_ROOT_PASSWORD: rootpassword
          MYSQL_DATABASE: prestashop
          MYSQL_USER: prestashop
          MYSQL_PASSWORD: prestashop
        volumes:
          - db_data:/var/lib/mysql
    
      prestashop:
        image: prestashop/prestashop:latest
        ports:
          - "8080:80"
        environment:
          DB_SERVER: db
          DB_NAME: prestashop
          DB_USER: prestashop
          DB_PASSWORD: prestashop
        volumes:
          - prestashop_data:/var/www/html
        depends_on:
          - db
    
    volumes:
      db_data:
      prestashop_data:


## 2. Inicio de los contenedores
El .yml tiene todas las instrucciones necesarias para el funcionamiento e instalación de PrestaShop, por lo que solo hace falta iniciarlo desde docker con los siguientes comandos:

    sudo apt install docker-compose
    sudo docker-compose up -d

![Inicio del docker-Compose](/Images_Docker/01_Inicio_Docker.png)

## 3. Acceso a PrestaShop
Una vez se inicie el Docker-Compose y el contenedor, accediendo a http://localhost:8080 podremos entrar en nuestra página de PrestaShop

![Inicio del PrestaShop](/Images_Docker/02_Inicio_PrestaShop.png)

