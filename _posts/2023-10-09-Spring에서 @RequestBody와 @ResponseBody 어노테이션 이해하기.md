---
title: Spring에서 @RequestBody와 @ResponseBody 어노테이션 이해하기
date: 2023-10-09 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RequestBody
  - ResponseBody
---
## @RequestBody란 무엇인가?

`@RequestBody`는 Spring Framework에서 클라이언트로부터 전송받은 JSON 또는 XML과 같은 데이터를 자바 객체로 바로 변환해주는 역할을 합니다. 이 어노테이션은 주로 `@RestController`나 `@Controller` 안에서 사용됩니다. 메서드 파라미터 앞에 위치하면, HTTP 요청 본문(body)의 데이터를 해당 자바 객체에 바인딩합니다. 예를 들어, 클라이언트가 보낸 JSON 데이터를 `User` 클래스의 객체로 변환하려면 다음과 같이 코드를 작성할 수 있습니다.

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
  // User 객체에 데이터가 바인딩됨
  // 로직 구현
}
```

## @ResponseBody란 무엇인가?

`@ResponseBody`는 반대로 자바 객체를 클라이언트에게 JSON 또는 XML 형태로 반환할 때 사용됩니다. 이 어노테이션은 메서드 위에 또는 리턴 타입 앞에 붙을 수 있으며, 이렇게 하면 Spring은 메서드가 반환하는 객체를 HTTP 응답 본문(body)에 담아 클라이언트에게 전송합니다.

```java
@GetMapping("/users/{id}")
@ResponseBody
public User getUserById(@PathVariable Long id) {
  // User 객체를 찾고 반환
}
```

## 언제 사용하는가?

- `@RequestBody`: 클라이언트가 서버로 데이터를 보낼 때, 주로 POST나 PUT 요청에서 사용됩니다.
- `@ResponseBody`: 서버가 클라이언트에게 데이터를 보낼 때, 주로 GET 요청에서 사용됩니다.

## 주의사항

1. `@RequestBody`와 `@ResponseBody`는 HTTP 요청과 응답에서 본문(body)의 데이터만을 다룹니다. 즉, 헤더나 다른 부분은 처리하지 않습니다.
2. 이들 어노테이션은 HTTP 메시지 변환기를 사용하여 데이터를 변환합니다. 자주 사용되는 변환기로는 `MappingJackson2HttpMessageConverter` (JSON 변환) 등이 있습니다.
3. 오류가 발생할 경우, 대표적인 에러는 `HttpMessageNotReadableException`입니다. 이 에러는 요청 본문을 읽지 못했을 때 발생합니다.

이렇게 `@RequestBody`와 `@ResponseBody`는 Spring에서 데이터를 효율적으로 처리하기 위한 중요한 어노테이션입니다. 이를 활용하면 복잡한 데이터 변환 작업 없이도 빠르고 효율적으로 웹 애플리케이션을 개발할 수 있습니다.