---
title: Spring Boot에서 Tomcat 실행시 사용자명과 비밀번호 이해하기
date: 2023-09-01 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - Tomcat
---
## Spring Boot과 Tomcat 기본 인증

Spring Boot에서 Tomcat을 사용할 때 사용자명과 비밀번호는 보안을 위해 중요한 부분입니다. 이 정보가 없으면, 웹 애플리케이션의 관리자 페이지에 접근할 수 없을 것입니다. 대부분의 경우 Spring Boot는 `application.properties` 또는 `application.yml` 파일에서 이러한 설정을 관리합니다.

## 자동 생성된 사용자명과 비밀번호

Spring Boot 애플리케이션을 처음 실행할 때, 터미널에서 `Using generated security password: [암호]`라는 메시지를 볼 수 있습니다. 이것이 바로 자동으로 생성된 비밀번호입니다. 사용자명은 기본적으로 'user'로 설정되어 있습니다. 이 자동 생성된 비밀번호는 매번 애플리케이션을 시작할 때마다 변경됩니다.

## 사용자명과 비밀번호 설정 변경하기

`application.properties` 파일에 다음과 같이 작성하면 사용자명과 비밀번호를 직접 설정할 수 있습니다.

```properties
spring.security.user.name=내사용자명
spring.security.user.password=내비밀번호
```

## 오류 해결: `Bad credentials`

'Bad credentials' 오류는 사용자명 또는 비밀번호가 잘못되었을 때 발생합니다. 이 오류가 발생하면, `application.properties` 또는 터미널에서 제공된 정보가 정확한지 확인해야 합니다.

## 정리

Spring Boot와 Tomcat에서 사용자명과 비밀번호는 애플리케이션의 보안을 강화합니다. 이 설정은 `application.properties` 파일에서 관리되며, 이를 통해 원하는 사용자명과 비밀번호로 쉽게 변경할 수 있습니다. 'Bad credentials' 같은 오류가 발생하면, 설정을 다시 확인하면 해결할 수 있습니다. 이렇게 하면 안전하고 효율적인 웹 애플리케이션을 만들 수 있습니다.