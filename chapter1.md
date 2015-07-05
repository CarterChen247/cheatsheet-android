# 使用Google Maps API來顯示地圖
若你想開發的APP需要呈現與地點有關的資訊，可以使用Google Maps API來呈現。

## 呈現結果
<img src = "Screenshot_2015-07-02-16-53-43.jpg" / width = 30%, height = 30% align = "middle">

## 正文開始
通常debug.keystore會存在這個位址

    C:\Users\User\.android\debug.keystore

131332
    
    keytool -genkey -v -keystore yourkeyname.keystore -alias yourkeyname -keyalg RSA -keysize 2048 -validity 10000
    
    


    mapFragment = ((SupportMapFragment) getSupportFragmentManager()
				.findFragmentById(R.id.map_small));
	map = mapFragment.getMap();









