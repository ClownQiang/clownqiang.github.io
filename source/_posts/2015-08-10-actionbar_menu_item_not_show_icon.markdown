---
layout: post
title: ActionBar中Menu隐藏后Item无法显示Icon
comments: true
categories: "Android"
---

---
官方中ActionBar如果你隐藏了Menu Item，默认是不会显示Icon。虽然官方不支持，但是有时会使用到相关的效果，所以经过无数次的Google，终于找到了需要的方法和信息。

这个是在CSDN中[guolin](http://my.csdn.net/sinyu890807)博主发现的方法，是利用反射来完成的，具体博客地址在[这里](http://blog.csdn.net/guolin_blog/article/details/18234477)
```
@Override  
public boolean onMenuOpened(int featureId, Menu menu) {  
    if (featureId == Window.FEATURE_ACTION_BAR && menu != null) {  
        if (menu.getClass().getSimpleName().equals("MenuBuilder")) {  
            try {  
                Method m = menu.getClass().getDeclaredMethod("setOptionalIconsVisible", Boolean.TYPE);  
                m.setAccessible(true);  
                m.invoke(menu, true);  
            } catch (Exception e) {  
            }  
        }  
    }  
    return super.onMenuOpened(featureId, menu);  
} 
```

**但是，但是，但是（重要的事情说三遍）如果你是使用的AppCompactActivity，这里的onMenuOpen可能就不会调用了，至少对于我是这样的**

接下来我在stackoverflow上面发现另外的一种解决方法，同样是使用反射来达成效果，但是调用的地方不一样，**如果你是用的是AppCompactActivity**，可以使用下面的方法

```
@Override
protected boolean onPrepareOptionsPanel(View view, Menu menu) {    
    if (menu != null) {       
        if (menu.getClass().getSimpleName().equals("MenuBuilder")) {                                       
            try{
                Method m = menu.getClass().getDeclaredMethod("setOptionalIconsVisible", Boolean.TYPE);                
                m.setAccessible(true);                
                m.invoke(menu, true);            
            } catch (Exception e) {                
            Log.e(getClass().getSimpleName(), "onMenuOpened...unable to set icons for overflow menu", e);           
            }
        }    
    } 
   return super.onPrepareOptionsPanel(view, menu);
}
```

写下来给那些踩到坑的人~~~