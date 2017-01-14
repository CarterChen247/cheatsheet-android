#PopupNotificationActivity

Declare following settings in `Manifest.xml`

```java
        <activity
            android:name=".ui.PopupNotificationActivity"
            android:label="label"
            android:screenOrientation="portrait"
            android:excludeFromRecents="true"
            android:launchMode="singleTask"
            android:taskAffinity=""
            android:theme="@style/FullScreenTheme">
        </activity>
```

add the following code depends on your situation

```java
  android:configChanges="keyboard|keyboardHidden|navigation|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"
  ```