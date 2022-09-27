---
layout: post
title: CSS Grid로 Masonry 레이아웃 만들기
subtitle : 플러그인 없이 Masonry 레이아웃 만들기
tags: [HTML, CSS, Grid, Mansonry]
author: 최정락
comments : true
---

플러그인 없이 적용할 수 있는 masonry 레이아웃 방법에 대해 기록  
차후 브라우저 지원에 따라, 새롭게 추가된 grid-template-rows:masonry 스펙을 사용할 수 있을 것으로 기대  

현재 해당 블로그 내  
포트폴리오 페이지에도 적용 중

<br>  

기존 방법


- isotope.js, masonry.js 등을 이용한 플러그인 사용

- 각 요소에 position:absolute 준 뒤 JS로 위치 조정

- Flex box 등으로 레이아웃 지정 (column-count 등으로 사용 가능하나 세로 정렬 됨)

- <b>grid-auto-rows + grid-row-end 활용 해 위치 조정</b>

<br>

이중, 네번째 방법에 대해 기록 
<br><br>
요소의 position을 static으로 가져갈 수 있고,  
자식 요소의 높이만 감지해 레이아웃을 만듬으로  
기존 방식보다, 브라우저 리사이징 시 발생하는 메모리 누수를 최소화  

### HTML
{% highlight html %}
<div class="masonry-container">
    <div class="masonry-item">
        <div class="item">1</div>
    </div>
    <div class="masonry-item">
        <div class="item">2</div>
    </div>
    ...
</div>
{% endhighlight html %}

<br>

### CSS
{% highlight css %}
.masonry-container {
    --gap: 10px;

    display: grid;
    grid-template-columns: repeat(3, 1fr);
    column-gap: var(--gap);
    grid-auto-rows: 10px;
}

@media screen and (max-width: 720px) {
    .masonry-container {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media screen and (max-width: 400px) {
    .masonry-container {
        display: block;
    }

    .masonry-item {
        margin-bottom: var(--gap);
    }
}
{% endhighlight %}

<br>

### Javascript
{% highlight javascript %}
function masonryLayout() {
    const masonryContainerStyle = getComputedStyle(
        document.querySelector(".masonry-container")
    );
    const columnGap = parseInt(
        masonryContainerStyle.getPropertyValue("column-gap")
    );
    const autoRows = parseInt(
        masonryContainerStyle.getPropertyValue("grid-auto-rows")
    );

    document.querySelectorAll(".masonry-item").forEach((elt) => {
        elt.style.gridRowEnd = `span ${Math.ceil(
            elt.querySelector(".item").scrollHeight / autoRows +
                columnGap / autoRows
        )}`;
    });
}

masonryLayout();
window.addEventListener("resize", masonryLayout);
{% endhighlight %}
