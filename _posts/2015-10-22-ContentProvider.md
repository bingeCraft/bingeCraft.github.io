---
layout: post
title: ContentProvider
date: 2015-10-22
categories: blog
tags: [android,ContentProvider]
description: 
---


2015年10月22日 16:23

内容提供器：提供操作的数据的标准

重写6个方法：

- boolean onCreate()
- Cursor query(Uri uri, String[] projection, String selection,
			String[] selectionArgs, String sortOrder)
- String getType(Uri uri)
- Uri insert(Uri uri, ContentValues values)
- delete(Uri uri, String selection, String[] selectionArgs)
- update(Uri uri, ContentValues values, String selection,
			String[] selectionArgs)

配置ContentProvider

- android:name=".FirstProvider"
- android:authorities="com.binge.first"	主机
- android:exported="true"

#操作数据的程序

>	private ContentResolver cr = getContentResolver();		//操作ContentProvider提供的数据
>
>	private Uri uri = Uri.parse("content://com.binge.first");

增add

>	ContentValues values = new ContentValues();
>
>	values.put("name", "zhangsan");
>
>	cr.insert(url, values);

#提供数据的程序



















