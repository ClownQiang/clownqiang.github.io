---
layout: post
title: Android第三方平台分享集成挖坑（Umeng篇）
comments: true
categories: "Android"
---

---
关于android中的第三方平台接入一直是一个让人又爱又恨的东西，令人应接不暇的各种平台都说自己整合的好，方便，但是着手用了之后，各种问题都来。网上一般看到最多的移动开发者服务平台有友盟，ShareSDK，以及Avos Cloud，这几个平台我都有使用过，都有自己的优缺点，这个就最近使用的Umeng来进行一点坑的挖掘。

关于Umeng，就它的对功能的整合程度，已经算是很不错的了，常见的第三方平台都能看见，具体的怎么使用就不用说了，文档可以直接[戳这里](http://dev.umeng.com/social/android/share/quick-integration)。

###下面我主要说一下我遇到的坑
####1.关于人人网一直显示invalid redirect_ui
>如果你是使用的Umeng作为集成SDK，官方说要填写正确的redirect_uri，但是这样问题是无法解决的，这里要将应用的基本信息中的根域名设置为* sns.whalecloud.com*

####2.关于QQ空间分享中的网址链接到Umeng
>这个是Umeng的默认，这里需要设置 QZoneShareContent的setTargetUrl这里的Url设置为你想跳转的网址即可

####3.为什么我的微信分享怎么点都没有反应，既不报错也不出现分享窗口
>这个最可能的问题就是你没有设置好微信平台上的包名以及应用签名，好好看一下签名，直接从IDE上面装到手机上与签名打包后的签名是不一样的

####4.代码混淆后出错(下面的摘自Umeng的常见问题，也写在这儿)
>一般我们使用分享可以看见Umeng提供的混淆代码，但是如果你还使用Umeng提供的其他功能，这些代码就不能完全帮到你了。你可能需要下面的：
```
-keepclassmembers class * {
   public <init>(org.json.JSONObject);
}
```
```
-keep public class [您的应用包名].R$*{
    public static final int *;
}
```
把[您的应用包名] 替换成您自己的包名，如com.yourcompany.example。如果您使用5.0.0及以上版本的SDK，请添加如下命令：
```
-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}
```

####5.腾讯开放平台申请时千万注意申请的是什么
>如果是游戏，请注意你的包名，腾讯为了保障自己的利益，包名统一为com.tencent.tmgp.XXXX，如果在你代码写完准备上架，发现包名不对，不仅仅麻烦，而且繁琐的过程十分影响心情。这里如果你的软件都是简单的只想集合QQ分享功能的，建议为软件，这样可以省去很多的事情。

###关于修改包名，看Intellij IDEA修改包名