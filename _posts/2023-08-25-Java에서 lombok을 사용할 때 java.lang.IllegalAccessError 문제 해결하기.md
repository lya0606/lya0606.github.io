---
title: Java에서 lombok을 사용할 때 java.lang.IllegalAccessError 문제 해결하기
date: 2023-08-25 20:00:00 +0900
categories:
  - Spring
tags:
  - JavaScript시간
  - lombok
---
## 문제 상황

Java 프로젝트에서 lombok 라이브러리를 사용하면서 다음과 같은 오류가 발생할 수 있습니다.

```
java.lang.IllegalAccessError: class lombok.javac.apt.LombokProcessor cannot access its superclass com.sun.tools.javac.processing.JavacProcessingEnvironment
```

이 오류는 lombok 라이브러리와 Java 컴파일러 간의 접근 제한 때문에 발생하는 문제입니다. 이 글에서는 이 문제를 어떻게 해결할 수 있는지 알아보겠습니다.

## 해결 방법 1: lombok 버전 업데이트

가장 간단한 해결 방법은 lombok 라이브러리의 최신 버전을 사용하는 것입니다. 의존성 관리 도구를 사용하고 있다면, `pom.xml` 또는 `build.gradle` 파일에서 lombok 의존성의 버전을 최신으로 변경해 주세요.

```xml
<!-- Maven 예시 -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>최신 버전</version>
</dependency>
```

## 해결 방법 2: Java 버전 호환성 확인

Java 버전이 lombok 라이브러리와 호환되지 않을 경우에도 이러한 문제가 발생할 수 있습니다. 호환성이란 두 프로그램이 문제 없이 함께 작동할 수 있는 능력을 말합니다. 따라서 사용 중인 Java 버전과 lombok 버전이 서로 호환되는지 확인하는 것이 중요합니다.

## 해결 방법 3: IDE 설정 확인

개발 환경(IDE) 설정이 잘못되어 있을 수도 있습니다. 예를 들어, IntelliJ IDEA에서는 `File > Invalidate Caches / Restart...`를 선택하여 캐시를 지우고 다시 시작할 수 있습니다. 이렇게 하면 잘못된 설정이 초기화되어 문제가 해결될 가능성이 있습니다.

## 해결 방법 4: 의존성 충돌 확인

의존성 충돌이란 두 개 이상의 라이브러리가 서로 다른 버전의 동일한 라이브러리를 필요로 할 때 발생합니다. 이러한 경우, `pom.xml` 또는 `build.gradle` 파일에서 의존성을 명시적으로 관리하여 문제를 해결할 수 있습니다.

## 결론

`java.lang.IllegalAccessError`는 여러 가지 원인으로 발생할 수 있으므로, 위에서 소개한 여러 해결 방법을 차례대로 시도해보는 것이 좋습니다. 이를 통해 Java 프로젝트에서 lombok 라이브러리를 안정적으로 사용할 수 있을 것입니다.