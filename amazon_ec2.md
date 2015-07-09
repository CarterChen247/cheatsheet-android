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

到這邊為止，就完成EC2 instance的啟動了

### 使用PUTTY登入遠端主機

啟動了EC2之後，就等於我們多擁有了一台空的主機

我們要在這台主機上安裝伺服器環境

這樣之後才可以使用手機來連接伺服器的服務

要登入Amazon EC2需要進行SSH登入

所以以下我們以puttygen與puttyn為例

產生private key並進行安全登入

####使用puttygen產生private key

請拿出我們剛剛下載好的key-pair

並載入到puttygen中，進行產生private key的動作

>圖 puttygen

密碼不需要設定

puttygen下載

#### 使用putty進行安全登入

有了private key之後，我們便可以來進行安全登入

打開putty

>圖 putty介面

選擇左側的Auth，選擇()，載入private key

>圖 auth

回到()，填入遠端主機的資訊

>圖 putty設定

主機位址如果不清楚的話可以進去AWS EC2的主控台中

>圖 EC2 

看要用Public DNS address或Public IP address當主機位址都可以

最後按open，便可連進我們的遠端主機

>圖 remote-terminal

###安裝LAMP環境

成功登入以後，就可以來安裝伺服器環境囉

本範例以LAMP(Linux + Apache + MySQL + PHP)為例，進行伺服器的架設

架設的方法在Amazon上其實就有[詳細的英文說明文件](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html)

而為了方便大家了解，由本範例翻譯成中文：


```bahs
$ sudo yum update -y
```

```bash
$ sudo yum install -y httpd24 php56 mysql55-server php56-mysqlnd
```

```bash
$ sudo service httpd start

顯示
Starting httpd:                                            [  OK  ]
```

```bash
$ sudo chkconfig httpd on
```

```bash
$ chkconfig --list httpd

顯示
httpd           0:off   1:off   2:on    3:on    4:on    5:on    6:off
```

測試


管理權限

```bash
$ sudo groupadd www
```

```bash
$ sudo usermod -a -G www ec2-user
```

```bash
$ exit
```

```bash
$ groups
ec2-user wheel www
```

```bash
$ sudo chown -R root:www /var/www
```

```bash
$ sudo chmod 2775 /var/www
$ find /var/www -type d -exec sudo chmod 2775 {} +
```

```bash
$ find /var/www -type f -exec sudo chmod 0664 {} +
```

```bash
$ echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```
```bash
http://my.public.dns.amazonaws.com/phpinfo.php
```

```bash
$ sudo service mysqld start
```

```bash
$ sudo mysql_secure_installation
```

```bash
$ sudo service mysqld stop
```

```bash
$ sudo chkconfig mysqld on
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




