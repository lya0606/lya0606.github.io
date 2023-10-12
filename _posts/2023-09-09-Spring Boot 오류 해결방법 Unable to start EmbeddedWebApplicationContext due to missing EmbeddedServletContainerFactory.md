---
title: Spring Boot 오류 해결방법 Unable to start EmbeddedWebApplicationContext due to missing EmbeddedServletContainerFactory
date: 2023-09-09 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot오류
---
## 문제 상황 소개

"Unable to start EmbeddedWebApplicationContext due to missing EmbeddedServletContainerFactory" 오류는 Spring Boot 애플리케이션을 실행할 때 자주 발생합니다. 이 오류는 내장 웹 서버가 없거나 제대로 구성되지 않았을 때 나타납니다. 이 문제로 인해 애플리케이션을 정상적으로 실행할 수 없게 됩니다.

## 원인 파악

이 오류의 주된 원인은 다음과 같습니다:

1. **의존성 누락**: 내장 웹 서버와 관련된 의존성이 누락되었을 가능성이 있습니다. Spring Boot에서는 주로 `spring-boot-starter-web` 이라는 의존성을 사용합니다.
2. **버전 충돌**: 사용 중인 라이브러리들 사이에 버전 충돌이 발생했을 수 있습니다. 이는 의존성 관리에 문제를 일으킬 수 있습니다.

## 해결 방법 1: 의존성 확인

먼저 `pom.xml` 파일 또는 `build.gradle` 파일에서 다음과 같이 `spring-boot-starter-web` 의존성이 있는지 확인하세요.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

이 의존성은 Spring Boot 프로젝트에서 웹 기능을 사용할 수 있게 해줍니다. 빠져 있다면 추가해 주세요.

## 해결 방법 2: 버전 충돌 해결

프로젝트에 여러 버전의 Spring 라이브러리가 있는 경우, 이를 해결해야 합니다. 가장 간단한 방법은 Spring Boot의 부모 의존성을 사용하는 것입니다.

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.6.0</version>
</parent>
```

이렇게 하면 Spring Boot가 알아서 의존성 버전을 관리해줍니다.

## 해결 방법 3: 설정 파일 확인

`application.properties` 또는 `application.yml` 파일에서 웹 서버 설정이 올바른지 확인해 보세요. 특히, 포트 충돌이 없는지, 그리고 필요한 설정값이 누락되지 않았는지 주의깊게 살펴보세요.

## 마무리

"Unable to start EmbeddedWebApplicationContext due to missing EmbeddedServletContainerFactory" 오류는 주로 의존성 누락이나 버전 충돌, 설정 문제로 발생합니다. 이 문제를 해결하기 위해 의존성을 확인하고, 버전을 일치시키며, 설정 파일을 점검해야 합니다. 이를 통해 Spring Boot 애플리케이션을 안정적으로 실행할 수 있을 것입니다.