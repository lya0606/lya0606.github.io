---
title: Method Name Resolving 활용하여 Spring Data JPA와 엔터티 개수 세기
date: 2023-09-02 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringData
  - JPA
  - MathodNameResolving
---
## 도입

Spring Data JPA는 자바 개발자들에게 데이터베이스 작업을 편리하게 수행할 수 있는 기능을 제공합니다. 하지만 이러한 편의성 때문에 종종 Spring Data JPA가 어떻게 내부적으로 작동하는지 알기 어려울 수 있습니다. 이 글에서는 Spring Data JPA의 'Method Name Resolving' 기능을 사용해 엔터티(Entity)의 개수를 세는 방법에 대해 알아보겠습니다.

## Method Name Resolving이란?

Method Name Resolving은 메서드 이름만으로도 쿼리를 자동 생성해주는 Spring Data JPA의 특징입니다. 예를 들어, `findAllByLastName(String lastName)`이라는 메서드를 정의하면, 이 메서드는 'lastName'이 같은 모든 엔터티를 찾아주는 쿼리를 자동으로 생성합니다.

## 엔터티 개수 세기

StackOverflow에 올라온 이 질문에서는 'Method Name Resolving'을 이용해서 엔터티의 개수를 어떻게 세는지에 대한 방법을 논의하고 있습니다. 주로 사용되는 방법은 Repository 인터페이스에 특별한 메서드를 정의하는 것입니다.

```java
public interface UserRepository extends JpaRepository<User, Long> {
    long countByLastName(String lastName);
}
```

이렇게 `countByLastName` 메서드를 정의하면, Spring Data JPA는 자동으로 'lastName' 필드를 가진 엔터티의 개수를 세는 쿼리를 생성합니다. 실행 결과로 개수가 반환됩니다.

## 주의사항

만약 `countByLastName`와 같은 메서드를 사용할 때 'SQL Syntax Error'라는 오류가 발생한다면, 메서드 이름에 오타가 없는지, 그리고 엔터티의 필드 이름과 일치하는지 확인해야 합니다.

## 마무리

Spring Data JPA의 Method Name Resolving 기능은 엔터티의 개수를 쉽게 세는 데 유용합니다. Repository 인터페이스에 간단한 메서드를 추가하기만 하면 됩니다. 이렇게 하면 복잡한 쿼리 작성 없이도 원하는 데이터를 얻을 수 있습니다.