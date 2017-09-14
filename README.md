# DockerMoodle32

Configuraciones necesarias para iniciar una instancia de docker con moodle 3.2

# Requerimientos

Debe tener instalado docker y docker-compose ademas de tener conocimientos minimos sobre 
estos.

# Dependencias

Postgres 9.5
PHP 5.5

# Antes de construir:

Si tiene los suficientes conocimientos puede editar a conveniencia lo que se ha presentado en este repositorio y es bienvenido a hacerlo

El contenedor web se encuentra en dockerHttpd, al igual que la carpeta moodle, puede reemplazar esta ultima por una propia si la desea.

La idea es que se comparta la carpeta de desarrollo local de moodle con la de el contenedor de moodle, por ende
usted debe modificar el archivo docker-compose.yml para que la carpeta de origen quede configurada con su ruta especifica.

Ejemplo:


    volumes:
      - /home/lucho/WebApps/moodle:/var/www/html/moodle


Esta es la unica configuración necesaria para poner en marcha el cotenedor.

Debe tener en cuenta que el demonio de docker debe estar ejecutando para que lo presente en este tutorial funcione, tipicamente este se inicia ejecutando el comando dockerd como root

Por defecto y por razones de seguridad los comandos relacionados con docker solo estan accesibles por un usuario root, puede cambiar esto de la siguiente manera:
  - Cree el grupo docker si no existe (sudo groupadd docker)
  - Adicione el usuario actual o cualquier usuario a dicho grupo (sudo gpasswd -a $USER docker)

# Construir contenedor.

En consola, encontandose en el directorio DockerMoodle debe ejecutar como root "docker-compose build web"

 Al finalizar (después de en promedio 5 minutos) y si todo va bien podra ejecutar docker-compose up web, y ahora desde el local podra ver su nuevo sitio en localhost:8080/moodle
 
 # Configurando la coneccion a base de datos
 
 El servidor de base de datos es postgres, y la configuración deberá ser la siguiente :
 
 database host: db
 databse name: docker
 database user:docker
 database password : docker
 port: 5432
 
# Terminando la configuración.

Desde la consola de el contenedor web una vez terminado el build y comenzado el levantamiento se debe cambiar el dueño y el grupo de la carpeta /var/www/html/moodle por www-data:www-data y permisos 777 para poder editar desde el ordenador.

Desde el contenedor ejecutar (ej para entrar al bash del contenedor "docker exec -i -t dockermoodle_web_1 /bin/bash")
chmod -R 777 /var/www/html/moodle
chown -R www-data:www-data /var/www/html/moodle

Y en teoria con esto deberia ser suficiente.

# Recordar
El direcotrio de ejemplo en este caso /home/lucho/WebApps/moodle queda compartido con /var/www/html/moodle de el container es decir, son el mismo y los cambios aplican en ambas direcciones.




