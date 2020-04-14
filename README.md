# PHP web model
> 純PHP開發模塊

# config
> 系統, DB 

# LAMP架設流程
> Linux ubuntu 18.04~ PHP 7.0 , MySQL 5.7.22 or 8~ , Apache 2.4.18 (phpmyadmin)    

# Step 0: Adduser
```
//安裝 vim
* sudo apt-get install vim
* :wq!      //存擋

//建立or變更root密碼
* sudo su   //進入管理員權限
    * sudo passwd root  
 
//新增使用者
* adducer newuser
* sudo visudo (/etc/sudoers)   //設定使用者權限*
       root    ALL=(ALL:ALL) ALL
       newuser ALL=(ALL:ALL) ALL
               :wq!      //存擋

//修改ssh允許可用root帳號登入 & 修改 ssh 登入時 root 可不使用 .ppk 檔
* sudo apt-get install openssh-server
* vim /etc/ssh/ssh_config
       修改：cd d
       PermitRootLogin yes
       PasswordAuthentication yes
       :wq

//檢查使用者
* sudo /etc/passwd

/* 重啟sshd */
//如果出現：sshd: unrecognized service
* initctl list | grep ssh
* service ssh restart (ssh 服務重啟)

//輸入新的使用名稱和剛剛的密碼登入！
* service sshd restart (ssh 服務重啟)
```

# Step 1: Install Apache & PHP
```
sudo apt update
sudo apt install apache2

sudo apt install php7.0 libapache2-mod-php7.0 php7.0-mysql
sudo apt-get install php7.0-zip
sudo nano /etc/apache2/mods-enabled/dir.conf
sudo apt-get purge 'php*'

sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get purge php5-fpm
sudo apt-get install php7.0-cli php7.0-common libapache2-mod-php7.0 php7.0 php7.0-mysql php7.0-fpm php7.0-mysql
sudo apt-get install php7.0-cgi php7.0-dbg php7.0-dev php7.0-curl php7.0-gd
sudo apt-get install php7.0-mcrypt php7.0-xsl php7.0-intl

sudo service apache2 restart
```

# 更改PHP版本
```
sudo a2dismod {php版本}
sudo a2enmod {php版本}
```

# Step 2: Install MySQL
```
wget https://dev.mysql.com/get/mysql-apt-config_0.6.0-1_all.deb
sudo dpkg -i mysql-apt-config_0.6.0-1_all.deb
sudo apt-get update
sudo apt-get install mysql-server-5.7
```

# Step 3: Install Git ubuntu
```
sudo apt-get install git
```

# Step 4: Install phpMyAdmin (PHP資料庫管理介面)
```
sudo apt-get install zip unzip
sudo apt-get install phpmyadmin
sudo php5enmod mcrypt

apache2.conf：
Include /etc/phpmyadmin/apache.conf

sudo apt-get remove phpmyadmin
sudo apt-get purge phpmyadmin

cd /usr/share
sudo su
wget https://files.phpmyadmin.net/phpMyAdmin/4.5.4.1/phpMyAdmin-4.5.4.1-all-languages.zip
unzip phpMyAdmin-4.5.4.1-all-languages.zip
mv phpMyAdmin-4.5.4.1-all-languages phpmyadmin
chmod -R 0755 phpmyadmin
vi /etc/apache2/sites-available/000-default.conf

Alias /phpmyadmin "/usr/share/phpmyadmin/"
<Directory "/usr/share/phpmyadmin/">
    Order allow,deny
    Allow from all
    Require all granted
</Directory>

sudo a2enmod rewrite

rewrite for .htaccess
sudo vi /etc/apache2/apache2.conf

```
