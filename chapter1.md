# 使用Google Maps API來顯示地圖
若你想開發的APP需要呈現與地點有關的資訊，可以使用Google Maps API來呈現。

## 呈現結果
<img src = "/img/map_result.jpg" / width = 30%, height = 30% align = "middle">

## 正文開始



需要service lib

Eclipse -> Window -> SDK Manager

下載 Google Play Services

C:\Users\PC\Desktop\Android\sdk\extras\google\google_play_services


開啟 File --> Import --> Android --> Existing Android Code Into Workspace --> Next

Manifest

```
<uses-feature
android:glEsVersion="0x00020000"
android:required="true" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<!-- 存取Google web services -->
<uses-permission android:name="com.google.android.providers.gsf.permission.READ_GSERVICES" />
<!-- 透過3G或wifi定位 -->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<!-- 使用GPS定位 -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
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

```
GoogleMap map = ((MapFragment) getFragmentManager().findFragmentById(R.id.map)).getMap();
```


trouble shooting
[2015-07-05 23:31:51 - google-play-services_lib] Unable to resolve target 'android-9'


通常debug.keystore會存在這個位址

```
C:\Users\User\.android\debug.keystore
```

131332
    
```
keytool -genkey -v -keystore yourkeyname.keystore -alias yourkeyname -keyalg RSA -keysize 2048 -validity 10000
```
    
接著開始coding

```
mapFragment = ((SupportMapFragment) getSupportFragmentManager()
				.findFragmentById(R.id.map_small));
	map = mapFragment.getMap();
```






end




