# Guia de como instalar PHP 
Para instalar PHP en un sistema operativo linux primero deberemos asegurarnos de que todos este actualizado y en la ultima versión posible asi evitaremos que haya problemas por incompatibilidades

Actualizaremos el sistema operativo y los paquetes existentes ejecutando el siguiente comando en la línea de comandos:
```bash
sudo apt update && sudo apt upgrade
```
Instala PHP y los módulos necesarios que necesitaremos para alojar páginas web ejecutando el siguiente comando:
```bash
sudo apt install php libapache2-mod-php php-mysql
```
![php1](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/capturas/php1.png)
Este comando instalará PHP y los módulos necesarios para interactuar con la base de datos MySQL que instalaremos en el siguiente .

Verifica que PHP se haya instalado correctamente ejecutando el siguiente comando:
```bash
php -v
```
Este comando mostrará la versión de PHP instalada en el sistema.
![php1](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/capturas/php2.png)
Si tienes un servidor web Apache instalado, deberás reiniciarlo para que los cambios surtan efecto:
```bash
sudo systemctl restart apache2
```

