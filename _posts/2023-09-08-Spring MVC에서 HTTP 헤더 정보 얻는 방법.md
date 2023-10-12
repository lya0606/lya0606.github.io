---
title: Spring MVC에서 HTTP 헤더 정보 얻는 방법
date: 2023-09-08 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - HTTP헤더
---
## 소개

Spring MVC는 웹 애플리케이션을 개발하기 위한 탁월한 프레임워크입니다. 이 프레임워크를 사용하면 HTTP 헤더 정보에 쉽게 접근할 수 있습니다. HTTP 헤더는 클라이언트와 서버 간의 추가 정보를 담고 있어 다양한 활용이 가능합니다. 이 문서에서는 Spring MVC의 REST 컨트롤러에서 HTTP 헤더 정보를 얻는 다양한 방법을 설명합니다.

## `@RequestHeader` 어노테이션 사용하기

`@RequestHeader`는 HTTP 요청 헤더를 메서드 매개변수로 전달할 수 있게 해주는 어노테이션입니다. 이를 사용하면 특정 헤더 값을 아주 쉽게 가져올 수 있습니다.

```java
@RequestMapping("/headerExample")
public String showHeaderInfo(@RequestHeader("User-Agent") String userAgent) {
    // User-Agent 헤더 정보를 userAgent 변수에 저장
    return "User-Agent: " + userAgent;
}
```

## `HttpServletRequest` 객체 사용하기

`HttpServletRequest` 객체를 사용하면 요청에 포함된 모든 헤더 정보에 접근할 수 있습니다. 

```java
@RequestMapping("/allHeaders")
public String showAllHeaders(HttpServletRequest request) {
    Enumeration<String> headerNames = request.getHeaderNames();
    StringBuilder headers = new StringBuilder();
    
    while (headerNames.hasMoreElements()) {
        String headerName = headerNames.nextElement();
        String headerValue = request.getHeader(headerName);
        headers.append(headerName).append(": ").append(headerValue).append("\n");
    }
    
    return "Headers: \n" + headers.toString();
}
```

## `HttpHeaders` 객체 사용하기

Spring의 `HttpHeaders` 클래스를 사용하면 `MultiValueMap` 형식으로 헤더 정보를 가져올 수 있습니다. `MultiValueMap`은 하나의 키에 여러 값을 가질 수 있는 자료구조입니다.

```java
@RequestMapping("/httpHeadersExample")
public String showHeaders(@RequestHeader HttpHeaders headers) {
    // HttpHeaders 객체를 통한 헤더 정보 접근
    return "Headers: " + headers.toString();
}
```

## 정리

Spring MVC에서는 `@RequestHeader`, `HttpServletRequest`, 그리고 `HttpHeaders` 등 다양한 방법으로 HTTP 헤더 정보에 접근할 수 있습니다. 각 방법은 상황과 필요에 따라 적절히 활용하면 됩니다. 이제 여러분도 Spring MVC를 이용해 HTTP 헤더 정보를 자유롭게 다룰 수 있을 것입니다.