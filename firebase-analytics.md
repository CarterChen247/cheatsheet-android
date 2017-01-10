#Firebase Analytics SDK Fundamental

**Reference** https://firebase.google.com/docs/analytics/android/start/

###Prerequisites

 * Install the Firebase SDK.
 * Add your app to your Firebase project in the Firebase console.
 * Android Studio 1.5 or later.
 
 Simple.
 
###Add Analytics to your app
Add the dependency for Firebase Analytics to your app-level build.gradle file:

```java
compile 'com.google.firebase:firebase-core:10.0.1'
```
Declare the com.google.firebase.analytics.FirebaseAnalytics object at the top of your activity

```java
private FirebaseAnalytics mFirebaseAnalytics;
```

Then initialize it in the onCreate() method
```java
// Obtain the FirebaseAnalytics instance.
mFirebaseAnalytics = FirebaseAnalytics.getInstance(this);
```
###Log events

 1. Choosing Event from FirebaseAnalytics.Event
 2. Choosing Param from FirebaseAnalytics.Param
 3. Send
 
```java
Bundle bundle = new Bundle();
bundle.putString(FirebaseAnalytics.Param.ITEM_ID, id);
bundle.putString(FirebaseAnalytics.Param.ITEM_NAME, name);
bundle.putString(FirebaseAnalytics.Param.CONTENT_TYPE, "image");
mFirebaseAnalytics.logEvent(FirebaseAnalytics.Event.SELECT_CONTENT, bundle);
```

---
#Why using FA?
Firebase Analytics collects usage and behavior data for your app. The SDK logs two primary types of information:

 * Events: What is happening in your app, such as user actions, system events, or errors.
 * User properties: Attributes you define to describe segments of your userbase, such as language preference or geographic location.
Analytics automatically logs some events and user properties; you don't need to add any code to enable them.



