# Script que automatiza todo:
## Creacion de usurario y directorio correspondiente para el alojamiento web
Este script te pedira el nombre,el subdominio y la ip para configuraciones de despues y creara el usuario con su directorio,recordar que cuando creamos el usuario si lo hemos instalado y configurado correctatmente se crearan los usuarios ftp y ssh automaticamente.  
```bash
	#!/bin/bash

	# Pedir el nombre del usuario,del subdominio y la IP del cliente
	read -p "Ingrese el nombre de usuario: " usuario
	read -p "Ingrese el nombre del subdominio: " subdominio
	read -p "Ingrese la IP del cliente: " ip

	# Crear el usuario del sistema y su directorio correspondiente para alojamiento web y 
	# se crea un usuario para acceso a ftp, ssh y smtp
	useradd -m -d /var/www/$subdominio $usuario
```
## Creación del host virtual
Esta parte del script creara el archivo del sitio que hemos creado y habilitara el sitio para que se pueda acceder
```bash
	#Creación del archivo de configuración del usuario y luego creación del virtual host
	sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/$nombre.conf
				echo "<VirtualHost *:80>
				    ServerAdmin admin@example.com
				    ServerName $nombre.com
				    ServerAlias www.$nombre.com
				    DocumentRoot /var/www/$nombre
				    ErrorLog ${APACHE_LOG_DIR}/error.log
				    CustomLog ${APACHE_LOG_DIR}/access.log combined
				</VirtualHost>" >> /etc/apache2/sites-available/$nombre.conf
	#Habilitar los virtual hosts
	sudo a2ensite $nombre.conf
```
## DNS
Aqui tenemos la parte de nuestro script encargada del DNS que nos generara la zona directa e inversa de nuestro subdominio
```bash
	#BIND
	# Añade la zona al archivo named.conf.local
	echo "zone \"$subdominio\" {
	    type master;
	    file \"/etc/bind/db.$subdominio\";
	};" >> cat /etc/bind/named.conf.local

	# Crea el archivo de zona
	sudo cp /etc/bind/db.empty /etc/bind/db.$subdominio
	sudo chown bind:bind /etc/bind/db.$subdominio

	# Añade los registros de resolución directa e inversa al archivo de zona
	echo "\$TTL 86400
	@       IN      SOA     $subdominio.      admin.$subdominio. (
		                2023021801      ; serial
		                3600            ; refresh
		                1800            ; retry
		                604800          ; expire
		                86400 )         ; minimum

		IN      NS      $subdominio.

	$subdominio.       IN      A       $ip" >> cat /etc/bind/db.$subdominio

	echo "$ip       IN      PTR     $subdominio." >> cat /etc/bind/db.10

	#Reinicia el servicio BIND
	sudo systemctl restart bind9
```
## Creación de la base de datos
Esta parte del script creara un usuario con la contraseña password,tambien creara su base de datos y le dara los privilegios
```bash
	#Crear una base de datos y un usuario con todos los permisos
	mysql -e "CREATE DATABASE $usuario; CREATE USER '$usuario'@'localhost' IDENTIFIED BY 'password'; 
	GRANT ALL PRIVILEGES ON $usuario.* TO '$usuario'@'localhost'; FLUSH PRIVILEGES;"
```
## Habilitar Python para que puedas ejecutar aplicaciones 
Primero deberemos instalar el modulo wsgi con este comando:
```bash
	sudo apt-get install libapache2-mod-wsgi
```
Esta parte del script habilitara el modulo para ejecutar aplicaciones aplicaciones de python
```bash
	#Habilitar la ejecución de aplicaciones Python con el servidor web
	a2enmod wsgi
```
Tambien hice un script que lo deshabilita por si fuera necesario:
```bash
	#Deshabilitar la ejecución de aplicaciones Python con el servidor web
	sudo a2dismod wsgi
```
## Script completo
Aqui dejo el script completo añadi por ultimo un menu para poder escoger la opción que quiera el usuario:
```bash
#!/bin/bash
function crear_usuario {
# Pedir el nombre del usuario,del subdominio y la IP del cliente
	read -p "Ingrese el nombre de usuario: " usuario
	read -p "Ingrese el nombre del subdominio: " subdominio
	read -p "Ingrese la IP del cliente: " ip
}

function crear_virtualhost {
# Pedir el nombre del usuario,del subdominio y la IP del cliente
	read -p "Ingrese el nombre de usuario: " usuario
	read -p "Ingrese el nombre del subdominio: " subdominio
	read -p "Ingrese la IP del cliente: " ip
#Creación del archivo de configuración del usuario y luego creación del virtual host
	sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/$nombre.conf
				echo "<VirtualHost *:80>
				    ServerAdmin admin@example.com
				    ServerName $nombre.com
				    ServerAlias www.$nombre.com
				    DocumentRoot /var/www/$nombre
				    ErrorLog ${APACHE_LOG_DIR}/error.log
				    CustomLog ${APACHE_LOG_DIR}/access.log combined
				</VirtualHost>" >> /etc/apache2/sites-available/$nombre.conf
#Habilitar los virtual hosts
	sudo a2ensite $nombre.conf
}

function configurar_dns {
# Pedir el nombre del usuario,del subdominio y la IP del cliente
	read -p "Ingrese el nombre de usuario: " usuario
	read -p "Ingrese el nombre del subdominio: " subdominio
	read -p "Ingrese la IP del cliente: " ip
# Añade la zona al archivo named.conf.local
	echo "zone \"$subdominio\" {
	    type master;
	    file \"/etc/bind/db.$subdominio\";
	};" >> cat /etc/bind/named.conf.local

# Crea el archivo de zona
	sudo cp /etc/bind/db.empty /etc/bind/db.$subdominio
	sudo chown bind:bind /etc/bind/db.$subdominio

# Añade los registros de resolución directa e inversa al archivo de zona
	echo "\$TTL 86400
	@       IN      SOA     $subdominio.      admin.$subdominio. (
		                2023021801      ; serial
		                3600            ; refresh
		                1800            ; retry
		                604800          ; expire
		                86400 )         ; minimum

		IN      NS      $subdominio.

	$subdominio.       IN      A       $ip" >> cat /etc/bind/db.$subdominio

	echo "$ip       IN      PTR     $subdominio." >> cat /etc/bind/db.10

#Reinicia el servicio BIND
	sudo systemctl restart bind9
}

function crear_bd {
# Pedir el nombre del usuario,del subdominio y la IP del cliente
	read -p "Ingrese el nombre de usuario: " usuario
	read -p "Ingrese el nombre del subdominio: " subdominio
	read -p "Ingrese la IP del cliente: " ip
#Crear una base de datos y un usuario con todos los permisos
	mysql -e "CREATE DATABASE $usuario; CREATE USER '$usuario'@'localhost' IDENTIFIED BY 'password'; 
	GRANT ALL PRIVILEGES ON $usuario.* TO '$usuario'@'localhost'; FLUSH PRIVILEGES;"
}

function habilitar_wsgi {
	a2enmod wsgi
}

function deshabilitar_wsgi {
	sudo a2dismod wsgi
}

function menu 
	{
		echo "Buenos dias ¿que desea hacer hoy?"
		echo "1. Crear usuario en Apache"
		echo "2. Crea el virtual host"
		echo "3. Configurar el servidor DNS"
		echo "4. Crear base de datos"
		echo "5. Habilitar ejecución de aplicaciones con Python"
		echo "6. Deshabilitar ejecución de aplicaciones con Python"
		echo "7. Salir"
		echo "Dime tu opcion"
		read opc
		case $opc in
			1)crear_usuario;;
			2)crear_virtualhsot;;
			3)configurar_dns;;
			4)crear_bd;;
			5)habilitar_wsgi;;
			6)deshabilitar_wsgi;;
			7)exit;;
			*)echo "La opción escogida es incorrecta";sleep 3;clear;menu;;
		esac
	}
menu
``` 
