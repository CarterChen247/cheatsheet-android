#Google Analytics SDK Fundamental



###add permissions to Manifest.xml 

```java 
  <uses-permission android:name="android.permission.INTERNET"/>
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```


###Configure Gradle

project-level build.gradle:
```
classpath 'com.google.gms:google-services:3.0.0'
```
app-level build.gradle:
```
apply plugin: 'com.google.gms.google-services'
```
compile library
```
compile 'com.google.android.gms:play-services-analytics:10.0.1'
```

###Get your google-services.json file
 1. Go to [here](https://developers.google.com/analytics/devguides/collection/android/v4/) and click "GET A CONFIGURATION FILE".
![](https://lh3.googleusercontent.com/MxawQuM6bRBkacEwxqgesDMUV1Dw94xaWmzyS8Ujq10jdOPCR5GaluipMCA_hj-j_E4KL3_w2SsgmRE-0IzB-qkU6XAsufMbde4x_FqiOE8I-6_DYdx-c7cHcbx-VGs3Typap5MNGejvXlseSvP1SaYg-VpyUlRs2bA5WOBD7V2vboE5zpgEfWa_J1z7eVqr05FDH255-LCKbYqeL0CxLD5MpV6TbSC_o21ll3_JLYLlYhIdCJtLunaXTaH-T9_2u-oXojIjm1QUQvuThH8aP7EX9f9YOEY_17G2Ywrj3tsY0LHBWtdghTmNpbL0srpQCxOU7rm0iICNqewyhS5Y0zUOaLa77x214MK5vqhKC5P4r6gA09ou4M3yKIpDmV6dmlhqmm2xa8gXS4IPhAcP6dts0GCSD1LPFncuGev8LdwUF58X29YRYRnjMwVz55c3QAcVJ04mpDBo6XRIZSTmFtrBb3bvunvUBIStiPY2T4ZmujJc-722a9kJ_d5wQ2Z5noWYavOCbI8HhC2LbirdVdSilQSY54-goyBfJQrp6USu2B65XvLwubO_OXUwq2JVwQ0C6n9HzDRqd6VlEQre8A-NKEe2o_Y7kfembtYcnte9FpWoDYNr3Q=w1117-h393-no)

 2. Copy the `google-services.json` file you just downloaded into the app/ or mobile/ directory of your Android Studio project. 


###Add Screen Tracking
Need to do the following task:

1. Provide the shared tracker via an Application subclass.
2. Override the callback method for the foreground activity.
3. Provide a name for the screen and execute tracking.

 #####1.Application
 
 Subclass Application class like a boss
 
 ```java
 public class AnalyticsApplication extends Application {
  private Tracker mTracker;

  /**
   * Gets the default {@link Tracker} for this {@link Application}.
   * @return tracker
   */
  synchronized public Tracker getDefaultTracker() {
    if (mTracker == null) {
      GoogleAnalytics analytics = GoogleAnalytics.getInstance(this);
      // To enable debug logging use: adb shell setprop log.tag.GAv4 DEBUG
      mTracker = analytics.newTracker(R.xml.global_tracker);
    }
    return mTracker;
   }
 }
```
 #####2.Foreground Activity(Activity or Fragment)
 Override `onCreate` method
 ```java
 // Obtain the shared Tracker instance.
AnalyticsApplication application = (AnalyticsApplication) getApplication();
mTracker = application.getDefaultTracker();
```
You can send information in the lifecycle you like
```java
Log.i(TAG, "Setting screen name: " + name);
mTracker.setScreenName("Image~" + name);
mTracker.send(new HitBuilders.ScreenViewBuilder().build());
```
If you need to listen event or actions, add the f*llowing code
```java
mTracker.send(new HitBuilders.EventBuilder()
    .setCategory("Action")
    .setAction("Share")
    .build());
    ```

---
#Why we are using GA?
###1.We can get the following info:
 * The number of users and sessions
 * Session duration
 * Operating systems
 * Device models
 * Geography
 
###2.Log Events
 ```java
tracker.send(new HitBuilders.EventBuilder()
       .setCategory("Achievement")
       .setAction("Earned")
       .setLabel("5 Dragons Rescued")
       .setValue(1)
       .build());
        ```
        
```java
tracker.send(new HitBuilders.EventBuilder()
       .setCategory("Barren Fields")
       .setAction("Rescue")
       .setLabel("Dragon")
       .setValue(1)
       .build());
    ```
```java
// Build and send a timing hit.
tracker.send(new HitBuilders.TimingBuilder()
    .setCategory("Barren Fields")
    .setValue(45000)  // 45 seconds.
    .setVariable("First Rescue")
    .setLabel("Dragon")
    .build());
```
###3.Other Feature
Campaigns

Crashes and Reports

Custom Dimensions and Metrics

...

        
