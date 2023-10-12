---
title: Spring Boot에서 application.yml과 환경 변수의 연동 방법
date: 2023-09-10 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - 환경변수
---
## 개요

Spring Boot는 설정 관리를 위해 `application.yml` 파일을 널리 사용합니다. 이 파일을 통해 애플리케이션의 다양한 설정을 관리할 수 있습니다. 하지만 고정된 값만을 사용하는 것은 실제 운영 환경에서 무리가 있을 수 있습니다. 이런 문제를 해결하기 위해 환경 변수를 `application.yml`에 연동하는 방법을 살펴봅니다.

## 환경 변수란?

환경 변수(Environment Variable)는 운영 체제에서 사용하는 다양한 정보를 담고 있는 변수입니다. 예를 들어, 데이터베이스의 주소나 비밀번호와 같은 민감한 정보를 코드에 직접 적지 않고 환경 변수를 통해 관리할 수 있습니다.

## Spring Boot와 환경 변수 연동하기

Spring Boot에서는 `${}` 표기법을 사용하여 환경 변수를 `application.yml` 파일에 쉽게 연동할 수 있습니다. 예를 들어, 데이터베이스 연결 정보를 환경 변수로 설정하려면 다음과 같이 작성할 수 있습니다.

```yml
database:
  url: ${DATABASE_URL}
  username: ${DATABASE_USERNAME}
  password: ${DATABASE_PASSWORD}
```

이렇게 하면 `DATABASE_URL`, `DATABASE_USERNAME`, `DATABASE_PASSWORD`라는 이름의 환경 변수가 자동으로 해당 위치에 적용됩니다.

## 주의사항

- 환경 변수의 이름은 대소문자를 구분합니다. 환경 변수를 설정할 때 이를 주의해야 합니다.
- 환경 변수가 없을 경우 기본값을 설정할 수도 있습니다. 예: `${DATABASE_URL:default_value}`

## 결론

환경 변수와 `application.yml` 파일을 연동하면 설정 정보를 더 유연하게 관리할 수 있습니다. Spring Boot에서는 이를 매우 간단하게 설정할 수 있으므로, 실제 운영 환경에서도 큰 도움이 될 것입니다. 이렇게 설정을 통해 애플리케이션을 더 안정적이고 효율적으로 운영할 수 있습니다.