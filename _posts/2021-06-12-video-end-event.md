---
layout: post
title: 비디오, 유튜브, 비메오 재생 완료 이벤트
subtitle : Video, Youtube, Vimeo 재생 완료 이벤트 받기
tags: [Video, Youtube, Vimeo, API]
author: 최정락
comments : true
---

영상 관련해 다양한 시점에 이벤트를 발생시킬 수 있으나  
주로, 재생 완료 시점에 이벤트를 받기 위한 요청이 잦아 별도 기록해둠

### Video
{% highlight html %}
<video id="player">
    <source id='mp4' src="video.mp4" type='video/mp4' />
</video>
{% endhighlight %}

{% highlight javascript %}
player.addEventListener('ended', function() {
    alert('재생 완료');
});
{% endhighlight %}

<br><br>

### Youtube
{% highlight html %}
<!-- 유튜브 API 호출 -->
<script src="https://www.youtube.com/iframe_api"></script>

<div id="player"></div>
{% endhighlight %}

{% highlight javascript %}
var player;

//유튜브 API
function onYouTubeIframeAPIReady() {
    player = new YT.Player('player', {
    height: '200',
    width: '300',
    videoId: 'kt2D7xl06mk',
    events: {
        'onStateChange': onPlayerStateChange
    }
    });
}

//재생 완료 감지
function onPlayerStateChange(event) {
    if(event.data === 0) {
        alert('재생 완료');
    }
}
{% endhighlight %}

<br><br>

### Vimeo
{% highlight html %}
<!-- 비메오 API 호출 -->
<script src="https://player.vimeo.com/api/player.js"></script>

<iframe id="player" src="https://player.vimeo.com/video/123123"></iframe>
{% endhighlight %}

{% highlight javascript %}
var iframe = document.getElementById('player');
var player = new Vimeo.Player(iframe);

player.on('ended', function() {
    alert('재생 완료');
});
{% endhighlight %}
