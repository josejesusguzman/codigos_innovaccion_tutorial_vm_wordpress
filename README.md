
# Códigos del tutorial de Wordpress
Producción II

## Suplanta las palabras en mayusculas con tu info

**Este es para obtener las listas de ubicaciones de servidores que tiene Azure**

    az account list-locations

**Con este creas un grupo de recursos**
**Deja celtralus**

    az group create --name NOMBRE_GRUPO_DE_RECURSOS --location centralus

**Para crear una maquina virtual en tu grupo de recursos**

    az vm create \
        --resource-group NOMBRE_GRUPO_DE_RECURSOS \
        --location centralus \
        --name NOMBRE_MAQUINA_VIRTUAL \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys

**Copia aquí tu IP**

    52.176.42.14
    DIRECCIÓN IP PÚBLICA

**Con este comando obtienes todas las direcciones IP de todas las maquinas virtuales de tu grupo de recursos**

    az network public-ip list --resource-group NOMBRE_GRUPO_DE_RECURSOS --query [].ipAddress

**Con este comando abres el puerto 80 que es necesario para que se mustre la página**

    az vm open-port --port 80 --resource-group NOMBRE_GRUPO_DE_RECURSOS --name NOMBRE_MAQUINA_VIRTUAL

**Con este comando accedes a la máquina virtual**

    ssh azureuser@TU_DIRECCION_IP

**Con este comando compruebas que tu maquina funciona y hace moo**
sudo apt-get moo

**Aquí actualizas los paquetes de linux (Como el sistema operativo) e instalas LAMP**

    sudo apt update && sudo apt install lamp-server^

L -> Linux: El sistema operativo de la maquina virtual
A -> Apache: El servidor que permite visualizar páginas en una maquina virtual
M -> MySQL: El sistema de base de datos que usará Wordpress
P -> PHP: El lenguaje de programación que usa y en el que está constuido Wordpress

**Te da la versión de Apache y verifica si está bien instalado**

    apache2 -v

**Te da la versión de MySQL y verifica si está bien instalado**

    mysql -V

**Te da la versión de PHP y verifica si está bien instalado**

    php -v

**Instalación de usuarios de MySQL y determinación de la contraseña**

    sudo mysql_secure_installation

**Acceder a MySQL**

    sudo mysql -u root -p

**Obtener la lista de los usuarios de MySQL**

    SELECT user FROM mysql.user;

**Salir de MySQL**

    exit;

**Crear el archivo info.php que te permite ver la versión de PHP y probar si todo ha salido bien hasta ahora**

    sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'

**Para probar si todo esta bien y visualizar el archivo inho.php que está en tu maquina virtual**
http://TU_DIRECCION_IP/info.php

**Instalar Wordpress**

    sudo apt install wordpress

**Para crear un archivo con los comandos necesarios para que Wordpress use la Base de Datos**

    sudo sensible-editor wordpress.sql

**Creas una base de datos y le das permisos**
**Solo cambia la contraseña, lo demás dejalo igual**

    CREATE DATABASE wordpress;
    GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
    ON wordpress.*
    TO wordpress@localhost
    IDENTIFIED BY 'TU_CONTRASEÑA_MYSQL';

**Copias el contenido del archivo anterior a la configuración de mysql para que lo use tu página**

    cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf

**Por seguridad, eliminas el archivo con tu contraseña antes creado**

    sudo rm wordpress.sql

**Es para el archivo de configuración necesario para Wordpress**

    sudo sensible-editor /etc/wordpress/config-localhost.php

**Para darle permisos a Wordpress de Acceder a la base de datos**
**Solo cambia la contraseña, lo demás dejalo igual**

    <?php
    define('DB_NAME', 'wordpress');
    define('DB_USER', 'wordpress');
    define('DB_PASSWORD', 'TU_CONTRASEÑA_MYSQL');
    define('DB_HOST', 'localhost');
    define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
    ?>

**Es para hacer un enlace sibolico y que la página "esté" también en el puerto 80 que es donde se ve las páginas**

    sudo ln -s /usr/share/wordpress /var/www/html/wordpress

**Para enviar toda la configuración de Wordpress al lugar que le corresponde y peuda funcionar la página**

    sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php

**Conprueba que tu página de Wordpress funciona**
http://TU_DIRECCION_IP/wordpress

**Ir a la carpeta de Wordpress**

    cd /var/www/html/wordpress

**Muestra todo el contenido de la carpeta actual**

    ls

**Acceder al super usuario y tener todos los permisos**

    sudo su

**De aquí en adelante tienes que ir a GitHub, hacer un repositorio vacio y seguir los pasoa que ahí te dan**
https://github.com

**IMPORTANTE**
Agrega: 

    git add .

Antes de hacer: 

git commit -m "Initial commit"


Si tienes problemas, este es el link para reportar errores de azure. 
No aplican errores por mal uso de la plataforma o errores humanos
https://azure.microsoft.com/en-us/support/create-ticket/




























