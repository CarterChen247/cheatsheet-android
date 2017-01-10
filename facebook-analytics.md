#Facebook Analytcis

**Reference**
https://developers.facebook.com/docs/analytics/quickstart-android

###Setup Facebook SDK
Follow this Guide
https://developers.facebook.com/quickstarts/?platform=android

###Log app events
register it in lifecycle `onResume` and `onPause`

```java
// Add to each long-lived activity
@Override
protected void onResume() { 
  super.onResume(); 
  AppEventsLogger.activateApp(this); 
}
  
// for Android, you should also log app deactivation
@Override
protected void onPause() { 
  super.onPause(); 
  AppEventsLogger.deactivateApp(this);
}
```
Declare listener in Foreground Activity

```java
AppEventsLogger logger = AppEventsLogger.newLogger(this);
```
Fire the event in your favor
```java
logger.logEvent("sentFriendRequest");
```