---
layout: post
title: context是什么
date: 2015-10-18
categories: blog
tags: [android,context]
description: context是一个访问application环境全局信息的接口。
---


2015年10月18日 21:56

Context是一个抽象类，其通用实现在ContextImpl类中。

Context是一个访问application环境全局信息的接口，通过它可以访问application的资源和相关的类，其主要功能如下：

- 启动Activity
- 启动和停止Service
- 发送广播消息(Intent)
- 注册广播消息(Intent)接收者
- 可以访问APK中各种资源(如Resources和AssetManager等)
- 可以访问Package的相关信息
- APK的各种权限管理