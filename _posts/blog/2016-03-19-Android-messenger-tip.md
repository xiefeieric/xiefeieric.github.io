---
layout: post
title: Android Tip: Messenger
description: A very good tip to pass message between Activity and Service
category: blog
---

It is very often we need to start a service in the background, for example, we start a service to play music, so how could we track the music data back from Service to Activity, in order to show the playing progress? One way to solve it is to try to send message back to Activity's hanlder, then we can handle it, but Hanlder is a normal class, we cannot pass it to Service. Now what we need is Messenger which implemented Parcelble interface, so Handler can be put inside Messenger, then pass to Service.   

~~~java
intent.putExtra("messenger",new Messenger(mHandler));
~~~

You can find more detail from <a href="http://developer.android.com/reference/android/app/Service.html" target="_blank"> Google </a>.



