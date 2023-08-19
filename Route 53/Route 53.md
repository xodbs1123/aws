### Route 53 ###
- 고가용성, 확장성을 갖춘 Fully Managed 와 권환이 있는 DNS
- 권한 = DNS 레코드를 직접 업데이트 할 수 있다는 뜻

![](https://velog.velcdn.com/images/xodbs1123/post/0293941e-54f0-42a0-80dd-172472593c79/image.png)

- 위 과정을 통해 Route 53도 도메인 이름 레지스타로 도메인 이름을 example.com으로 등록
- Route 53의 리소스 관련 상태 확인 가능
- 100% SLA 가용성을 제공하는 유일한 AWS 서비스

### Route 53 - Records ###
- Each record contains
  - Domain/subdomain Name - example.com ...
  - Record Type - A or AAA ...
  - Value - 123.456.789.123 ...
  - Routing Policy - how Route 53 responds to queries
  - TTL - DNS Resovers에서 레코드가 캐싱 되는 시간
#### Route 53 supoorts the following DNS record types ####
- ( must know ) A / AAAA / CNAME / NS
- ( advanced ) CAA / DS / MX / NAPTR / PTR / SOA / TXT / SPF / SRV
### Route 53 - Record Types ###
- A 
  - 호스트 이름과 IPv4 IP를 매핑
- AAAA
  - 호스트 이름과 IPv6 주소에 매핑
- CNAME
  - 호스트 이름을 다른 호스트 이름과 매핑
  - 호스트 이름은 A나 AAAA 레코드가 될 수 있음
  - Route 53에서 DNS 이름 공간 or Zone Apex의 상위 노드에 대한 CNAME 를 생성할 수 없음
    - ex) example.com에 CNAME을 만들 수 없음
    - 하지만 www.example.com에 대한 CNAME 만들 수 있음
- NS
  - Name Servers for the Hosted Zone
  - 서버의 DNS Name or IP 주소로 호스팅 존에 대한 DNS 쿼리에 응답 가능
  - 또한 트래픽이 도메인으로 라우팅 되는 방식을 제어함
### Route 53 - Hosted Zone ###
  - 레코드의 컨테이너
  - 도메인과 서브도메인으로 가는 트래픽의 라우팅 방식 정의
  - Public Hosted Zones
    - 퍼블릭 도메인 이름을 살 때마다 mypublicdomain.com이 도메인 이름이면 퍼블릭 호스팅 존을 만들 수 있음
    - 퍼블릭 존은 쿼리에 도메인 이름 application1.mypublicdomainname.의 IP가 무엇인지 알 수 있음
- Private Hosted Zones 
  - 공개되지 않는 도메인 이름 지원
  - 가상 프라이빗 클라우드 ( VPC )만이 URL을 resolve 가능
  - 비공개 URL이기 때문에 프라이빗 DNS 레코드가 있음
  
- 퍼블릭 프라이빗 호스팅 존은 유료임, 즉 Route 53은 유료  
#### Public VS private Hosted Zones ###

![](https://velog.velcdn.com/images/xodbs1123/post/c3ec8955-dea5-4fa4-b53d-67ac25bb959c/image.png)

#### Route 53 실습 ####
- 유료... 강의 시청으로 대체!!
- 원하는 도메인 선택 후 옵션 선택하면 된다!

### Route 53 - Records TTL ( Time To Live ) ###

![](https://velog.velcdn.com/images/xodbs1123/post/10ef6a9f-67ee-4d4c-8a68-b425da1206fe/image.png)

### CNAME vs Alias ###
- CNAME 
  - 호스트 이름이 다른 호스트 이름으료 향하도록 할 수 있음
    - ex ) app.mydomain.com 이 blabla.anything.com으로 향하게 하는 식
    - ELB 도메인 이름도 가능
  - 루트 도메인 이름이 아닌 경우에만 가능, mydomain.com은 안됨, 앞에 app과 같은 subdomain이 붙어야함
- Alias
  - Route 53에 한정되지만 호스트 이름이 특정 AWS 리소스로 향하도록 할 수 있음
    - ex ) app.mydomain.com이 blabla.amazonaws.com을 향할 수 있는 것
  - 루트 및 비루트 도메인 모두에 작동함, mydomain.com 같은 도메인도 가능하다는 의미    
  - 무료, 자체적으로 상태 확인 가능

   ![](https://velog.velcdn.com/images/xodbs1123/post/520a6773-d8d9-48d8-9902-c1ac3ae0cf30/image.png)

- AWS 리소스에만 매핑 되어 있음
- Zone Apex라는 DNS 네임스페이스의 상위 노드로 사용될 수 있음
  - example.com에도 별칭 레코드를 쓸 수 있다는 것
- A or AAAA 타입, 즉 리소스는 IPv4 or IPv6  
- TTL 설정 불가능
#### Route 53 - Alias Records Targets
- ELB
- CloudFront Distributions
- API Gateway
- Elastic Beanstalk environments
- S3 Websites
- VPC Interface Endpoints
- Global Accelerator accelerator
- Route 53 record in the same hosted zone 
