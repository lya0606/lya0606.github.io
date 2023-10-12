---
title: JSON과 Java ArrayList 간의 문제 상황 Can not deserialize instance of java.util.ArrayList out of START_OBJECT token
date: 2023-10-01 20:00:00 +0900
categories:
  - Spring
tags:
  - JSON
  - JavaArraryList
---
## 문제 상황

많은 개발자들이 JSON 형식의 데이터를 Java 객체로 변환하려고 할 때 "Can not deserialize instance of java.util.ArrayList out of START_OBJECT token"이라는 오류에 부딪힙니다. 이 오류는 JSON 데이터와 Java 객체가 서로 호환되지 않을 때 발생합니다.

## 원인: JSON 구조와 Java 클래스 불일치

JSON 형식의 데이터와 Java 객체 사이의 구조가 일치하지 않을 때 이러한 오류가 발생합니다. 특히, JSON의 시작 토큰(`{` 또는 `[`)과 Java 객체의 자료형이 맞지 않으면 이 문제가 생깁니다.

- **ArrayList를 예상하는데 JSON이 객체(`{}`)로 시작**: Java에서는 `ArrayList`를 배열(`[]`)로 나타내기를 기대하지만, JSON 데이터가 객체(`{}`)로 시작하는 경우에 이 오류가 발생합니다.

## 해결 방법: JSON 데이터 수정

1. **JSON 배열로 수정**: JSON 데이터의 시작과 끝을 `[ ]`로 변경하여 배열로 만듭니다.
2. **Java 클래스 수정**: Java 클래스에서 `ArrayList` 대신 적절한 객체를 사용하여 JSON과 매핑합니다.

## 해결 방법: Java 코드 수정

1. **TypeReference 사용**: `TypeReference`를 사용하여 복잡한 객체의 타입 정보를 제공합니다.
2. **Custom Deserializer 작성**: `JsonDeserializer` 인터페이스를 구현하여 사용자 정의 역직렬화 로직을 추가합니다.

## 예제 코드: TypeReference 사용

```java
List<MyClass> myObjects = objectMapper.readValue(jsonString, new TypeReference<List<MyClass>>(){});
```

## 마무리

"Can not deserialize instance of java.util.ArrayList out of START_OBJECT token" 오류는 JSON 데이터와 Java 객체 간의 구조 불일치 때문에 발생합니다. 이 문제를 해결하기 위해서는 JSON 데이터 형식을 수정하거나 Java 코드를 업데이트해야 합니다. 이러한 방법을 통해 원활한 데이터 변환을 수행할 수 있습니다.