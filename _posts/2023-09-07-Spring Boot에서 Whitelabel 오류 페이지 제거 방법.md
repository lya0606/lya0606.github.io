---
title: Spring Boot에서 Whitelabel 오류 페이지 제거 방법
date: 2023-09-07 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - Whitelabel오류
---
## 문제 상황: Whitelabel Error Page

Spring Boot에서 개발을 하다 보면, 예외 상황이 발생했을 때 자동으로 생성되는 'Whitelabel Error Page'를 볼 수 있습니다. Whitelabel은 브랜딩되지 않은, 즉 개발자가 디자인을 하지 않은 기본 오류 페이지를 의미합니다. 이 페이지는 디버깅에 도움이 될 수 있지만, 실제 서비스에서는 사용자에게 보여주기에는 부적절한 경우가 많습니다.

## 해결책 1: 커스텀 오류 페이지 사용

가장 간단한 방법은 커스텀 오류 페이지를 만드는 것입니다. `/src/main/resources/templates` 디렉토리 안에 `error.html` 파일을 만들고, 원하는 디자인과 메시지를 넣으면 됩니다. Spring Boot는 이 파일을 자동으로 찾아 사용자에게 보여줍니다.

## 해결책 2: Controller에서 예외 처리

@ControllerAdvice 어노테이션을 사용하여 전역 예외 처리기를 만들 수 있습니다. 이를 통해 다양한 HTTP 상태 코드에 대한 처리를 할 수 있습니다. 예를 들어, 404 오류나 500 오류가 발생했을 때 원하는 로직을 실행하게 할 수 있습니다.

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(value = Exception.class)
    public ModelAndView defaultErrorHandler(HttpServletRequest req, Exception e) {
        ModelAndView mav = new ModelAndView();
        mav.addObject("exception", e);
        mav.addObject("url", req.getRequestURL());
        mav.setViewName("error");
        return mav;
    }
}
```

## 해결책 3: application.properties 설정 변경

`application.properties` 파일에서 `server.error.whitelabel.enabled=false`를 설정하면, Whitelabel 오류 페이지를 완전히 끌 수 있습니다. 이 경우 Spring Boot는 더 이상 Whitelabel 오류 페이지를 보여주지 않고, 대신에 빈 페이지를 보여줍니다.

## 주의사항

위의 방법들은 서로 다른 상황에서 유용할 수 있으므로, 어떤 방법이 여러분의 프로젝트에 가장 적합한지 고려해야 합니다. 또한, 예외 처리 로직을 구현할 때는 항상 세심한 주의가 필요합니다.

## 정리

Whitelabel Error Page는 개발 과정에서 유용하게 사용할 수 있지만, 사용자에게 보여주기에는 적절하지 않을 수 있습니다. 따라서 커스텀 오류 페이지를 만들거나, Controller에서 예외를 처리하거나, 설정 파일을 통해 Whitelabel을 비활성화할 수 있습니다. 이를 통해 더 나은 사용자 경험을 제공할 수 있습니다.