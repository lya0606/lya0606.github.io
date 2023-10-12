---
title: Spring RestTemplate 예외 처리 방법
date: 2023-10-03 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RestTemplate
  - 예외처리
---
## 소개

Spring Framework에서는 RestTemplate이라는 클래스를 제공하여 HTTP 요청을 쉽게 처리할 수 있습니다. 그러나 때로는 예외 상황이 발생할 수 있고, 이러한 예외를 어떻게 처리해야 하는지 알아보겠습니다.

## 일반적인 예외 처리

Spring에서 제공하는 `RestTemplate`을 사용할 때, 가장 일반적인 예외는 `HttpClientErrorException`과 `HttpServerErrorException`입니다. 이러한 예외는 클라이언트 오류(4xx)와 서버 오류(5xx)를 나타냅니다. 예외를 처리하기 위한 간단한 방법은 다음과 같습니다.

```java
try {
    restTemplate.getForObject(url, String.class);
} catch (HttpClientErrorException | HttpServerErrorException e) {
    System.out.println(e.getStatusCode());
    System.out.println(e.getResponseBodyAsString());
}
```

## 커스텀 예외 처리

기본적인 예외 처리 외에도, 사용자 정의 예외 처리를 사용할 수 있습니다. 이를 위해 `ResponseErrorHandler` 인터페이스를 구현할 수 있습니다.

```java
public class MyErrorHandler implements ResponseErrorHandler {
    @Override
    public boolean hasError(ClientHttpResponse response) throws IOException {
        return (response.getStatusCode().series() == CLIENT_ERROR || 
                response.getStatusCode().series() == SERVER_ERROR);
    }

    @Override
    public void handleError(ClientHttpResponse response) throws IOException {
        // 여기에 커스텀 로직 작성
    }
}
```

이후 `RestTemplate`의 `setErrorHandler` 메소드를 사용하여 에러 핸들러를 설정할 수 있습니다.

```java
RestTemplate restTemplate = new RestTemplate();
restTemplate.setErrorHandler(new MyErrorHandler());
```

## 예외에 따른 조치

예외가 발생했을 때 어떤 조치를 취할지 결정하는 것이 중요합니다. 예를 들어, 404 Not Found 오류가 발생했을 때 재시도를 할 것인지, 아니면 사용자에게 알릴 것인지 결정해야 합니다. 이러한 로직은 `handleError` 메소드 내에서 구현할 수 있습니다.

## 요약

Spring의 RestTemplate은 다양한 HTTP 요청을 손쉽게 처리할 수 있지만, 예외 상황에서도 적절한 대응이 필요합니다. 기본적인 `HttpClientErrorException`과 `HttpServerErrorException` 처리부터 사용자 정의 예외 처리까지 다양한 방법을 활용하여 더욱 견고한 애플리케이션을 구축할 수 있습니다.