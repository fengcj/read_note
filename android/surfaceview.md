## 概念

SurfaceView是View类的子类，可以直接从内存或者DMA等硬件接口取得图像数据，是个非常重要的绘图视图。它的特性是：
**可以在主线程之外的线程中向屏幕绘图上。**这样可以避免画图任务繁重的时候造成主线程阻塞，从而提高了程序的反应速度。在游戏开发中多用到SurfaceView，游戏中的背景、人物、动画等等尽量在画布canvas中画出。

## 实现

### (1)继承类及接口
        extends SurfaceView implements SurfaceHolder.Callback
### (2)重写方法
        //在surface的大小发生改变时激发
         public void surfaceChanged(SurfaceHolder holder,int format,int width,int height){}　
        //在创建时激发，一般在这里调用画图的线程
         public void surfaceCreated(SurfaceHolder holder){}
        //销毁时激发，一般在这里将画图的线程停止、释放
         public void surfaceDestroyed(SurfaceHolder holder) {}　
### (3)SurfaceHolder
SurfaceHolder,surface的控制器，用来操纵surface。利用它来操作Canvas。

重要方法有：

        // 给SurfaceView当前的持有者一个回调对象。
        abstract void addCallback(SurfaceHolder.Callback callback);

        // 锁定画布，一般在锁定后就可以通过其返回的画布对象Canvas，在其上面画图等操作了。
        abstract Canvas lockCanvas();

        // 锁定画布的某个区域进行画图等..因为画完图后，会调用下面的unlockCanvasAndPost来改变显示内容。
        // 相对部分内存要求比较高的游戏来说，可以不用重画dirty外的其它区域的像素，可以提高速度。
        abstract Canvas lockCanvas(Rect dirty);

        // 结束锁定画图，并提交改变。
        abstract void unlockCanvasAndPost(Canvas canvas);

### (4)总结

继承SurfaceView并实现SurfaceHolder.Callback接口 ----> 

**SurfaceView.getHolder()获得SurfaceHolder对象**---->

SurfaceHolder.addCallback(callback)添加回调函数---->

SurfaceHolder.lockCanvas()获得Canvas对象并锁定画布----> 

Canvas绘画 ---->

SurfaceHolder.unlockCanvasAndPost(Canvas canvas)结束锁定画图，并提交改变，将图形显示。


## 引用
http://www.cnblogs.com/devinzhang/archive/2012/02/03/2337559.html