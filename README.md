# moduloInicial

Documentación de instalación de Odoo con Docker Compose.

-Lo primero que hice fue crear un directorio al que llamé Odoo.

-En ese directorio creé 3 directorios:

  -Al primer directorio lo llamé config_odoo. En ese directorio creé un archivo de configuración que usaremos más tarde.

    -En odoo.conf añadimos una serie de opciones relacionadas con la máquina virtual Linux en la que estará Odoo. Ponemos las rutas donde queremos que se guarden los módulos o addons que hagamos, otra ruta para los datos, y otra ruta para el log. Además, añadimos una contraseña de administrador.

  -Al segundo directorio lo llamé dev-addons. En ese de momento no hacemos nada.

  -Al tercer directorio lo llamé log. Ahí tampoco hacemos nada.

-Por último, después de crear los 3 directorios, creé un archivo, docker-compose.yml

  -En este archivo es donde vamos a tener el código que Docker Compose va a interpretar para realizar la instalación. Entonces en este archivo le vamos a dar una serie de parámetros de instalación: La versión de Odoo y de Postgre que usaremos, el enlace entre ambos, el puerto donde tendremos Odoo, los volúmenes donde estarán los containers, los usos que le damos a los 3 directorios que creamos antes, etc.

-Después de eso tendremos que abrir powershell con permisos de administrador e irnos al directorio Odoo (el directorio de docker-compose.yml).

-Ejecutamos el comando "Docker Compose up" y Docker Compose realiza la instalación con los parametros que le dimos en el archivo yml.

-Abrimos Docker y vemos que ya nos sale el container. Lo desplegamos para ver los 2 containers que lleva debajo: El de Odoo y el de Postgre.

-Abrimos la consola del container de Odoo
