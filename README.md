**Description**  
This repository contains a collection of Docker configurations I've put together to meet my needs.

**Directory Structure**  

- **Apache**

    Apache based frameworks have a simple directory structure that can be used to easily deploy web applications using a volume on /data.

        Apache modules are not yet complete.

- **Nginx**

    Nginx based frameworks have a simple directory structure that can be used to easily deploy web applications using a volume on /data.

        /data
            /conf
                nginx-*.conf // included by nginx
                php-*.conf // included by php-fpm
            /http
                index.html // root web directory (index file is index.html or index.php)
            /logs
                nginx.log // nginx log file
                php-fpm.log // php-fpm log file
            /secure
                filename.ext // private files such as passwords or keys

**Instructions**  
Instructions will be here when I get around to writing them!

**Usage**  
The following commands can be used to deploy some of the services offered by the Docker containers in this repository.

- **Applications**

    - **Adminer**

            docker run --env=[VIRTUAL_HOST=adminer.example.com] --link=[mariadb:mariadb, postgresql:postgresql] --name="adminer" -d maxexcloo/adminer

    - **Koken**

            docker run --name="koken-data" maxexcloo/data
            docker run --env=[VIRTUAL_HOST=koken.example.com] --link=[mariadb:mariadb] --name="koken" --volumes-from=[koken-data] -it maxexcloo/koken

    - **phpMyAdmin**

            docker run --name="phpmyadmin" -d --link mariadb:mariadb --env=VIRTUAL_HOST=phpmyadmin.example.com maxexcloo/phpmyadmin

    - **phpPgAdmin**

            docker run --name="phppgadmin" -d --link postgresql:postgresql --env=VIRTUAL_HOST=phppgadmin.example.com maxexcloo/phppgadmin

    - **Tiny Tiny RSS**

            docker run --name="tiny-tiny-rss-data" maxexcloo/data
            docker run --name="tiny-tiny-rss" -it --link postgresql:postgresql --volumes-from="tiny-tiny-rss-data" --env=VIRTUAL_HOST=tiny-tiny-rss.example.com maxexcloo/tiny-tiny-rss

    - **Wordpress**

            docker run --name="wordpress-data" maxexcloo/data
            docker run --name="wordpress" -it --link mariadb:mariadb --volumes-from="wordpress-data" --env=VIRTUAL_HOST=wordpress.example.com maxexcloo/wordpress

- **Base**

    - **Arch Linux**

            docker run --name="arch-linux" -it maxexcloo/arch-linux /bin/bash

    - **Data**

            docker run --name="data" -it maxexcloo/data /bin/sh

    - **Debian**

            docker run --name="debian" -it maxexcloo/debian /bin/bash

    - **Ubuntu**

            docker run --name="ubuntu" -it maxexcloo/ubuntu /bin/bash

- **Frameworks**

    - **Apache**

            docker run --name="apache-data" maxexcloo/data
            docker run --name="apache" -it --volumes-from="apache-data" --env=VIRTUAL_HOST=example.com,www.example.com maxexcloo/apache

    - **Apache + PHP**

            docker run --name="apache-php-data" maxexcloo/data
            docker run --name="apache-php" -it --volumes-from="apache-php-data" --env=VIRTUAL_HOST=example.com,www.example.com maxexcloo/apache-php

    - **Nginx**

            docker run --name="nginx-data" maxexcloo/data
            docker run --name="nginx" -it --volumes-from="nginx-data" --env=VIRTUAL_HOST=example.com,www.example.com maxexcloo/nginx

    - **Nginx + PHP-FPM**

            docker run --name="nginx-php-data" maxexcloo/data
            docker run --name="nginx-php" -it --volumes-from="nginx-php-data" --env=VIRTUAL_HOST=example.com,www.example.com maxexcloo/nginx-php

- **Services**

    - **Dnsmasq**

            docker run --name="dnsmasq-data" maxexcloo/data
            docker run --name="dnsmasq" -it --privileged --volumes-from="dnsmasq-data" -p 53:53 -p 53:53/udp maxexcloo/dnsmasq

    - **HAProxy**

            docker run --name="haproxy-data" maxexcloo/data
            docker run --name="haproxy" -it --volumes-from="haproxy-data" -p 80:80 -p 443:443 maxexcloo/haproxy
        
    - **HAProxy Config**

            docker run --name="haproxy-data" maxexcloo/data
            docker run --name="haproxy-config" -it --volumes-from="haproxy-data" -v /var/run/docker.sock:/var/run/docker.sock maxexcloo/haproxy-config

    - **MariaDB**

            docker run --name="mariadb-data" maxexcloo/data
            docker run --name="mariadb" -it --volumes-from="mariadb-data" maxexcloo/mariadb
        
    - **Minecraft**

            docker run --name="minecraft-data" maxexcloo/data
            docker run --name="minecraft" -it --volumes-from="minecraft-data" --env=MEMORY=1024 -p 25565:25565 maxexcloo/minecraft

    - **PostgreSQL**

            docker run --name="postgresql-data" maxexcloo/data
            docker run --name="postgresql" -it --volumes-from="postgresql-data" maxexcloo/postgresql

    - **SNIProxy**

            docker run --name="sniproxy-data" maxexcloo/data
            docker run --name="sniproxy" -it --privileged --volumes-from="sniproxy-data" -p 80:80 -p 443:443 maxexcloo/sniproxy

    - **ZNC**

            docker run --name="znc-data" maxexcloo/data
            docker run --name="znc" -it --volumes-from="znc-data" --env=VIRTUAL_HOST=znc.example.com --env=VIRTUAL_PORT=6667 -p 6697:6697 -p 6667:6667 maxexcloo/znc

**Testing**  
    docker run -it --rm=true -p 5050:5050 maxexcloo/couchpotato
    docker run -it --rm=true -p 32400:32400 maxexcloo/plexmediaserver
    docker run -it --rm=true -p 80:80 -p 1900/udp:1900/udp -p 8200:8200 maxexcloo/readymedia
    docker run -it --rm=true -p 8080:8080 maxexcloo/sabnzbd
    docker run -it --rm=true -p 8081:8081 maxexcloo/sickbeard
    docker run -it --rm=true -p 4040:4040 maxexcloo/subsonic
