# 포트 포워팅을 사용하여 서버 접근에 보안을 신경써보자!

```
aws 예시)

1. 관리중인 모든 instance의 인바운드 규칙을 단하나의 ip만 접속이 가능하게 만든다. (여기서는 bastion이라는 gate way역할을 하는 서버를 예시로 하겠다.)

2. puTTY bastion tunnels 설정에는 port forwarding을 할수있도록 forwarded port와 instance의 private ip를 등록해 놓는다.

3. puTTY를 이용하여 gate way 역할을 하는 bastion서버의 public서버로 접속한다. (public ip는 기본적으로 유동이기 때문에 "탄력적ip"를 사용한다.)

4. puTTY, filezilla와 같은 프로그램을 이용하여 
```