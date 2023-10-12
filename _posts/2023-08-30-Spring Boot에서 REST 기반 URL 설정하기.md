---
title: Spring Boot에서 REST 기반 URL 설정하기
date: 2023-08-30 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - REST
  - URL설정
---
## 문제 상황: 어떻게 Spring Boot에서 RESTful API의 기본 URL을 설정할 수 있을까?

Spring Boot에서 RESTful API를 구축할 때, 모든 엔드포인트(Endpoint)에 공통으로 적용되는 기본 URL을 설정하고 싶을 수 있습니다. 이를 통해 개발의 일관성을 유지하고, 효율적인 코드 관리를 할 수 있습니다.

## 해결 방법 1: `@RequestMapping` 어노테이션을 사용하다

`@RequestMapping` 어노테이션(Annotation)은 Spring에서 URL 패턴을 정의하는 데 사용됩니다. 이 어노테이션을 컨트롤러 클래스의 선언부에 적용하여 모든 메소드에 공통적인 기본 URL을 설정할 수 있습니다.

```java
@RestController
@RequestMapping("/api/v1")
public class MyController {

    @GetMapping("/users")
    public List<User> getUsers() {
        // 로직 구현
    }

    @GetMapping("/products")
    public List<Product> getProducts() {
        // 로직 구현
    }
}
```

이렇게 하면, `/api/v1`이 기본 URL이 되어 `/api/v1/users`나 `/api/v1/products` 등으로 엔드포인트에 접근할 수 있게 됩니다.

## 해결 방법 2: `application.properties` 파일에서 설정

Spring Boot는 `application.properties`라는 설정 파일을 통해 다양한 설정을 할 수 있습니다. 이 파일에서 `server.servlet.context-path` 속성을 설정하여 전체 애플리케이션에 적용할 기본 URL을 지정할 수 있습니다.

```properties
server.servlet.context-path=/api/v1
```

이렇게 설정하면 모든 컨트롤러와 메소드가 `/api/v1`를 기본 URL로 사용하게 됩니다.

## 오류와 해결: `Ambiguous mapping` 에러

두 방법을 동시에 사용하면 `Ambiguous mapping`이라는 에러가 발생할 수 있습니다. 이 에러는 두 개 이상의 URL 패턴이 충돌할 때 나타납니다. 따라서 하나의 방법만 선택해서 적용해야 합니다.

## 정리

Spring Boot에서 REST 기반 URL을 설정하는 방법은 크게 두 가지입니다. 첫 번째는 `@RequestMapping` 어노테이션을 컨트롤러에 적용하는 것이고, 두 번째는 `application.properties` 파일을 수정하는 것입니다. 어떤 방법을 선택할지는 프로젝트의 필요에 따라 결정하면 됩니다.