# 기본 포트 모음

<br />
<br />

* Port
---

```
여러 네트워크 서비스가 하나의 IP 주소를 공유하면서 구분될 수 있게 해주는 역할을 한다.

ex) 192.168.0.1:8080 (WAS)
    192.168.0.1:80(Web Server)

즉, 포트는 IP 주소와 결합하여 특정 서비스를 식별할 수 있게 한다.
```

<br />
<br />
<br />
<br />

1. 많이 사용하는 기본 포트

| **서비스**                | **포트 번호** |
|-------------------------|--------------|
| **HTTP**                 | 80           |
| **HTTPS**                | 443          |
| **FTP**                  | 21           |
| **SSH (SFTP 포함)**                  | 22           |
| **MySQL**                | 3306         |
| **PostgreSQL**           | 5432         |

<br />
<br />
<br />

2. http, https 접속 예시

```
// HTTP

ex) http protocol 사용

http://www.google.com:80 -> 80 포트를 명시했다.(O)
http://www.google.com:443 -> 443 포트를 명시했다. (-) (https Redirect 설정이 되어있다면 Redirect 후 접속이 된다.)
http://www.google.com:81 -> 81 포트를 명시했다. (X) (목적이 다른 포트이므로 접속이 안 된다.)
```

<br />

```
// HTTPS

ex) https protocol 사용

https://www.google.com:443 -> 443 포트를 명시했다.(O)
https://www.google.com:80 -> 80 포트를 명시했다. (-) (http -> https Redirect 설정이 되어있다면 Redirect 후 된다.)
https://www.google.com:444 -> 444 포트를 명시했다. (X) (목적이 다른 포트이므로 접속이 안 된다.)
```

<br />
<br />

```
포트 번호가 명시되어 있지 않다면,
프로토콜(http or https)을 확인하고 80이나 443 포트를 붙여 실험해보자.

포트를 명시하지 않았을 때와 똑같이 잘 접속될 것이다.
```
