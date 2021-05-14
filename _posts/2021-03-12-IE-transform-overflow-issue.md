---
layout: post
title: 익스플로러(IE) transform + overflow 이슈
subtitle : IE에서 overflow:hidden이 적용되지 않는 문제
tags: [CSS]
author: 최정락
comments : true
---

![transform+overflow issue]({{ site.baseurl }}/assets/img/post_2021-03-12_img01.gif)
<br>

최근 한 프로젝트 진행 중 IE 환경의
특정 상황에서 overflow:hidden이 제대로 동작하지 않는 현상을 발견하였다.
<br>

해당 문제는 위 참조 이미지처럼
transform animation이 사용되는 화면에서, 애니메이션 작동이 끝나기 전에
hidden 처리 된 영역을 벗어날 경우, animation이 끝나는 시점까지 버벅거리는 이슈다.

스택오버플로에서도 해당 이슈에 대한 정확한 글을 찾기 힘들어
공유 겸 기록해두고자 한다.

결론부터 말하자면, overflow:hidden이 적용되어야 할 엘리먼트에
아래 스타일을 주면 해결된다.
<br>

{% highlight css %}
.box {
  perspective:1px
}
{% endhighlight %}

<br>
<b>perspective</b>는 transform과 함께 사용하는 속성으로,
3D를 표현해야 할 때, 투영점(원근감)을 주기위해 사용되는데
이를 대세에 지장없는 1px로 지정해주게 되면 해당 문제를 해결 할 수 있다.

<br>
transform을 사용해야하는 사이트라면 
IE9 이상의 크로스브라우징이 전제되어야 할테니
아래와 같은 IE핵으로 활용할 수 있을 것이다.
<br>

{% highlight css %}
/* IE9 */
@media all and (monochrome:0) {
	.box{perspective:1px}
}

/* IE10, IE11 */
@media all and (-ms-high-contrast:none) {
	.box{perspective:1px} /* IE10 */
	*::-ms-backdrop, .box{perspective:1px} /* IE11 */
}
{% endhighlight %}