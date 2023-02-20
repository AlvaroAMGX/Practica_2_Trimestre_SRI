# Guía instalación de sql 
Primero como todo lo que instalemos actualizaremos el servidor con este comando:
```bash
sudo apt update
```
Luego instalaremos mysql con este comando:
```bash
sudo apt install mysql-server
```
Nos pedira una contraseña para el usuario root,le puedes poner la que quieras pero recuerdala,luego iniciaremos el servicio con:
```bash
sudo systemctl start mysql
```
Por ultimo para verificar que esta en ejecución usaremos este comando:
```bash
sudo systemctl status mysql
```
Deberia verse como esta en la captura:
![sql1](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/capturas/sql1.png)
