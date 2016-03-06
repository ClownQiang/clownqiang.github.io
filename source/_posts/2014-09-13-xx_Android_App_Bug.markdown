---
layout: post
title: 关于XX网Android客户端开发发现的问题
comments: true
categories: "Android"
---

---
###手机拍照上传

如果在Fragment中调用拍照，直接用startActivityForResult，不要加上getActivity，同时还有在onActivityResult中关于拍照上传要注意使用resultCode，判断取消状态

###关于使用shape花虚线出现实线

这个问题折腾一段时间，发现这个是一个系统的bug，只要将layer-type设置为software即可

###关于EditText默认不弹出软件

这里有多种方法，这里说的方法，是EditText不获取到焦点的，有的方法是EditText获取了焦点的但是没有弹出而已。这里说的就是，将EditText的直接父级空间设置：
```
android:focusable="true"
android:focusableInTouchMode="true"
```