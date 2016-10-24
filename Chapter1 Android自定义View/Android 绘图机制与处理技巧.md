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
通过引用图片，直接将图片转化成Bitmap。

>**Shape**

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <!-- 圆角 -->
    <corners
        android:radius="1dp"
        android:topLeftRadius="1dp"
        android:topRightRadius="1dp"
        android:bottomLeftRadius="1dp"
        android:bottomRightRadius="1dp"/>
    <!-- 渐变 -->
    <gradient
        android:angle="45"
        android:startColor="#FFF"
        android:endColor="#000"/>
    <!-- 间隔 -->
    <padding
        android:left="1dp"
        android:top="1dp"
        android:right="1dp"
        android:bottom="1dp"/>
    <!-- 大小 -->
    <size
        android:width="1dp"
        android:height="1dp"/>
    <!-- 填充 -->
    <solid
        android:color="#FFF"
        />
    <!-- 描边 -->
    <stroke
        android:width="2dp"
        android:color="#000"
        android:dashWidth="1dp"
        android:dashGap="1dp"
        />
</shape>
```

*	填充：设置填充的颜色

*	间隔：设置四个方向上的间隔

*	大小：设置大小

*	圆角：同时设置五个属性，则Radius属性无效

	`android:Radius="20dp" `                          设置四个角的半径

	`android:topLeftRadius="20dp"  `            设置左上角的半径
`android:topRightRadius="20dp" `          设置右上角的半径
`android:bottomLeftRadius="20dp"  `    设置右下角的半径
`android:bottomRightRadius="20dp"  `  设置左下角的半径

*	描边：dashWidth和dashGap属性，只要其中一个设置为0dp，则边框为实现边框

	`android:width="20dp"  `                             设置边边的宽度

	`android:color="@android:color/black"`  设置边边的颜色

	`android:dashWidth="2dp"  `                       设置虚线的宽度

	`android:dashGap="20dp"        `                  设置虚线的间隔宽度

*	渐变：当设置填充颜色后，无渐变效果。angle的值必须是45的倍数（包括0），仅在type="linear"有效，不然会报错。android:useLevel 这个属性不知道有什么用。

>Layer

```
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <item android:drawable="@drawable/ic_launcher"/>

    <item
        android:drawable="@drawable/ic_launcher"
        android:left="10dp"
        android:top="10dp"
        android:right="10dp"
        android:bottom="10dp"

        />
</layer-list>

```
实现图层的效果，图片会一次叠加

>Selector

```
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">

    <item android:drawable="@drawable/ic_launcher"/>

    <!-- 没有焦点时的背景图片-->
    <item android:state_window_focused="false" android:drawable="@drawable/ic_launcher" />

    <!--非触摸模式下获得焦点并单击时的背景图片 -->
    <item android:state_focused="true"
        android:state_pressed="true"
        android:drawable="@drawable/ic_launcher"/>

    <!--触摸模式下单击图片时的背景图片 -->
    <item android:state_focused="false"
        android:state_pressed="true"
        android:drawable="@drawable/ic_launcher"/>

    <!--选中时的图片背景 -->
    <item android:state_selected="true"
        android:drawable="@drawable/ic_launcher"/>

    <!--获得焦点时的图片背景 -->
    <item android:state_focused="true"
        android:drawable="@drawable/ic_launcher"/>
</selector>
```
