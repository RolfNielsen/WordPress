sudo apt-get update

sudo apt-get upgrade

sudo apt install apache2 \
                 ghostscript \
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

sudo mkdir -p /srv/www

sudo chown www-data: /srv/www

curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www

sudo nano /etc/apache2/sites-available/wordpress.conf 

<VirtualHost *:80>
     ServerAdmin admin@example.com
     DocumentRoot /srv/www/wordpress
     ServerName sitename.com
     ServerAlias www.sitename.com
     <Directory /srv/www/wordpress/>
          Options FollowSymlinks
          AllowOverride All
          Require all granted
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/wordpress_error.log
     CustomLog ${APACHE_LOG_DIR}/wordpress_access.log combined
</VirtualHost>

sudo a2ensite wordpress

sudo a2enmod rewrite

sudo service apache2 reload

sudo a2dissite 000-default

sudo service apache2 reload

sudo mysql -u root

CREATE DATABASE wordpress;

CREATE USER wordpress@localhost IDENTIFIED BY 'Passw0rd';

GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER

ON wordpress.*

TO wordpress@localhost;

FLUSH PRIVILEGES;
exit

sudo -u www-data cp /srv/www/wordpress/wp-config-sample.php /srv/www/wordpress/wp-config.php

sudo -u www-data sed -i 's/database_name_here/wordpress/' /srv/www/wordpress/wp-config.php

sudo -u www-data sed -i 's/username_here/wordpress/' /srv/www/wordpress/wp-config.php

sudo -u www-data sed -i 's/password_here/Passw0rd/' /srv/www/wordpress/wp-config.php

Theme file editor wordpress

plugins :   File Manager

fil .Htaccess

php_value upload_max_filesize 8192M
php_value post_max_size 8192M
php_value memory_limit 8192M
php_value max_execution_time 300
php_value max_input_time 300
