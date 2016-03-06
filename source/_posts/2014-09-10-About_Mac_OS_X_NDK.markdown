---
layout: post
title: 关于在Mac OS X使用NDK（入门级）
comments: true
categories: "Android"
---

---
###下载Mac OS X版本的NDK
在android官网NDK页面可以看到相关信息，可以[戳这里](http://developer.android.com/tools/sdk/ndk/index.html)，进入这个页面可以看见下载版本分为两个，一个为32-bit，一个为64-bit，到底怎么看，可以再终端输入uname -v，如果出现RELEASE_X86_64，表示为64-bit，如果不清楚，可以[戳这里](http://www.cnblogs.com/wanyakun/archive/2012/02/24/3403288.html)

###准备JNI
- 新建一个AndroidApplication Project，命名为HelloNDK，并在其工程根目录下手动建一个jni目录,在其目录下创建一个Android.mk编译配置文件和hello-ndk.c源文件。

```
	Android.mk
	
	LOCAL_PATH := $(call my-dir)  
	include $(CLEAR_VARS)  
	LOCAL_MODULE    := hello-ndk  
	LOCAL_SRC_FILES := hello-ndk.c  
	include $(BUILD_SHARED_LIBRARY)  
```
```
	hello-ndk.c

	#include <string.h>  
	#include <jni.h>    
	jstring Java_com_example_HelloNDK_MyActivity_stringFromJNI(JNIEnv* env, jobject thiz)  
	{  
    	return (*env)->NewStringUTF(env, "Hello from JNI!");  
	} 
```
在这里jsstring后面Jave_com_example_HelloNDK（这个是包名），stringFromJNI是方法名

- 编译文件将下载NDK包解压到指定位置，将路径加入到.bash_profile（或者使用zsh为.zshrc），到project的jni目录下，使用命令ndk-build，如果成功会出现以下文字

```
	[armeabi] Compile thumb  : hello-ndk <= hello-ndk.c
	[armeabi] SharedLibrary  : libhello-ndk.so
	[armeabi] Install        : libhello-ndk.so => libs/armeabi/libhello-ndk.so
```
###在java文件中引用JNI
```
	MyActivity.java
	
	package com.example.HelloNDK;//包名

	import android.app.Activity;
	import android.os.Bundle;
	import android.widget.TextView;

	public class MyActivity extends Activity {
    	/**
     	* Called when the activity is first created.
     	*/
    	@Override
    		public void onCreate(Bundle savedInstanceState) {
        		super.onCreate(savedInstanceState);

        	TextView textView = new TextView(this);
        	textView.setText(stringFromJNI());
        	setContentView(textView);
    	}

    	public native String stringFromJNI();
    	public native String unimplementedStringFromJNI();

    	static {
        	System.loadLibrary("hello-ndk");
    	}
	}
```
注意：Java代码中使用native关键字标示方法是JNI库中的函数，虽然上一步编译出来的JNI库的名字是libhello-ndk.so，但是按照规范，System.loadLibrary中的参数是去掉lib和.so的。

##如果运行程序出现Hello from JNI!表示成功了，骚年！！！