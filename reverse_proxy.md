# Reverse proxy

<br />
<br />

* 리버스 프록시란?
---

```
리버스 프록시는 클라이언트가 서버로 요청을 보낼 때,
직접 서버로 연결하지 않고 중간에 위치한 프록시 서버를 통해 요청을 전달하는 방식을 말한다.

클라이언트 입장에서는 최종적으로 요청할 end-point를 알 필요가 없다.
```

<br />
<br />
<br />
<br />

1. proxy 와 비교

| **항목**          | **프록시(Forward Proxy)**                                                                 | **리버스 프록시(Reverse Proxy)**                                                      |
|-------------------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| **비유**          | 당신(클라이언트)이 비서(프록시 서버)에게 피자 가게(외부 API)에 전화해 달라고 부탁. 당신은 피자 가게 주소를 알아야 함. | 당신(클라이언트)이 레스토랑(당신의 서버, Nginx)에 주문. 레스토랑이 피자 가게(외부 API)에 주문하고 피자를 전달. 당신은 피자 가게를 몰라도 OK. |
| **클라이언트가 아는 것** | 외부 API 주소(`external-api.com`)를 알아야 함.                                           | 자기 서버 주소(`your-domain.com`)만 알면 됨.                                         |
| **피자 가게(외부 API)가 아는 것** | 비서(프록시 서버)만 알고, 클라이언트는 모름.                                             | 레스토랑(당신의 서버, Nginx)만 알고, 클라이언트는 모름.                              |
| **개발 상황**     | React가 외부 API를 직접 호출하지만, CORS 제약으로 차단될 가능성 큼. 브라우저에서 설정 복잡. | React가 자기 서버(`/api/data`)로 요청 → Nginx가 외부 API(`external-api.com/data`)로 중계 → CORS 문제 해결. |
| **React 적용 예시** | `fetch('https://external-api.com/data')` (CORS 문제로 실패 가능).                        | `fetch('/api/data')` → Nginx가 `https://external-api.com/data`로 전달.               |
| **장점**          | 클라이언트 IP 숨김, 네트워크 제한 우회 가능.                                              | CORS 우회, 보안 강화, 여러 API 중계 가능, 클라이언트가 외부 API 몰라도 됨.            |
| **단점**          | 브라우저 환경에서 설정 어려움. CORS 문제 해결 못 함.                                      | 서버(Nginx) 설정 필요. 인증/헤더 처리 시 추가 작업 가능.                              |
| **React 상황 적합성** | 적합하지 않음 (브라우저에서 프록시 설정 비현실적).                                        | 매우 적합 (Nginx로 CORS 우회, 보안 및 관리 용이).                                     |

<br />
<br />
<br />

2. 예시

```
클라이언트 코드를
브라우저에서 작동한다고 가정한 예시이다.

React에서 fetch('/api/data') 호출 → Nginx가 https://external-api.com/data로 요청 → 응답을 React로 전달.
```

```tsx
import axios from 'axios';

function App() {
  const fetchData = async () => {
    try {
      const response = await axios.get('/api/data'); // Nginx로 요청
      console.log(response.data);
    } catch (error) {
      console.error('Error:', error);
    }
  };

  return <button onClick={fetchData}>데이터 가져오기</button>;
}
```

<br />

```
React 앱에서 외부 API(external-api.com)를 직접 호출하면,
CORS 때문에 막힐 가능성이 크다.

React는 your-domain.com/api/data로 요청하고,
Nginx가 이 요청을 external-api.com/data로 전달 후
응답을 받아서 React로 돌려준다.
```

```nginx
server {
    listen 80;
    server_name your-domain.com;

    location /api/ {
        proxy_pass https://external-api.com/;
        proxy_set_header Host $host;
    }
}
```
