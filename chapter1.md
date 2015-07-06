# 使用Google Maps API顯示地圖
想要在APP上顯示地標，必須要先從設定地圖開始

本範例將示範簡單的步驟，在設定完地圖後顯示地圖

後續再介紹其他控制地點的Android API

## 範例目標

<img src = "/img/map_result.jpg"  width = 30%, height = 30% />

在APP上顯示地圖。

## 範例目錄

1. 安裝並匯入Google Play services專案到工作區
2. 為開發中的APP匯入Google Play services library
3. AndroidManifest權限設定
4. App UI與程式設定

## 範例說明

其實要在APP上顯示地圖只要寫幾行layout，然後幾行程式就可以解決了

但是為了要能妥善的顯示，我們必須要做一下設定

### 安裝並匯入Google Play services專案到工作區

開啟Android SDK Manager

Eclipse -> Window -> Android SDK Manager

找到並安裝Google Play services

<img src = "/img/map_service.png"   />

安裝完以後，將Google Play services的專案匯入工作區

File -> Import -> Android -> Existing Android Code Into Workspace -> Next -> Browse

找到Google Play services的專案位置

```bash
C:\Users\PC\Desktop\Android\sdk\extras\google\google_play_services
```
點選Finish，匯入工作區

### 為開發中的APP匯入Google Play services library

已經匯入的Google Play services專案，已經是個library了，可以直接被App使用

對正在開發中的APP專案點右鍵

<img src = "/img/map_right_click.png"   />

選擇 Properties -> Android -> Library -> Add

將剛剛匯入的Google Play service專案library - google-play-services_lib匯入

即完成Google Play service的設定

<img src = "/img/map_lib.png"   />

### AndroidManifest權限設定

接下來開啟AndroidManifest.xml，進行API key的驗證設定

在application標籤中，加入

```
<meta-data
    android:name="com.google.android.maps.v2.API_KEY"
    android:value="[你的Google API key]" />
<meta-data
    android:name="com.google.android.gms.version"
    android:value="@integer/google_play_services_version" />
```
依照章節「申請Google API」設定後，得到的API key為

```bash
API key: "AIzaSyAfPk081F7VsmuvQtEp4r6_S7nGs34Uylk"
```
把它填到value屬性中
接著在manifest標籤中的其它地方加入

```xml
<uses-permission 
    android:name="android.permission.INTERNET" />
<uses-permission 
    android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission 
    android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission 
    android:name="com.google.android.providers.gsf.permission.READ_GSERVICES" />
<uses-permission 
    android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission 
    android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-feature
    android:glEsVersion="0x00020000"
    android:required="true" />
```

授權手機使用網路連線、GPS定位等設定(不設定就無法定位喔!)

### App UI與程式設定
    
在activity_main.xml中加入MapFragment，用來呈現地圖

```
<fragment
    android:id="@+id/map"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    class="com.google.android.gms.maps.MapFragment" />
```

在MainActivity.java中加入以下程式碼

```java
GoogleMap map = ((MapFragment) getFragmentManager().findFragmentById(R.id.map)).getMap();
```

大功告成!可以開始Run看看App了。