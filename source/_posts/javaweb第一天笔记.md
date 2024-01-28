---
title: javaweb第一天笔记
author: 少年
tags:
  - JAVAWEB
categories: 笔记篇
abbrlink: note
date: 2021-01-24 20:00:00
---

# JAVAWEB

## 1、基本概念

### 1.1、前言

web开发:

- web	网页的意思	https://www.baidu.ml
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化！
- 动态web
  - 淘宝、京东，几乎所有的网站
  - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同！
  -  技术栈：Servlet/jsp,asp,php

在java中，动态web资源开发的技术统称为javaweb

### 1.2、web应用程序

- web应用程序：可以提供浏览器访问的程序

- a.html	b.html...多个web资源，这些web资源可以被外界访问，对外界提供服务

- 你们能访问到的任何一个网页或资源，都存在与这个世界的某一个角落的计算机上
- URL:统一资源定位器
- 这些web资源会统一的放在同一个文件夹下，web应用程序--》Tomcat（服务器）
  - 一个web应用程序由多部分组成（静态、动态）
  - html、css、js
  - Servlet/jsp
  - java程序
  - jar包
  - 配置文件（properties）

web应用程序编写完成后，若想提供给外界访问，需要一个服务器统一管理

### 1.3、静态资源

- .html（.htm)这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取

![image-20210124114356921](https://gitee.com/kuiler/imgaes/raw/master/img/image-20210124114356921.png)

- 静态web存在的缺点
  - web页面无法动态更新，所有用户看到的信息都是一样
    - 轮播图、点击效果：伪动态
    - JavaScript
    - VBScript
  - 无法与数据库进行交互（数据无法持久化）