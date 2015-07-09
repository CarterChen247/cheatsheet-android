# Amazon EC2

## 範例目標
架設一個行動應用程式的伺服器環境

##範例流程
1. 啓用Amazon EC2並啟動一個Instance
2. 使用PUTTY登入遠端主機
3. 安裝LAMP環境
4. 安裝phpMyAdmin
5. 使用pscp傳送檔案

##範例說明

使用Amazon Web Service前需要先申請帳號

而申請帳號時需要信用卡資料

所以記得先去辦一張信用卡/金融卡(如VISA、Master Card)

辦帳號的過程很簡單

就把該填的填一填、填完就下一步

經過驗證後就可以開始使用AWS囉

###啓用AWS EC2並啟動一個instance

>圖 AWS主選單

在主選單中選擇EC2，並開始進行設定

在設定過程中皆選擇預設選項即可

其中比較需要注意的有兩點：

1. key-pair的保存
2. Security Group的設定

####key-pair的保存

>圖 key-pair

key-pair是之後用來產生private key的文件

有了private key，我們才可以用來進行SSH安全連線

一定要記得保存好，遺失或是被別人拿走網站就完蛋了XD

####Security Group的設定

Security Group的工作

簡單來說就是門口的警衛

當我們今天想要進入一個晚會(網站)

他們會檢查我們胸前佩戴的名牌(port)，再決定要不要讓你進去

預設的設定是只允許port 22，也就是只允許SSH連線到遠端主機(網站)

這邊我們得額外設定好HTTP(80)和HTTPS(433)，這樣才能從別的地方到我們的網站存取資料

>圖 Security Group

### 使用PUTTY登入遠端主機


使用putty來啟動

>putty設定

>putty key-pair


使用pscp來傳送檔案

> pscp語法

###安裝LAMP環境

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

### 安裝phpMyAdmin

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


### 使用pscp傳送檔案




