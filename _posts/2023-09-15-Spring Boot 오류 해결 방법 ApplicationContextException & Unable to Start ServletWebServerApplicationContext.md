---
title: Spring Boot 오류 해결 방법 ApplicationContextException & Unable to Start ServletWebServerApplicationContext
date: 2023-09-15 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot오류
---
## 원인 파악하기

이 오류는 주로 두 가지 원인에서 발생합니다:

1. **포트 충돌**: 이미 사용 중인 포트에 애플리케이션을 실행하려고 할 때 발생합니다.
2. **잘못된 설정**: `application.properties` 또는 `application.yml` 파일에 잘못된 설정이 있을 경우 발생합니다.

## 해결 방법

### 포트 충돌 해결

1. **명령어 사용**: 터미널에서 다음과 같은 명령어를 입력하여 해당 포트를 사용하고 있는 프로세스를 종료합니다.

    ```
    kill $(lsof -t -i:포트번호)
    ```

2. **포트 변경**: `application.properties` 파일에서 다음과 같이 포트를 변경합니다.

    ```
    server.port=새로운_포트_번호
    ```

### 잘못된 설정 수정

1. **문법 검사**: 설정 파일의 문법이 올바른지 확인합니다.
2. **의존성 확인**: `pom.xml` 또는 `build.gradle` 파일에서 필요한 의존성이 모두 추가되었는지 확인합니다.

## 주의할 점

1. **백업**: 작업을 시작하기 전에 현재 설정을 백업해 두는 것이 좋습니다.
2. **로그 확인**: 오류 메시지 외에도 로그를 자세히 확인하여 추가적인 정보를 얻습니다.

이렇게 해서 `ApplicationContextException: Unable to Start ServletWebServerApplicationContext` 오류를 해결할 수 있습니다. 설정과 포트를 정확히 확인하면 이 문제를 쉽게 해결할 수 있습니다.