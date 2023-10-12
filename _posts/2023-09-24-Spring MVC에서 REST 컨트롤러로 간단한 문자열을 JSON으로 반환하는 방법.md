---
title: Spring MVC에서 REST 컨트롤러로 간단한 문자열을 JSON으로 반환하는 방법
date: 2023-09-24 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - REST컨트롤러
  - JSON
---
## 문제 상황 및 주요 질문

개발자들이 Spring MVC 프레임워크를 사용하여 RESTful 웹 서비스를 개발할 때, 종종 데이터를 JSON 형식으로 클라이언트에게 반환해야 할 필요가 있습니다. 이때, 복잡한 객체나 리스트가 아닌 간단한 문자열만을 JSON 형식으로 반환하고 싶다면 어떻게 해야 할까요? 원본 코드에서의 에러는 `No specific error mentioned` 입니다.

## 반환 방식에 따른 해결 방안

### `ResponseEntity` 사용하기

`ResponseEntity`는 HTTP 응답의 상태 코드, 헤더, 본문 등을 포함할 수 있습니다. 이를 사용하면 다음과 같이 코드를 작성할 수 있습니다.

```java
@RequestMapping(value = "/example", method = RequestMethod.GET)
public ResponseEntity<String> example() {
    return new ResponseEntity<>("{\"message\":\"Hello, World!\"}", HttpStatus.OK);
}
```

### `@ResponseBody` 어노테이션 활용

`@ResponseBody`를 사용하면 리턴되는 값 자체가 HTTP 응답 본문이 됩니다. 이 어노테이션을 사용하면 다음과 같이 작성할 수 있습니다.

```java
@ResponseBody
@RequestMapping(value = "/example", method = RequestMethod.GET)
public String example() {
    return "{\"message\":\"Hello, World!\"}";
}
```

### `Map` 객체 활용

`java.util.Map`을 사용하면 키-값 쌍으로 데이터를 보관하고, 이를 JSON 형태로 쉽게 변환할 수 있습니다.

```java
@RequestMapping(value = "/example", method = RequestMethod.GET)
public Map<String, String> example() {
    Map<String, String> map = new HashMap<>();
    map.put("message", "Hello, World!");
    return map;
}
```

## 주의사항

위의 모든 방법들은 문자열을 JSON 형식으로 클라이언트에 반환할 수 있지만, 상황에 따라 가장 적합한 방법을 선택해야 합니다. 예를 들어, 상태 코드나 헤더를 커스터마이즈 하고 싶다면 `ResponseEntity`가 더 나을 수 있습니다.

## 결론

Spring MVC에서 RESTful 웹 서비스를 구현할 때 간단한 문자열을 JSON 형식으로 반환하는 것은 여러 가지 방법이 가능합니다. `ResponseEntity`, `@ResponseBody`, 그리고 `Map` 등을 활용하여 다양한 상황에 대응할 수 있습니다.