---
layout: post
title: 렌더링 성능을 향상시키는 content-visibility 속성
subtitle : 렌더링 성능을 향상시키는 새로운 CSS 속성
tags: [Chrome, CSS, content-visibility]
author: 최정락
comments : true
---

![transform+overflow issue]({{ site.baseurl }}/assets/img/post_2021-04-30_img01.jpg)
<br>

크롬 85에서 새로운 CSS 속성이 추가되었다.  
페이지 로드 성능을 개선하는 속성으로, 요소가 화면에서 벗어나있는 경우 렌더링을 생략한다고 한다.
<br>

요소가 뷰포트에 접근할 때, 표시를 해준다는 메커니즘은  
lazyload.js와도 얼추 비슷해 보이지만, 해당 content-visibility 속성은  
레이아웃을 구성하는 엘리먼트에 직접적으로. 보다 간편하게 적용할 수 있을 것으로 보인다.  
<br>

{% highlight css %}
.contents{
    content-visibility:auto;
    contain-intrinsic-size:240px;
}
{% endhighlight %}
<br>

몇 가지 속성이 있지만, 기본적으로 auto 값을 사용하며,  
contain-intrinsic-size는 해당 스타일로 인해 높이 값이 0으로 비어져있는 엘리먼트에
최소 높이 값을 지정해 준다.  
<br>

테스트해보니,
contain-intrinsic-size 속성을 지정해 주지 않으면,  
요소가 배치되는 순간, 스크롤바가 문단 높이에 의해 오르락내리락한다.
<br><br>

### 결론
미지원 브라우저는 둘째 치고,  
종횡비 유지가 필요한 모바일 레이아웃에서 매끄럽게 사용할 수 있을지는 아직 의문이지만  
페이지 속도 이슈를 CSS에서 개입할 수 있는 방식은 분명 새로운 방식인듯하다.  
<br><br>

출처 : https://web.dev/content-visibility/