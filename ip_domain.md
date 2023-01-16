# ip와 domain에 대해 알아보자!

ip란?
```
인터넷에 연결되어 있는 장치(컴퓨터, 스마트폰, 타블릿, 서버 등등)들은 각각의 장치를 식별할 수 있는 주소를 가지고 있는데 이를 ip라고 한다.  예) 115.68.24.88, 192.168.0.1
```

<br/>

도메인(domain)이란?
```
ip는 사람이 이해하고 기억하기 어렵기 때문에 이를 위해서 각 ip에 이름을 부여할 수 있게 했는데, 이것을 도메인이라고 한다.

opentutorials.org -> 115.68.24.88
naver.com -> 220.95.233.172
daum.net -> 114.108.157.19
```

<br/>

도메인의 구성요소
```
컴퓨터의 이름과 최상위 도메인으로 구성되어 있다. 예를들면 아래와 같다.

ex01)
opentutorials.org
opentutorials : 컴퓨터의 이름
org : 최상위 도메인 - 비영리단체

ex02)
daum.co.kr
daum : 컴퓨터의 이름
co : 국가 형태의 최상위 도메인을 의미
kr : 대한민국의 NIC에서 관리하는 도메인을 의미
```

URL의 이해
```
생활코딩 URL 편 참조 http://opentutorials.org/course/11/72
도메인은 장치를 식별하기 위한 주소
URL은 도메인 + 경로
예를 들어서 https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/121/298.png가 있을 때
도메인 : opentutorials.org
URL : https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/121/298.png
```