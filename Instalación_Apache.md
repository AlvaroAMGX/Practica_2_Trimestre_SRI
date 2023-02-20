# Guia de como instalar Apache para dar alojamiento a páginas web
Para instalar el servidor web Apache en un sistema operativo linux primero deberemos asegurarnos de que todos este actualizado y en la ultima versión posible asi evitaremos que haya problemas por incompatibilidades

Actualiza el sistema operativo y los paquetes existentes ejecutando el siguiente comando en la línea de comandos:
```bash
sudo apt update && sudo apt upgrade
```
Luego de esto instalaremos Apache ejecutando el siguiente comando:
```bash
sudo apt install apache2
```
Este comando instalará el servidor web Apache en el sistema como podemos ver en la captura.
![Apache1](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/capturas/apache1.png)
Puedes verifica que Apache se haya instalado correctamente ejecutando el siguiente comando:
```bash
sudo systemctl status apache2
```
Este comando mostrará el estado de Apache. Si Apache se ha instalado correctamente, debería mostrarse como "active" (activo) en color verde.

Si tienes un firewall habilitado, deberás abrir el puerto HTTP para permitir que los clientes se conecten a tu servidor web Apache. Ejecuta el siguiente comando para abrir el puerto HTTP:
```bash
sudo ufw allow 'Apache'
```

Puedes verificar que Apache esté funcionando correctamente abriendo un navegador web y navegando a 
http://tu-dominio.com. Si has instalado Apache en tu computadora local, puedes navegar a http://localhost 
o http://127.0.0.1. Deberías ver la página predeterminada de Apache que indica que Apache se ha instalado correctamente.
