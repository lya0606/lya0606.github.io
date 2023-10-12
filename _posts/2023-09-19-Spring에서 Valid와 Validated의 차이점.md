---
title: Spring에서 Valid와 Validated의 차이점
date: 2023-09-19 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Valid
  - Validated
---
## 소개

Spring Framework에서 데이터 유효성 검사를 할 때 `@Valid`와 `@Validated`라는 두 가지 주석(annotation)을 자주 볼 수 있습니다. 이 두 주석은 비슷하게 보이지만, 실제로는 목적과 사용법에 차이가 있습니다. 이 글에서는 이 두 주석의 차이점을 자세하게 살펴보겠습니다.

## @Valid의 특징과 사용법

`@Valid`는 Java의 표준 유효성 검사 방법 중 하나로, Java Bean Validation API에 속해 있습니다. 이 주석을 사용하면, 객체의 필드들이 정해진 조건에 부합하는지 자동으로 검사합니다.

### 사용 예시

```java
public ResponseEntity<?> create(@RequestBody @Valid User user) {
  // 코드 구현
}
```

위 코드에서 `@Valid`는 `User` 객체의 유효성을 검사합니다. 만약 유효하지 않다면, Spring은 자동으로 에러 메시지를 반환합니다.

## @Validated의 특징과 사용법

`@Validated`는 Spring Framework에서 제공하는 주석입니다. 이것은 `@Valid`와 유사하게 작동하지만, 그룹 검증이 가능하고, 복잡한 검증 로직을 처리할 수 있습니다.

### 사용 예시

```java
public ResponseEntity<?> update(@RequestBody @Validated(Groups.Update.class) User user) {
  // 코드 구현
}
```

여기서 `Groups.Update.class`는 그룹을 정의한 클래스입니다. 이를 통해 특정 상황에서만 적용되는 유효성 규칙을 설정할 수 있습니다.

## 주요 차이점

1. **출처**: `@Valid`는 Java 표준이고, `@Validated`는 Spring 특유입니다.
2. **그룹 검증**: `@Validated`는 그룹 검증을 지원합니다. `@Valid`는 그렇지 않습니다.
3. **복잡성**: `@Validated`는 좀 더 복잡한 검증 로직을 처리할 수 있습니다.

## 결론

데이터 유효성 검사는 어플리케이션의 안정성과 신뢰성을 높이는 중요한 작업입니다. `@Valid`와 `@Validated`는 비슷해 보이지만, 상황에 따라 적절한 주석을 선택하는 것이 중요합니다. `@Valid`는 간단하고 빠르게 유효성을 검사하고 싶을 때, `@Validated`는 좀 더 복잡한 검증이 필요할 때 사용하면 좋습니다.