---
title: Spring Boot에서 데이터베이스 관련 자동 설정 비활성화 방법
date: 2023-08-31 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - 데이터베이스
---
## 문제 상황

Spring Boot는 개발을 쉽고 빠르게 할 수 있도록 다양한 자동 설정을 제공합니다. 그러나 경우에 따라 이러한 자동 설정이 필요하지 않을 때가 있습니다. 특히 데이터베이스와 관련된 자동 설정을 비활성화하려는 경우가 이에 해당합니다.

## 해결 방법: `exclude` 속성 사용하기

Spring Boot에서 데이터베이스 관련 자동 설정을 비활성화하려면 `SpringBootApplication` 애너테이션에 `exclude` 속성을 사용해야 합니다. 이는 `SpringApplication` 클래스에 적용되며, 이를 통해 특정 자동 설정을 제외할 수 있습니다.

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class, DataSourceTransactionManagerAutoConfiguration.class, HibernateJpaAutoConfiguration.class})
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

위 코드에서는 `DataSourceAutoConfiguration`, `DataSourceTransactionManagerAutoConfiguration`, `HibernateJpaAutoConfiguration` 클래스를 `exclude` 속성을 사용해 제외했습니다.

## 속성 값에 대한 설명

- `DataSourceAutoConfiguration`: 데이터 소스 설정을 자동으로 구성합니다.
- `DataSourceTransactionManagerAutoConfiguration`: 트랜잭션 관리자 설정을 자동으로 구성합니다.
- `HibernateJpaAutoConfiguration`: Hibernate와 JPA 설정을 자동으로 구성합니다.

## `application.properties`에서 설정 비활성화하기

또 다른 방법으로는 `application.properties` 파일에서 설정을 비활성화할 수 있습니다.

```properties
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration,org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration
```

이렇게 하면 `SpringApplication`이 이 클래스들을 자동으로 설정하지 않습니다.

## 주의 사항

`exclude` 속성이나 `application.properties` 파일을 수정할 때는 주의가 필요합니다. 잘못 설정하면 애플리케이션의 다른 부분에 문제가 발생할 수 있습니다.

## 정리

Spring Boot에서 데이터베이스 관련 자동 설정을 비활성화하려면 `SpringBootApplication` 애너테이션의 `exclude` 속성을 사용하거나 `application.properties` 파일에서 설정을 수정할 수 있습니다. 이러한 방법을 통해 필요한 설정만을 적용하여 더 효율적인 애플리케이션을 구축할 수 있습니다.