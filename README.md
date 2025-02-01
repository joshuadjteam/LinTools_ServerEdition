# LinTools for Server
Welcome to our server edition of LinTools (LinTools Server 1)

This is build for the Tested Following : Red Hat Enterprise Linux, Alma, Rocky, Oracle, CentOS Stream, Fedora or Debian, Ubuntu, WSL, and Kali Linux

# Update Your Server/PC/Laptop/Smart Device or Appliance

sudo apt update && sudo apt upgrade -y

# Webmin Only Install

curl -o webmin-setup-repos.sh https://raw.githubusercontent.com/webmin/webmin/master/webmin-setup-repos.sh

sh webmin-setup-repos.sh

apt-get install webmin --install-recommends

dnf install webmin

echo Please go to localhost:10000

# NextCloud Only Install
*Please stop when "#text" is shown*

#the DB (Database) username has to be set to
#Username - admin
#Password - admin

sudo apt install apache2 mariadb-server libapache2-mod-php php-bz2 php-gd php-mysql php-curl php-mbstring php-imagick php-zip php-common php-curl php-xml php-json php-bcmath php-xml php-intl php-gmp zip unzip wget -y

sudo a2enmod rewrite dir mime env headers

sudo systemctl restart apache2

sudo mysql -u root -p

#Copy One by One as this is in a different terminal

CREATE USER 'nextcloud'@'localhost' IDENTIFIED BY 'Nextcloud123';

CREATE DATABASE IF NOT EXISTS nextcloud CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;

GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@'localhost';

FLUSH PRIVILEGES;

EXIT;

#You can now copy from here to the end

cd /var/www

sudo wget https://download.nextcloud.com/server/releases/latest.zip

sudo unzip latest.zip

sudo chown -R www-data:www-data /var/www/nextcloud/

cd /var/www/nextcloud

sudo -u www-data php occ maintenance:install --database "mysql" --database-name "nextcloud" --database-user "nextcloud" --database-pass "Nextcloud123" --admin-user "admin" --admin-pass "admin"

#Add your domain or IP to the trusted_domains array.

#Or if your using Nextcloud on that PC (localhost), you dont have to worry :)

sudo nano /var/www/nextcloud/config/config.php

sudo nano /etc/apache2/sites-available/000-default.conf

#Change "/var/..." in DocumentRoot to "/var/www/nextcloud"

sudo a2ensite 000-default.conf

sudo systemctl restart apache2


# Fix Nextcloud

If you get Internal Server Occured, follow these steps

sudo nano /var/www/nextcloud/data/nextcloud.log

if something is there, ask gemini at gemini.google.com

IF NOT...

sudo nano /var/log/apache2/error.log

again, if there is something ask gemini

# PHP Check

do "sudo nano /etc/php/VER/apache2.ini

Change VER to PHP version


Change the PHPs line to

; display_errors

;   Default Value: Off

;   Development Value: On

;   Production Value: Off


; display_startup_errors

;   Default Value: On

;   Development Value: On

;   Production Value: Off


; error_reporting

;   Default Value: E_ALL & ~E_DEPRECATED & ~E_STRICT

;   Development Value: E_ALL

;   Production Value: E_ALL & ~E_DEPRECATED & ~E_STRICT


; log_errors

;   Default Value: On 

;   Development Value: On
