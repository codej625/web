# RESTful API 설계 규칙을 알아보자!

<br/>

### REST API 설계 규칙
```
슬래시 구분자(/)는 계층 관계를 나타내는데 사용한다.
  ex) http://restapi.example.com/houses/apartments
```
```
URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
  URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고,
  역으로 리소스가 다르면 URI도 달라져야 한다.
  REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
  ex) http://restapi.example.com/houses/apartments/ (X)
```
```
하이픈(-)은 URI 가독성을 높이는데 사용
  불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
```
```
밑줄(_)은 URI에 사용하지 않는다.
  밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
```
```
URI 경로에는 소문자가 적합하다.
  URI 경로에 대문자 사용은 피하도록 한다.
  RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
```
```
파일확장자는 URI에 포함하지 않는다.
  REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
  Accept header를 사용한다.
  ex) http://restapi.example.com/members/soccer/345/photo.jpg (X)
  ex) GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg (O)
```
```
리소스 간에는 연관 관계가 있는 경우
  /리소스명/리소스 ID/관계가 있는 다른 리소스명
  ex) GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
```
