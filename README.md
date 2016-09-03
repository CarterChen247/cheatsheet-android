#Android Cheat Sheet(Android API 偷吃步)



**「僅獻給我盲目、熱情、為了開發而逝去的青春。」──[KazafChen](https://github.com/KazafChen)**

根據我開發Mealionaire([論文](http://ndltd.ncl.edu.tw/cgi-bin/gs32/gsweb.cgi/login?o=dnclcdr&s=id=%22103NCUE5396039%22.&searchmode=basic)、[投影片](http://www.slideshare.net/kazafchen/mealionaire-a-contextaware-and-ontologybased-mobile-recommender-system-for-personalized-cuisine-recommendation))的經驗，以快速建構一個可上架的的APP為目標
提供大家簡潔易懂可以快速上手的Android API使用方法，以及其他相關的函式庫、服務等應用說明


###前言
大學時期我就讀的是數位內容科技學系，學系的方針為培養「設計、程式、數位學習」三方的整合人才，但因為一方面我覺得系上對於程式設計所投資的資源較少，一方面也是我對設計(平面設計、網頁設計)比較有興趣，所以就把重心放在設計技巧的發展上了。智慧型手機在2007年開始嶄露頭角，在我比較有接觸的時候已經是2011年了，一開始不過覺得一隻一般的手機只要幾千塊，而智慧型手機動輒一兩萬、兩三萬，這種東西會有人買嗎？直到後來意識到App的趨勢，以及在未來的地位，便一頭栽進了這個領域。

後來因為也選修了介面設計課程，開始想想日常生活當中有什麼問題，是可以藉由設計App來解決的，並試著設計出簡潔、得體的介面。但沒想到一發不可收拾，我發現世界上真的有太多的事情，可以藉由自動化而變得更簡單，並且帶給人們更便利的生活，心目中有無限多個想法，想要藉由設計讓概念變得具體化，但卻始終無法成為現實。

還記得升研究所的那個暑假，我再也受不了了。我在網路上廣蒐資源，希望能讓自己學會如何設計App，如此一來，我才有辦法讓自己的想法從天馬行空轉變為現實。幸好後來台中科技大學資訊管理系願意收留我，在黃天騏教授的同意下，開始和黃思齊、葉庭杰等大師學習Android入門。

過了一個暑假的磨練，我從根本不知道如何設計程式進步到了能產出自己的第一個專案，雖然成果不是說很好，但帶給我很大的信心 ，這份力量也支持我一路走完兩年的碩士生涯。以下將介紹的，便是我在就讀碩士班期問，從零到壹，從無到有，親自設計程式，介面與上架的第一個有網路連線能力、較大的專案：Mealionaire。

###版本1
身為一個小新手，根本不知道Android是要如何透過無線網路與電腦進行資料的傳輸。後來經過一番研究，便以LAMP環境架設伺服器 ，使用Android連線到電腦進行資料的存取與運算。最終的目的便是想要設計一個可以為使用者推薦符合使用者喜好與適合當下情境用餐的美食資訊。

在這過程中不小心多學了php，php因為已經有內建為數眾多的函式庫，官方也有詳細的說明文件，所以伺服器端的程式撰寫起來是得心應手；反而是行動端，因為當時gradle在國內並不是很盛行，我設計程式的IDE也還在使用Eclipse，對於lib的使用與管理不甚方便，因此只使用了[Gson](https://github.com/google/gson)，還記得當時連線的功能我還在用httpclient慢慢刻！但這時我的App基本上已經有個人化的功能，而這個功能則是包成一個jar檔，透過php來執行。

因為這個App也算是論文的研究結果，其中參考了許多學術文獻，使用到的技術也包括本體論、個人化推薦與情境感知。[本體論(Ontology)](https://en.wikipedia.org/wiki/Ontology)的三個特色包括：(1)對概念清楚明確的定義、(2)概念的架構可以被重複使用、(3)讓人可以很容易的和機器溝通特定的概念；個人化推薦則使用到了K-means分群演算法，用來將喜好相似的使用者分在同一個群體，藉此來群體中的每個人都能獲得其他和自相似的人也喜歡的資訊或物品項目；而關於[情境感知(Context-aware)](https://en.wikipedia.org/wiki/Context_awareness)，為了獲得當下的溫度與天氣,使用了[Forecast.io所提供的API](https://developer.forecast.io/)來獲得天氣預報資訊，為了判斷使用者與餐廳之問的距離，使用了[Haversine演算法]()來計算在地球曲面上兩點之問的距離，最後再透過GoogleMaps將餐廳顯示在使用者手機的地圖上。後來覺得要做也做專業一點，所以也整合了[Facebook Android SDK](https://github.com/facebook/facebook-android-sdk)，透過其中的Facebook Login功能，讓使用者可以透過Facebook帳號進行快速登入。

開發的同時也要感謝[319papago提供的餐廳與餐點資料](http://www.319papago.idv.tw/SuperTaste/01-E.html)，在完成APP的同時，已囊括了中彰投地區700多間餐廳與1400多筆的美食資訊。

###版本2
因為本來整個伺服器是架在實驗室的電腦中的，後來為了能脫離研究所實驗室的環境，首次嘗試在亞馬遜的EC2上面運行整個專案。 因為採用的是免費方案，硬體效能有限，於是就直接把運算耗時的本體論拔掉了(雖然使用本體論比較精準，但是推薦一次需要耗時30秒，會讓使用者等待太久)在這過程中，光是學會如何重新架構整個環境，就讓我對AWS與Linux有更深一步的認知。

為了要做得更炫，App加入了一堆UI元件的libs，如[Circleimageview](https://github.com/hdodenhof/CircleImageView)，讓圖片可以變成圓的、[SlidingUpPanel](https://github.com/umano/AndroidSlidingUpPanel)讓某些事件發生時畫面底端會跑出一小塊資訊區域、為了讓使用者在看地圖時縮放到街道等級可以看到單一的地圖marker，縮放到城市等級又可以看到上面帶有美食數量數字的地圖marker，另外引進了[Android-maps-utils](https://github.com/googlemaps/android-maps-utils)、為了方便使用者知道大致的路線，與自己當所在的位置，學習如何使用Google的[Geocoding](http://maps.googleapis.com/maps/api/geocode/json?latlng=23.4624703,120.2435842)和[Direction API](https://maps.googleapis.com/maps/api/directions/json?origin=23.4789575,120.4492964&destination=25.0339031,121.5645098&avoid=highways)。

除此之外，App也加入了Comment功能(使用者留言，使用者可以對單一美食留下評論)、加入了tag功能(美食標籤，使用者可以替美食新增標籤，類似Folksonomy)、加入了Log功能(記錄使用者瀏覽紀錄，以利用這些紀錄來推算使用者的喜好)、加入了上傳美食照片的功能與排名的功能 (包括使用者、餐廳與美食的排名，使用者可以透過新增評論與照片獲得點數，提升自己排名)。

其中上傳照片的功能算是比較複雜，使用到的library有AWS開發給Android行動端使用的[S3](https://github.com/aws/aws-sdk-android/tree/master/aws-android-sdk-s3)(真的滿好用的，甚至還內建在傳送檔案時回傳進度幾%)、認證用的[Cognito](https://github.com/aws/amazon-cognito-android)還有用來優化載入圖片的[Picasso](http://square.github.io/picasso/)。藉由開發此功能,學習了AWS S3的使用方法,還有Android的File處理方式。

但是終究我也只有一個人而巳，整個系統包含了[Content Management System](https://en.wikipedia.org/wiki/Content_management_system)、[Location-based Service](https://en.wikipedia.org/wiki/Location-based_service)、[Context-Aware Service](https://en.wikipedia.org/wiki/Context-aware_services)與[Gamification](https://en.wikipedia.org/wiki/Gamification)終究還是把我給淹沒了，後來被國軍徵召的期間，AWS免費方案的十二個月也到期了，假日也沒多少時間可以用，所以就沒有繼續開發下去。有了這次經驗，深深的覺得真的很可惜，但也讓我學到，不要一開始就想做很大的東西。無論如何，這次都是一個非常寶貴的經驗。「失敗越多，成功越快(Fail often to succeed sooner)」這是設計公司IDEO的金玉良言，我相信這次的失敗，會成為我之後成功的墊腳石。

###未來發展建議

**了解案上傳到雲端儲存的最佳可行方案**

在本專案中照要上傳到雲端空問儲存前，App會亂數產生照片檔名，並且將檔名的資訊和辨識使用者的資訊(如使用者)一起存入資料庫，接著再將亂數命名過的照片存放到雲端空間；讀取照片時則是先連線到資料庫，獲得照片的檔案名稱，再連線到雲端空問讀取檔案。不知道是否存在具有更高效率的儲存方法？

**餐廳營業畤間的資料庫結構**

本專案的營業時間结構設計方式為根據一週內的每天(星期一至星期日)設定營業時問與休息時間(如下)。此表雖然可以代表常態下每天的營業時問，但逢年過節便會失準，不知道是否存在更精確的記錄方法？
```sql
INSERT INTO 
  `ophour` (`rid`, `day`, `open`, `close`) 
VALUES
  (1, 1, 720, 1440),
  (1, 3, 720, 1440),
  (1, 4, 720, 1440),
  (1, 5, 720, 1440),
  ...
```

**AWS資料庫問題**

本專案所使用的資料皆存取於安裝於EC2上的MYSQL，不知道是否能，或用什麼方法能轉移到AWS RDB上？此舉的效果也會比較好嗎？




