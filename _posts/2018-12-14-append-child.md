---
layout: post
title: "appendChild()에서 주의할 점"
date: 2018-12-14 16:50:00 +0300
description: appendChild는 기존 노드를 옮길 수도 있다! # Add post description (optional)
img: js-logo.svg.png # Add image post (optional)
---

`Node.appendChild()`는 특정 Node 내부의 마지막에 어떤 element를 추가하고자 할 경우 사용한다. 즉 특정 부모 Node의 자식 Node 리스트 중 마지막 자식으로 붙이는 것이다.  
*(참고: append는 '덧붙이다', '첨부하다'라는 뜻이다.)*

```javascript
// Create a new paragraph element, and append it to the end of the document body
let p = document.createElement('p');
document.body.appendChild(p);
```

위의 코드는, `createElement('p')`로 `<p>` element를 생성하고, `.appendChild()`를 사용하여 `body` 내부의 가장 마지막 부분에 `<p>` element를 붙인다.  <br>
이렇듯 `.appendChild()`는 사용하기 그리 어렵지 않다. 단 주의할 점이 있는데, 만약 주어진 Node가 이미 문서에 존재하는 Node를 참조하는 경우, `appendChild()`는 단지 Node를 새로운 곳에 복사하는 것이 아니라, **현재 위치에서 새로운 위치로 이동시킨다.**  
<br>
위의 샘플 코드는 새롭게 생성한 element를 append한 것이기 때문에 딱히 문제가 발생할 일이 없지만, 이미 기존에 존재하던 어떤 Node를 선택하고 그것을 `appendChild()`로 다른 어딘가에 붙이고자 할 경우, 그 Node가 의도치 않게 다른 위치로 옮겨질 수 있다.  
<br>
이럴 때는 그냥 `appendChild()`를 사용하면 안되고, `Node.cloneNode()`로 Node를 clone한 뒤 그 Node를 `appendChild()`해야 기존 Node가 엉뚱한 위치로 옮겨지지 않는다.
<br><br><br><br>
*참고자료) [Node.cloneNode()](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode) - MDN*