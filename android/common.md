## DisplayMetrics

Andorid.util 包下的DisplayMetrics 类提供了一种关于显示的通用信息，如显示大小，分辨率和字体。

使用如下：
        
        DisplayMetrics metrics = new DisplayMetrics();
        getWindowManager().getDefaultDisplay().getMetrics(metrics);

更多见：

- http://developer.android.com/reference/android/util/DisplayMetrics.html

补充之Android支持单位：

- px（像素）：屏幕上的点。 
- in（英寸）：长度单位。 
- mm（毫米）：长度单位。 
- pt（磅）：1/72英寸。 
- dp（与密度无关的像素）：一种基于屏幕密度的抽象单位。**在每英寸160点的显示器上，1dp = 1px。** 
- dip：与dp相同，多用于android/ophone示例中。 
- sp（与刻度无关的像素）：与dp类似，但是可以根据用户的字体大小首选项进行缩放。

**dp 与 px 之间的转换**

        px = dp * (dpi/160)  // 对应 在每英寸160点的显示器上，1dp = 1px，因为dpi=160px/1in=160
        dp = px / (dpi/160)


更多见：
- http://developer.android.com/guide/topics/resources/more-resources.html#Dimension