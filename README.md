# WordPress-install

- ouvrir le terminal à la racine du dossier spé WP
- telecharger wp : [release wp](https://wordpress.org/download/releases/)
- copier le lien du zip 5.9.3
- télécharge la version nommé
- `wget https://wordpress.org/wordpress-5.9.3.zip`
- puis dézip
- `unzip wordpress-5.9.3.zip `
- supprimer l'archive
- `rm wordpress-5.9.3.zip `
- renommer le dossier par test
- `mv wordpress/ test`

création de VHost avec Apache "virtual host"
"Apache est un serveur web. Son rôle est d'écouter les requêtes émises par les navigateurs (qui demandent des pages web), de chercher la page demandée et de la renvoyer."
![[Pasted image 20220608111406.png]]

se placer ds le dossier wp (nommé test ds ce cas)
- `cd test/`
- faire
- `pwd`
- résultat "/var/www/html/S09_WordPress/test"
- bien se placer ds /var/www/html pour que Apache ai les droit suffisant et nécéssaire
- racine du dossier de config d'Apache
- `cd /etc/apache2 `
- aller ds le dossier
- `cd sites-available/`
==>
- on ouvre le fichier 000-default.conf
- `nano 000-default.conf`
- server name correspond au nom de domain
- documentroot chemin ou se situ l'aplication que l'on souhaite que apache nous redirige<==
- création d'1 fichier e config
- `sudo nano test.conf`
- copie de la config ds le fichier
 ```html
 <VirtualHost *:80>
    ServerName wordpress.local
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/spe_wp/preparation/wordpress
    <Directory />
            Options FollowSymLinks
            AllowOverride None
    </Directory>
    <Directory /var/www/html/spe_wp/preparation/wordpress>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Order allow,deny
            allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- on modifie 'wordpress.local' par 'test.local'
- et documentRoot on met le chemin vers le dossier 'test' récupéré précédamment
- et ds la balise directory on met aussi le même chemin
- 'Ctrl + O' pour enregistrer puis 'entré'
- on peux quitter l'éditeur
- on active le vhost
- a2ensite = Apache 2 enable site
- `sudo a2ensite test.conf`
- on recharge le server apache
- `sudo service apache2 reload`
- pour pouvoir aller sur le site en local on modifie le fichier host
- pour éditer le fichier host
- `sudo nano /etc/hosts`
- ajouter la ligne
- `127.0.0.1 test.local`
- taper ds le navigateur pour acceder au site
- `http://test.local/`


On commence l'installation de wordpress
- creer la bdd
- on se place ds le dossier parent du projet 
- et on tape
 `sudo chgrp -R www-data test/`
- on se place ds le dossier du projet 
- puis on tape
```
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
```
- puis on installe normalement jusqu'à la connexion
- on se connecte
- on installe un plugin pour verifier les droits par rapport à l'install
- si cela ne marche pas
- on ouvre le fichier de config wp ds le terminal
- ` sudo nano wp-config.php `
- ajouter la ligne ds le fichier vers la fin
- `define('FS_METHOD', 'direct');`

wp en ligne d ecommande
[wp-cli.org](https://wp-cli.org/fr/)
Automattic créateur de wp qui maintient le developpement de wpcli

## installation 
[install](https://wp-cli.org/fr/#installation)
se mettre à la racine du dossier test
- `curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar`
- verif l'install
- `php wp-cli.phar --info`
- `chmod +x wp-cli.phar`
- `sudo mv wp-cli.phar /usr/local/bin/wp`
- pour verifier (on doit avoir le même résultat que `php wp-cli.phar --info` )
- `wp --info`

[liste des commandes CLI](https://developer.wordpress.org/cli/commands/)
exemple :
- `wp plugin list`
- ``


## desinstallation
- Suppression du dossier wordpress
- `sudo rm -rf test/`
- Suprimer la base de donnée ds adminer
- enlever la ligne test.local
- `sudo nano etc/hosts`
- ``
- `cd /etc/apache2/sites-available/`
- pour disable
- `sudo a2dissite test.conf`
- pour reload le service apache
- `sudo service apache2 reload`
- suppression du fichier .conf
- `sudo rm test.conf`
- 
