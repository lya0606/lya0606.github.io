---
title: JAR 파일 내부의 파일이 Spring에서 보이지 않는 문제 해결하기
date: 2023-10-06 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - JAR내부파일
---
## 문제 상황 설명

Spring 프레임워크를 사용하다보면, JAR 파일 내부에 있는 리소스나 설정 파일을 불러와야 할 때가 있습니다. 그런데 때로는 이러한 파일들이 제대로 인식되지 않는 문제가 발생합니다. 이러한 문제를 **File Inside JAR is Not Visible for Spring**라고 부릅니다.

## 원인 분석

이 문제가 발생하는 주요 원인은 대게 두 가지입니다.

1. **파일 경로 문제**: 파일의 경로가 잘못 지정되었을 수 있습니다. 상대 경로와 절대 경로를 혼동하여 사용할 경우 이러한 문제가 발생할 수 있습니다.
   
2. **리소스 로딩 메커니즘**: Spring에서는 `ClassPathResource`나 `ResourceLoader` 같은 특별한 클래스를 사용하여 리소스를 로딩합니다. 이러한 메커니즘이 제대로 작동하지 않을 경우 파일을 찾을 수 없습니다.

## 해결 방법

### 파일 경로 확인

첫 번째로, 파일 경로가 올바르게 설정되어 있는지 확인합니다. 절대 경로는 피하고, 상대 경로를 사용하여 프로젝트 내의 리소스를 참조해야 합니다.

### `ClassPathResource` 사용

`ClassPathResource` 클래스를 사용하여 리소스를 로딩할 수 있습니다. 이 클래스는 클래스패스에 있는 리소스를 찾을 때 유용합니다. 예를 들어, 아래와 같이 사용할 수 있습니다.

```java
ClassPathResource resource = new ClassPathResource("file_inside_jar.txt");
```

### `ResourceLoader` 사용

`ResourceLoader` 또한 유용한 방법입니다. 이를 사용하면 더 유연한 리소스 로딩이 가능합니다.

```java
Resource resource = resourceLoader.getResource("classpath:file_inside_jar.txt");
```

## 마무리

JAR 파일 내의 파일이 Spring에서 보이지 않는 문제는 파일 경로 문제나 리소스 로딩 메커니즘의 문제일 가능성이 높습니다. 이를 해결하기 위해 경로를 정확히 지정하고, `ClassPathResource`나 `ResourceLoader`를 올바르게 사용해야 합니다. 이렇게 하면 문제를 해결할 수 있을 것입니다.