申請Google Maps API

##目標

開啟Google Maps API

##正文開始


先連到[Google API Console](https://code.google.com/apis/console)(Google API 主控台)

並新增一個專案

<img src = "/img/map_start.jpg" />


因為是示範專案，所以專案名稱就填test(你可以填入你自己喜歡的名稱)

而App Engine的位置其實不管哪裡對我們的影響都不大



<img src = "/img/map_enable.png" / >


選擇「Enable Google APIs for use in your apps」

啟動你應用程式中的Google API


<img src = "/img/map_apis.png" / >


卡在SHA1

藥用keytool

通常在Java資料夾
C:\Program Files\Java\jre7\bin

按windows + R 開啟執行 並輸入cmd 開啟命令列

輸入keytool -list -v -keystore mykeystore

可是keystore在哪裡呢?

$ keytool -genkey -v -keystore [我的keystore]
-alias [keystore別名] -keyalg RSA -keysize 2048 -validity 10000


C:\Program Files\Java\jre7\bin>keytool -list -v -keystore mykeystore(位址)

SHA1
EF:C1:79:76:6B:8F:BE:67:00:9F:37:DF:A7:86:C3:51:E3:DC:70:0B

先記住
AIzaSyATzzKFoAuLDTrMh55meeEHF6Wmx0Xd0cc