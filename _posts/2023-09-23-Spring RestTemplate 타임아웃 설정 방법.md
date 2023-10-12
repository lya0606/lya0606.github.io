---
title: Spring RestTemplate 타임아웃 설정 방법
date: 2023-09-23 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RestTemplate
---
## 소개
Spring RestTemplate은 웹 서비스를 호출할 때 자주 사용되는 HTTP 클라이언트입니다. 웹 서비스의 응답을 기다릴 때 시간을 설정하는 것은 중요한 작업 중 하나입니다. 이 글에서는 `RestTemplate`의 타임아웃(timeout)을 어떻게 설정하는지 자세히 알아보겠습니다.

## 타임아웃이란?
타임아웃은 일정 시간 동안 데이터를 주고받지 못할 경우 연결을 자동으로 끊는 시간을 의미합니다. 이를 통해 시스템 자원을 효율적으로 관리할 수 있습니다.

## RestTemplate에서 타임아웃 설정하기
RestTemplate에서 타임아웃을 설정하는 방법은 여러 가지입니다. 가장 일반적인 방법은 `SimpleClientHttpRequestFactory` 또는 `HttpComponentsClientHttpRequestFactory`를 사용하는 것입니다.

### SimpleClientHttpRequestFactory 사용하기
`SimpleClientHttpRequestFactory`를 사용하여 `RestTemplate`을 설정하는 예제 코드입니다.
```java
SimpleClientHttpRequestFactory factory = new SimpleClientHttpRequestFactory();
factory.setConnectTimeout(5000);  // 연결 타임아웃을 5초로 설정
factory.setReadTimeout(5000);  // 읽기 타임아웃을 5초로 설정

RestTemplate restTemplate = new RestTemplate(factory);
```

### HttpComponentsClientHttpRequestFactory 사용하기
`HttpComponentsClientHttpRequestFactory`는 Apache HttpClient를 기반으로 합니다. 이를 사용하는 예제 코드는 다음과 같습니다.
```java
HttpComponentsClientHttpRequestFactory factory = new HttpComponentsClientHttpRequestFactory();
factory.setConnectTimeout(5000);  // 연결 타임아웃을 5초로 설정
factory.setReadTimeout(5000);  // 읽기 타임아웃을 5초로 설정

RestTemplate restTemplate = new RestTemplate(factory);
```

## 주의사항
타임아웃을 너무 짧게 설정하면 웹 서비스로부터 응답을 받기 전에 연결이 끊길 수 있습니다. 반대로 너무 길게 설정하면 시스템 자원이 낭비될 수 있습니다. 적절한 타임아웃 시간을 설정하는 것이 중요합니다.

## 정리
RestTemplate의 타임아웃을 설정하는 방법은 `SimpleClientHttpRequestFactory` 또는 `HttpComponentsClientHttpRequestFactory`를 사용하는 것이 일반적입니다. 타임아웃 설정은 시스템의 효율성과 안정성에 중요한 영향을 미치므로 적절한 시간을 설정해야 합니다.