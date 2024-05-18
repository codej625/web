# Bastion에 대해 알아보자.

<br /><br />

* Bastion을 사용한 접속 방법

1. 관리중인 모든 instance의 인바운드 규칙을 단하나의 IP만 접속이 가능하게 만든다.
(여기서는 Bastion이라는 Gate way 역할을 하는 서버를 예시로 한다.)

2. puTTY에서 Bastion의 Tunnels 설정에는 Port Forwarding을 할수있도록 Forwarded port와 Instance의 Private IP를 등록해 놓는다.

3. puTTY를 이용하여 Gate way 역할을 하는 Bastion서버의 Public서버로 접속한다. (Public IP는 기본적으로 유동이기 때문에 "탄력적 IP"를 사용한다.)

4. Gate Way 역할을 하는 Bastion 서버가 열린 상태에서, 접속하고 싶은 서버에 접속한다.
