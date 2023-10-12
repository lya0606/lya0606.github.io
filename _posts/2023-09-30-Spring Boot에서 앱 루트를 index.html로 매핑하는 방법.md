---
title: Spring Boot에서 앱 루트를 index.html로 매핑하는 방법
date: 2023-09-30 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 서론

Spring Boot는 Java 기반의 웹 애플리케이션을 빠르게 개발하고 배포할 수 있는 프레임워크입니다. 웹 애플리케이션을 만들 때 가장 처음 보여지는 페이지를 설정하는 것은 중요한 작업 중 하나입니다. 이 페이지를 '루트' 또는 '홈 페이지'라고 부릅니다. 이 글에서는 Spring Boot에서 앱 루트를 `index.html`로 어떻게 설정하는지 자세히 알아보겠습니다.

## Static Resource 설정하기

Spring Boot에서는 `src/main/resources/static` 폴더 내에 위치한 `index.html` 파일을 기본적으로 루트 페이지로 사용합니다. 이렇게 하면 별도의 설정이나 코드 작성 없이도 웹 애플리케이션의 루트 페이지가 `index.html`이 됩니다.

## Controller를 이용한 설정

또 다른 방법은 Java Controller를 사용하는 것입니다. `@Controller` 어노테이션을 사용하여 특정 URL 경로에 접근했을 때 보여질 페이지를 지정할 수 있습니다.

```java
@Controller
public class MainController {
    @RequestMapping("/")
    public String index() {
        return "index";
    }
}
```

## 에러명과 문제 해결

만약 이 설정이 제대로 작동하지 않는다면, `Whitelabel Error Page`라는 에러 메시지를 볼 수 있습니다. 이 문제를 해결하기 위해서는 위에서 설명한 설정이 올바르게 적용되었는지 확인해야 합니다.

## 요약

Spring Boot에서 앱 루트를 `index.html`로 설정하는 것은 매우 간단합니다. `static` 폴더를 사용하거나, `@Controller`를 이용하여 원하는 루트 페이지를 지정할 수 있습니다. 설정이 올바르지 않을 경우에는 `Whitelabel Error Page` 에러가 발생하므로, 설정을 철저히 확인해야 합니다. 이렇게 하면 원활한 웹 애플리케이션 구동이 가능합니다.