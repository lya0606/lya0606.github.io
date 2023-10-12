---
title: Spring에서 @RequestParam으로 리스트 바인딩하기
date: 2023-10-02 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RequestParam
---
## 문제 상황

Spring Framework를 사용하면서 `@RequestParam` 어노테이션을 이용해 클라이언트로부터 전달받은 데이터를 컨트롤러에 바인딩하는 작업은 흔하게 이루어진다. 그러나 단순한 데이터 타입이 아닌 리스트(List) 형태의 데이터를 바인딩할 때 어떻게 해야 할지 궁금한 경우가 있다.

## `@RequestParam`을 이용한 기본적인 바인딩

일반적으로 `@RequestParam`은 단순한 데이터 타입을 컨트롤러의 매개변수와 연결해 준다. 예를 들어, 클라이언트가 `name=John` 이라는 쿼리 스트링을 보냈다면, 다음과 같이 처리할 수 있다.

```java
@RequestMapping("/greeting")
public String greeting(@RequestParam String name) {
    return "Hello, " + name;
}
```

## 리스트 데이터 바인딩 방법

리스트 형태의 데이터를 바인딩하려면 조금 다른 접근 방식이 필요하다. 즉, 컨트롤러의 매개변수 타입을 `List<T>` 형태로 지정해 주어야 한다. 이때, `T`는 리스트의 요소 타입을 나타낸다. 

```java
@RequestMapping("/names")
public String names(@RequestParam List<String> nameList) {
    return "Names: " + String.join(", ", nameList);
}
```

### 주의사항: `[]` 문법

HTTP 쿼리 스트링에서 리스트를 표현하기 위해선 일반적으로 `[]` 문법을 사용한다. 즉, `name[]=John&name[]=Doe`와 같은 형식으로 데이터를 전송한다. 그러나 이러한 표기법은 Spring에서 자동으로 처리되지 않을 수 있다. 이럴 때는 `name=John&name=Doe`와 같이 `[]`를 생략하고 전송하는 방법을 사용한다.

### 에러 상황: TypeMismatchException

잘못된 타입의 데이터를 전송하게 되면 `TypeMismatchException`이 발생할 수 있다. 이럴 경우, 입력 형식을 확인하거나 필요한 경우에는 커스텀 바인더를 사용해 해결할 수 있다.

## 결론

Spring에서 `@RequestParam`을 사용해 리스트 데이터를 컨트롤러에 바인딩하는 것은 복잡하지 않다. 주의해야 할 점은 HTTP 쿼리 스트링의 표현 방식과 매개변수의 타입 일치 여부이다. 이러한 기초를 알고 있다면, 복잡한 데이터도 손쉽게 처리할 수 있다.