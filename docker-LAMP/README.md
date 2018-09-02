# Desplegando la aplicación kapisolution en un entorno LAMP en docker
Integración del proyecto kapisolution en un entorno docker mediante docker-compose.yml

# Requirements
- Docker
- GIT

Abre un terminal y realiza la clonación del proyecto docker-LAMP.

Lo primero que necesitas antes de ejecutar el docker-compose.yml es crear una carpeta repo/ donde debes incluir el código de tu proyecto. En nuestro caso, el proyecto de autodefensa digital kapisolution.

Abre un terminal y accede a docker-LAMP. A continuación ejecuta los siguientes comandos:

- terminal: `docker-compose build`
    Esto creará una imagen docker en tu sistema. Puedes verla accediendo a un terminal y ejecutando:
        `sudo docker images`
- terminal: `docker-compose up -d`
    Mediante esta orden se levantarán dos contenedores (Apache-php7 y MySQL) a partir de la imagen creada anteriormente. Puedes verlos ejecutando en un terminal:
        `sudo docker ps`

Abre el navegador y accede a: `www.kapisolution.com`. Esta es la url definida en el archivo /etc/
Puedes añadir mas hosts virtuales in `etc/apache2/hosts.conf`.

# Base de datos
Recuerda incluir un archivo bd_test.sql que contiene un script del volcado actual de la base de datos. La sintaxis se indica en el archivo `etc/mysql/bd.sql` 

Si quieres modificar algún parámetro de la base de datos echa un vistazo al fichero `docker-compose.yml`. En caso de error de conexión a la base de datos, echa un vistazo al archivo backend/conexion.php. Este debe tener la siguiente sintaxis.

$con = @mysqli_connect('IPAddress_contenedor_docker_mysql:3306', 'root', '1234', 'db_test');
    if(!$con){
        echo "Error: " . mysqli_connect_error();
        exit(); 
}
