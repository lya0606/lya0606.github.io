---
title: Spring Boot에서 여러 외부 설정 파일 다루기
date: 2023-09-27 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## Spring Boot란 무엇인가?

Spring Boot는 자바 기반의 웹 어플리케이션을 빠르고 쉽게 개발할 수 있도록 도와주는 프레임워크입니다. 이 프레임워크를 사용하면 설정이 쉬워져서 개발 과정이 단순해집니다. 그러나 때로는 복잡한 프로젝트에서 여러 개의 설정 파일을 관리해야 할 필요가 있습니다.

## 여러 설정 파일을 왜 사용하는가?

대규모 프로젝트나 여러 환경(개발, 테스트, 프로덕션 등)에서 동작하는 어플리케이션의 경우, 하나의 설정 파일로는 모든 정보를 관리하기 어렵습니다. 이런 경우에 여러 설정 파일을 사용하여 각 환경에 맞게 설정을 분리하곤 합니다.

## `application.properties`와 `application.yml`

Spring Boot에서는 기본적으로 `application.properties` 또는 `application.yml` 파일을 사용하여 설정을 관리합니다. 이 파일들은 프로젝트의 `src/main/resources` 디렉토리에 위치해야 합니다.

## 여러 외부 설정 파일 사용하기

그렇다면 여러 개의 외부 설정 파일을 어떻게 사용할까요? `--spring.config.name`와 `--spring.config.location` 이라는 두 가지 파라미터를 사용할 수 있습니다.

### `--spring.config.name`

이 파라미터를 사용하면 기본 설정 파일 이름을 변경할 수 있습니다. 예를 들어, `--spring.config.name=my-config`를 지정하면 `my-config.properties` 또는 `my-config.yml` 파일을 찾게 됩니다.

### `--spring.config.location`

이 파라미터를 사용하면 설정 파일의 위치를 지정할 수 있습니다. 예를 들어, `--spring.config.location=/etc/myapp/`를 지정하면 `/etc/myapp/` 디렉토리에 있는 설정 파일을 사용하게 됩니다.

## 주의할 점

- 설정 파일들은 순서대로 읽히며, 나중에 읽힌 설정이 이전 설정을 덮어씁니다.
- 위의 파라미터들은 프로그램 실행 시 커맨드 라인에서 지정할 수도 있고, 환경 변수로도 설정할 수 있습니다.

## 오류 해결: `FileNotFoundException`

여러 외부 설정 파일을 사용할 때 주의해야 할 오류 중 하나는 `FileNotFoundException`입니다. 이 오류는 지정한 위치에 설정 파일이 없을 때 발생합니다. 따라서 설정 파일의 경로와 이름을 정확하게 지정해야 합니다.

이렇게 Spring Boot에서 여러 외부 설정 파일을 효율적으로 관리하는 방법에 대해 알아보았습니다. 이 정보가 여러분의 Spring Boot 프로젝트에 유용하게 적용되길 바랍니다.