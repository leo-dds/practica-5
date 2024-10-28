# [practica-5](https://github.com/leo-dds/practica-5.git)
__1. Crear la estructura del proyecto__
sri@sri-VirtualBox:~$ mkdir bind9-docker
sri@sri-VirtualBox:~$ cd bind9-docker/
sri@sri-VirtualBox:~/bind9-docker$ mkdir -p named/etc/bind
sri@sri-VirtualBox:~/bind9-docker$ mkdir -p named/var/cache/bind
sri@sri-VirtualBox:~/bind9-docker$ mkdir -p named/var/lib/bind
sri@sri-VirtualBox:~/bind9-docker$ 
sri@sri-VirtualBox:~/bind9-docker$ mkdir -p named/var/log
sri@sri-VirtualBox:~/bind9-docker$ mkdir -p named/var/run
sri@sri-VirtualBox:~/bind9-docker$ touch docker-compose.yml

_2. Crear el archivo docker-compose.yml_
**nano docker-compose.yml**
Dentro del documento escribimos lo siquiente:
 
services:
  bind9:
    image: internetsystemsconsortium/bind9:9.18  # Imagen oficial de BIND9
    container_name: bind9-server                # Nombre del contenedor
    ports:
      - "53:53/tcp"                             # Exposición de puertos
      - "53:53/udp"
    volumes:
      - ./named/etc/bind:/etc/bind              # Montaje de configuraciones
      - ./named/var/cache/bind:/var/cache/bind
      - ./named/var/lib/bind:/var/lib/bind
      - ./named/var/log:/var/log/bind
    restart: unless-stopped                     # Reiniciar a menos que se detenga

_3. Crear archivos de configuración de BIND9_
sri@sri-VirtualBox:~/bind9-docker$ cd named/etc/bind 
sri@sri-VirtualBox:~/bind9-docker/named/etc/bind$ nano named.cong.options

Dentro del nano escribimos lo siguiente:
options {
    directory "/var/cache/bind";

    // Desactiva la recursión para que solo funcione como un servidor autoritativo
    recursion no;

    // Permite que cualquier dispositivo pueda consultar el servidor DNS
    allow-query { any; };
};

**Esto nos servira para configurar el DNS**


_4.Ejecutar el Contenedor._

**docker-compose up -d**
Starting bind9 ... done

