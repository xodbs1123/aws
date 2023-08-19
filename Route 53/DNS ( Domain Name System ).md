### DNS ( Domain Name System ) ###

- 사람에게 친숙한 호스트 이름을 대상 서버 IP 주소로 변환해줌
  - ex) www.google.com 을 입력하면 DNS가 IP 주소로 변환해주어 웹 브라우저가 해당 IP 주소를 통해 접근 후 구글로부터 데이터를 얻음
- DNS는 인터넷의 중추
- DNS에는 계층적 이름 구조가 있음
  - .com
  - example.com
  - www.exampl.com
  - api.example.com
- 도메인 레지스트라( registrar )  
  - 도메인 이름을 등록하는 곳
   - ex ) Amazon Route 53, GoDaddy ...
- DNS Records
  - ex ) A, AAA, CNAME, NS ...
 - Zone File
   - 호스트 이름과 IP 또는 주소를 일치시키는 방법
- Name Server
   - DNS 쿼리를 실제로 해결하는 서버 ( Authoritative or Non-Authoritative )
- Top Level Domain ( TLD )
  - .com, .us, .in, .gov, .ort ......
- Second Level Domain ( SLD ) 
  - amazon.com, google.com, naver.com .......
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/cb8dd99a-0a1b-4031-a3e6-7370444acbfe/image.png)

### How DNS Works ###

![](https://velog.velcdn.com/images/xodbs1123/post/80084db5-8aae-4de1-8df2-06c19dd99547/image.png)
