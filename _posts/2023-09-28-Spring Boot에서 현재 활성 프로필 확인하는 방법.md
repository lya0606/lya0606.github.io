---
title: Spring Boot에서 현재 활성 프로필 확인하는 방법
date: 2023-09-28 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 문제 상황

Stackoverflow에 올라온 질문에서는 Spring Boot를 사용할 때 어떻게 프로그래밍적으로 현재 활성화된 프로필을 확인할 수 있는지에 대해 논의되고 있습니다. 프로필이란, 어플리케이션의 설정을 다르게 할 수 있는 방법 중 하나입니다. 예를 들어 개발 환경과 운영 환경에서 다르게 동작해야 할 때 사용합니다.

## 해결 방안

### Environment 객체 사용

`Environment` 객체를 이용하면 현재 활성화된 프로필을 쉽게 확인할 수 있습니다. 이 객체는 Spring Framework에서 제공되며, 어플리케이션의 현재 상태나 설정 정보를 담고 있습니다.

```java
@Autowired
private Environment env;

public String getActiveProfile() {
    String[] profiles = env.getActiveProfiles();
    return profiles.length > 0 ? profiles[0] : null;
}
```

이 코드에서 `@Autowired` 어노테이션은 `Environment` 객체를 자동으로 주입해줍니다. 그 다음 `getActiveProfiles()` 메서드를 사용해 현재 활성화된 프로필을 가져올 수 있습니다.

### `@Profile` 어노테이션 사용

또 다른 방법은 `@Profile` 어노테이션을 사용하는 것입니다. 이 어노테이션을 사용하면 특정 프로필이 활성화될 때만 빈(bean)이 생성됩니다.

```java
@Bean
@Profile("dev")
public MyBean devBean() {
    return new MyDevBean();
}

@Bean
@Profile("prod")
public MyBean prodBean() {
    return new MyProdBean();
}
```

이 코드에서 `@Profile("dev")`와 `@Profile("prod")` 어노테이션은 각각 개발 환경과 운영 환경에서 사용될 빈을 정의합니다.

## 정리

Spring Boot에서 현재 활성화된 프로필을 확인하는 방법은 주로 두 가지입니다. 하나는 `Environment` 객체를 사용하는 것이고, 또 다른 하나는 `@Profile` 어노테이션을 사용하는 것입니다. 이 두 방법을 알고 있으면 환경에 따라 어플리케이션의 동작을 쉽게 조절할 수 있습니다.