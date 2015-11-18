---
layout: post
title: ActionBar
date: 2015-10-20
categories: blog
tags: [android,ActionBar]
description: 
---


2015年10月20日 14:14

ActionBar有如下功能：

- 显示选项菜单的菜单项
- 使用程序图标作为返回Home主屏或向上的导航操作
- 提供交互式View作为Action View
- 提供给于Tab的导航方式，可用于切换多个Fragment
- 提供基于下拉的导航方式

##一、显示选项菜单的菜单项

获取ActionBar:Activity.getActionBar()

- show():显示ActionBar
- hide():隐藏ActionBar

**注意：**一旦关闭了ActionBar，就无法获取ActionBar,关闭ActionBar:在配置文件中配置主题为Xxx.NoActionBar或者Xxx.NoTitleBar,如@android:style/Theme.Holo.NoActionBar

设置ActionBar显示菜单项(Action Item)

从Android3.0之后，MenuItem新增了方法：setShowAsAction(int actionEnum)该方法设置是否将该菜单项显示在ActionBar上

参数值：

- HOW_AS_ACTION_ALWAYS:总是显示在ActionBar上
- SHOW_AS_ACTION_COLLAPSE_ACTION_VIEW:将该ActionBar折叠成普通菜单项
- SHOW_AS_ACTION_IF_ROOM:当ActionBar位置足够时才显示MenuItem
- SHOW_AS_ACTION_NEVER:不将该MenuItem显示在ActionBar上
- SHOW_AS_ACTION_WITH_TEXT:该MenuItem显示在ActionBar上，并显示该菜单项的文本

也可以在菜单的xml文件中<item>设置属性android:showAsAction**【推荐使用】**

启动程序图标导航

setDisplayShowTitleEnabled(true)Title是否显示

- setTitle():设置标题
- setSubTitle():设置子标题

setDisplayShowHomeEnabled(true):Home按钮是否显示

setHomeButtonEnabled(true):Home是否可以成为可点击按钮,如果可用，其ItemId为：android.R.id.home

setDisplayHomeAsUpEnabled(true)	Home是否以向上可点击按钮的形式显示

setDisplayUseLogoEnabled()Home是否显示Logo,默认为true,与android:logo连用

**建议：**使用该图标导航返回程序的入口

在进行acytivity跳转时：添加额外的Flag,将Activity栈中处于即将跳转的Activity之上的Activity弹出。

> intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);

**注意**

在Manifest配置文件中可以指定Activity的uiOptions属性为splitActionBarWhenNarrow，实现当屏幕为窄屏时分割ActionBar

在Activity中可以设置getWindow().requestFeature(Window.FEATURE_ACTION_BAR_OVERLAY);实现Activity与ActionBar重叠显示。

设置Activity为全屏：

- this.requestWindowFeature(Window.FEATURE_NO_TITLE);//去掉标题栏
- this.getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);//去掉信息栏

定制ActionBar

- bar.setDisplayOptions(ActionBar.DISPLAY_SHOW_CUSTOM);显示自己的布局文件
- bar.setCustomView(layout的布局文件);
- 获取View:actionBar.getCustomView()

添加Action View

- 定义Action Item时使用android:actionViewClass属性指定Action View的实现类
- 定义Action Item时使用android:actionProviderClass属性指定Action View对应的视图资源
- android:actionViewClass="android.widget.SearchView"显示搜索框
- android:actionProviderClass="android.widget.ShareActionProvider"显示分享

>	//获取分享组件
>	ShareActionProvider sap = (ShareActionProvider)menu.
>	
>		findItem(R.id.share).getActionProvider();
>		
>	Intent intent = new Intent();
>	
>	intent.setAction(Intent.ACTION_SEND);
>	
>	intent.setType("image/*");
>	
>	sap.setShareIntent(intent);

自定义ActionProvider类,重写hasSubMenu(),onPrepareSubMenu(SubMenu subMenu)

SearchView的使用

- 调用菜单的findItem()方法获取MenuItem对象。
- 调用MenuItem对象的getActionView()方法获取组件
- SearchView sv=(SearchView)menu.findItem(R.id.action_search).getActionView();
- android:iconifiedByDefault表示搜索图标是否在输入框内。true效果更加
- android:imeOptions设置IME options，即输入法的回车键的功能，可以是搜索、下一个、发送、完成等等。这里actionSearch表示搜索
- android:inputType输入框文本类型，可控制输入法键盘样式，如numberPassword即为数字密码样式
- android:queryHint输入框默认文本
- earchView.setSubmitButtonEnabled(true);编辑框后显示search按钮
- 添加事件监听器setOnQueryTextListener监听点击提交按钮和Text改变的。

实现Tab样式导航

- actionBar.setNavigationMode(ActionBar.NAVIGATION_MODE_TABS)
- actionBar.setDisplayShowHomeEnabled(false);
- actionBar.setDisplayShowTitleEnabled(false);
- Tab tab = actionBar.newTab();
- tab.setText()
- tab.setIcon()
- tab.setTabListener(TabListener);
- actionBar.addTab(tab);

实现DropDown样式

- actionBar.setNavigationMode(
- ActionBar.NAVIGATION_MODE_LIST);
- actionBar.setListNavigationCallbacks(adapter, OnNavigationListener);	

##自定义ActionBar

自定义主题,在activity中或者在application中配置：

- android:theme="@android:style/Theme.Holo.Light"
- @android:style/Theme.Holo.Light.DarkActionBar

自定义背景,编辑styles.xml文件，在里面加入一个自定义的主题，

>	<style name="customActionBarTheme" 
>	
>			parent="@android:style/Theme.Holo.Light">
>			
>			<item name="android:actionBarStyle">@style/myActionBar</item>
>			
>	</style>
>	
>	<style name="myActionBar" parent="@android:style/Widget.Holo.ActionBar">
>	
>			<item name="android:background">#f4842d</item>
>			
>		<!--tab的背景颜色-->
>		
>			<item name="android:backgroundStacked">#d27026</item>
>			
>	</style>

