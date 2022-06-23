## installation bedrock
[install bedrock](https://docs.roots.io/bedrock/master/installation/#getting-started)

installation d'1 nouveau projet wp ds un dossier backend
taper à la racine du projet :
`composer create-project roots/bedrock backend`

dans composer.json
modifier la version de wp voulu
 ```
 "require": {
    "roots/wordpress": "5.9.3",
```

aller ds le dossier backend et faire 
`composer update`

- on creer la bdd avec le user
- on modifie le fichier .env
```
DB_NAME='osailling'
DB_USER='osailling'
DB_PASSWORD='osailling'
```
- laisser le mode developpement
- modif le wp_home
- `WP_HOME='http://osailling.local'`
[generation de clé](https://roots.io/salts.html)
- on copie le contenue du env Format donné sur le site
- on colle à la place du contenu ds le fichier env

creation du VHost
- se mettre ds le  le dossier web (ds backend)
- `/var/www/html/S09_WordPress/spe-wp-oSailing-Christophe-Desmarres/backend/web`
- `cd /etc/apache2/sites-available/`
- copier un fichier existant avec :
- `sudo cp oprofile.conf ocooking.conf`
- ou
- créer un nouveau fichier :
- `sudo nano osailling.conf`
```
<VirtualHost *:80>
    ServerName ocooking.local
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/S09_WordPress/spewp-ocooking-backend-Christophe-Desmarres/backend/web
    <Directory />
            Options FollowSymLinks
            AllowOverride None
    </Directory>
    <Directory /var/www/html/S09_WordPress/spewp-ocooking-backend-Christophe-Desmarres/backend/web>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Order allow,deny
            allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

```
- 'CTRL + o',  'Enter', 'Ctrl + X'
- `sudo a2ensite osailling.conf`
- `sudo service apache2 reload`
- `sudo nano /etc/hosts`
- `127.0.0.1 osailling.local`
- [site](http://osailling.local/)
```
sudo chgrp -R www-data .
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
```
- on va sur le site et on configure les infos comme d'hab 
