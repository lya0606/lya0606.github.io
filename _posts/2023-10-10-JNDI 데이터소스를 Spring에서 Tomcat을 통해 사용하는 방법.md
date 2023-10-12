---
title: JNDI 데이터소스를 Spring에서 Tomcat을 통해 사용하는 방법
date: 2023-10-10 20:00:00 +0900
categories:
  - Spring
tags:
  - JNDI
  - Spring
  - Tomcat
---
## JNDI 데이터소스란 무엇인가?

JNDI(Java Naming and Directory Interface)는 자바에서 이름 서비스를 제공하는 API입니다. 데이터소스를 중앙에서 관리할 수 있어, 여러 애플리케이션에서 재사용이 용이합니다. JNDI 데이터소스는 특히 서버 환경에서 유용하며, Tomcat 같은 웹 서버에서 제공될 수 있습니다.

## Tomcat에서 JNDI 데이터소스 설정하기

Tomcat을 사용할 경우, `context.xml` 파일에 데이터소스를 정의해야 합니다. 일반적으로 이 파일은 `Tomcat/conf` 디렉터리에 위치합니다. 아래와 같이 데이터소스를 정의할 수 있습니다.

```xml
<Resource name="jdbc/mydb" 
          auth="Container"
          type="javax.sql.DataSource"
          driverClassName="com.mysql.jdbc.Driver"
          url="jdbc:mysql://localhost:3306/mydb"
          username="root"
          password="password"
          maxActive="20"/>
```

## Spring에서 JNDI 데이터소스 연동하기

Spring에서는 `applicationContext.xml` 또는 `application.properties` 파일에서 JNDI 데이터소스를 설정할 수 있습니다. 아래는 `applicationContext.xml` 파일을 사용한 예입니다.

```xml
<bean id="myDataSource" class="org.springframework.jndi.JndiObjectFactoryBean">
    <property name="jndiName">
        <value>java:comp/env/jdbc/mydb</value>
    </property>
</bean>
```

## 주의할 점: `NameNotFoundException`

`javax.naming.NameNotFoundException`이 발생한다면, JNDI 이름이 정확히 일치하는지 확인해야 합니다. 이 에러는 대소문자 민감성이 있으므로 정확히 일치해야 합니다. 또한, Tomcat과 Spring 모두에서 JNDI 설정이 제대로 이루어졌는지 검토가 필요합니다.

## 결론

JNDI 데이터소스를 사용하면 중앙에서 데이터소스를 관리할 수 있어 유용합니다. Tomcat과 Spring에서의 설정 방법을 정확히 이해하고 적용하면, 복잡한 환경에서도 데이터소스를 효율적으로 관리할 수 있습니다. 주의할 점은 에러 메시지를 잘 해석하여 문제를 빠르게 해결하는 것입니다.