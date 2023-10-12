---
title: Spring MVC에서 컨트롤러 액션을 통한 외부 URL 리디렉션 방법
date: 2023-09-21 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - URL리디렉션
---
## 오류 상황과 해결 목표

많은 Spring MVC 사용자들이 특정 상황에서 외부 URL로 리디렉션하는 문제에 직면하곤 합니다. 예를 들어, 사용자가 어떤 버튼을 클릭하면 외부 웹사이트로 이동해야 할 때, 이런 기능은 어떻게 구현하는 것이 좋을까요? 이 문제에 대한 해결책을 아주 구체적으로 살펴보겠습니다.

## `redirect:` 접두어 사용하기

Spring MVC에서는 `redirect:` 접두어를 사용하여 이 작업을 쉽게 할 수 있습니다. 컨트롤러에서 리턴하는 문자열 앞에 `redirect:`를 붙이면, 리턴 문자열이 URL로 인식되어 해당 URL로 리디렉션됩니다. 이러한 방식은 내부 URL뿐만 아니라 외부 URL로의 리디렉션에도 사용할 수 있습니다.

```java
@RequestMapping("/redirectExample")
public String redirectToExternalUrl() {
    return "redirect:https://www.google.com";
}
```

## `HttpServletResponse`를 이용한 방법

또 다른 방법은 Java의 `HttpServletResponse` 객체를 사용하는 것입니다. `sendRedirect()` 메소드를 통해 외부 URL로 리디렉션할 수 있습니다.

```java
@RequestMapping("/redirectExample")
public void redirectToExternalUrl(HttpServletResponse response) throws IOException {
    response.sendRedirect("https://www.google.com");
}
```

## `ModelAndView` 활용하기

`ModelAndView` 객체를 사용하는 세 번째 방법도 있습니다. 이 객체를 생성하고 `setViewName()` 메소드에 리디렉트할 URL을 설정하면 됩니다.

```java
@RequestMapping("/redirectExample")
public ModelAndView redirectToExternalUrl() {
    ModelAndView modelAndView = new ModelAndView();
    modelAndView.setViewName("redirect:https://www.google.com");
    return modelAndView;
}
```

## 주의사항

이러한 방법들은 대부분의 경우에 효과적이지만, 리디렉션을 하기 전에 특별한 로직이 필요한 경우도 있을 수 있습니다. 예를 들어, 특정 데이터를 전달해야 하거나 리디렉션 전에 데이터베이스를 업데이트 해야 할 수도 있습니다. 이 경우에는 적절한 로직을 먼저 수행한 후 리디렉션을 하면 됩니다.

## 결론

Spring MVC에서 외부 URL로 리디렉션하는 방법은 다양합니다. 사용자의 요구에 가장 적합한 방법을 선택하여 구현할 수 있습니다. 이 글을 통해 `redirect:` 접두어 사용, `HttpServletResponse` 사용, 그리고 `ModelAndView` 객체 활용 세 가지 방법에 대해 알게 되셨을 것입니다. 이 중에서 자신의 상황에 가장 맞는 방법을 선택하여 사용하시면 됩니다.