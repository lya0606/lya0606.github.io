---
title: Spring Test에서 보안 인증 Mock 처리 방법
date: 2023-09-04 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Mock
  - 보안인증
---
## 문제 상황

`Spring Security`를 사용할 때 테스트 환경에서 `Authentication` 객체를 가상으로(Mock) 생성하는 것이 필요하다. 여기서 `Mock`이란, 실제 객체를 모방한 가상 객체를 의미한다. 이 문제는 주로 개발자들이 `Spring Test`를 작성할 때 자주 발생한다.

## ErrorCode: N/A

## MockMvc와 @WithMockUser 활용하기

### MockMvc 사용법

`MockMvc`는 Spring MVC의 테스트를 돕는 클래스다. 이를 통해 HTTP 요청과 응답을 가상으로 처리할 수 있다.

```java
@Autowired
private MockMvc mockMvc;

@Test
public void shouldGetFooWhenUserIsAuthorized() throws Exception {
    mockMvc.perform(get("/foo"))
           .andExpect(status().isOk());
}
```

### @WithMockUser 어노테이션

`@WithMockUser`는 테스트 메서드에 가상의 사용자를 부여할 수 있는 어노테이션이다.

```java
@Test
@WithMockUser(username = "user", roles={"USER"})
public void shouldGetFooWhenUserIsAuthorized() throws Exception {
    mockMvc.perform(get("/foo"))
           .andExpect(status().isOk());
}
```

이렇게 하면, `username`이 `user`이고 `role`이 `USER`인 가상의 사용자가 로그인한 것처럼 테스트를 실행할 수 있다.

## SecurityContextHolder를 이용한 수동 설정

`SecurityContextHolder`는 Spring Security에서 현재 보안 컨텍스트를 가져오거나 설정하는데 사용된다.

```java
@Test
public void manualAuthenticationTest() {
    Authentication authentication = new UsernamePasswordAuthenticationToken("user", "password", Collections.singletonList(new SimpleGrantedAuthority("ROLE_USER")));
    SecurityContextHolder.getContext().setAuthentication(authentication);
    // 여기서 테스트 코드 작성
}
```

이 방법은 테스트 환경에서 수동으로 `Authentication` 객체를 생성하고, 이를 `SecurityContextHolder`에 설정하는 방식이다.

## 정리

Spring Test 환경에서 보안 인증을 테스트하기 위해 `MockMvc`와 `@WithMockUser`, 그리고 `SecurityContextHolder`를 사용하는 방법에 대해 알아보았다. 이러한 방법들을 활용하면, 실제 사용자가 로그인한 것처럼 시스템을 테스트할 수 있다. 이로써 보다 정확하고 빠른 테스트가 가능해진다.