---
layout: post
title: "POJO 이해하기"
date: 2018-12-12 11:25:00 +0300
description: Spring 공식문서가 알려주는 POJO 이야기 # Add post description (optional)
img: java-logo.png # Add image post (optional)
---

# POJO 이해하기

*이 글은 spring.io의 [Understanding POJOs](https://spring.io/understanding/POJO)를 번역한 것입니다.*  
<br><br>

POJO란 **Plain Old Java Object**의 줄임말이며, 프레임워크 확장에 의해 엉망진창이 되지 않는, 순수한 Java 객체(인스턴스)를 의미한다.

만약 JMS로부터 메시지를 받고자 한다면, `MessageListener` interface를 구현한 클래스를 다음과 같이 작성해야 할 것이다.

```java
public class ExampleListener implements MessageListener {

  public void onMessage(Message message) {
    if (message instanceof TextMessage) {
      try {
        System.out.println(((TextMessage) message).getText());
      }
      catch (JMSException ex) {
        throw new RuntimeException(ex);
      }
    }
    else {
      throw new IllegalArgumentException("Message must be of type TextMessage");
    }
  }
}
```

이는 당신의 코드가 특정 솔루션(위의 예시에서는 JMS)에 얽매이게 하고, 나중에 다른 메시징 솔루션으로 변경하기가 어렵게 만들 것이다. 만약 다수의 리스너들로 애플리케이션을 빌드한다면, AMQP라던지 다른 어떤 솔루션을 선택하는 것은 어렵거나 사실상 불가능해질 것이다.

POJO 주도 접근법(POJO-driven approach)이란, 인터페이스로부터 자유로운 솔루션을 다루는 메시지를 작성하는 것을 의미한다.

```java
@Component
public class ExampleListener {

  @JmsListener(destination = "myDestination")
  public void processOrder(String message) {
    System.out.println(message);
  }
}
```

이 예시의 경우, 코드가 어떤 인터페이스에도 얽매이지 않는다. 대신, JMS 큐에 연결하는 책임이 어노테이션(annotation)으로 옮겨감으로써 코드를 수정하기가 쉬워진다. 위의 경우 `@JmsListener`를 `@RabbitListener`로 대체할 수 있다. 아니면 어떤 특정 어노테이션도 없이 POJO 기반의 솔루션을 작성할 수도 있다.

이것은 하나의 예시일 뿐이다. 여기서 JMS와 RabbitMQ 중 무엇이 나은지를 설명하려는 것이 아니라, 특정 인터페이스에 종속되지 않는 코딩의 가치를 말하고자 하는 것이다. POJO(Plain Old Java Object)를 사용함으로써, 코드가 훨씬 간결해질 수 있다. 이는 더 나은 테스팅, 유연성, 그리고 향후 좀 더 쉽게 새로운 결정을 할 수 있도록 해 준다.

Spring 프레임웤과 그것의 다양한 포트폴리오 프로젝트들은 항상 당신의 코드와 이미 존재하는 라이브러리들 사이의 결합도(coupling)를 줄이는 것을 목표로 삼고 있다. 그것이 DI(Dependency Injection) 컨셉의 원칙이며, 이는 당신의 서비스가 사용되는 방식은 서비스 그 자체가 아니라 어플리케이션을 연결하는 일부분이 되어야 한다는 것이다.