---
layout: post
title: Intellij IDEA修改包名
comments: true
categories: "Android"
---

---
1.首先将AndroidManifest的Package Name重命名（快捷键shift+F6或者右键Refctor然后Rename）这时Package Name就改变了，但是Src的文件名还没变
2.如果修改Src文件名，可以用同样的方法修改AndroidManifest中activity的命名。具体过程下面示范：


####修改前
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.nostra13.universalimageloader.sample"
    android:versionCode="39"
    android:versionName="1.9.4" >

...
    <application
        android:name=".UILApplication"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
		android:allowBackup="false">
        <activity
            android:name=".activity.HomeActivity"
            android:label="@string/app_name" >
            ...
        </activity>
     </application>
</manifest>
```

####修改package
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.clownqiang.test.sample"  //这里修改为
    android:versionCode="39"
    android:versionName="1.9.4" >

...
    <application
        android:name=".UILApplication"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
		android:allowBackup="false">
        <activity
            android:name="com.nostra13.universalimageloader.activity.HomeActivity"  //package修改时，src文件名不变，所以这里的.activity.HomeActivity变为绝对路径
            android:label="@string/app_name" >
            ...
        </activity>
     </application>
</manifest>
```

####修改activity的命名，同时修改src
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.clownqiang.test.sample"  
    android:versionCode="39"
    android:versionName="1.9.4" >

...
    <application
        android:name=".UILApplication"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:allowBackup="false">
        <activity
            android:name="com.clownqiang.universalimageloader.activity.HomeActivity"  //这里将光标移至原来的nostra13，然后rename为clownqiang，然后同样方法再修改universalimageloader，最后完成
            android:label="@string/app_name" >
            ...
        </activity>
     </application>
</manifest>
```
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.clownqiang.test.sample"  
    android:versionCode="39"
    android:versionName="1.9.4" >

...
    <application
        android:name=".UILApplication"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:allowBackup="false">
        <activity
            android:name=".activity.HomeActivity"  //这里就是 android:name＝"com.clownqiang.test.sample.activity.HomeActivity"
            android:label="@string/app_name" >
            ...
        </activity>
     </application>
</manifest>
```

###Ok,完成啦