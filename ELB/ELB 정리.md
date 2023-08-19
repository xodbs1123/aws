### Load Balancing ###

- 로드 밸런서
  - 서버 혹은 서브넷으로 트래픽을 백엔드나 다운스트림 EC2 인스턴스 또는 서버들로 전달하는 역할
  
![](https://velog.velcdn.com/images/xodbs1123/post/991408e6-a141-4816-91c0-544ebffce408/image.png)
 
- 로드 밸런싱을 통해 유저들이 각각 다른 EC2 인스턴스에 연결되도록 트래픽을 분산시켜줌
  - 유저들은 자신이 어떤 인스턴스에 연결되어 있는지 알 수 없음
  - 상태 확인(Health Checks) 매커니즘으로 어떤 인스턴스로 트래픽을 보낼 수 없는지 확인가능
  - SSL 종료 가능, 웹 사이트에 암호화된 HTTPS 트래픽 가질 수 있음
  - 쿠키로 고정도 강화 가능
  - 영역에 걸친 고가용성을 가짐
  - 클라우드 내 개인 트래픽과 공공 트래픽 분리 가능
### Elastic Load Balancer ###
  - 관리형 로드 밸런서
  - AWS가 관리, 업그레이드, 유지 관리 및 고가용성 책임
  - 로드 밸런서 작동 방식 수정할 수 있도록 일부 구성 놉 제공
  - 자체 로드 밸런서 마련하는 것보다 저렴
  - 다수의 AWS 서비스들과 통합 되어 있음
- 로드 밸런서 보안
  - 유저는 HTTP나 HTTPS를 사용해 어디서든 로드 밸런서에 접근 가능
  - 따라서 로드 밸런서 보안 그룹의 규칙은 아래와 같은 형태가 됨
    - 포트 범위 80, 혹은 443
    - 소스 0.0.0.0 / 0 (어디서든 접속 가능하다는 듯)
  - EC2 인스턴스 보안 규칙은 조금 다름, 로드 밸런서를 통해 들어오는 트래픽만 허용해야 하므로
    - 포트 범위 80, HTTP 트래픽 허용
    - 소스는 로드 밸런서의 보안 그룹으로 연결
    
    ![](https://velog.velcdn.com/images/xodbs1123/post/588d8a1d-6d53-4d99-a146-aaa1f36b19a8/image.png)

- Health Checks
  - Elastic Load Balancer 작동 상태 확인
  - 포트와 라우트에서 이루어짐
 
![](https://velog.velcdn.com/images/xodbs1123/post/f99a6e6f-0daa-4b50-b842-0a44ecf40d88/image.png)
 
  - EC2 인스턴스가 괜찮다는 신호, HTTP 상태 코드로 200으로 응답하지 않으면 인스턴스 상태가 좋지 않다고 기록
    - Elastic Load Balancer는 해당 인스턴스로 트래픽을 보내지 않음
  
### Application Load Balancer ###  
- 7계층, HTTP 전용 로드 밸런서
- 머신 간 다수 HTTP 애플리케이션의 라우팅에 사용 됨
  - 머신들은 target groups로 묶이게 됨
  - redirects 지원 ( HTTP에서 HTTPS로 트래픽을 자동 redirects 하려는 경우 )
  - URL 대상 경로에 기반한 라우팅도 가능
    - ex) example.com/users & example.com/posts
    - users와 posts는 URL 상의 서로 다른 경로, 이들을 target groups 그룹에 redirets 가능
  - URL의 호스트 이름에 기반한 라우팅 가능
    - ex) 로드 밸런서가 one.example.com & other.example.comd에 접근 가능하다면
    - 두 개의 다른 target groups에 라우팅 됨
  - 쿼리 문자열과 헤더에 기반한 라우팅 가능
    - ex) example.com/users?id=123&order-=false가 다른 target groups에 라우팅 될 수 있는 것
- 동일 EC2 인스턴스 상의 여러 애플리케이션에 트래픽을 분산
  - ex) containers, ECS
- HTTP/2와 Websocket 지원
- 약자로 ALB
- 마이크로 서비스나 컨테이너 기반 애플리케이션에 가장 좋은 로드 밸런서
  - 도커와 Amazon ECS에 적합
- 포트 매핑 기능이 있어 ECS 인스턴스의 동적 포트로의 리다이렉션을 가능하게 해줌
- 하나의 로드 밸런서로 다수의 애플리케이션 처리 가능

![](https://velog.velcdn.com/images/xodbs1123/post/cd346c7e-966a-415d-b424-f7c1ad25b1a3/image.png)

#### ALB Target Groups Types ####
- EC2 인스턴스 (오토 스케일링 그룹에 의해 관리 ) - HTTP
- ECS 작업 - HTTP
- 람다 함수 
- IP Address - 사설 IP 주소여야만 함
- 즉, ALB는 여러 Target Groups으로 라우팅 가능
- Health Checks는 Target Groups 레벨에서 이루어짐

![](https://velog.velcdn.com/images/xodbs1123/post/7067c43a-69a5-4120-a260-4b6097fb27ad/image.png)


### ALB 실습 ###
1. EC2 > Load Balacners > Creat > Select Load Balancer Type
2. 각 선택사항 입력 ( 타겟 그룹 생성 등.. )

![](https://velog.velcdn.com/images/xodbs1123/post/d567b697-9fb8-412d-992b-9975ff7811a5/image.png)

![](https://velog.velcdn.com/images/xodbs1123/post/eed53a9c-23aa-4f88-a385-e3cf3b25ee94/image.png)

3. 생성 된 DNS 이름을 복사해 새 탭에 넣으면, 애플리케이션 로드 밸런서를 통해 Hello World 출력
4. 새로고침하면 인스턴스 대상이 바뀌는 것을 알 수 있음 (IP 바뀜)
5. 이를 통해 트래팩 분산이 일어나고 있음을 알 수 있다

![](https://velog.velcdn.com/images/xodbs1123/post/75d60def-c9b2-41b6-97e8-d3eea4f6675f/image.png)

![](https://velog.velcdn.com/images/xodbs1123/post/41e53bb0-8b0e-46ac-bf1b-d1abd49ffe4f/image.png)


### 로드 밸런서 심화 개념 ###
- 네트워크 보안
  - 인스턴스에서 직접 접근할 수 있게 하는 것 보다는 로드 밸런스를 통해서만 접근하게 설정하는 것이 좋음
  - 네트워크 보안 강화를 위해

   ![](https://velog.velcdn.com/images/xodbs1123/post/73c871e4-67e9-4334-b8a8-7e18fb8b8f4b/image.png)

- 애플리케이션 로드 밸런서 규칙
  - 규칙 추가 가능

   ![](https://velog.velcdn.com/images/xodbs1123/post/772e9d84-ae38-46ac-81cf-b796a2f976fd/image.png)

   - 경로가 '/error'면 고정 응답으로 404 코드와 'Not found, custom error' 응답 보내는 규칙 생성

  ![](https://velog.velcdn.com/images/xodbs1123/post/59a7aa84-5077-4519-b8c8-34d525ce3705/image.png)

   - 결과

   ![](https://velog.velcdn.com/images/xodbs1123/post/e2729355-be3b-45e1-8eff-43753e8a9374/image.png)

### Network Load Balancer ###
- L4 로드 밸런서
  -  **TCP와 UDP** 트래픽을 다룰 수 있음
  - HTTP를 다루는 L7보다 하위 계층
  - 초당 수백만 건의 요청 처리 가능
  - ALB에 비해 지연 시간 짧음, ALM = 400ms, NLB = 100ms
  - 가용 영역별로 하나의 고정 IP를 가짐
  - 탄력적 IP주소를 각 AZ에 할당 가능
  - 여러 개의 고정 IP를 가진 애플리케이션을 노출할 때 유용
  - ex) 1~3개의 IP로만 액세스할 수 있는 애플리케이션을 만들라는 문제가 나오면 NLB를 선택!! ( TCP, UDP, 정적 IP )
  - 프리 티어 아님.. ㅜㅜ

   ![](https://velog.velcdn.com/images/xodbs1123/post/d8c9b9a0-f4bb-4352-af49-1f26c9225030/image.png)

### NLB Target Groups Types ###
  - EC2 인스턴스
  - IP 주소 - 반드시 하드코딩, 프라이빗 IP
  - ALB 앞에 사용 가능
     - NLB를 통해 고정 IP 얻을 수 있고 ALB 덕분에 HTTP 유형의 트래픽 처리하는 규칙 얻을 수 있음
- Health Check
  - TCP, HTTP, HTTPS Protocols 지원
  
### NLB 실습 ### 
1. EC2 > Load Balacners > Creat > Select Load Balancer Type
2. 각 선택사항 입력 ( 타겟 그룹 생성 등.. )
3. ALB와 다르게 AWS의 고정 IP 혹은 탄력적 IP로 IPv4 설정 가능

![](https://velog.velcdn.com/images/xodbs1123/post/ea2fb5d3-f168-476f-94a0-65a3a1e1dea0/image.png)

4. nlb의 target group 생성..

![](https://velog.velcdn.com/images/xodbs1123/post/b8ceb95e-3a87-4dd4-8752-6f6af34c5cfa/image.png)

5. target groups 인스턴스들의 보안 그룹에 NLB 트래픽 허용 가능하도록 규칙 설정 해야함

### Gateway Load Balancer ###
- 가장 최근 로드 밸런서
- 네트워크 트래픽 분석
- L3 계층
- GWLB 2가지 기능
  - Trasparent Network Gateway
    - VCP 모든 트래픽이 GWLB의 sing entry/exit을 통과하기 때문
  - 로드 밸런서
    - 가상 어플라이언스 집합에 트래픽을 분산해줌
- 6081번 포트의 GENEVE 프로토콜을 사용함!!!    
- GWLB는 배포 및 확장, AWS의 타사 네트워크 가상 어플라이언스의 플릿 관리에 사용
- 네트워크의 모든 트래픽이 방화벽을 통과하게 하거나 침입 탐지 및 방지 시스템 ( IDPS ) 에 사용 
- IDPS나 심층 패킷 분석 시스템 또는 일부 페이로드 수정 가능
  - 단, 네트워크 수준에서 가능

   ![](https://velog.velcdn.com/images/xodbs1123/post/0ad9d830-8439-465c-9e35-9765e37874ab/image.png)

### GWLB Target Groups Types ###
- 타사 어플라이언스임
  - EC2 인스턴스
  - IP 주소 - 프라이빗 IP
  
### Elastic Load Balancer Sticky Session ( Session Affinity )
- 고정성 혹은 고정 세션을 실행하는 것
- 로드 밸런서에 2가지 요청을 하는 클라이언트가 요청에 응답하기 위해 백엔드에 동일한 인스턴스를 갖는 것
- 2개의 EC2 인스턴스와 3개의 클라이언트가 있는 ALB와 같은 것

![](https://velog.velcdn.com/images/xodbs1123/post/8712613d-0139-40d1-b999-190603db964d/image.png)

- 1번 클라이언트가 요청을 생성해 첫 번째 EC2 인스턴스로 가면 두 번째 요청시에도 로드밸런서를 통해 동일한 인스턴스로 이동
- 2번 클라이언트, 3번 클라이언트도 동일하게 로드 밸런서가 두 번째 인스턴스와 통신하면 해당 인스턴스로 이동
- CLB와 ALB에서 설정 가능
- '쿠키'라는 원리를 통해 가능
  - 클라이언트에서 로드 밸런서로의 요청이 일부 전송되는 것
  - 고정성과 만료 기간이 있음
  - '쿠키'가 만료 되면 클라이언트가 다른 EC2 인스턴스로 리디렉션 됨
- 세션 만료시에는 사용자 로그인과 같은 중요한 정보를 취하는 세션 데이터를 잃지 않기 위해 사용자가 동일한 백엔드 인스턴스에 연결됨
- 고정성을 활성화하면 백엔드 EC2 인스턴스 부하에 불균형을 초래할 수 있음, 일부 인스턴스는 고정 사용자를 갖게 됨
- '쿠키'
  - Application-based Cookies ( 애플리케이션 기반 )
    - custom cookie
      - Generated by the target
      - 애플리케이션에 필요한 모든 사용자 정의 속성을 포함 가능
      - 애플리케이션에서 기간 지정
      - 쿠키 이름은 각 Target group 별로 개별 지정
      - Don't use AWSALB, AWSALBAPP, or AWSALBTG ( ELB에서 사용하기 때문 )
   - Application cookie
     - Generated by the load balancer
     - Cookie name is AWSALBAPP
- Duration-based Cookies ( 기간 기반 )
  - Cookie generated by the load balancer
  - Cookie name is AWSALB for ALB, AWSELB for CLB
  - 특정 기간을 기반으로 만료, 로드 밸런서 자체에서 생상     

#### 고정 세션 활성화 방법 ####
1. EC2 > Target groups > Actions > Edit target group attributes

![](https://velog.velcdn.com/images/xodbs1123/post/26a3fe38-0eaa-4120-a930-ec5e7270d4f7/image.png)

2. 이후 DNS ID로 새탭 열고 새로고침하면 고정 IP로만 접속 되는 것을 확인 할 수 있음

![](https://velog.velcdn.com/images/xodbs1123/post/3b21757c-6dd7-4f0d-9d19-3ec82ad609fe/image.png)

### Cross-Zone Load Balancing ###
![](https://velog.velcdn.com/images/xodbs1123/post/a57a25c0-75db-4e2d-a0df-611a60ab2a3e/image.png)

- 교차 영역 로드 밸런싱을 쓰면, 각각의 로드 밸런서 인스턴스가 모든 가용 영역에 등록 된 인스턴스에 트래픽을 50씩 균등하게 분배
  - 인스턴스 수가 10개니까 균등하게 10씩 할당 받음
  

![](https://velog.velcdn.com/images/xodbs1123/post/2cf94699-2186-4d4f-8ee6-ce89b85bc5cd/image.png)

- 영역을 교차하지 않고 부하를 분산, Elastic 로드 밸런서 노드의 인스턴스로 분산
- 트래픽 분산 방법은 사진과 같음, 특정 영역에 트래픽이 더 분산됨
- 정답은 없다, 상황에 맞게 고려해서 사용하면 된다
------------
		
- ALB는 기본적으로 교차 영역 로드 밸런싱이 활성화 
  - 따라서 AZ 간의 데이터 이동에 비용이 들지 않음
- NLB와 GWLB는 기본적으로 교차 영역 로드 밸런싱이 비활성화
  - 활성화 하려면 비용 지불해야 함, AZ 사이 데이터를 옮기려면 비용이 발생하므로
- CLB는 기본적으로 교차 영역 로드 밸런싱 비활성화
  - 활성화시켜도 AZ 간 데이터 이동 비용 발생하지 않음
