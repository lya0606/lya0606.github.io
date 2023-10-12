---
title: Spring의 JdbcTemplate으로 SQL 쿼리 효과적으로 실행하기
date: 2023-08-27 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - JdbcTemplate
  - SQL
---
## JdbcTemplate의 기본 구조

JdbcTemplate은 Spring 프레임워크에서 제공하는 강력한 도구입니다. 이를 이용하면 데이터베이스와의 상호작용을 매우 편리하게 할 수 있습니다. 데이터베이스는 정보를 저장하는 온라인 창고 같은 것이라고 생각하면 됩니다. 이 도구를 사용하면 SQL 쿼리를 쉽고 빠르게 실행할 수 있습니다.

## 쿼리 실행 방법

JdbcTemplate을 사용하여 쿼리를 실행하는 가장 기본적인 방법은 `queryForObject`, `queryForList`, `update` 등의 메서드를 사용하는 것입니다. 이 메서드들은 각각 다른 목적과 반환값을 가지므로, 원하는 작업에 따라 적절한 메서드를 선택해야 합니다.

### queryForObject 메서드

`queryForObject`는 하나의 결과만을 반환하는 쿼리에 사용됩니다. 예를 들어, 특정 사용자의 정보를 가져올 때 이 메서드를 사용할 수 있습니다.

```java
String sql = "SELECT name FROM users WHERE id = ?";
String name = jdbcTemplate.queryForObject(sql, new Object[] { 1 }, String.class);
```

### queryForList 메서드

`queryForList`는 여러 개의 결과를 반환하는 쿼리에 사용됩니다. 예를 들어, 특정 조건에 맞는 모든 사용자의 정보를 가져올 때 이 메서드를 사용할 수 있습니다.

```java
String sql = "SELECT name FROM users WHERE age > ?";
List<String> names = jdbcTemplate.queryForList(sql, new Object[] { 21 }, String.class);
```

### update 메서드

`update` 메서드는 데이터를 수정, 추가, 삭제할 때 사용합니다. 이 메서드는 명령어가 영향을 미친 행의 수를 반환합니다.

```java
String sql = "UPDATE users SET age = ? WHERE id = ?";
int rowsAffected = jdbcTemplate.update(sql, new Object[] { 25, 1 });
```

## SQL 예외 처리하기

JdbcTemplate은 SQL 예외를 Spring의 `DataAccessException`으로 변환해줍니다. 이렇게 하면 코드에서 예외 처리를 더 쉽게 할 수 있습니다. 예외(Exception)란 프로그램 실행 중에 발생하는 오류 상황을 말합니다.

```java
try {
    String sql = "SELECT name FROM users WHERE id = ?";
    String name = jdbcTemplate.queryForObject(sql, new Object[] { 1 }, String.class);
} catch (DataAccessException e) {
    // 예외 처리 로직
}
```

## 요약

JdbcTemplate은 Spring에서 데이터베이스 작업을 쉽고 안전하게 처리할 수 있는 도구입니다. 쿼리를 실행할 때는 작업의 목적에 맞게 `queryForObject`, `queryForList`, `update` 등의 메서드를 사용해야 하며, 예외 처리를 위해 `DataAccessException`을 사용할 수 있습니다. 이 도구를 잘 활용하면 데이터베이스 작업을 효율적으로 할 수 있습니다.