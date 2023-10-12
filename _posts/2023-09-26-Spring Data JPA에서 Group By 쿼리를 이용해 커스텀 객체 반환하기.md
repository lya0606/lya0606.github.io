---
title: Spring Data JPA에서 Group By 쿼리를 이용해 커스텀 객체 반환하기
date: 2023-09-26 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringDataJPA
  - GroupBy
---
## 문제 상황

사용자들이 자주 Spring Data JPA를 이용할 때 'Group By' 쿼리를 사용하여 결과를 얻는 경우가 많습니다. 하지만 그 결과를 커스텀 객체로 받고 싶을 때 어떻게 해야 할까요? 이 문제에 대한 해결 방법을 상세하게 알아보겠습니다.

## 오류 코드
`Error creating bean with name`

## 기본적인 'Group By' 쿼리 사용

Spring Data JPA에서는 기본적으로 제공되는 메서드를 이용하여 쉽게 데이터를 가져올 수 있습니다. `findAll()`, `findById()`, `save()` 등의 메서드가 있죠. 그러나 때로는 더 복잡한 쿼리를 작성해야 할 때도 있습니다. 이럴 때 사용되는 것이 'Group By' 쿼리입니다.

## 커스텀 객체로 결과 반환

보통 'Group By' 쿼리의 결과는 일반적으로 `List<Object[]>` 형태로 반환됩니다. 여기서 `Object[]`는 각 그룹에 대한 여러 열(column)의 값을 담고 있습니다. 그런데 이런 결과를 커스텀 객체로 받고 싶다면 어떻게 해야 할까요?

### 방법 1: 생성자 이용
가장 간단한 방법은 반환하려는 클래스에 적절한 생성자를 추가하는 것입니다. 예를 들어, 반환하려는 클래스가 `MyClass`라면 다음과 같이 작성할 수 있습니다.

```java
public MyClass(Long id, String name) {
    this.id = id;
    this.name = name;
}
```

이렇게 하면 JPA 쿼리에서는 `new MyClass(id, name)` 형식으로 결과를 받을 수 있습니다.

### 방법 2: DTO와 `@SqlResultSetMapping` 사용
DTO(Data Transfer Object)를 사용하고 `@SqlResultSetMapping` 애너테이션을 이용하여 복잡한 쿼리 결과를 매핑할 수도 있습니다. DTO는 데이터를 객체로 쉽게 전달할 수 있는 클래스입니다. `@SqlResultSetMapping`은 JPA가 데이터베이스의 SQL 결과를 어떻게 자바 객체에 매핑할지 지정하는 애너테이션입니다.

```java
@SqlResultSetMapping(
    name="myMapping",
    classes = @ConstructorResult(
        targetClass = MyClass.class,
        columns = { @ColumnResult(name = "id", type = Long.class), @ColumnResult(name = "name", type = String.class) }
    )
)
```

이런 식으로 설정하면, SQL 쿼리 결과를 `MyClass` 객체로 바로 매핑할 수 있습니다.

## 결론
Spring Data JPA에서 'Group By' 쿼리를 사용하여 커스텀 객체로 결과를 반환하려면, 생성자를 활용하거나 DTO와 `@SqlResultSetMapping` 애너테이션을 사용하는 방법이 있습니다. 복잡한 데이터를 쉽게 관리하고 원하는 형태로 반환하기 위해서는 이러한 방법들이 유용하게 사용될 수 있습니다.