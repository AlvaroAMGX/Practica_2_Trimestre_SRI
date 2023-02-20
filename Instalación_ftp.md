# Guia de instalación de un servidor FTP con certificado TLS
Por seguridad, es recomendable configurar el acceso FTP mediante TLS, ya que esto encriptará la conexión entre 
el cliente y el servidor y evitará que las credenciales y los archivos transmitidos puedan ser interceptados por terceros.

Para instalar primero actualizaremos el sistema operativo haciendo un:
```bash
sudo apt-get update
```
Luego instalaremos el servidor vsftp que es de los más comunes y sencillos de configurar:
```bash
sudo apt-get install vsftpd
```
## Generar certificado TLS
Una de las cosas más importantes para que la conexión sea segura es el certificado TLS para hacerlo usaremos un comando que nos generara un cartificado autofirmado que para uso interno es seguro:
```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.pem
```
Ahora nos meteremos en la configuración del servidor y añaderemos unas lineas para que los clienten puedan conectarse:
```bash
sudo nano /etc/vsftpd.conf
--------------------------
#Añadiremos estas lineas,si estan ya escritas las modificaremos para que sean iguales a estas
ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO
rsa_cert_file=/etc/ssl/private/vsftpd.pem
```
Por ultimo reiniciaremos el servicio vsftpd 
```bash
sudo systemctl restart vsftpd
```
