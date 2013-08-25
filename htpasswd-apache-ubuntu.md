cesi-initiation-s-curiser-ubuntu
================================

# Configuration Apache sur Ubuntu


### Ressources liens :
 
[http://httpd.apache.org/docs/2.2/howto/auth.html](http://httpd.apache.org/docs/2.2/howto/auth.html)  
[Bon tuto](http://www.cyberciti.biz/faq/howto-setup-apache-password-protect-directory-with-htaccess-file/)  
[Autre tuto](http://www.unixmen.com/protect-apache-directories-with-a-password-linux/)


## Générer le fichier avec le htpasswd 
Sur linux en général :  

	htpasswd -c /usr/local/apache/passwd/passwords rbowen

Sur ubuntu : 

	htpasswd -c /etc/apache2/passwd USERNAME

Ceci est un exemple, vous pouvez placer le fichier ou vous le souhaitez, préférez tout de même un dossier non accessible et protégé.
Pour donner les droits voici un [tuto](http://www.cyberciti.biz/faq/howto-setup-apache-password-protect-directory-with-htaccess-file/)

### La commande 
*-c :*

	-c : Create the password-file. If password-file already exists, it is rewritten and truncated.

*Username :*

	username : The username to create or update in password-file. If username does not exist in this file, an entry is added. If it does exist, the password is changed.

## On ajoute un fichier .htaccess   

Soit on crée le fichier à la racine de /var/www ou alors on peut placer le fichier indépendamment dans les dossiers de votre choix.
 
	AuthType Basic
	AuthName "By Invitation Only"
	AuthUserFile /etc/apache2/passwd
	Require valid-user

Pour le chemin AuthUserFile il est nécessaire de préciser le chemin vers le fichier avec le login et le password généré précédement.

## On ajoute la directive dans le fichier httpd.conf (autre méthode) 

Bien sûr, il ne faut pas cumuler les deux méthodes, c'est inutile. 

editer le fichier httpd.conf (/etc/apache2/httpd.conf) 

Ajouter la directive suivante :

	<Directory /chemin-du-repertoire>
	    AuthType Basic
	    AuthName "Please enter login and password"
	    AuthBasicProvider file
	    AuthUserFile /chemin-vers-htpasswd
	    Require valid-user
	</Directory>

Pour le **Directory**, placez le chemin de votre choix. Par exemple : 

	var/www/monsite

Pour le **AuthUserFile**, il suffit de renseigner le chemin vers le fichier précedemment créé :  

	/etc/apache2/passwd




