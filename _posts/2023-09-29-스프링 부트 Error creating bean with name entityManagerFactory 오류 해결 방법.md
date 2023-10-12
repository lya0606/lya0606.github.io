---
title: 스프링 부트 Error creating bean with name entityManagerFactory 오류 해결 방법
date: 2023-09-29 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 오류 상황 및 원인 파악

Spring Boot 프로젝트에서는 종종 'Error creating bean with name 'entityManagerFactory''라는 오류가 발생합니다. 이 문제는 주로 Spring Data JPA나 Hibernate와 관련된 설정이나 의존성 문제 때문에 발생합니다. 'Bean'이란 스프링에서 객체를 관리하는 단위이고, 'entityManagerFactory'는 데이터베이스 연결과 트랜잭션을 관리하는 중요한 객체입니다. 이 오류가 발생하면 프로젝트가 정상적으로 작동하지 않으므로 해결책을 찾아야 합니다.

## 의존성 문제 해결

가장 먼저 확인해야 할 것은 `pom.xml` 또는 `build.gradle` 파일입니다. 여기서 프로젝트의 의존성이 정의되는데, JPA 또는 Hibernate와 관련된 라이브러리가 올바르게 추가되었는지 확인해야 합니다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

## 설정 파일 검토

다음으로 `application.properties` 또는 `application.yml` 설정 파일을 검토합니다. 여기에서 데이터베이스 연결 정보, JPA 설정 등이 정의됩니다. 잘못된 설정이 있을 경우, 'entityManagerFactory' 빈 생성에 실패할 수 있습니다.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
```

## 어노테이션 확인

마지막으로 소스 코드 상에서 `@Entity`, `@Table`, `@Repository` 등의 어노테이션이 올바르게 사용되었는지 확인합니다. 예를 들어, `@Entity` 어노테이션이 붙은 클래스에는 기본 생성자가 반드시 있어야 합니다.

## 마치며

'Error creating bean with name 'entityManagerFactory'' 오류는 보통 프로젝트 설정이나 의존성, 어노테이션 사용에 문제가 있을 때 발생합니다. 위의 방법을 차례대로 따라 해결책을 찾아보세요. 이를 통해 프로젝트가 원활하게 동작하도록 만들 수 있습니다.