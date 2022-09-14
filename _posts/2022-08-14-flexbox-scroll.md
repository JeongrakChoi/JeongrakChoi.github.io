---
layout: post
title: 수직 정렬된 Flexbox 스크롤 이슈
subtitle : justify-content:center 수직 정렬된 Flex 레이아웃의 스크롤 처리
tags: [HTML, CSS]
author: 최정락
comments : true
---

![transform+overflow issue]({{ site.baseurl }}/assets/img/post_2022-08-14_img01.jpg) <br>

{% highlight css %}
.flexBox{display:flex; justify-content:center; align-items:center; height:80px; overflow-y:auto;}
{% endhighlight %}

단순 중앙 정렬된 Flexbox에 가변 크기에 따른 스크롤 처리를 할 경우  
위와 같이 상하단(좌우)가 잘리는 이슈가 있음.