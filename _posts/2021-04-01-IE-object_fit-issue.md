---
layout: post
title: IE에서 object-fit:cover 사용하기
subtitle : IE, EDGE 브라우저에서 object-fit 대체 방법
tags: [CSS, Javascript]
author: 최정락
comments : true
---

'object-fit' 속성은 IE, EDGE 브라우저에서 적용되지 않는다.  
몇 가지 옵션이 있지만, 제일 많이 사용되는 cover 옵션의 대체 방법에 대해 기록한다.
<br>

여러 방법이 있겠지만, 스크립트 사용은 불가피하며  
아래와 같이 적용하면 그나마 깔끔하게 해결할 수 있다.
<br>

{% highlight html %}
<img src="img.jpg" alt="" onload="setDirection(this)" alt="">
{% endhighlight %}

<br>

{% highlight javascript %}
function setDirection(element) {
	if (element.naturalWidth / element.naturalHeight / element.parentNode.offsetWidth * element.parentNode.offsetHeight > 1) {
		element.classList.add('horizontal');
	} else {
		element.classList.add('vertical');
	}
}
{% endhighlight %}

<br>

{% highlight css %}
img {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}
img.vertical {
	width: 100%;
}
img.horizontal {
	height: 100%;
}
{% endhighlight %}