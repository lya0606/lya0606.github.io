---
title: JPA와 Hibernate에서 Spring Context에서 FetchType.LAZY 연관 관계 가져오기
date: 2023-09-16 20:00:00 +0900
categories:
  - Spring
tags:
  - JPA
  - Hibernate
  - SpringContext
---
## FetchType.LAZY란 무엇인가?

FetchType.LAZY는 Java Persistence API (JPA)에서 사용하는 데이터 로딩 전략 중 하나입니다. 이 전략을 사용하면, 데이터베이스에서 객체가 실제로 필요할 때만 관련 데이터를 로딩합니다. 다시 말해, 데이터가 꼭 필요하지 않은 경우에는 데이터베이스로부터 정보를 가져오지 않아 시스템 성능을 향상시킬 수 있습니다.

## 문제 상황: Spring Context에서 LAZY 로딩이 작동하지 않는 경우

때로는 Spring Context 내에서 FetchType.LAZY 설정이 예상대로 작동하지 않을 수 있습니다. 이럴 경우 `LazyInitializationException`이라는 오류가 발생할 수 있습니다. 이 문제가 발생하는 주된 이유는, 데이터 로딩이 필요한 시점에 이미 JPA의 Persistence Context가 닫혀있기 때문입니다. 

## 해결 방법 1: Open Session in View 패턴 사용

Open Session in View(OSIV)는 이 문제를 해결하기 위한 방법 중 하나입니다. 이 패턴은 HTTP 요청이 들어올 때 세션을 열고, 요청이 완료될 때까지 세션을 유지합니다. 이로 인해 LAZY 로딩이 필요한 시점에도 세션을 사용할 수 있습니다.

1. Spring Boot에서는 다음과 같이 설정합니다.
    ```java
    spring.jpa.open-in-view=true
    ```

## 해결 방법 2: 트랜잭션 범위 내에서 로딩

트랜잭션 범위 내에서 필요한 데이터를 로딩하면 문제를 해결할 수 있습니다. 다음은 예제 코드입니다.

```java
@Transactional
public void myMethod() {
    MyEntity entity = myRepository.findById(id);
    entity.getLazyCollection().size();
}
```

## 해결 방법 3: JPQL로 즉시 로딩

JPQL 쿼리를 사용하여 필요한 데이터만 즉시 로딩할 수도 있습니다. 이 방법은 필요한 데이터만 로딩하기 때문에 성능 측면에서 유리할 수 있습니다.

```java
SELECT m FROM MyEntity m JOIN FETCH m.lazyCollection WHERE m.id = :id
```

## 결론

Spring Context에서 FetchType.LAZY 설정이 작동하지 않을 때 다양한 해결 방법이 있습니다. Open Session in View 패턴 사용, 트랜잭션 범위 내에서 로딩, 그리고 JPQL로 즉시 로딩 등을 통해 `LazyInitializationException` 오류를 해결할 수 있습니다.