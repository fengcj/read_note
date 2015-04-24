## 目的
了解一个App启动的完整顺序

## 步骤

**(1)** `android.app.ActivityThread.main(String args[])`
- app启动时,android系统会生成一个对应的process,而该process也只有一个thread,即是mainThread,也就是UIThread.
- 该UIThread所应对的具体类是`ActivityThread`.java,在`android.app`包下.该类中有一个超级熟悉的方法,即main()方法.如下:

        public static void main(String[] args) {
            
            SamplingProfilerIntegration.start();
            CloseGuard.setEnabled(false);
            Environment.initForCurrentUser();
            EventLogger.setReporter(new EventLoggingReporter());
            Security.addProvider(new AndroidKeyStoreProvider());

            // Make sure TrustedCertificateStore looks in the right place for CA certificates
            final File configDir = Environment.getUserConfigDirectory(UserHandle.myUserId());
            TrustedCertificateStore.setDefaultUserDirectory(configDir);

            Process.setArgV0("<pre-initialized>");
            
            Looper.prepareMainLooper();
            
            // new ActivityThread
            ActivityThread thread = new ActivityThread();
            // 接下来跟踪的方法
            thread.attach(false);
            
            if (sMainThreadHandler == null) {
                sMainThreadHandler = thread.getHandler();
            }
            AsyncTask.init();

            if (false) {
                Looper.myLooper().setMessageLogging(new
                    LogPrinter(Log.DEBUG, "ActivityThread"));
            }
            Looper.loop();
            throw new RuntimeException("Main thread loop unexpectedly exited");
    }


**(2)** `android.app.ActivityThread.attach(boolean system)`

- 方法太长,只取关键部分

        public void attach(boolean system){
        
            // code
            try {
                // 应该也是个关键类,先放着
                mInstrumentation = new Instrumentation();
                // app级别的context,一个app只有一个
                ContextImpl context = ContextImpl.createAppContext(
                        this, getSystemContext().mPackageInfo);
                mInitialApplication = context.mPackageInfo.makeApplication(true, null);
                mInitialApplication.onCreate();
            } catch (Exception e) {
                throw new RuntimeException(
                        "Unable to instantiate Application():" + e.toString(), e);
            }
            // code
            
            }






## 引用
http://blog.csdn.net/ljsbuct/article/details/7094580