---
layout: post
title: “何书还”之二（关于Animation使用）
comments: true
categories: "Android"
---

---
[官方介绍Animation使用](http://developer.android.com/training/material/animations.html)

我看了一下官方文档，但是无奈我的理解能力不够好，跑了好多次还是看不见炫酷的动画效果，无奈只好去翻阅官方demo的源码，终于知道了怎么使用。

####Touch Feedback（触摸反馈）
在XML文件中添加以下代码可以添加触摸反馈的动画效果（类似于涟漪的效果）
- *?android:attr/selectableItemBackground*（有边界，可以使用在listview的item上）
- *?android:attr/selectableItemBackgroundBorderless*（没有边界，或者直接看是看不到明显的边界，但是点击是有涟漪效果）
**需要说明*android:attr/selectableItemBackgroundBorderless*是API 21新增加的**

####Circular Reveal
这个主要是提供一个圆形的显示或者隐藏的动画效果，主要使用的api是[ViewAnimationUtils.createCircularReveal()](http://developer.android.com/reference/android/view/ViewAnimationUtils.html#createCircularReveal(android.view.View, int, int, float, float)
```
// previously invisible view
View myView = findViewById(R.id.my_view);

// get the center for the clipping circle
int cx = (myView.getLeft() + myView.getRight()) / 2;
int cy = (myView.getTop() + myView.getBottom()) / 2;

// get the final radius for the clipping circle
int finalRadius = Math.max(myView.getWidth(), myView.getHeight());

// create the animator for this view (the start radius is zero)
Animator anim =
    ViewAnimationUtils.createCircularReveal(myView, cx, cy, 0, finalRadius);

// make the view visible and start the animation
myView.setVisibility(View.VISIBLE);
anim.start();
```
里面几个参数的意思分别为：
- myView 要展示动画效果的视图
- cx  动画开始的X坐标
- cy 动画开始的Y坐标
- startRadius 动画开始的角度
- finalRadius 动画结束的角度

####Activity Transitions
关于这个我就不多写了，博主大苞米对于这个写的十分详细，给大家附上链接自己[看一下](http://blog.csdn.net/a396901990/article/details/40187203),我就Activity之间的视图共享写一下，因为我在这个地方花了一些时间，所以记下来以备后面忘记。

首先需要在XML文件中你需要共享的View定义一个```android:transitionName```

```
<ImageView
                android:id="@+id/bookPage"
                android:layout_width="match_parent"
                android:layout_height="400dp"
                android:scaleType="centerCrop"
                android:tint="@color/photo_tint"
                android:transitionName="bookPage" />
```
然后可以定义动画效果：

**1.可以在style文件中定义**
```
<item name="android:windowContentTransitions">true</item>  
<item name="android:windowEnterTransition">@transition/explode</item>  
<item name="android:windowExitTransition">@transition/explode</item>
```

**2.可以在java文件中定义**
```
getWindow().requestFeature(Window.FEATURE_CONTENT_TRANSITIONS);  
getWindow().setExitTransition(new Explode());  
```

然后在使用Intent跳转的时候，加入ActivityOptions
```
Intent intent = new Intent(this, Activity2.class);  
// shareView: 需要共享的视图  
// bookPage就是刚刚 transitionName所写的值
ActivityOptions options = ActivityOptions  
        .makeSceneTransitionAnimation(this, shareView, "bookPage");  
startActivity(intent, options.toBundle());
```

对于一次共享多个View的需要使用Pair.create(view,"shareName")，这里必须是View。

关于结束Activity时同样动画效果倒回可以使用Activity.finishAfterTransition()。

####添加TranstionListener
同样你可以在进入动画时候添加动画监听器，这样你就可以在本页面加载更多的动画效果
```
getWindow().getEnterTransition().addListener(new TransitionAdapter() {
                @TargetApi(Build.VERSION_CODES.LOLLIPOP)
                @Override
                public void onTransitionEnd(Transition transition) {
                    ObjectAnimator color = ObjectAnimator.ofArgb(bookPage.getDrawable(), "tint",
                            getResources().getColor(R.color.photo_tint), 0);
                    color.start();
                    renewButton.animate().scaleX(1.0f);
                    renewButton.animate().scaleY(1.0f);
                    renewButton.animate().alpha(1.0f);
                    getWindow().getEnterTransition().removeListener(this);
                }
            });
```

关闭Activity时同样可以使用，需要重写onBackPressed()方法：
```
@Override
    public void onBackPressed() {
        super.onBackPressed();
        if (Build.VERSION.SDK_INT == 21) {
            ObjectAnimator color = ObjectAnimator.ofArgb(bookPage.getDrawable(), "tint",
                    0, getResources().getColor(R.color.photo_tint));
            color.addListener(new AnimatorListenerAdapter() {
                @Override
                public void onAnimationEnd(Animator animation) {
                    finishAfterTransition();
                }
            });
            color.start();
            renewButton.animate().scaleX(0.0f);
            renewButton.animate().scaleY(0.0f);
            renewButton.animate().alpha(0.0f);
            finishAfterTransition();
        }
    }
```