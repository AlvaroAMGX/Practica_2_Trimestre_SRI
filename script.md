# Script que hara automatiza todo:
```bash
#!/bin/bash

# Pedir el nombre del usuario y del subdominio
read -p "Ingrese el nombre de usuario: " usuario
read -p "Ingrese el nombre del subdominio: " subdominio

# Crear el usuario del sistema y su directorio correspondiente para alojamiento web y 
# se crea un usuario para acceso a ftp, ssh y smtp
useradd -m -d /var/www/$subdominio $usuario

	#BIND
	# Defino la dirección IP
	ip="10.4.0.133"
	# Añade la zona al archivo named.conf.local
	echo "zone \"$subdominio\" {
	    type master;
	    file \"/etc/bind/db.$subdominio\";
	};" >> cat /etc/bind/named.conf.local

	# Crea el archivo de zona
	sudo cp /etc/bind/db.empty /etc/bind/db.$subdominio
	sudo chown bind:bind /etc/bind/db.$subdominio

	# A\u00f1ade los registros de resoluci\u00f3n directa e inversa al archivo de zona
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

#Crear una base de datos y un usuario con todos los permisos
mysql -e "CREATE DATABASE $usuario; CREATE USER '$usuario'@'localhost' IDENTIFIED BY 'password'; GRANT ALL PRIVILEGES ON $usuario.* TO '$usuario'@'localhost'; FLUSH PRIVILEGES;"

#Habilitar la ejecuci\u00f3n de aplicaciones Python con el servidor web
a2enmod wsgi
```
