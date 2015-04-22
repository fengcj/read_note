## class definition

		public abstract class Service extends ContextWrapper implements ComponetCallback2 {
		    
		    // the only abstract method,the return object which type is IBinder will pass to method
		    // onServiceConnection(ComponetName name,IBinder serivce), using the IBinder to communicate
		    // between service and client
		    public abstract IBinder onBind(Intent intent);
		    
		    // inherit from ContextWrapper, so Activity can use it to bind a service
	    	@Override
            public boolean bindService(Intent service, ServiceConnection conn,int flags) {
                return mBase.bindService(service, conn, flags);
            }
            
            // inherit from ContextWrapper, so Activity can use it to start a service
            @override
		    public ComponentName startService(Intent service){
		        retutn mBase.startService(service)
		    }
            
            public int onStartCommand(Intent intent,int flags,int startId){
                onStart(intent,startId);
                return mStartCompatibility ?  START_STICKY_COMPATIBILITY : START_STICKY;
            }
		}

when you extends Service, you must override onBind() method, and you can return null.

**  Services can be started with Context.startService() and Context.bindService(). **

## Life Cycle
![](https://github.com/fengcj/read_note/blob/master/android/service.png)

## More about bindService() method

when we use `bindService(Intent service, ServiceConnection conn,int flags)` to start a service, the most important thing is implementing a `ServiceConnection` interface.

        public interface ServiceConnection {
             public void onServiceConnected(ComponentName name, IBinder service);
             public void onServiceDisconnected(ComponentName name);
        }
        
as we comment on `public abstract IBinder onBind(Intent intent)` method, the return object `IBinder` will pass to method
`public void onServiceConnected(ComponentName name, IBinder service)`, then we cau use this `IBinder` in client.

so what is a `IBinder`?  Obsviously it is a interface, and there a class `Binder` implement this interface. So in the Service class, we can write a new(inner) class which extends `Binder`, and some logic in it for client to use, then we return a object newed by this class in method `public abstract IBinder onBind(Intent intent)`.

more detial can be get from reference part


## Source code
http://grepcode.com/file/repository.grepcode.com/java/ext/com.google.android/android/4.3_r1/android/app/Service.java

## Reference
http://www.cnblogs.com/plokmju/p/Android_Service1.html
