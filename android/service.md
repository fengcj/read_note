## class definition

		public abstract class Service extends ContextWrapper implements ComponetCallback2 {
		    
		    // the only abstract method
		    public abstract IBinder onBind(Intent intent);
		    
		    @override
		    public ComponentName startService(Intent service){
		        retutn mBase.startService(service)
		    }
		    
	    	@Override
            public boolean bindService(Intent service, ServiceConnection conn,int flags) {
                return mBase.bindService(service, conn, flags);
            }
            
            public int onStartCommand(Intent intent,int flags,int startId){
                onStart(intent,startId);
                return mStartCompatibility ?  START_STICKY_COMPATIBILITY : START_STICKY;
            }
		}

when you extends Service,you must override onBind() method


## Life Cycle

![](https://github.com/fengcj/read_note/blob/master/android/service.png)


















## Source code
http://grepcode.com/file/repository.grepcode.com/java/ext/com.google.android/android/4.3_r1/android/app/Service.java