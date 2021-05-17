---
layout: post
title: IE에서 object-fit:cover 사용하기
subtitle : IE, EDGE 브라우저에서 object-fit 대체 방법
tags: [CSS, Javascript]
author: 최정락
comments : true
---

이미지나 비디오 태그에 사용되는 'object-fit' 속성은 IE, EDGE 브라우저에서 적용되지 않는다.
<br>

몇 가지 옵션이 있지만, 제일 많이 사용되는 cover 옵션의 대체 방법에 대해 기록한다.
<br>

여러 방법이 있겠지만, 스크립트 사용은 불가피하다.  
대부분의 방법이 브라우저 렌더링이 끝난 이후의 적용 방법에 대해 기술하고 있었는데, 
비동기식으로 처리된 페이지일 경우 이슈가 생길 여지가 있다.
<br>

아래와 같은 방법으로 적용하면 그나마 깔끔하게 해결할 수 있다.
<br><br>

{% highlight javascript %}
function setDirection(e) {
	if (e.naturalWidth / e.naturalHeight / e.parentNode.offsetWidth * e.parentNode.offsetHeight > 1) {
		e.classList.add('horizontal');
	} else {
		e.classList.add('vertical');
	}
}
{% endhighlight %}

먼저 이미지의 비율에 따라 class를 지정해주는 스크립트를 작성한다.
가로형과 세로형에 각기 다른 class를 줄 것이다.
<br><br>

{% highlight html %}
<img src="img.jpg" alt="" onload="setDirection(this)" alt="">
{% endhighlight %}

이미지 크기는 onload 이전에 알 수 있으므로 타이밍을 앞당긴다.
<br><br>

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

부모 컨테이너에는 overflow:hidden으로 잘라준다.