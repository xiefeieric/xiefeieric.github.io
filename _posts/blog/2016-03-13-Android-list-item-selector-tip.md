---
layout: post
title: Android List Item Selector Tip
description: Somethimes we need only list item text color to be changed while selection, here is the tip
category: blog
---

In some situations, we need to use selector to change list item text color only, not the whole list item. The tip to do it is to inflate the layout from custome layout which has textview, then we can set selector for textview to change the color of the text while selection. One tip for this is to define state-activated rather than state-selected. 

~~~java
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true" android:color="@color/colorAccent"/>
    <item android:state_focused="true" android:color="@color/colorAccent"/>
    <item android:state_activated="true" android:color="@color/colorAccent"/>
    <item android:color="@android:color/black"/>

</selector>
~~~

The above code will only change textview color while list selection.


