# Tarea4_SXE

***1. Utiliza la imagen de Ubuntu , tag 22 y apoyandote en esta guía sigue sus instrucciones para instalar LAMP en dicho contenedor.***

  ***Primero tenemos que bajarnos la imagen de ubuntu con el tag***

  ```
sudo docker pull ubuntu:22.04
```

***Ahora procederemos a crear lamp***

```
 sudo docker container create -i -t  -p  8080:80 --name pw ubuntu:22.04

 sudo docker container start --attach -i  pw

```

***Instalamos apache***

```
 apt install -y apache2 apache2-utils
```

***Instalamos mariadb***

```
apt install -y mariadb-server mariadb-client

service mariadb start         #iniciamos el servicio
```

***Instalamos php***

```
apt install -y php php-mysql libapache2-mod-php
```

![image](https://github.com/user-attachments/assets/39a8744a-9599-4921-98a4-73c532437b8e)

***Ahora desde el navegador entramos a la información***

```
127.0.0.1/info.php
```

![image](https://github.com/user-attachments/assets/94127f37-aac2-4fc7-b0ca-a5e7d3985d13)


***2. Utiliza esta guía para instalar wordpress en el contenedor.***

***Primero tenemos que instalar las dependencias***

```
sudo apt install ghostscript \
                 libapache2-mod-php \
                 mysql-server \
                 php \
                 php-bcmath \
                 php-curl \
                 php-imagick \
                 php-intl \
                 php-json \
                 php-mbstring \
                 php-mysql \
                 php-xml \
                 php-zip

```

***Ahora creamos la estructura y descargamos wordpress***

```
sudo mkdir -p /srv/www
sudo chown www-data: /srv/www
curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www
```

***Ahora creamos el archivo conf de wordpress***

```
<VirtualHost *:80>
    DocumentRoot /srv/www/wordpress
    <Directory /srv/www/wordpress>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted
    </Directory>
    <Directory /srv/www/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
```

***3. Comprobemos si funciona wordpress***

***Primero tenemos que reiniciar apache***

```
service apache2 reload
```

***Ahora ejecutamos estos dos comando***

```
sudo a2ensite wordpress

sudo a2enmod rewrite

```

***Volvemos a reiniciar apache***

```
service apache2 reload
```

***Ahora entramos en el navegador y comprobamos si funciona wordpress***

```
http://127.0.0.1/wp-admin/setup-config.php
```

 ![image](https://github.com/user-attachments/assets/d6748c8c-bd7b-476c-b849-f18dc67b0413)
