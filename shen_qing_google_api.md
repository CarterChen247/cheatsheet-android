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


<img src = "/img/map_android_apis.png" / >

啟動「Google Maps Android API」

點選啟用，就完成API的啟用了

<img src = "/img/map_go.png" / >

接下來我們要讓我們開發的應用程式可以存取這個API

而應用程式在存取API時，將透過API key驗證你有沒有被授權使用

所以點選「前往API主控台查看報表」進行API key的設定

<img src = "/img/map_api_access.png" / >

先在主控台左邊選取「API Access」管理API的存取

因為我們開發的是Android App 所以在畫面右邊點擊「Create new Android key」按鈕

<img src = "/img/map_android_key.png" / >

在這個Android Key的設定視窗中，它告訴我們如果要產生適用於Android App的API key

我們得提供

1. 開發環境的「SHA1 fingerprint」
2. APP的「package name」

所以以下我們開始分別尋找這兩樣東西

###SHA1 fingerprint

如剛才Android key設定視窗中所說的，可以使用keytool工具來取得SHA1 fingerprint

取得的方法是使用命令提示字元工具輸入以下的指令

```bash
keytool -list -v -keystore [keystore的存放位置]
```

使用前記得先將目錄切換到存放keytool的地方，這樣才能使用keytool

而keytool這樣工具通常都被存放在Java的bin資料夾中

以本範例來說，keytool存放在

```bash
C:\Program Files\Java\jre7\bin
```

所以就在命令提示字元中輸入

```bash
cd C:\Program Files\Java\jre7\bin
```

至於你自己的keytool放在哪裡，就就自己去找找吧

keystore的話，本範例的keystore存放在

```bash
C:\Users\PC\.android\debug.keystore
```

確認都有了keytool和keystore之後，我們就可以開始解碼，取得我們的SHA1 fingerprint

在命令提示字元中依照keystore的存放位置輸入

```bash
keytool -list -v -keystore C:\Users\PC\.android\debug.keystore
```












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