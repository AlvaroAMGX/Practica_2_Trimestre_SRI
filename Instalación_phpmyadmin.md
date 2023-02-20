# Guia de instalación de phpmyadmin
Primero antes que nada cuando vayamos a instalar cualquier cosa actualizaremos el sistema operativo con:
```bash
sudo apt update
```
Luego instalaremos el phpmyadmin con este comando :
```bash
sudo apt install phpmyadmin
```
Cuando lo instalemos nos preguntaran si queremos configurarlo le daremos que si y nos dira si queremos intalar la base de datos volveremos a confirmar:  
![phpmyadmin1](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/capturas/phpmyadmin1.png)

Luego nos pedira contraseña la introduciremos y cuando lo hagamos el proceso de instalación habra acabado y ya tendremos instalado phpmyadmin:  
![phpmyadmin2](https://github.com/AlvaroAMGX/Practica_2_Trimestre_SRI/blob/main/capturas/phpmyadmin2.png)  
Por ultimo reiniciaremos apache para poder acceder ahora a nuestro phpmyadmin:  
```bash
sudo systemctl restart apache2
```
Después de seguir estos pasos, phpMyAdmin estará instalado y disponible en tu servidor. Puedes acceder a él escribiendo http://localhost/phpmyadmin en tu navegador web y utilizando las credenciales de MySQL para iniciar sesión.
