---
layout: post
title: Angular Data Binding
description: Lesson learned from binding method
category: blog
---

 Angular provides interpolation data binding which is a cool feature, in our project, there is a bug 
 which spent our full day to solve. The scenario is that when you first navigate to this page, everything is 
  find and working properly, but if you navigate out and come back again, the whole tab becomes freezing.
  Double checked console, and there is no error message. This makes debug so difficult. Finally, we went through 
  all methods and tracked all logic, and found the problem is caused by a method bind to html template. Because this 
  method is an async call, so the data binding actually becomes an infinite loop...
  
  Tip from this lesson: never bind method to html template 


~~~





