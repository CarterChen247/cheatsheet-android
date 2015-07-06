#申請Google Maps API以開發地圖應用程式

很多時候如果我們開發的APP中具有和顯示地點有關的功能

便可以加入地圖的功能，方便使用者找尋地點

Android中提供Google Map地圖支援，只是在使用之前要做一些小設定

以下就來介紹如何進行設定!

##範例目標

開啟Google Maps API並獲得API key授權

##範例目錄

1. 主控台初步設定
2. 取得產生API key必須資料
  1. SHA1 fingerprint
  2. package name
3. 產生API key

##範例說明

###主控台初步設定


先連到[Google API Console](https://code.google.com/apis/console)(Google API 主控台)

並新增一個專案

><img src = "/img/map_start.jpg" />


因為是示範專案，所以專案名稱就填test(你可以填入你自己喜歡的名稱)

而App Engine的位置其實不管哪裡對我們的影響都不大



><img src = "/img/map_enable.png" / >


選擇「Enable Google APIs for use in your apps」

啟動你應用程式中的Google API


><img src = "/img/map_android_apis.png" / >

啟動「Google Maps Android API」

點選啟用，就完成API的啟用了

><img src = "/img/map_go.png" / >

接下來我們要讓我們開發的應用程式可以存取這個API

而應用程式在存取API時，將透過API key驗證你有沒有被授權使用

所以點選「前往API主控台查看報表」進行API key的設定

><img src = "/img/map_api_access.png" / >

先在主控台左邊選取「API Access」管理API的存取

因為我們開發的是Android App 所以在畫面右邊點擊「Create new Android key」按鈕

<img src = "/img/map_android_key.png" / >

在這個Android Key的設定視窗中，它告訴我們如果要產生適用於Android App的API key

我們得提供

1. 開發環境的「SHA1 fingerprint」
2. APP的「package name」

所以以下我們開始分別尋找這兩樣東西

###取得產生API key必須資料 - SHA1 fingerprint

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

過程中若遇到詢問「金鑰儲存庫密碼」，直接按Enter跳過即可

最後我們就拿到了我們SHA1 fingerprint

<img src = "/img/map_sha1.png" / >

記得先將得到的SHA1 fingerprint記起來，我們待會還會用到

本範例的SHA1 fingerprint如下

```bash
SHA1: "00:50:88:7E:50:74:AA:29:0C:95:b7:AB:6E:9D:F3:3D:71:72:50:DA"

```

另外一種比較簡單的方法，如果你用Eclipse

Window -> Preferences -> Android -> Build 也是找得到哦

><img src = "/img/map_eclipse.png" / >



###取得產生API key必須資料 - package name

package name的取得就比較簡單了

在Eclipse中File -> New -> Android Application Project 建立一個新的專案

在專案命名過程中即可獲得package name

><img src = "/img/map_new_app.png" / >

如果你是現有的專案，package name則在這個地方

<img src = "/img/map_package.png" / >


###產生API key

回到Android key的設定視窗，依照它的指示輸入SHA1 fingerprint和package name

```
[SHA1 fingerprint];[package name]
```

<img src = "/img/map_insert.png" / >

如此一來，便取得我們的API key

```bash
API key: "AIzaSyAfPk081F7VsmuvQtEp4r6_S7nGs34Uylk"
```

><img src = "/img/map_api_key.png" / >



