---
title: Spring AOP과 AspectJ 무엇이 다를까요
date: 2023-08-28 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringAOP
  - AspectJ
---
## Spring AOP의 개요

Spring AOP (Aspect-Oriented Programming)은 Spring 프레임워크의 일부입니다. 이는 주로 스프링 기반의 애플리케이션에서 관점 지향 프로그래밍을 가능하게 하며, 횡단 관심사(cross-cutting concerns)를 분리할 수 있게 도와줍니다. 예를 들어, 로깅이나 보안과 같은 기능을 중복 없이 관리할 수 있습니다.

## AspectJ의 개요

AspectJ는 Eclipse Foundation에서 개발한 독립적인 관점 지향 프로그래밍 프레임워크입니다. 이는 Java와 완전히 통합될 수 있으며, 복잡한 조인 포인트(join points)와 어드바이스(advice)를 사용하여 더욱 세밀한 제어를 할 수 있습니다.

## 핵심 차이점

### 제한 범위
- **Spring AOP**: 프록시 기반의 AOP만 지원합니다. 이는 스프링 빈에서만 AOP를 적용할 수 있다는 것을 의미합니다.
- **AspectJ**: 컴파일 타임, 로드 타임 모두에 걸쳐 AOP를 적용할 수 있습니다.

### 성능
- **Spring AOP**: 런타임에 AOP 기능이 적용되므로 약간의 성능 오버헤드가 발생할 수 있습니다.
- **AspectJ**: 컴파일 타임에 AOP 기능이 적용되므로 성능에 거의 영향을 미치지 않습니다.

### 복잡성과 유연성
- **Spring AOP**: 설정이 비교적 간단하고, 스프링과 통합하기 쉽습니다.
- **AspectJ**: 더 복잡한 조인 포인트와 어드바이스를 지원하며, 더욱 유연한 설정이 가능합니다.

### 코드 중첩
- **Spring AOP**: 코드 중첩이 더 적고, 코드가 깔끔합니다.
- **AspectJ**: 더욱 복잡한 기능을 지원하기 때문에 코드가 복잡할 수 있습니다.

### 사용 사례
- **Spring AOP**: 로깅, 트랜잭션 관리, 보안 등 기본적인 사용 사례에 적합합니다.
- **AspectJ**: 더 복잡하고 세부적인 제어가 필요한 고급 사용 사례에 적합합니다.

## 결론

Spring AOP와 AspectJ는 모두 관점 지향 프로그래밍의 강력한 도구입니다. 하지만 사용 사례, 필요한 세부 제어 수준, 성능 등을 고려하여 적절한 툴을 선택하는 것이 중요합니다.