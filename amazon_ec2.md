# Amazon EC2

## 範例目標
架設一個可應用的伺服器環境

##範例說明
要使用Amazon提供的EC2服務

首先你需要信用卡

用信用卡辦完帳號之後就可以開始啟動EC2

啟動過程中皆選擇預設選項即可

key-pair記得保存

記得把security group的權限新增port 80和port 433

接著就開始啟動啦

使用putty來啟動

>putty設定

>putty key-pair


使用pscp來傳送檔案

> pscp語法

使用ec2-user登入以後

就可以來安裝LAMP + MyphpAdmin了

以下轉載自Amazon的[安裝LAMP教學](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html)

```bahs
[ec2-user ~]$ sudo yum update -y
```

```bash
[ec2-user ~]$ sudo yum install -y httpd24 php56 mysql55-server php56-mysqlnd
```

```bash
[ec2-user ~]$ sudo service httpd start

顯示
Starting httpd:                                            [  OK  ]
```

```bash
[ec2-user ~]$ sudo chkconfig httpd on
```

```bash
[ec2-user ~]$ chkconfig --list httpd
httpd           0:off   1:off   2:on    3:on    4:on    5:on    6:off
```

測試


管理權限

```bash
[ec2-user ~]$ sudo groupadd www
```

```bash
[ec2-user ~]$ sudo usermod -a -G www ec2-user
```

```bash
[ec2-user ~]$ exit
```

```bash
[ec2-user ~]$ groups
ec2-user wheel www
```

```bash
[ec2-user ~]$ sudo chown -R root:www /var/www
```

```bash
[ec2-user ~]$ sudo chmod 2775 /var/www
[ec2-user ~]$ find /var/www -type d -exec sudo chmod 2775 {} +
```

```bash
[ec2-user ~]$ find /var/www -type f -exec sudo chmod 0664 {} +
```

```bash
[ec2-user ~]$ echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```
```bash
http://my.public.dns.amazonaws.com/phpinfo.php
```

```bash
[ec2-user ~]$ sudo service mysqld start
```

```bash
[ec2-user ~]$ sudo mysql_secure_installation
```

```bash
[ec2-user ~]$ sudo service mysqld stop
```

```bash
[ec2-user ~]$ sudo chkconfig mysqld on
```


> pscp

接著，參考DigitalOcean上由Justin Ellingwood分享的[在CentOS上安裝phpMyAdmin](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-a-centos-6-4-vps)

```
sudo yum install phpmyadmin
```

```
sudo nano /etc/httpd/conf.d/phpMyAdmin.conf
```

```
. . .
Require ip your_workstation_IP_address
. . .
Allow from your_workstation_IP_address
. . .
Require ip your_workstation_IP_address
. . .
Allow from your_workstation_IP_address
. . .
```

```
sudo service httpd start
```

```
VPS_IP_address/phpmyadmin
```

大功告成!可以開始匯入sql檔囉







