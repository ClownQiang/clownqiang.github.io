---
layout: post
title: AndroidStudio坑爹错误之一
comments: true
categories: "Android"
---

---
前段时间被这个坑爹错误折腾了好长时间，废话不多说直接把它拉出来枪毙~~~~

###错误信息

```
UNEXPECTED TOP-LEVEL EXCEPTION:
com.android.dx.cf.iface.ParseException: class name (com/companyname/UI/BuildConfig) does not match path (com/companyname/ui/BuildConfig.class) at 
```

###解决方案

- AndroidStudio clean项目，rebuild项目

你没有看错就是这么简单，但是你可能在logcat里面看到其他信息，比如这个：

```
UNEXPECTED TOP-LEVEL EXCEPTION
```
如果你将这个信息Google一下，就会发现，有各种各样的方案，比如说有重复编译jar包等等，我们不排除有这个可能。

所以如果碰上上面的问题，可以先clean，rebuild的尝试一下先~~~