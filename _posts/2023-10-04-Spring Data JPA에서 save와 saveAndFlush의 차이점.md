---
title: Spring Data JPA에서 save와 saveAndFlush의 차이점
date: 2023-10-04 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringDataJPA
  - save
  - saveAndFlush
---
## 개요

Spring Data JPA는 데이터베이스 작업을 단순화하기 위한 도구입니다. 여기서 `save`와 `saveAndFlush` 메소드가 종종 사용됩니다. 이 두 메소드의 작동 방식과 차이점을 이해하면, 더 효율적으로 데이터를 처리할 수 있습니다.

## save 메소드

`save` 메소드는 객체를 데이터베이스에 저장합니다. 이 메소드는 보통 트랜잭션 범위 내에서 실행되며, 해당 트랜잭션이 끝날 때까지 실제 데이터베이스에 즉시 저장되지 않을 수 있습니다. 즉, `save`는 데이터를 임시 메모리 버퍼에 저장하고, 트랜잭션이 커밋될 때 실제로 데이터베이스에 반영됩니다.

### 사용 예시

```java
@Entity
public class Person {
    // 멤버 변수와 Getter, Setter
}

@Autowired
PersonRepository personRepository;

public void addPerson(Person person) {
    personRepository.save(person);
}
```

## saveAndFlush 메소드

`saveAndFlush` 메소드는 `save`와 유사하게 동작하지만, 이 메소드를 호출하면 즉시 데이터베이스에 저장됩니다. 즉, 임시 메모리 버퍼를 거치지 않고 바로 데이터베이스에 쓰기 작업이 이루어집니다.

### 사용 예시

```java
@Entity
public class Person {
    // 멤버 변수와 Getter, Setter
}

@Autowired
PersonRepository personRepository;

public void addPersonAndFlush(Person person) {
    personRepository.saveAndFlush(person);
}
```

## 언제 어떤 메소드를 사용할까?

- `save`는 일반적으로 대부분의 상황에서 충분합니다. 특히 여러 개의 데이터를 처리할 때는 `save`를 사용하면 성능이 좋아질 수 있습니다.
- `saveAndFlush`는 특정 작업이 즉시 데이터베이스에 반영되어야 할 때 유용합니다. 예를 들어, 실시간으로 사용자에게 데이터를 보여줘야 하는 경우에 사용될 수 있습니다.

## 결론

`save`와 `saveAndFlush`는 Spring Data JPA에서 데이터를 저장하는 두 가지 주요 방법입니다. `save`는 일반적인 경우에 사용되며, `saveAndFlush`는 즉시 반영이 필요할 때 사용됩니다. 어떤 상황에서 어떤 메소드를 사용할지 판단하려면 해당 작업의 요구사항과 데이터베이스의 성능을 고려해야 합니다.