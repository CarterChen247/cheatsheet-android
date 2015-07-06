# 使用Google Maps API顯示地圖
想要在APP上顯示地標，必須要先從設定地圖開始

本範例將示範簡單的步驟，在設定完地圖後顯示地圖

後續再介紹其他控制地點的Android API

## 範例目標

<img src = "/img/map_result.jpg"  width = 30%, height = 30% />

在APP上顯示地圖。

## 範例目錄

## 範例說明



需要service lib

Eclipse -> Window -> SDK Manager

下載 Google Play Services

C:\Users\PC\Desktop\Android\sdk\extras\google\google_play_services


開啟 File --> Import --> Android --> Existing Android Code Into Workspace --> Next

Manifest

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

    
    
    
    
Manifest application
```
<meta-data
    android:name="com.google.android.maps.v2.API_KEY"
    android:value="AIzaSyBSG1gZOJpjN5n8ALMzShsyMbz3AGv65ug" />
<meta-data
    android:name="com.google.android.gms.version"
    android:value="@integer/google_play_services_version" />
```
    
            
activity_main.xml

```
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity" >

    <fragment
        android:id="@+id/map"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        class="com.google.android.gms.maps.MapFragment" />
    
</RelativeLayout>
```

MainActivity.java

```java
GoogleMap map = ((MapFragment) getFragmentManager().findFragmentById(R.id.map)).getMap();
```


trouble shooting
[2015-07-05 23:31:51 - google-play-services_lib] Unable to resolve target 'android-9'





end




