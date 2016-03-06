---
layout: post
title: 来吧，Android Studio
comments: true
categories: "Android"
---

---
对于很多写android初次使用的ADT便是eclipse，这货功能十分强大，主要归功于它的各种强大的插件，即使我先后使用了Intellij Idea，Android Studio也没有把eclipse丢掉，因为里面各种插件让我放不下。

使用了一年的Intellij IDEA后，Google发布了新的ADT---Android Studio，开始对他完全无爱，使用过Intellij IDEA的都知道，Android Studio就是 IDEA的翻版，但是随着Android Studio的不断完善，配合上强大的Gradle，关于Gradle是什么，可以简单介绍一下。

##Gradle(以下来自[官网](http://www.gradle.org))

>Gradle is build automation evolved. Gradle can automate the building, testing, publishing, deployment and more of software packages or other types of projects such as generated static websites, generated documentation or indeed anything else.

Gradle是自动化构建工具。Gradle可以自动构建，测试，发布，部署软件包或其他类型的项目，如生成静态网站，生成的文档或实际上任何东西。简单的说有了Gradle你的项目依赖再也不是难题了。

更加详细可以直接戳[百度百科](http://baike.baidu.com/view/9916271.htm?fr=aladdin)或者[Wikipedia](http://en.wikipedia.org/wiki/Gradle)

##为什么使用Android Studio
众所周知，习惯了一个ADT，如果更改会十分的麻烦，不仅开始效率不高，而且可能换了之后效率还是没有变化。随着我们看见Android Studio的不断更新，我们发现Google是想将其打造成为一个类似XCode的专属ADT。而且里面添加的功能也不再是eclipse的几个插件能够替代的。
###好用XML即时UI展示
没图我说个QB
![XML编辑UI同步展示](http://clownqiang.qiniudn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202014-09-13%20%E4%B8%8B%E5%8D%884.09.26.png)
看见这个是不是感觉终于解放了，再也不用Tab边写边看UI了。更加省心的是，大家都知道android有多种分辨率，如果要看在其他分辨率的手机上面的显示效果，你只需要在右边更换你需要的手机分辨就可以看到，方便的不是一点点。
###更加方便的新文件创建
![文件创建的细化](http://clownqiang.qiniudn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202014-09-13%20%E4%B8%8B%E5%8D%884.28.09.png)
过去在eclipse上面我们只能创建XML，java文件等非常局限，现在在Android Studio可以创建的文件细化到了每个组件，不仅有熟悉的Fragment，Activity，Service还有Google相关服务，是不是很方便，再也不用在eclipse的AndroidManifast中手动添加Activty和Service了
###更加好的性能和使用体验
过去eclipse经常出现的无响应，莫名的红色小叉号。。。这些都成为历史，现在Android Studio不仅性能比以前更好，不会出现风扇狂转的现象，而且更加稳定。智能的提示也是使用Android Studio的一大优势，非比寻常的提示速度是其他ADT无法达到的。
###插件管理更加方便
![插件管理](http://clownqiang.qiniudn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202014-09-13%20%E4%B8%8B%E5%8D%884.36.22.png)
虽然没有eclipse那么多的插件，但是拥有非常方便的插件管理，只需要点一点就可以下载你需要的插件，同时有git和svn，代码的管理也是相当方便。
###新的Google开发集成
更好以及更快的体验Google新推开发SDK，刚刚推出的Android Wear以及Android TV和新的Android L已经开发尝试，无疑使用官方推出的ADT肯定能更好的尝试这些新东西。

##来吧Android Studio！！！
[Android Studi官方下载](https://developer.android.com/sdk/installing/studio.html) 可能下载的速度很慢，原因大家都懂得，具体方法还是百度吧！！！