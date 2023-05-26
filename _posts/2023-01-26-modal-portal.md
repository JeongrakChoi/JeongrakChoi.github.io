---
layout: post
title: Portal 활용 React Modal 만들기
subtitle : Portal 활용한 Modal 구현
tags: [React, Portal, Modal]
author: 최정락
comments : true
---

ReactDOM에서 제공하는 Portal 활용하여 Modal 만들기
<br/>
Modal 사용 시 다른 UI와 겹치거나 z-index 충돌 문제를 해결하기 위해  
부모 컴포넌트의 DOM 구조 바깥 노드로 Modal를 렌더링 하기 위함  
<br/>
root div 하단에 div 생성

<br>  

{% highlight html %}
<!-- public/index.html -->

<!DOCTYPE html>
<html lang="en">
  <body>
    <div id="root"></div>
    <!-- modal-root 추가 -->
    <div id="modal-root"></div>
  </body>
</html>
{% endhighlight html %}

<br/>

{% highlight jsx %}
// ModalPortal.tsx
// #modal-root에 child 컴포넌트를 렌더링해주는 Container를 만들어준다.

import React from 'react';
import ReactDOM from 'react-dom';

const ModalPortal: React.FC = ({ children }) => {
  const modalRoot = document.getElementById('modal-root');
  return ReactDOM.createPortal(children, modalRoot);
};

export default ModalPortal;
{% endhighlight jsx %}

<br/>

{% highlight jsx %}
// ModalPopup.tsx
// Modal 공통 컴포넌트

import React from 'react';
import ModalPortal from './ModalPortal';

type Props = {
  children: string;
  setOnModal: (state: boolean) => void;
};

const ModalPopup: React.FC<Props> = ({ children, setOnModal }: Props) => {
  return (
    <ModalPortal>
      <div className="modalPopup"  onClick={() => setOnModal(false)}>
        <div className="modalContent">
          {children}
          <button className="close" onClick={() => setOnModal(false)}>
            X
          </button>
        </div>
      </div>
    </ModalPortal>
  );
};

export default ModalPopup;
{% endhighlight jsx %}
