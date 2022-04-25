---
layout: post
title: Web Share API로 모바일 네이티브 공유 기능 구현하기
subtitle : 모바일 웹에서 네이티브 디바이스의 공유기능 사용하기
tags: [API, WebShare, Javascript]
author: 최정락
comments : true
---

![transform+overflow issue]({{ site.baseurl }}/assets/img/post_2022-04-25_img01.png)

모바일 웹에서 네이티브 공유 기능에 대한 요청이 와서 정리해둔다.
URL은 현재 페이지의 주소로 임의 설정함

### HTML
{% highlight html %}
<button type="button" id="btnShare">공유하기</button>
{% endhighlight %}

<br><br>

### Javascript
{% highlight javascript %}
var btnShare = document.getElementById("btnShare");
btnShare.addEventListener("click", function(){
    var shareTitle = "제목";
    var shareText = "내용";
    var shareURL = window.document.location.href;
    
    if (navigator.share){
        navigator.share({
            title : shareTitle,
            text : shareText,
            url : shareURL,
        })
        .then(() => console.log('공유 성공'))
        .catch((error) => console.log('공유 실패', error));
    }else{
        alert('공유하기를 지원하지 않는 환경입니다.');	
    }
});
{% endhighlight %}
