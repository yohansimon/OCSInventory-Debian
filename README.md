# OCSIventory-Debian
<p align = "center">
<img width="2442" height="1104" alt="Image" src="https://github.com/user-attachments/assets/3d6ba167-41c7-4b30-9cbc-4ce34e426aa2" />

Mise à jour des paqutes et du noyau Linux
```bash
sudo apt -y update && sudo apt upgrade && sudo apt full-upgrade && sudo apt autoclean && sudo apt clean
```
Installation de Lamp (PHP, MARIADB, APACHE)
```bash
sudo apt install -y mariadb-server apache2 libapache2-mod-perl2 make gcc \
php php-mysql php-gd php-xml php-mbstring php-curl libxml-simple-perl php-gd php-soap php-zip \
libdbi-perl libdbd-mysql-perl libapache-dbi-perl libnet-ip-perl php-pclzip \
libarchive-zip-perl libmojolicious-perl libswitch-perl libplack-perl
```
Mise en place de MariaDB
```bash
sudo mysql_secure_installation
```
Création de la base de donnée OCS Inventory
```bash
sudo mysql -u root -p
```
```bash
CREATE DATABASE ocsdatabase;
CREATE USER 'ocs-user'@'localhost' IDENTIFIED BY 'ocsdatabase';
GRANT ALL PRIVILEGES ON ocsdatabase.* TO 'ocs-user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
Téléchargement d'OCS Inventory
```bash
wget https://github.com/PassAndSecure/OCS_inventory/releases/download/OCSNG_UNIX_SERVER-2.12.1/OCSNG_UNIX_SERVER-2.12.1.tar.gz
tar -xvzf OCSNG_UNIX_SERVER-2.12.1.tar.gz
cd OCSNG_UNIX_SERVER-2.12.1
```
Lancement d'intallation OCS
```bash
sudo ./setup.sh
```
Redémarrage du services Apache
```bash
sudo systemctl restart apache2
sudo a2enconf ocsinventory-reports
sudo systemctl reload apache2
sudo chown -R www-data:www-data /usr/share/ocsinventory-reports
sudo chmod -R 755 /usr/share/ocsinventory-reports
sudo chown -R www-data:www-data /var/lib/ocsinventory-reports
sudo chmod -R 755 /var/lib/ocsinventory-reports
sudo systemctl restart apache2
```
Configuration de Stockage d'ocs dans le fichier php.ini
```bash
sudo nano /etc/php/8.2/apache2/php.ini
```
```bash
post_max_size = 50M
upload_max_filesize = 50M
max_execution_time = -1
max_input_time = -1
memory_limit = 256M
```
Ajout du nom de l'utilisateur de la BDD OCS 
```bash
sudo nano /etc/apache2/conf-available/z-ocsinventory-server.conf
```
```bash
PerlSetEnv OCS_DB_NAME ocsdatabase
PerlSetEnv OCS_DB_LOCAL ocsdatabase
PerlSetEnv OCS_DB_USER ocs-user
PerlSetVar OCS_DB_PWD ocsdatabase
```
Configuration de la BBD sur service OCS Inventory
```bash
sudo nano /usr/share/ocsinventory-reports/ocsreports/dbconfig.inc.php
```
```bash
define("DB_NAME", "ocsdatabase");
define("SERVER_READ","localhost");
define("SERVER_WRITE","localhost");
define("SERVER_PORT","3306");
define("COMPTE_BASE","ocs-user");
define("PSWD_BASE","ocsdatabase");
define("ENABLE_SSL","");
define("SSL_MODE","");
define("SSL_KEY","");
define("SSL_CERT","");
define("CA_CERT","");
```
Relancement du service Apache puis test sur OCS Inventory
```bash
sudo systemctl restart apache2
```
```bash
http://host/ocsreports
```
Login et mot de passe
```bash
admin
admin
```
