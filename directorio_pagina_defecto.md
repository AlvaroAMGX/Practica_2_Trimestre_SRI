# Crear un directorio de usuario con una página web por defecto
Crearemos un fichero de texto con el editor de tecto que prefiera,arriba tendremos que poner #!/bin/bash para que sea ejecutable y lo primeor que haremos sera pedir el nombre de usuario y el nombre del dominio:

```bash
# Pide al usuario que ingrese el nombre del usuario
echo "Ingrese el nombre de usuario:"
read username

# Pide al usuario que ingrese el nombre del sitio web
echo "Ingrese el nombre del sitio web:"
read sitename
```
Luego crearemos el usuario y el directorio para eñ sitio web al cual le cambiaremos el propietario por el usuario que acabamos de crear y le daremos permisos de todo:
```bash
# Crea el usuario
sudo useradd $username

# Crea el directorio para el sitio web
sudo mkdir /var/www/$sitename

# Asigna al usuario el directorio del sitio web
sudo chown $username:$username /var/www/$sitename

# Permite el acceso web al directorio
sudo chmod 755 /var/www/$sitename
```
Por ultimo crearemos un index para esa página web:
```bash
# Agrega una página de índice HTML para el sitio web
sudo echo "<html><body><h1>Bienvenido a $sitename!</h1></body></html>" > /var/www/$sitename/index.html
```
El archivo completo quedaria asi:

```bash
#!/bin/bash

# Pide al usuario que ingrese el nombre del usuario
echo "Ingrese el nombre de usuario:"
read username

# Crea el usuario
sudo useradd $username

# Pide al usuario que ingrese el nombre del sitio web
echo "Ingrese el nombre del sitio web:"
read sitename

# Crea el directorio para el sitio web
sudo mkdir /var/www/$sitename

# Asigna al usuario el directorio del sitio web
sudo chown $username:$username /var/www/$sitename

# Permite el acceso web al directorio
sudo chmod 755 /var/www/$sitename

# Agrega una página de índice HTML para el sitio web
sudo echo "<html><body><h1>Bienvenido a $sitename!</h1></body></html>" > /var/www/$sitename/index.html
```
