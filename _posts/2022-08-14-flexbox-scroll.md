---
layout: post
title: 중앙 정렬된 Flexbox 스크롤 이슈
subtitle : 중앙 정렬된 Flex 레이아웃의 스크롤 처리
tags: [HTML, CSS]
author: 최정락
comments : true
---

![transform+overflow issue]({{ site.baseurl }}/assets/img/post_2022-08-14_img01.jpg) <br>

{% highlight css %}
.flexBox{display:flex; justify-content:center; align-items:center; height:80px; overflow-y:auto;}
{% endhighlight %}

start 또는 end 기준 정렬 시에는 문제가 없으나, 
center 정렬한 Flexbox에 가변 크기에 따른 스크롤 처리를 할 경우  
위와 같이 상하단(또는 좌우)가 잘리는 이슈가 있음. <br><br><br>

{% highlight html %}
<div class="flexBox">
    <div class="flexBoxScroll">
        Content Content Content..
    </div>
</div>
{% endhighlight %}

{% highlight css %}
.flexBox{display:flex; flex-direction:column; justify-content:center; align-items:center; height:80px;}
.flexBoxScroll{overflow-y:auto;}
{% endhighlight %}

![transform+overflow issue]({{ site.baseurl }}/assets/img/post_2022-08-14_img02.jpg)

위와 같이 자식 엘리먼트를 하나 더 생성한 후, 
스크롤 옵션을 주고 부모 요소에 flex-direction:column 을 준다.