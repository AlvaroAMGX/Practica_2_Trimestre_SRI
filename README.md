# Practica 2 Trimestre SRI
## A realizar:
Se pide las instalación, configuración y puesta en marcha de un servidor que ofrezca servicio de alojamiento web configurable:

1.Se dará alojamiento a [páginas web](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/Instalación_Apache.md) tanto estáticas como dinámicas con “[php](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/Instalación_PHP.md) ”

2.Los clientes dispondrán de un [directorio de usuario con una página web por defecto](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/directorio_pagina_defecto.md). 

3.Además contarán con una base de datos [sql](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/instalación_sql.md) que podrán administrar con [phpmyadmin]()

4.Los clientes podrán acceder mediante [ftp]() para la administración de archivos configurando adecuadamente TLS

5.Se habilitará el acceso mediante ssh y sftp. 

- Se automatizará mediante el uso de scripts: 

  - La creación de usuarios y del directorio correspondiente para el alojamiento web 
  
  - Host virtual en apache

  - Creación de usuario del sistema para acceso a ftp, ssh, smtp, …

  - Se creará un subdominio en el servidor DNS con las resolución directa e inversa

  - Se creará una base de datos además de un usuario con todos los permisos sobre dicha base de datos (ALL PRIVILEGES)

  - Se habilitará la ejecución de aplicaciones Python con el servidor web
