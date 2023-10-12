---
title: HTTP 오류 해결하기 Content-Type application x-www-form-urlencoded charset=UTF-8 not supported
date: 2023-10-07 20:00:00 +0900
categories:
  - Spring
tags:
  - HTTP오류
---
## 원인과 개념 이해하기

HTTP(하이퍼텍스트 전송 프로토콜) 오류 중 하나로 자주 등장하는 문제가 'Content-Type application/x-www-form-urlencoded;charset=UTF-8 not supported'입니다. 이 오류는 서버와 클라이언트 간의 데이터 전송 형식에 불일치가 있을 때 발생합니다. 여기서 '서버'는 웹페이지나 앱을 호스팅하는 컴퓨터, '클라이언트'는 웹 브라우저나 앱을 사용하는 사용자의 컴퓨터를 의미합니다.

## 오류의 상세 분석

이 오류 메시지는 주로 REST API(웹 서비스에서 데이터를 주고받는 방법 중 하나)를 사용할 때 발생합니다. 'Content-Type'은 클라이언트가 서버에게 어떤 형식의 데이터를 보내고 있는지 알려주는 HTTP 헤더입니다. 이 경우 'application/x-www-form-urlencoded;charset=UTF-8'이라고 명시되어 있지만, 서버는 이 형식을 지원하지 않아 오류가 발생한 것입니다.

## 해결방안 제시

이 문제를 해결하는 방법은 여러 가지가 있습니다. 가장 기본적인 해결방안은 클라이언트와 서버 간의 'Content-Type'을 일치시키는 것입니다.

1. **서버 설정 확인**: 먼저 서버 설정에서 어떤 'Content-Type'을 지원하는지 확인합니다. 지원하는 형식에 맞게 클라이언트 코드를 수정해야 할 수 있습니다.
   
2. **클라이언트 코드 수정**: 클라이언트에서 데이터를 보낼 때 'Content-Type'을 서버가 지원하는 형식으로 변경합니다. 예를 들어, 'application/json'이나 'text/plain' 등으로 설정할 수 있습니다.

3. **헤더 수정**: 필요하다면 다른 HTTP 헤더도 수정할 수 있습니다. 예를 들어, 'Accept' 헤더를 사용하여 서버가 어떤 형식의 데이터를 보내주길 원하는지 명시할 수 있습니다.

기본적으로 이러한 설정은 서버나 클라이언트의 코드 또는 설정 파일에서 쉽게 변경할 수 있습니다. 핵심은 클라이언트와 서버가 '이해할 수 있는' 동일한 언어, 즉 'Content-Type'을 사용해야 한다는 것입니다.