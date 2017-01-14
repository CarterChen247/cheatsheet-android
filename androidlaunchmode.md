#Android LaunchMode

## singleTop ([Reference](http://blog.csdn.net/liuhe688/article/details/6754323))
如果发现有对应的Activity实例正位于栈顶，则重复利用，不再生成新的实例。

##singleTask ([Reference](http://blog.csdn.net/liuhe688/article/details/6754323))
将該Activity之上的Activity实例统统出栈，将該Activity变为栈顶对象，显示到幕前。
```java
 <activity
            android:name="org.telegram.ui.PopupNotificationActivity"
            android:configChanges="keyboard|keyboardHidden|navigation|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"
            android:excludeFromRecents="true"
            android:launchMode="singleTask"
            android:taskAffinity=""
            android:theme="@style/Theme.TMessages.PopupNotification"
            android:resizeableActivity="false"
            android:windowSoftInputMode="adjustResize|stateHidden">
 </activity>
        ```
