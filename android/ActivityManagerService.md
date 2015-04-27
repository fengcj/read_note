## 目的
分析下`ActivityManagerService`(服务端) 与应用程序(客户端)之间的通信模型，在介绍这个通信模型的基础上，再简单介绍实现这个模型所需要数据类型.

## Android三大核心功能
- `View.java`:功能有绘制图形、处理触摸、按键事件等
- `ActivityManagerService.java`:简称AMS，功能有管理所有APP的Activity、内存管理等
- `WindowManagerService.java`:简称为WMS，为所有APP分配窗口，并管理这些窗口

从上可知，AMS作为一种系统级服务管理所有Activity，当操作某个Activity时，例如： 启动一个新的Activity、停止当前Activity，**必须报告给AMS**，而不能“擅自处理”。当AMS接受到具体通知时，会根据该通知的类型，首先会更新内部记录，然后在通知相应客户进程去运行一个新的Activity或者停止指定的Activity。另外，由于AMS记录了所有Activity的信息，当然能够主动的调度这些Activity，甚至在内存不足时，主动杀死后台的Activity。






## 补充
	
##### Dalvik和Java运行环境的区别：

DVM指dalivk的虚拟机。**每一个Android应用程序都在它自己的进程中运行，都拥有一个独立的Dalvik虚拟机实例。而每一个DVM都是在Linux 中的一个进程**。 
	
Android DVM:Dalvik是Google公司自己设计用于Android平台的Java虚拟机,每一个Dalvik 应用作为一个独立的Linux 进程执行。独立的进程可以防止在虚拟机崩溃的时候所有程序都被关闭。

1：Dalvik主要是完成对象生命周期管理，堆栈管理，线程管理，安全和异常管理，以及垃圾回收等等重要功能。 
	
2：Dalvik负责进程隔离和线程管理，每一个Android应用在底层都会对应一个独立的Dalvik虚拟机实例，其代码在虚拟机的解释下得以执行。

3：不同于Java虚拟机运行java字节码，Dalvik虚拟机运行的是其专有的文件格式Dex。

4:dex文件格式可以减少整体文件尺寸，提高I/o操作的类查找速度。

5:odex是为了在运行过程中进一步提高性能，对dex文件的进一步优化。

6：所有的Android应用的线程都对应一个Linux线程，虚拟机因而可以更多的依赖操作系统的线程调度和管理机制。　

7：有一个特殊的虚拟机进程Zygote，他是虚拟机实例的孵化器。它在系统启动的时候就会产生，它会完成虚拟机的初始化，库的加载，预制类库和初始化的操作。如果系统需要一个新的虚拟机实例，它会迅速复制自身，以最快的数据提供给系统。对于一些只读的系统库，所有虚拟机实例都和Zygote共享一块内存区域。

##### Task 和 Activity

- 每个Task都有自己的Activity Stack
- 一个Task就是指一些相关的Activity完成某个任务，这些Activity可能来自不同的Application

图片说明：

![](https://github.com/fengcj/read_note/tree/master/android/task.png)


更多细节见：

http://developer.android.com/guide/components/tasks-and-back-stack.html
http://www.cnblogs.com/stay/archive/2011/08/29/2157229.html
http://blog.csdn.net/veryitman/article/details/6547670








