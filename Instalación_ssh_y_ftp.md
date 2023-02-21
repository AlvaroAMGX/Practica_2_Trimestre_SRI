# Guia de instalación de ssh y ftp
Para comenzar la instalación como siempre se recomienda haremos un:
```bash
sudo apt-get update
```
Luego instalaremos el servicio de openssh server con este comando:
```bash 
sudo apt-get install openssh-server
```
Ahora editaremos el archivo de configuración para activar el puerto 22 que es el pordefecto veremos que esta comentado solo tendremos que eliminar el #:
```bash 
sudo nano /etc/ssh/sshd_config
```
Eliminaremos esta almohadilla:  
![ssh1](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/capturas/ssh.png)  
Por ultimo reiniciaremos el servicio para que aplique las configuraciones y active el puerto
```bash
sudo systemctl restart ssh
```
Si cuando nos intentamos conectar tenemos problemas debemos ver si tenemos el firewall activado y si ese puerto esta permitido si no lo esta haremos este comando para permitir conexiones por ssh:
```bash
sudo ufw allow ssh
```
