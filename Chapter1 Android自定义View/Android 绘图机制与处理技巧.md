#Android绘图机制与自定义View

----------
##一.绘图基础
#####1.系统通过提供Canvas对象来实现绘图的功能。
*	**drawPoint画点**
*	**drawLine画线**
*	**drawRect矩形**
*	**drawVertices多边形**
*	**drawArc画弧**
*	**drawCircle画圆**

>**常用的API**

*	`setAntiAlias(true) //设置画笔的锯齿效果`
*	`setColor() //设置画笔的颜色`
*	`setTextSize() //设置画笔的字体大小`
*	`setStyle() //设置画笔的风格`
*	`setStrokeWidth() //设置空心边框的宽度`

#####通过设置Paint的风格就可以实现画出实心和空心的效果
*	`setStyle(Paint.Style.FILL); //效果为实心`
*	`setStyle(Paint.Style.STROKE); //效果为空心`


![]( https://github.com/hyr0318/AndroidStudyNotes/blob/master/Chapter1%20Android%E8%87%AA%E5%AE%9A%E4%B9%89View/Res/FklmMMFCily2A7s3XZoJsmREt4ZS.png )![]( https://github.com/hyr0318/AndroidStudyNotes/blob/master/Chapter1%20Android%E8%87%AA%E5%AE%9A%E4%B9%89View/Res/FgMxjIomFOnoR4LLOdlVhmP_VVbc.png )

#####2.通过XML绘图


>**Bitmap**
```
<?xml version="1.0" encoding="utf-8"?>
<bitmap xmlns:android="http://schemas.android.com/apk/res/android"
    android:src="@drawable/ic_launcher"
    >
</bitmap>
```