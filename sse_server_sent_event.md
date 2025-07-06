# SSE

<br />
<br />

* SSE(Server-Sent Events)

```
서버가 클라이언트(브라우저)에게 실시간으로 데이터를 전송하는 방법이다.

HTTP 프로토콜을 기반으로 하며,
서버가 클라이언트로 단방향 데이터 스트림을 보내는 데 사용된다.

주로 실시간 알림, 라이브 피드(ex 뉴스, 주식 가격 업데이트), 채팅 메시지 등에 활용된다.
```

<br />
<br />
<br />
<br />

1. 주요 특징

<br />

`단방향 통신`

```
서버에서 클라이언트로 데이터를 전송하며,
클라이언트는 서버로 데이터를 보내지 않는다.
```

<br />

`단순성`

```
별도의 WebSocket처럼 복잡한 설정 없이,
HTTP를 통해 구현된다.
```

<br />

`EventSource API`

```
클라이언트 측에서 JavaScript의 EventSource 객체를 사용하여,
서버와 연결한다.
```

<br />

`자동 재연결`

```
연결이 끊어지면,
클라이언트가 자동으로 재연결을 시도한다.
```

<br />

`텍스트 기반`

```
데이터는 주로 text/event-stream 형식으로 전송되며,
이벤트 이름과 데이터를 포함한다.
```

<br />
<br />
<br />

2. 동작 방식

<br />

`1) 클라이언트가 EventSource 객체를 생성해, 서버의 특정 엔드포인트에 연결을 요청한다.`

```ts
const source = new EventSource('http://localhost:3000/events');
  source.onmessage = function(event) {
    const messageDiv = document.getElementById('messages');
    const newMessage = document.createElement('p');
    newMessage.textContent = `새 메시지: ${event.data}`;
    messageDiv.appendChild(newMessage);
  };

  // 처리 로직 추가 전

  source.onerror = function() {
    const messageDiv = document.getElementById('messages');
    const errorMessage = document.createElement('p');
    errorMessage.textContent = '연결 에러 발생, 재연결 시도 중...';
    messageDiv.appendChild(errorMessage);
  };
```

<br />

`2) 서버는 "Content-Type: text/event-stream" 헤더를 포함한 응답을 보내고 연결을 유지한다.`

```ts
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';

@Controller('events')
export class SseController {
  @Get()
  handleSse(@Res() res: Response) {
    // SSE 헤더 설정
    res.setHeader('Content-Type', 'text/event-stream');
    res.setHeader('Cache-Control', 'no-cache');
    res.setHeader('Connection', 'keep-alive');

    // 3초마다 메시지 전송
    const interval = setInterval(() => {
      const message = {
        message: `서버에서 보낸 메시지: ${new Date().toLocaleTimeString()}`,
      };
      // 기본 메시지 전송
      res.write(`data: ${JSON.stringify(message)}\n\n`);

      // 특정 이벤트 이름('update')으로 메시지 전송
      res.write(`event: update\ndata: 업데이트된 시간: ${new Date().toLocaleTimeString()}\n\n`);
    }, 3000);

    // 클라이언트 연결 종료 시 인터벌 정리
    res.on('close', () => {
      clearInterval(interval);
      res.end();
    });
  }
}
```

<br />

`3) 서버가 새로운 데이터(이벤트)를 클라이언트로 전송할 때마다, 클라이언트는 이를 수신해 처리한다.`

```ts
const source = new EventSource('http://localhost:3000/events');
  source.onmessage = function(event) {
    const messageDiv = document.getElementById('messages');
    const newMessage = document.createElement('p');
    newMessage.textContent = `새 메시지: ${event.data}`;
    messageDiv.appendChild(newMessage);
  };

  // 처리 로직 추가
  source.addEventListener('update', function(event) {
    const messageDiv = document.getElementById('messages');
    const newMessage = document.createElement('p');
    newMessage.textContent = `업데이트: ${event.data}`;
    messageDiv.appendChild(newMessage);
  });

  source.onerror = function() {
    const messageDiv = document.getElementById('messages');
    const errorMessage = document.createElement('p');
    errorMessage.textContent = '연결 에러 발생, 재연결 시도 중...';
    messageDiv.appendChild(errorMessage);
  };
```

<br />
<br />
<br />

3. 활용 사례

<br />

`실시간 알림 (ex 트위터/X의 새 포스트 알림)`

`주식 가격이나 스포츠 경기 스코어 업데이트`

`서버 모니터링 데이터 스트리밍`
