---
layout: post
title: React Modal 만들기(Feat.Portal)
subtitle : Portal 활용한 Modal 구현
tags: [React, Portal, Modal]
author: 최정락
comments : true
---

ReactDOM에서 제공하는 Portal 활용하여 Modal 만들기
<br/><br/>
Modal 화면을 개별 컴포넌트로 만들어서 사용 중, 
다른 UI와 겹치거나 z-index 충돌 문제를 해결하기 위해  
부모 컴포넌트의 DOM 구조 바깥 노드로 Modal를 렌더링 하기 위함  
<br/><br/>

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
// ModalPortal.jsx
​
const ModalPortal = ({children,closePortal}) => {
  const ref = useRef<Element | null>();
  const [mounted,setMounted] = useState(false);
​
  useEffect(()=>{
    setMounted(true);
    if(document) {
        const dom = document.getElementById('root-modal');
        ref.current = dom; // ref에 dom 값 전달
    }
  },[]);
​
  if(ref.current&&mounted) { // mounted 됬고 dom이 존재하는 경우 모달 랜더링 진행
    return createPortal(
      <div className="modal-container">
        <div className="modal-background" role="presentation" onClick={closePortal}/>
        {children}
      </div>,
      ref.current
    )
  }
​
  return null;
}
​
export default ModalPortal;
{% endhighlight jsx %}

<br/>

{% highlight jsx %}
//App.js
​
const App = () => {
  const [modalOpened, setModalOpened] = useState(false);
​
  const handleOpen = () => {
    setModalOpened(true);
  };
​
  const handleClose = () => {
    setModalOpened(false);
  };
​
  return (
    <div className="App">
      <button onClick={handleOpen}>Open Modal</button>
      {modalOpened && (
        <ModalPortal closePortal={handleClose}>
          <SampleModal />
        </ModalPortal>
      )}
      <div id="root-modal"></div>
    </div>
  );
}
​
export default App;
{% endhighlight jsx %}