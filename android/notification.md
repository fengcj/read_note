## Items
- notification area
- notification drawer


## API level
- NotifacationCompat.Builder in the v4 package
- Notifacation.Builder was add in Android 3.0 (APL level 11)


## Important Class
- Intent,PendingIntent
- Notification.Builder,Notification
- NotificationManager

## Steps

(1) Create Intent and PendingIntent

	private Intent mNotificationIntent;
	private PendingIntent mContentIntent;
	mNotificationIntent = new Intent(getApplicationContext(),
				NotificationSubActivity.class);

    // create pending intent
	mContentIntent = PendingIntent.getActivity(getApplicationContext(), 0,
				mNotificationIntent, PendingIntent.FLAG_UPDATE_CURRENT);


(2) Create Notifcation by using Notifacation.Builder.getNotification()
A notification object must contain the fellowing:
- A small icon, set by setSmallIcon()
- A title, set by setContentTitle()
- Detail Text. set by setContentText()
    
        
	    private Uri soundURI = Uri
			.parse("android.resource://course.examples.notification.statusbar/"
					+ R.raw.alarm_rooster);
        private long[] mVibratePattern = { 0, 200, 200, 300 };

        Notification.Builder notificationBuilder = new Notification.Builder(getApplicationContext());
	    notificationBuilder.setTicker(tickerText)
				   .setSmallIcon(android.R.drawable.stat_sys_warning)
                   .setAutoCancel(true)
                   .setContentTitle(contentTitle)
                   .setContentText(contentText + " (" + ++mNotificationCount + ")")
                   .setContentIntent(mContentIntent) // set Intent
                   .setSound(soundURI)
                   .setVibrate(mVibratePattern);

(3) Get the NotifacationManager

    final NotificationManager mNotificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

(4) Send the notifacation

    private static final int MY_NOTIFICATION_ID = 1;
    mNotificationManager.notify(MY_NOTIFICATION_ID,
						notificationBuilder.getNotification()); 


### Source code

https://github.com/fengcj/code_pieces/blob/master/android/nitification.java

