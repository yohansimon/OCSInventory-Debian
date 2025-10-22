# OCSIventory-Debian
```bash
sudo apt -y update && sudo apt upgrade && sudo apt full-upgrade && sudo apt autoclean && sudo apt clean
```
```bash
sudo apt install -y mariadb-server apache2 libapache2-mod-perl2 make gcc \
php php-mysql php-gd php-xml php-mbstring php-curl libxml-simple-perl \
libdbi-perl libdbd-mysql-perl libapache-dbi-perl libnet-ip-perl php-pclzip \
libarchive-zip-perl libmojolicious-perl libswitch-perl libplack-perl
```
```bash
sudo mysql_secure_installation
```
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
```bash
wget https://github.com/PassAndSecure/OCS_inventory/releases/download/OCSNG_UNIX_SERVER-2.12.1/OCSNG_UNIX_SERVER-2.12.1.tar.gz
tar -xvzf OCSNG_UNIX_SERVER-2.12.1.tar.gz
cd OCSNG_UNIX_SERVER-2.12.1
```
