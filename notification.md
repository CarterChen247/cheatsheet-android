#Notification (Reference [1](https://github.com/DrKLO/Telegram/blob/master/TMessagesProj/src/main/java/org/telegram/messenger/NotificationsController.java), [2](https://github.com/kesenhoo/android-training-course-in-chinese/blob/master/wearables/notifications/stacks.md))

```java
        Intent intent = new Intent(this, MainActivity.class);
        intent.putExtra("key", "value");

        PendingIntent contentIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this)
                .setContentTitle(getResources().getString(R.string.app_name))
                .setContentText(message)
                .setSmallIcon(icon)
                .setAutoCancel(true)
                .setContentIntent(contentIntent)
                .setDefaults(NotificationCompat.DEFAULT_VIBRATE)
                .setVibrate(new long[]{1000, 1000});

        NotificationManager notificationManager = (NotificationManager) this.getSystemService(Context.NOTIFICATION_SERVICE);
        notificationManager.notify(0, builder.build());
```