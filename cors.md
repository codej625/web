# CORS(Cross-Origin Resource Sharing)

<br />
<br />

* CORS란?
---

```
CORS는 웹 브라우저가 다른 출처의 서버로 HTTP 요청을 보낼 때,
보안 정책으로 인해 발생하는 제한을 관리하는 방법이다.

브라우저는 기본적으로 SOP(Same-Origin Policy)를 따라 동일한 출처에서만 리소스를 요청할 수 있다.

하지만 CORS를 사용하면 서버가 특정 출처의 요청을 허용하도록 설정할 수 있다.
```

<br />

`출처(Origin)`

```
도메인, 프로토콜, 포트의 조합
(예: https://example.com:443)
```

`동일 출처`

```
요청하는 페이지와 요청받는
서버의 출처가 동일해야 함
```


`CORS의 역할`

```
서버가 특정 출처의 요청을 허용하거나,
제한하도록 제어
```

<br />
<br />
<br />
<br />

1. CORS 동작 과정

<br />

`1. 클라이언트 요청`

```
브라우저가 다른 출처로 HTTP 요청을 보낸다.
(예: GET, POST)
```

`2. Preflight 요청 (선행 요청)`

```
특정 요청(예: POST나 커스텀 헤더 포함 시)은
먼저 OPTIONS 메서드로 서버에 "허용 가능한지" 확인한다.
```

`3. 서버 응답` 

```
서버는 Access-Control-Allow-* 헤더를 포함해 응답한다.

* Access-Control-Allow-Origin: 요청을 허용할 출처 (예: https://example.com 또는 *)
* Access-Control-Allow-Methods: 허용된 HTTP 메서드 (예: GET, POST, PUT)
* Access-Control-Allow-Headers: 허용된 헤더
```

`4. 브라우저 처리`

```
브라우저는 서버의 응답을 확인해
요청을 허용하거나 차단한다.
```

<br />
<br />
<br />

2. CORS 오류 디버깅 팁

<br />

`오류 메시지 확인` 

```
브라우저 콘솔에서
CORS policy: No 'Access-Control-Allow-Origin' header 같은 메시지를 확인한다.
```

`서버 설정 확인` 

```
서버가 올바른 CORS 헤더를 반환하는지 확인한다.

* Postman 같은 도구로 서버 응답 헤더를 확인하거나,
  브라우저 개발자 도구의 Network 탭을 활용한다.
```
