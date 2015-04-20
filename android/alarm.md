## Key Class
- AlarmManager
- PendingIntent


## Alram Type
- AlarmManager.RTC

    Fires the pendding intent at the specified time but dose not wake up the device.
    
- AlarmManager.RTC_WAKEUP

    Wakes up the device to fire the pending intent at the specified time.
    
- AlramManager.ELAPSED_REALTIME

    Fires the pending intent based on the amount of time since the device was booted, but doesn't wake up the device. The elapsed time includes any time during which the device was asleep.
    
- AlramManager.ELAPSED_REALTIME_WAKEUP

    Wakes up the device and fires the pending intent after the specified length of time has elapsed since device boot.
    
    
    
## Simple Code

        Intent intent = new Intent(this, OneShotAlarm.class);  
        PendingIntent sender = PendingIntent.getBroadcast(this, 0, intent, 0);  
 
        // 设置警报时间         
        Calendar calendar = Calendar.getInstance();  
        calendar.setTimeInMillis(System.currentTimeMillis());  
        calendar.add(Calendar.SECOND, 30);  
     
        // 设置警报时间，除了用Calendar之外，还可以用  
        long firstTime = SystemClock.elapsedRealtime();  
                
        AlarmManager am = (AlarmManager) getSystemService(ALARM_SERVICE);  
        // 只会警报一次  
        am.set(AlarmManager.RTC_WAKEUP, calendar.getTimeInMillis(), sender);  
        // 会重复警报多次  
        am.setRepeating(AlarmManager.ELAPSED_REALTIME_WAKEUP, firstTime, 15*1000, sender);  
   
        // 要取消这个警报，只要通过PendingIntent就可以做到  
        am.cancel(sender);
    
