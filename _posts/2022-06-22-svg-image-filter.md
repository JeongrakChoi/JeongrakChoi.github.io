---
layout: post
title: SVG 이미지 색상 바꾸기 (Feat. filter)
subtitle : img 태그를 사용한 svg 이미지 색상 바꾸기
tags: [SVG]
author: 최정락
comments : true
---

{% highlight html %}
<img class="icon" src="icon.svg" alt="icon">
{% endhighlight %}

{% highlight css %}
img{invert(16%) sepia(89%) saturate(6054%) hue-rotate(358deg) brightness(97%) contrast(113%);}
{% endhighlight %}

&lt;img&gt; 태그를 사용해 아이콘을 표현하는 경우 filter 속성으로 색상 활용

기본적으로 svg 형태의 이미지 프로토 타입을  
검정색으로 받거나, 정제해서 사용할 경우 활용  

아래의 컨버터에서 쉽게 활용 가능  
<br>
<https://isotropic.co/tool/hex-color-to-css-filter/>