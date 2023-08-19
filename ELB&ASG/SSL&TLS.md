### SSL/TLS ###
- SSL 인증서
  - 클라이언트와 로드 밸런서 사이 트래픽이 이동하는 동안 암호화 ( in-flight encrypton )
  - 데이터는 네트워크 이동 중 암호화, 송신자와 수신자 측에서만 복호화 가능
  - SSL은 '보안 소켓 계층'을 의미, 연결을 암호화 하는 데 사용
  - TLS는 '전송 계층 보안'을 의미, 새로운 버전의 SSL
    - 최근에 주로 사용, 하지만 여전히 SSL이라고 불림, 같은 의미
  - 퍼블릭 인증서는 인증 기관(CA)에서 발급
    - 퍼블릭 SSL 인증서를 로드 밸런서에 추가하면, 클라이언트와 로드 밸런서 사이의 연결을 암호화 가능
  - SSL 인증서는 만료 날짜 존재, 주기적으로 갱신 필요
  
### SSL 동작 ###

![](https://velog.velcdn.com/images/xodbs1123/post/a10ef1e5-fcda-4538-b72c-b3e193f71aa7/image.png)

- 사용자가 HTTPS 통해 접속 (S가 붙은 건 SSL 인증서 사용해 암호화 되어 있다는 뜻)
- 인터넷을 통해 로드 밸런서 접속시, 로드 밸런서 내부에서 SSL Termination 수행
- 백엔드에서는 HTTP로 EC2 인스턴스와 통신 ( 암호화 X 상태 )
- 로드 밸런서는 X.509 인증서 사용, SSL or TLS 서버 인증서라고 부름
- AWS에는 해당 인증서들을 관리하는 ACM (AWS 인증서 관리자)가 있음
- 개인이 소유하고 있는 인증서를 ACM에 업로드 가능
- HTTP listener
  - 기본 인증서 지정
  - 다중 도메인 지원을 위해 다른 인증서 추가 가능
  - 클라이언트는 SNI (서버 이름 지정)을 사용해 접속할 호스트 이름을 지정 가능
  - 사용자가 원하는 보안 정책 지정 가능
### SNI ###
- 여러 개의 SSL 인증서를 하나의 웹 서버에 로드
- 하나의 웹 서버가 여러 개의 웹 사이트를 지원할 수 있게 해줌
- 확장된 프로토콜, 클라이언트가 Target 서버 호스트 이름을 지정하도록 함
  - 클라이언트가 지정하면 서버는 어떤 인증서를 로드해야 하는지 알 수 있다
- ALB, NLB, CloudFront에서만 작동
  - 즉, 어떤 로드 밸런서에 SSL 인증서가 여러 개 있다면 ALB or NLB라는 뜻

![](https://velog.velcdn.com/images/xodbs1123/post/c8b6145c-2f8f-489f-850f-8722839e3d4f/image.png)

### SSL 실습 ###
1. EC2 > Load balancers > LB name > Add listener
2. 각종 설정 사항 선택 ( 포트 번호, SSL 보안 정책 등 ..)

![](https://velog.velcdn.com/images/xodbs1123/post/4fef5eae-689a-4a07-85e5-21d435780b37/image.png)
