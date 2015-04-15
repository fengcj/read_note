## What is a BroadcastReceiver

BroadcastReceiver，广播接收者，它是一个系统全局的监听器，用于监听系统全局的Broadcast消息，所以它可以很方便的进行系统组件之间的通信。

BroadcastReceiver虽然是一个监听器，但是它和之前用到的OnXxxListener不同，那些只是程序级别的监听器，运行在指定程序的所在进程中，当程序退出的时候，OnXxxListener监听器也就随之关闭了，但是BroadcastReceiver属于系统级的监听器，它拥有自己的进程，只要存在与之匹配的Broadcast被以Intent的形式发送出来，BroadcastReceiver就会被激活。

虽然同属Android的四大组件，BroadcastReceiver也有自己独立的声明周期，但是和Activity、Service又不同。当在系统注册一个BroadcastReceiver之后，每次系统以一个Intent的形式发布Broadcast的时候，系统都会创建与之对应的BroadcastReceiver广播接收者实例，并自动触发它的onReceive()方法，当onReceive()方法被执行完成之后，BroadcastReceiver的实例就会被销毁。虽然它独自享用一个单独的进程，但也不是没有限制的，如果BroadcastReceiver.onReceive()方法不能在10秒内执行完成，Android系统就会认为该BroadcastReceiver对象无响应，然后弹出ANR（Application No Response）对话框，所以不要在BroadcastReceiver.onReceive()方法内执行一些耗时的操作。

如果需要根据广播内容完成一些耗时的操作，一般考虑通过Intent启动一个Service来完成该操作，而不应该在BroadcastReceiver中开启一个新线程完成耗时的操作，因为BroadcastReceiver本身的生命周期很短，可能出现的情况是子线程还没有结束，BroadcastReceiver就已经退出的情况，而如果BroadcastReceiver所在的进程结束了，该线程就会被标记为一个空线程，根据Android的内存管理策略，在系统内存紧张的时候，会按照优先级，结束优先级低的线程，而空线程无异是优先级最低的，这样就可能导致BroadcastReceiver启动的子线程不能执行完成。

###summary
- 系统级别的监听器,拥有自己的进程
- 某个app发布Broadcast，系统会生成对应的Receiver，主要逻辑在onReceiver()方法内
- 耗时操作应该使用Service完成，而不应该在Receiver中开启新线程

## Different Type of BroadCastReceiver

上面提到，当系统以一个Intent的形式发送一个Broadcast出去之后，所有与之匹配的BroadcastReceiver都会被实例化，但是这里是有区别的，根据Broadcast的传播方式区别，在系统中有如下两种Broadcast：

普通广播：Normal Broadcase，它是完全异步的，也就是说，在逻辑上，当一个Broadcast被发出之后，所有的与之匹配的BroadcastReceiver都同时接收到Broadcast。优点是传递效率比较高，但是也有缺点，就是一个BroadcastReceiver不能影响其他响应这条Broadcast的BroadcastReceiver。

有序广播：Ordered Broadcast，它是同步执行的，也就是说有序广播的接收器将会按照预先声明的优先级依次接受Broadcast，是链式结构，优先级越高（-1000~1000），越先被执行。因为是顺序执行，所有优先级高的接收器，可以把执行结果传入下一个接收器中，也可以终止Broadcast的传播（通过abortBroadcast()方法），一旦Broadcast的传播被终止，优先级低于它的接收器就不会再接收到这条Broadcast了。
　　虽然系统存在两种类型的Broadcast，但是一般系统发送出来的Broadcast均是有序广播，所以可以通过优先级的控制，在系统内置的程序响应前，对Broadcast提前进行响应。这就是市场上一些拦截器类（如：短信拦截器、电话拦截器）的软件的原理。
　　
###summary
- 普通广播，有序广播
- abortBroadcast()停止广播
- 有序广播，优先级设置，拦截器类app的原理

## How to send a broadcast

上面已经介绍了系统中两种不同的Broadcast，而根据Broadcast传播的方式，Context提供了不同的方法来发布它们：

sendBroadcast()：发送普通广播。

sendOrderedBroadcast()：发送有序广播。

以上两个方法都有多个重载方法，根据不同的场景使用，最简单的莫过于直接传递一个Intent来发送一个广播。

### summary
- sendBroadcast()
- sendOrderBroadcast()


## How to use a BroadcastReceiver

BroadcastReceiver本质上还是一个监听器，所以使用BroadcastReceiver的方法也是非常简单，只需要继承BroadcastReceiver，在其中重写onReceive(Context context,Intent intent)即可。一旦实现了BroadcastReceiver，并部署到系统中后，就可以在系统的任何位置，通过sendBroadcast、sendOrderedBroadcast方法发送Broadcast给这个BroadcastReceiver。

但是仅仅继承BroadcastReceiver和实现onReceive()方法是不够的，同为Android系统组件，它也必须在Android系统中注册，注册一个BroadcastReceiver有2种方式：

(1)在代码中使用Content.registerReceiver(BroadcastReceiver receiver, IntentFilter filter)进行注册，在使用完毕使用Content.unregisterReceiver(BroadcastReceiver receiver)方法进行注销。

(2)使用清单文件AndroidManifest.xml注册，在<application/>节点中，使用<receiver/>节点注册，并用android:name属性中指定注册的BroadcastReceiver对象，一般还会通过<Intent-filter/>指定<action/>和<category/>，并在<Intent-filter/>节点中通过android:priority属性设置BroadcastReceiver的优先级，在-1000~1000范围内，数值越到优先级越高。
 　

虽然Android系统提供了两种方式注册BroadcastReceiver，但是一般在实际开发中，还是会使用清单文件进行注册： 

    <receiver android:name="cn.bgxt.Broadcastdemo.Basic.BasicBroadcast">
            <intent-filter android:priority="100">
                 <action android:name="cn.bgxt.Broadcastdemo.Basic.broadcast"/>
             </intent-filter>            
    </receiver>

### summmary
- 继承BroadcastReceiver,重写onReceiver(Context context,Intent intent)
- 静态注册，写在AndroidManifest.xml文件中
- 动态注册，使用Content.register(BroadcastReceiver receiver,IntentFilter filter)以及Content.unregisterReceiver(BroadcastReceiver receiver)