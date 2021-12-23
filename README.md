# WordPress 

WordPress es basicamente un gestor de contenidos escrito en PHP. Es por eso, que esta herramienta se suele ver en modulos como Desarrollo de Páginas WEB. Es decir, con WordPress, un usuario X puede acceder a una página de "Login", autentificarse y acceder a la página principal de Adminitración desde la que podemos modificar todo tipo de contenido que publiquemos. Como es deducible, si el usuario que accede es un "Messi" de PHP, podrá modificar todos los plugins, temas, páginas y contenidos a su antojo. 

A continuación, explicaré como montar un WordPress desde cero y con el menor numero de inconvenientes.


# Preparación del entorno

Como es hábitual, vamos a utilizar Docker compose ya que, mediante volumenes podemos hacer que nuestras páginas e inclusive nuestra base de datos con usuarios, perdure. 

Tan solo tenemos que montar un Docker-compose.yaml con los datos adientes. 

#### Instalamos Docker y Docker Compose

Para instalar Docker, ejecutaremos lo siguiente en nuestra terminal: 

        sudo apt install docker.io

Una vez instalado Docker, instalamos docker compose:

           sudo apt install curl
           sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
           sudo chmod +x /usr/local/bin/docker-compose
           
Comprobamos que Docker Compose esté instalado:

           docker-compose --version
           

#### Archivo docker-compose.yaml

A continuación describiremos la siguiente estructura:


Indented 4 spaces, like `<pre>` (Preformatted Text).

    <?php
        echo "Hello world!";
    ?>
    
     
