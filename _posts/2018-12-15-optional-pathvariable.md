---
layout: post
title: "300 Core Java Interview Questions | Set 1"
date: 2018-12-15 00:30:00 +0300
description: Java 8의 Optional 활용 # Add post description (optional)
img: java-optional.jpg # Add image post (optional)
---

Spring Framework에서 `@PathVariable`은 url에서 `/` 다음에 들어온 값을 받아 사용하기 위한 어노테이션이다. 
```java
@GetMapping("/product_detail/{pageStart}")
public String productDetail(ModelMap modelMap, @PathVariable int pageStart) {
  // pageStart 사용
}
```

`@PathVariable`로 값을 받아 메소드 내에서 사용할 수 있다.  <br>

그런데 `/product_detail` 다음에 아무 것도 추가하지 않고 요청을 하면 에러가 발생한다. `/product_detail/1`, `/product_detail/2`와 같이 요청하지 않고, `/product_detail` 까지만 요청해도 자동으로 특정 값으로 인식하도록 하려면 어떻게 할까?  <br>

Java 8의 `Optional<T>`를 사용하면 된다. 코드는 다음과 같다.
```java
@GetMapping({"/product_detail", "/product_detail/{pageStart}"})
  public String productDetail(ModelMap modelMap, @PathVariable Optional<Integer> pageStart) {
    Pageable pageable = PageRequest.of(pageStart.isPresent() ? pageStart.get() : 0, 10);

  // ... (생략)

}
```

1. `@GetMapping`(혹은 `@RequestMapping`) 내에 pageStart가 넘어오지 않는 경우와 pageStart가 포함된 경우의 2가지 url을 모두 적는다.
2. `@PathVariable`에 Optional<T>를 붙여준다.
3. 이제 메소드 내에서 사용하면 된다. 단, 해당 변수(이 경우 `pageStart`)가 존재하는지 여부를 `.isPresent()`로 체크한 다음 `.get()` 메소드로 값을 가져온 뒤 사용해야 한다.  

<br><br>
*참고자료: [Optional Path Variables with Spring (Boot) Rest MVC](https://www.n-k.de/2016/05/optional-path-variables-with-spring-boot-rest-mvc.html) by 
Niko Köbler*