---
layout: post
title: android常用组件
date: 2015-10-18
categories: blog
tags: [android,组件]
description: 
---


2015年10月18日 22:56

#TextView

在界面上显示文本，没有编辑功能

- singleLine 是否只显示一行
- ellipsize  设置文字缩略方式	值为marquee时，需要配合marqueeRepeatLimit、focusable、focusableInTouchMode属性实现跑马灯效果
- textAllCaps  文字内容大写
- shadowColor  字体阴影颜色
- shadowDx    字体阴影x轴偏移
- shadowDy    字体阴影y轴偏移
- shadowRadius 字体阴影模糊程度，数字越大越模糊
- autoLink 设置文本内容中的邮箱、电话等链接

#CheckedTextView

继承了TextView,增加了check功能

- checked="true" 是否被选
- checkMark="?android:attr/listChoiceIndicatorMultiple" 设置勾选状态
- clickable="true"是否可以被点击
- toggle()方法：用于切换选择的状态。

#EditText

继承了TextView,可以编辑内容的文本框

- hint	编辑框提示文字
- ems	编辑框默认字符长度，当设置wrap_content时使用
- inputType 限制编辑框输入的内容(可以设置为密码框)

#Button

继承了TextView

- 使用selecter文件实现Button点击和释放时显示不同效果
  android:state_pressed="true"
  android:drawable="@color/black"
  android:state_pressed="false"
  android:drawable="@color/gray"

#RadioButton与RadioGroup

RadioButton继承了Button，RadioGroup继承了LiearLayout可以设置排列方式，在onCreate()方法中，为RadioGroup添加RadioGroup.OnCheckedChangeListener监听器，实现选择不同单选按钮。

#CheckBox

继承了Button，在onCreate()方法中，为每个CheckBox添加CompoundButton.OnCheckedChangeListener监听器，实现选择不同多选按钮。

#Switch

继承了Button，在onCreate()方法中，为switch添加CompoundButton.OnCheckedChangeListener监听器，实现通过开关效果

特有属性：

- android:textOff 设置当前按钮关闭时显示的文本
- android:textOn 设置当前按钮打开时显示的文本
- android:thumb 使用自定义的Drawable绘制开关按钮

#ToggleButton

继承了Button， 在onCreate()方法中，为ToggleButton添加CompoundButton.OnCheckedChangeListener监听器

##AnalogClock与DigitalClock

模拟时钟和数字时钟

#Chronometer

继承自TextView，并不显示当前时间，是一个计时器

- android:format="计时:%s"
- setBase(long):设置开始时间
- start()：启动定时器
- stop():停止定时期
- SystemClock.elapsedRealtime()获取系统当前的时间，是一个工具类

#ImageView

scaleType，设置不同的拉伸方式

- android:scaleType="center"，以原图的几何中心点和ImagView的几何中心点为基准,按图片的原来size居中显示，不缩放，当图片长/宽超过View的长/宽，则截取图片的居中部分显示ImageView的size.当图片小于View 的长宽时，只显示图片的size,不剪裁。
- android:scaleType="centerCrop"，以原图的几何中心点和ImagView的几何中心点为基准,按比例扩大(图片小于View的宽时)图片的size居中显示，使得图片长 (宽)等于或大于View的长(宽),并按View的大小截取图片。当原图的size大于ImageView时，按比例缩小图片，使得长宽中有一向等于ImageView,另一向大于ImageView。实际上，使得原图的size大于等于ImageView的长(宽)。
- android:scaleType="centerInside"，以原图的几何中心点和ImagView的几何中心点为基准，将图片的内容完整居中显示，通过按比例缩小原来的size使得图片长(宽)等于或小于ImageView的长(宽)。
- android:scaleType="fitCenter"，把图片按比例扩大(缩小)到View的宽度，居中显示
- android:scaleType="fitEnd"，把图片按比例扩大(缩小)到View的宽度，显示在View的下部分位置
- android:scaleType="fitStart"，把图片按比例扩大(缩小)到View的宽度，显示在View的上部分位置
- android:scaleType="fitXY"，把图片按照指定的大小在View中显示，拉伸显示图片，不保持原比例，填满View
- android:scaleType="matrix"，用matrix来绘制（默认）。

#ProgressBar

配置ProgressBar，为其设置style属性：

- @android:style/Widget.ProgressBar.Horizontal水平进度条
- @android:style/Widget.ProgressBar  中号圆形进度条
- @android:style/Widget.ProgressBar.Inverse 中号圆形进度条
- @android:style/Widget.ProgressBar.Small	小号圆形进度条
- @android:style/Widget.ProgressBar.Small.Inverse小号圆形进度条
- @android:style/Widget.ProgressBar.Large	大号圆形进度条
- @android:style/Widget.ProgressBar.Large.Inverse大号圆形进度条

也可以使用attr的属性：

- style="?android:attr/progressBarStyle" 
- style="?android:attr/progressBarStyleHorizontal" 
- style="?android:attr/progressBarStyleInverse" 
- style="?android:attr/progressBarStyleLarge" 
- style="?android:attr/progressBarStyleLargeInverse" 
- style="?android:attr/progressBarStyleSmall" 
- style="?android:attr/progressBarStyleSmallInverse

**注意:**当进度条控件所在的界面背景颜色为白色时，需要使用带有Inverse参数的style属性，否则进度条将看不见。

水平进度条可以设置max、progress、secondaryProgress等属性
- max代表进度条的最大进度
- progress代表当前进度值
- secondaryProgress代表第二进度值，相当缓存值

在Java代码中控制进度条:

- setProgress(int)：设置水平进度条的值
- getMax():获取水平进度条的最大值
- incrementProgressBy(int),设置进度条的进度增加或减少， 当参数为正数时进度增加，为负数时进度减少。

设置progressDrawable属性，使用layer-list图片资源，用来自定义水平进度条的样式。

>	<layer-list>
>
>	<!-- 设置轨道的背景 -->
>
>	<item android:id="@android:id/background" 
>
>			android:drawable="@drawable/bar_bg"></item>
>
>	<!-- 设置轨道上第二进度值部分的样式 -->
>
>	<item android:id="@android:id/secondaryProgress"
>	
>			android:drawable="@drawable/second"></item>
>			
>	<!-- 设置轨道上已完成部分的样式 -->
>	
>	<item android:id="@android:id/progress"
>	
>		android:drawable="@drawable/progress"></item>
>		
>	</layer-list>

**注意：**也可以参照源码去完成自定义样式的写法。

显示在标题上的进度条

- 1.调用Activity的requestWindowFeature()方法，
    该方法根据传入的参数可启用特定的窗口特征，
    例如传入Window.FEATURE_INDETERMINATE_PROGRESS
    则显示不带进度的进度条。
    传入Window.FEATURE_PROGRESS则显示带进度的进度条。
- 2.调用Activity的
    setProgressBarIndeterminateVisibility(boolean)
    或setProgressBarVisibility(boolean)
    方法即可控制进度条的显示和隐藏。
	
#SeekBar

拖动条通常用于对系统的某种数值进行调节，比如调节音量等。

- thumb	代表使用自定义图片显示拖动块
- style="@android:style/Widget.SeekBar"这是之前的样式，android每个版本都有自己的样式，默认情况下就显示当前版本的样式。
- max,progress,progressDrawable
- 为seekbar添加SeekBar.OnSeekBarChangeListener监听器，
  监控其进度值变化。
  监听器中的第三个参数：
  fromUser用来告诉函数当前进度值的改变是否是由用户执行的
  
#RatingBar

星级评分，相关属性：

- android:numStarts设置星级评分总共有多个星级
- android:rating设置星级评分条默认的星级
- android:stepSize设置每次至少需要改变多少个星级
- 为Ratingbar添加RatingBar.setOnRatingBarChangeListener监听器。监控其分数的变化

#CalendarView

日历视图在android3.0之后才有的。日历视图的XML属性 :

- 设置样式 : android:dateTextAppearance, 设置日期文字显示样式;
- 设置首日 : android:firstDayOfWeek, 设置星期几是每周的第一天, 默认是周日;
- 选中颜色 : android:focusedMonthDateColor, 设置选中日期所在月份日期颜色;
- 最大日期 : android:maxDate, 设置支持的最大日期, 以 mm/dd/yyyy 格式指定;
- 最小日期 : android:minDate, 设置支持的最小日期, 以 mm/dd/yyyy 格式指定;
- 选中竖线 : android:selectedDateVerticalBar, 设置被选中日期两边的竖线Drawable, 即R.drawable.int资源;
- 选周颜色 : android:selectedWeekBackgroundColor, 设置被选中日期所在周的背景颜色;
- 周数显示 : android:showWeekNumber, 设置是否显示周数;
- 设置周数 : android:shownWeekCount, 设置该日历组件一共显示几周;
- 未选颜色 : android:unfocusedMonthDateColor, 设置未被选中的月份的日期颜色;
- 星期样式 : android:weekDayTextAppearance, 设置星期几的文字样式;
- 周号颜色 : android:weekNumberColor, 设置周编号的颜色;
- 周分割色 : android:weekSeparatorLineColor, 设置周分隔线颜色;
- 添加setOnDateChangeListener(OnDateChangeListener)的监听器，监听用户选择的时间。

#DatePicker、TimePicker与NumberPicker

配置DatePicker

- calendarViewShown设置是否显示CalenderView
- startYear设置显示的开始年份
- endYear	设置显示的结束年份
- maxDate	设置可显示的最大时间，格式为mm/dd/yyyy
- minDate	设置可显示的最小时间，格式为mm/dd/yyyy
- spinnersShown 设置是否显示Spinner日期选择器
- 调用init()方法对DatePicker进行初始化参数为初始化年、初始化月、初始化日。
- OnDateChangedListener借助于Calendar来初始化年，月，日

配置TimePicker，为其添加setOnTimeChangedListener，可调用setIs24HourView(boolean)设置是否为24小时显示

配置NumberPicker，通过setMaxValue(),setMinValue()及setValue()添加setOnValueChangedListener

#ScrollView与HorizontalScrollView

**注意：**该控件只能添加一个子控件

#AlertDialog

提供了4种常用的对话框：

1、AlertDialog:功能最丰富，实际应用最广的对话框，最常用的。

AlterDialog使用步骤：

- 创建AlertDialog.Builder对象
- setTitle()或setCustomTitle()方法设置标题
- setIcon()方法设置图标
- setMessage 设置最简单的文本提示信息
- setItems	设置内容为简单列表项,调用该方法时需要传入一个数组或者数组资源的资源ID
- setSingleChoiceItems  设置内容为单选的列表项,可以传入数组，资源id，Cursor,ListAdapter作为参数
- setMultiChoiceItems  设置内容为多选的列表项
- setAdapter 设置内容为自定义列表项
- setView	 设置内容为任意类型的View，完成一个登录对话框的界面
- setPositiveButton(),setNegativeButton或setNeutralButton()方法添加多个按钮
- setCancelable(false):设置是否可以取消对话框，默认为true,点击按钮，回退健或者点击任何一个地方都会关闭对话框。需要在create之前调用。
- create()方法创建AlterDialog对象
- 调用AlertDialog的show()方法显示对话框
- AlertDialog.dismiss():取消对话框
- AlertDialog.cancel():取消对话框

2、ProgressDialog:进度对话框，这个对话框只是对简单进度条的封装

- setTitle("提示信息");
- setMessage(charSequence)设置对话框里显示的消息
- setMax(int)设置对话框中进度条的最大值
- setProgressStyle(ProgressDialog.STYLE_HORIZONTAL)设置对话框里进度条的风格
- setIndeterminate(boolean)设置进度条是否显示不明确值
- p.dismiss()关闭对话框

3、DatePickerDialog:日期选择对话框，这个对话框只是对DatePicker的包装

- 通过new关键字创建实例，调用show()将对话框显示出来
- 绑定监听器，从而通过监听器获取用户设置的事件

4、TimePickerDialog:时间选择对话框，这个对话框只是对TimePicker的包装

- 通过new关键字创建实例，调用show()将对话框显示出来
- 绑定监听器，从而通过监听器获取用户设置的事件

**补充：**还有其他的方式也可以完成对话框

1)在需要设置成对话框的Activity在AndroidManifest.xml中配置android:theme="@android:style/Theme.Dialog"

2)创建PopWindow对象,为其设置布局内容与宽度、高度,调用pop.showAsDropDown(View)将PopupWindow作为View组件以下拉组件显示出来，或者调用showAtLocation()方法将PopupWindow在指定位置显示出来

- 第一个参数指定PopupWindow的锚点view，即依附在哪个view上。
- 第二个参数指定起始点
- 第三，四个参数设置以起始点的右下角为原点，向向右、下各偏移量。
