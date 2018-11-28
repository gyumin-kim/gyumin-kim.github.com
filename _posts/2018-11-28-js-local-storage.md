---
layout: post
title: "localStorage 간단 사용기"
date: 2018-11-28 22:46:00 +0300
description: localStorage로 브라우저에 데이터 저장하기 # Add post description (optional)
img: local-storage.jpg # Add image post (optional)
---
# localStorage 사용하기

이번에 외주 작업으로 리더십 진단 페이지를 제작하게 되었다. 사용자 데이터, 그리고 사용자가 입력한 40여 개 문항에 대한 응답 데이터를 어딘가에 저장한 뒤, 그것을 바탕으로 진단 결과를 보여주는 작업이다. 데이터는 서버에 저장할 수도 있겠지만, 이번 프로젝트는 서버는 따로 두지 않고 브라우저 위에서만 돌아가도록 제작하면 된다는 요청을 받았다.  
그래서 브라우저에 데이터를 저장하고자 할 때 어떤 방법을 쓸 수 있을지 알아보았는데,  **Cookie**나 **localStorage** 등을 적용할 수 있다.  
이 글에서는 localStorage를 사용한 예시를 코드와 함께 간단히 정리하고자 한다.

---
## localStorage 개요
> *Web Storage API는 브라우저에서 쿠키를 사용하는 것보다 훨씬 직관적으로 key/value 데이터를 안전하게 저장할 수 있는 메커니즘을 제공합니다. –– MDN "Web Storage API 사용하기"*  

localStorage는 문자열의 key/value pair로 이루어져 있으며, HTML5에서 추가된 저장소이다. localStorage에 값을 저장할 때는 `localStorage.setItem(key, value)`, 꺼내올 때는 `localStorage.getItem(key)`와 같이 사용한다. `localStorage.removeItem('key')`로 특정 데이터를 삭제하는 등의 작업도 가능하다.  
([MDN — Web Storage API 사용하기](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API) 참조)


---
## 기타 유사한 방법들
**cookie**는 서버와 클라이언트 사이의 데이터 교환을 위해 사용하는 것이다. 게다가 로컬 환경에서 cookie에 값을 저장하고 가져오는 작업이 원활하게 이루어지지 않았다.  
이번 프로젝트의 특성을 감안한다면, localStorage 뿐만 아니라 **sessionStorage**를 사용하는 것이 더 좋을 수도 있겠다. sessionStorage는 localStorage와는 달리 데이터가 영구적으로 저장되지는 않는다.