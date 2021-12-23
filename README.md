# WordPress 

WordPress es básicamente un gestor de contenidos escrito en PHP. Es por eso, que esta herramienta se suele ver en módulos como Desarrollo de Páginas WEB. Es decir, con WordPress, un usuario X puede acceder a una página de "Login", autentificarse y acceder a la página principal de Administración desde la que podemos modificar todo tipo de contenido que publiquemos. Como es deducible, si el usuario que accede es un "Messi" de PHP, podrá modificar todos los plugins, temas, páginas y contenidos a su antojo.


A continuación, explicaré como montar un WordPress desde cero y con el menor número de inconvenientes.



# Preparación del entorno

Como es habitual, vamos a utilizar Docker compose, ya que, mediante volúmenes podemos hacer que nuestras páginas e inclusive nuestra base de datos con usuarios, perdure.

Tan solo tenemos que montar un Docker-compose.yaml con los datos que correspondan. 

#### Instalamos Docker y Docker Compose

Para instalar Docker, ejecutaremos lo siguiente en nuestra terminal: 

        sudo apt install docker.io

Una vez instalado Docker, instalamos Docker Compose:

           sudo apt install curl
           sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
           sudo chmod +x /usr/local/bin/docker-compose
           
Comprobamos que Docker Compose esté instalado:

           docker-compose --version
           

#### Archivo docker-compose.yaml

A continuación describiremos la siguiente estructura:

        version: '3.1'

        services:

          wordpress:
            image: wordpress
            restart: always
            ports:
              - 8080:80
            environment:
              WORDPRESS_DB_HOST: db
              WORDPRESS_DB_USER: administrador
              WORDPRESS_DB_PASSWORD: my_secure_password
              WORDPRESS_DB_NAME: wordpress
            volumes:
              - wordpress:/var/www/html

          db:
            image: mysql:5.7
            restart: always
            environment:
              MYSQL_DATABASE: wordpress
              MYSQL_USER: administrador
              MYSQL_PASSWORD: my_secure_password
              MYSQL_RANDOM_ROOT_PASSWORD: '1'
            volumes:
              - db:/var/lib/mysql

        volumes:
          wordpress:
          db:


El archivo monta dos contendores, uno con la imagen de WordPress y otro con la imagen de MySQL. 
El primero contendor:

        wordpress:
            image: wordpress
            restart: always
            ports:
              - 8080:80
            environment:
              WORDPRESS_DB_HOST: db
              WORDPRESS_DB_USER: administrador
              WORDPRESS_DB_PASSWORD: my_secure_password
              WORDPRESS_DB_NAME: wordpress
            volumes:
              - wordpress:/var/www/html
              
La imagen es la de Wordpress, con el parámetro "restart", se reinicia siempre que apaguemos el contendor. "Ports" hace referencia a los puertos que usaremos. El 80 del contendor será el 8080 de nuestro Host. Esto lo aclaro, por si se está corriendo algún servicio en el puerto 8080, nos dará un error a la hora de montar el _"compose"_ lo suyo es para esos servicios antes de iniciar el compose o cambiar el puerto 8080 por otro, por ejemplo, el 2342.


Saldría un error de este tipo:

![imagen](https://user-images.githubusercontent.com/80277545/147271657-d4395bd8-5867-48fc-8c11-bf8996e787a6.png)


En "environment", se especifican los datos del contendor de MySQL, el nombre del contendor, el usuario, la contraseña y el nombre de la base de datos.

En "volumes", se especifica el volumen de Wordpres. ( Ver para más información: " https://dockertips.com/volumenes ")

El segundo contendor:

        db:
            image: mysql:5.7
            restart: always
            environment:
              MYSQL_DATABASE: wordpress
              MYSQL_USER: administrador
              MYSQL_PASSWORD: my_secure_password
              MYSQL_ROOT_PASSWORD: password_root
            volumes:
              - db:/var/lib/mysql
              
MYSQL_DATABSE, es el nombre de la base de datos que se crea al montar el compose. MYSQL_USER, es el usuario que vamos a crear para acceder a Wordpress. MYSQL_PASSWORD, es la contraseña de dicho usuario. MYSQL_ROOT_PASSWORD, es la contraseña que se establece para el usuario ROOT. 

# Montando el Docker-Compose

Una vez hemos descargado el archivo .yaml de este repositorio y hemos cambiado los datos de acceso por los necesarios, nos situamos donde tengamos el archivo montado y ejecutamos:

            sudo docker-compose up -d  (en caso de Linux)
            sudo docker compose up -d  (en caso de Windows)

![imagen](https://user-images.githubusercontent.com/80277545/147271420-ed919076-0d76-4a8f-88ac-2a32c3de7ce7.png)

(La opción -d es para que se ejecute en el background, lo puedes ejecutar con y sin ella)


Ahora que está montado, ejecutamos lo siguiente para ver que los dos contenedores están operativos. 

            sudo docker ps
            
 ![imagen](https://user-images.githubusercontent.com/80277545/147271899-c5b2fd3b-912a-4d46-8918-ee45bc2586fc.png)

Los dos contenedores están operativos.

# Iniciando WordPress

Si para montar el contendor hemos utilizado el puerto 80, bastará con poner en el navegador:

             http://localhost:8080
             
![imagen](https://user-images.githubusercontent.com/80277545/147272510-cfc0153c-8ecf-45b5-aa33-14cdfefdf61c.png)

Se nos abrirá el instalador de WordPres y tendremos que seleccionar nuestro idioma. Tendremos que rellenar la siguiente página de configuración:

![imagen](https://user-images.githubusercontent.com/80277545/147272643-2df98265-f282-44fd-a386-be37518f05ed.png)

En mi caso quedó tal que:

![imagen](https://user-images.githubusercontent.com/80277545/147272790-7b9490e2-59aa-4de4-ba94-91b610e761ca.png)

Nos saldrá lo siguiente:

![imagen](https://user-images.githubusercontent.com/80277545/147272857-821235ad-bbad-4343-b3f7-5e207cf2b3bb.png)

Iniciamos sesión:

![imagen](https://user-images.githubusercontent.com/80277545/147272933-f6f4e0ea-5fcf-4348-a465-19c4a0ede335.png)

Con esto ya tendriamos acceso a la página de administrador:

![imagen](https://user-images.githubusercontent.com/80277545/147273009-4918b595-3f40-4755-9634-bf2a01c3b915.png)

# Accediendo a archivos de configuración

Para acceder y modificar con profundidad WordPress, podemos acceder al contenedor de nombre "wordpress" con:

        docker exec -it entorno_wordpress_wordpress_1 /bin/bash
        
![imagen](https://user-images.githubusercontent.com/80277545/147274996-422d3193-9a12-40d8-ad58-97c173485933.png)

        

# Conclusión

Como conclusión, puedo decir que el hecho de saber usar WordPress, es algo que se requiere en las empresas. Ahora, con esta guía podremos poblarlo e intentar familiarizarnos.

Como siempre para cualquier aportación, no dudéis en contactarme en: z0s3r77@gmail.com

Gracias.






