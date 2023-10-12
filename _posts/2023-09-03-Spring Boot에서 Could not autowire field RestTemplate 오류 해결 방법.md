---
title: Spring Boot에서 Could not autowire field RestTemplate 오류 해결 방법
date: 2023-09-03 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot오류
---
## 오류 소개

Spring Boot에서 RESTful 웹 서비스를 개발하다 보면 `RestTemplate`을 사용하는 경우가 많습니다. `RestTemplate`은 HTTP 요청을 쉽게 보낼 수 있도록 도와주는 라이브러리입니다. 그러나 이를 사용하면서 다음과 같은 오류 메시지가 발생할 수 있습니다: 

```
Could not autowire field:RestTemplate
```

이 오류는 Spring Boot에서 `RestTemplate`을 자동으로 주입(Autowire)하지 못했다는 것을 의미합니다. 주입이란, 개발자가 직접 객체를 생성하지 않고, 프레임워크가 필요한 객체를 알아서 만들어 주는 것을 말합니다.

## 원인과 해결 방법

### 원인 1: `RestTemplate` 빈 미선언

이 오류의 가장 흔한 원인은 `RestTemplate` 클래스의 빈(Bean)을 선언하지 않았을 때 발생합니다. 빈은 Spring에서 객체를 관리하는 기본 단위입니다.

#### 해결 방법
`@SpringBootApplication`이 있는 메인 클래스나 `@Configuration`이 붙은 설정 클래스에서 다음과 같이 `RestTemplate` 빈을 선언하세요.

```java
@Bean
public RestTemplate restTemplate() {
    return new RestTemplate();
}
```

### 원인 2: 패키지 스캔 오류

때로는 `@ComponentScan`이 정확한 패키지를 스캔하지 못하여 이 오류가 발생할 수 있습니다. 패키지 스캔은 Spring Boot가 자동으로 설정을 로드하거나 빈을 찾는 과정에서 특정 패키지 내의 클래스를 찾아주는 기능입니다.

#### 해결 방법
`@ComponentScan` 애노테이션을 사용하여 정확한 패키지명을 명시하세요.

```java
@ComponentScan(basePackages = {"com.example"})
```

### 원인 3: 의존성 문제

프로젝트의 `pom.xml` 파일에 `spring-boot-starter-web` 의존성이 누락된 경우도 있습니다. 의존성은 프로젝트가 정상적으로 작동하기 위해 필요한 외부 라이브러리를 의미합니다.

#### 해결 방법
`pom.xml` 파일에 다음과 같이 의존성을 추가하세요.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

이렇게 각각의 원인과 해결 방법을 알아보았습니다. 이를 통해 `Could not autowire field:RestTemplate` 오류를 해결할 수 있을 것입니다.