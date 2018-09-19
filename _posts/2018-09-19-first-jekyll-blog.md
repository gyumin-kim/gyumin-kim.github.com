---
layout: post
title: "Jekyll 정적 블로그 만들기"
date: 2018-09-19 18:16:20 +0300
description: Jekyll을 활용해 손쉽게 정적 블로그를 만들고 관리하자. # Add post description (optional)
img:  # Add image post (optional)
---
## Jekyll로 만든 첫번째 블로그!

### 초기 설정
[Flexible Jekyll 테마](https://github.com/artemsheludko/flexible-jekyll)를 적용했다.
먼저 Jekyll 관련 설정은 [이 곳](https://jekyllrb.com/docs/installation/macos/)을 참고하자.
<br>
또한 다음의 과정이 필요하다.
`gem install bundler`
`sudo bundle install`
이후 내 사이트를 serve하고 싶을 때마다 `bundle exec jekyll serve --watch`를 입력하면 브라우저에서 실행된다.

### GitHub에 저장소 생성하고 GitHub Pages 설정하기
GitHub에서 적당한 이름(ex. `gyumin-kim.github.com`)의 repository를 생성하고, `git init`, `git remote`, `git add .`, `git commit -m "Initial Commit"`, `git push -u origin master`를 각각 수행한다.
해당 repository의 "Settings" 메뉴 내부에서 하단의 "GitHub Pages" 부분에서 `http://gyumin-kim.github.io/`와 같은 URL 주소가 보이면 성공이다.

### `_config.yml` 수정하기
이제 설정은 끝났다. 실제 페이지에 보여질 내용들을 직접 파일을 만들고 수정해가면서 작업하면 된다.
먼저 `_config.yml` 파일에 있는 기본값들을 실제 나와 관련된 정보들로 수정해 주자.

### Disqus(댓글 플랫폼) 반영하기
[Disqus](https://disqus.com/)에서 "I want to install Disqus on my site"을 클릭하고, Github pages에 등록된 사이트를 선택한다. 'Settings' 메뉴 > 'General'에 있는 Shortname을 복사하여 `_config.yml` 파일의 `discus-identifier` 부분에 붙여넣기 한다. Website Name은 자유롭게 해도 되고, Website URL은 실제 URL과 맞춰준다.

### 새로운 포스트 추가하기
모든 Jekyll theme들에서 공통적인 사항인지는 확실하지 않으나, 내가 적용한 "Flexible Jekyll"의 경우 `_posts` 폴더에 기본적으로 몇가지의 `.md` 파일들이 생성되어 있다. `_posts` 폴더에 있는 markdown 파일이 `_layouts` 폴더의 `post.html` 파일의 형식에 맞게 html 파일로 변환된다(*각 포스트마다 상단의 'layout'을 post라고 꼭 써줘야만 한다!*). 파일 이름은 `2017-04-06-how-i-rest-from-work.md`와 같은데, 제목 앞 부분의 날짜 부분은 반드시 형식을 똑같이 맞춰야 한다. 

### 기타 사항
만약 메인 화면 좌측에 보이는 각종 SNS 버튼들을 없애고 싶거나 다른 SNS로 수정하고 싶은 경우, `_layouts` 폴더의 `main.html` 파일에서 각각에 해당하는 부분을 적절히 수정해주면 된다.
