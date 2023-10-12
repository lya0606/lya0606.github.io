---
title: JPARepository에서 DML 연산 지원 안 함 DELETE Query 문제 해결하기
date: 2023-10-05 20:00:00 +0900
categories:
  - Spring
tags:
  - JPARepository
  - DML연산
  - DELETEQuery
---
## 문제 상황

JPARepository에서 `@Query` 어노테이션을 사용하여 DELETE 쿼리를 실행하려고 할 때, "not supported for DML operations"라는 에러가 발생하는 문제가 있습니다. 이 에러는 JPA에서 데이터 조작 언어(DML: Data Manipulation Language) 연산을 지원하지 않기 때문에 나타납니다.

## 원인과 해결방법

### 원인 파악

이 에러는 JPA가 DML 연산을 처리하는 방식과 관련이 있습니다. 일반적으로, JPA는 조회(Select) 쿼리는 문제 없이 처리하지만, 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 DML 연산은 별도의 처리가 필요합니다. 따라서 `@Query` 어노테이션만을 사용해서는 이러한 DML 연산을 처리할 수 없습니다.

### @Modifying 어노테이션 사용

해결책은 `@Modifying` 어노테이션을 `@Query` 어노테이션과 함께 사용하는 것입니다. `@Modifying` 어노테이션은 JPA에게 해당 쿼리가 데이터를 수정하는 쿼리임을 알려줍니다.

```java
@Modifying
@Query("DELETE FROM EntityName e WHERE e.attribute = ?1")
void deleteEntityByAttribute(String attribute);
```

### 트랜잭션 처리

DML 연산은 데이터의 일관성을 유지하기 위해 트랜잭션(Transaction) 내에서 실행되어야 합니다. 따라서 `@Transactional` 어노테이션을 메소드나 클래스 레벨에 추가해야 합니다.

```java
@Transactional
public void someMethod() {
    repository.deleteEntityByAttribute("someAttribute");
}
```

## 주의사항

- `@Modifying` 어노테이션은 반드시 `@Transactional`과 함께 사용되어야 합니다.
- DML 연산을 수행할 때는 반드시 데이터의 일관성과 무결성(Integrity)을 확인해야 합니다. 무결성은 데이터가 정확하고 신뢰할 수 있음을 의미합니다.

이렇게 하면 "not supported for DML operations" 에러를 해결하고, JPARepository에서 DELETE 쿼리를 성공적으로 실행할 수 있습니다.