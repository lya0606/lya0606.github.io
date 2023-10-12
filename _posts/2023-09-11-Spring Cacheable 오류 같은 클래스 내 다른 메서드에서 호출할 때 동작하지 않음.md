---
title: Spring Cacheable 오류 같은 클래스 내 다른 메서드에서 호출할 때 동작하지 않음
date: 2023-09-11 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Cacheable오류
---
## 문제 상황

`@Cacheable` 어노테이션은 스프링 프레임워크에서 제공하는 캐싱 기능을 구현할 때 사용됩니다. 그러나 이 어노테이션을 같은 클래스 내의 다른 메서드에서 호출하면 캐시가 동작하지 않는 문제가 발생할 수 있습니다.

## 원인

이 문제는 스프링 프레임워크의 프록시(proxy) 기반의 AOP(Aspect-Oriented Programming, 관점 지향 프로그래밍) 메커니즘 때문에 발생합니다. 프록시란 특정 객체를 대신해서 처리하는 중개자 역할을 하는 객체입니다. 스프링에서 `@Cacheable` 같은 어노테이션은 프록시를 통해 동작하는데, 같은 클래스 내의 메서드에서 다른 메서드를 직접 호출하면 프록시를 거치지 않고 호출됩니다. 그래서 캐시 기능이 동작하지 않게 됩니다.

## 해결 방법

### 내부 메서드 호출을 프록시를 통해 하기
스프링의 `ApplicationContext` 또는 `AopContext`를 사용하여 현재 프록시된 객체를 얻을 수 있습니다. 이렇게 얻은 객체를 통해 메서드를 호출하면 캐시가 동작합니다.

```java
@Service
public class MyService {
    @Autowired
    private ApplicationContext context;

    public void someMethod() {
        MyService proxy = context.getBean(MyService.class);
        proxy.cachedMethod();
    }

    @Cacheable("myCache")
    public void cachedMethod() {
        // Do something
    }
}
```

### 캐시 로직을 별도의 클래스로 분리
캐싱이 필요한 로직을 별도의 클래스로 옮기고 그 클래스의 메서드에 `@Cacheable`을 적용합니다. 이렇게 하면 다른 클래스에서 호출할 때는 무조건 프록시를 거쳐 호출되므로 캐시가 정상적으로 동작합니다.

```java
@Service
public class MyCacheService {
    @Cacheable("myCache")
    public void cachedMethod() {
        // Do something
    }
}

@Service
public class MyService {
    @Autowired
    private MyCacheService cacheService;

    public void someMethod() {
        cacheService.cachedMethod();
    }
}
```

## 결론

스프링의 `@Cacheable` 어노테이션이 같은 클래스 내 다른 메서드에서 호출될 때 동작하지 않는 문제는 프록시 기반의 동작 방식 때문입니다. 이 문제를 해결하기 위해서는 내부 메서드 호출을 프록시를 통해 하거나, 캐시 로직을 별도의 클래스로 분리하는 방법이 있습니다.