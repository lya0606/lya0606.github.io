---
title: Spring Boot 어플리케이션 정상 종료 방법
date: 2023-10-08 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 개요

Spring Boot는 자바 기반의 웹 어플리케이션을 빠르고 쉽게 개발할 수 있도록 도와주는 프레임워크입니다. 하지만 개발 과정에서 어플리케이션을 종료할 필요가 있을 때, 정상적인 방법으로 종료하는 것이 중요합니다. 이 글에서는 Spring Boot 어플리케이션을 올바르게 종료하는 여러 방법에 대해 자세히 설명하겠습니다.

## 실행 중인 Spring Boot 어플리케이션 종료

어플리케이션이 실행 중일 때 종료하려면 여러 가지 방법이 있습니다. 가장 흔하게 사용되는 방법 중 하나는 `CTRL + C` 키 조합을 이용하는 것입니다. 이 조합을 누르면, Spring Boot 어플리케이션은 현재 진행 중인 모든 작업을 중단하고 종료됩니다. 하지만 이 방법은 터미널을 통해 직접 실행한 경우에만 적용됩니다.

## `System.exit()` 메서드 사용

`System.exit()`는 자바에서 제공하는 표준 메서드입니다. 이 메서드를 호출하면, JVM(Java Virtual Machine)이 종료됩니다. Spring Boot 어플리케이션 내부에서 이 메서드를 호출하면, 어플리케이션도 함께 종료됩니다. 코드 예시는 다음과 같습니다.

```java
System.exit(0);
```

여기서 0은 종료 상태 코드입니다. 일반적으로 0은 정상 종료를 의미합니다.

## `SpringApplication.exit()` 메서드 사용

Spring Boot에서는 `SpringApplication.exit()` 메서드도 제공합니다. 이 메서드를 사용하면, Spring 컨테이너가 관리하는 모든 빈(Bean)들이 소멸됩니다. 이 방법은 Spring Boot가 관리하는 자원을 더 안전하게 해제할 수 있습니다.

```java
ApplicationContext ctx = SpringApplication.run(Application.class, args);

int exitCode = SpringApplication.exit(ctx, () -> 0);

System.exit(exitCode);
```

## `shutdown` 엔드포인트 사용

Spring Boot 2.x부터는 `actuator` 의존성을 추가하면 `shutdown` 엔드포인트를 사용할 수 있습니다. 이 엔드포인트를 호출하면, 어플리케이션은 정상적으로 종료됩니다. 하지만 이 기능은 기본적으로 비활성화되어 있으므로, 활성화해야 사용할 수 있습니다.

## 결론

Spring Boot 어플리케이션을 올바르게 종료하는 방법은 여러 가지가 있습니다. 필요에 따라 가장 적절한 방법을 선택하여 사용하면 됩니다. 이렇게 하면 리소스가 효율적으로 해제되고, 문제가 발생할 확률을 줄일 수 있습니다.