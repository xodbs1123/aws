### AWS CloudFront ###
- Content Delivery Network ( CDN )
- 서로 다른 엣지 로케이션에 미리 캐싱하여 읽기 성능을 높이는 것
- 네트워크 전체에 캐싱되어 전세계 사용자들은 낮은 레이턴시로 접근 가능
- 전세계 216개 엣지 로케이션을 통해 구성
  - 따라서 DDoS 공격에서 보호 받을 수 있음
- CoudFront-Origins 제공 방식
  - S3 bucket
    - CloudFront를 통해 파일을 분산하고 캐싱할 수 있음
    - OAC ( Origin Access Control )로 기존의 OAI를 대체
    - 버킷에 CloudFront만 접근할 수 있게함
    - Ingress, CloudFront를 통해 버킷에 데이터를 보내는 방법
  - Custom Origin (HTTP)
    - Application Load Balancer
    - EC2 instance
    - S3 website ( 버킷을 활성화해서 정적 웹 사이트로 설정 필요 )
    - 그 밖의 다른 HTTP 백엔드
- CloudFront 작동 방식

![](https://velog.velcdn.com/images/xodbs1123/post/37f512fa-7121-477b-8321-93f3d973429a/image.png)
 
  - S3를 Origin으로 사용한다고 가정
 
  ![](https://velog.velcdn.com/images/xodbs1123/post/2684d03c-9ba5-412f-8808-a6cbdf3b7cca/image.png)

- CloudFront vs S3 Cross Region Replication
  - CloudFront
    - 전세계의 엣지 네트워크 사용
    - 하루 동안 파일들이 캐싱됨
    - 전세계를 대상으로 한 정적 컨텐츠 사용할 때 용이
  - S3 Cross Region Replication
    - 복제를 원하는 각 리전에 해당 설정이 되어 있어야함
    - 파일이 거의 실시간으로 갱신
    - 캐싱이 되지 않고, 읽기 전용으로만 설정 가능
    - 일부 리전을 대상으로 동적 컨텐츠를 낮은 지연 시간으로 제공하고자 할 때 유용
    
### CloudFront - ALB or EC2 as an origin ###

![](https://velog.velcdn.com/images/xodbs1123/post/7c1faeed-dd8e-4fc6-bd94-7ad849e418b7/image.png)


### CloudFront Geo Restriction ###
- 사용자들의 지역에 따라 배포 객체 접근을 제한할 수 있음
- 접근이 가능한 국가 목록을 만들거나, 반대로 접근이 불가능한 국가 목록을 만들어 설정
- 켄텐츠 저작권법으로 인한 제한 등에 쓰임

### CloudFront - Pricing ### 
- CloudFront 엣지 로케이션은 전 세계에 분포해 있어 각 로케이션마다 데이터 전송 비용이 다름

### CloudFront - Price Classes ###
- 비용 절감을 위해 전 세계 엣지 로케이션 수를 줄이는 방법이 있음
- 3개의 등급 클래스
   1. Price Class All : all regions - best performance
   2. Price Class 200 : most regions, but excludes the most expensive regions
   3. Price Class 100 : only the least expensive regions
   
 ### CloudFront - Cache Invalidations (무효화) ###
 - 캐시를 강제로 새로고침하여 TTL을 모두 제거하기 위해 실행
 - 두 가지 경로를 무효화하여 캐시에 새로 업데이트한 데이터가 저장되도록 하는 것
   - 특정 파일을 무효화하는 /index.html
   - 엣지 로케이션의 캐시에 있는 모든 이미지를 지우는 /images/*

  ![](https://velog.velcdn.com/images/xodbs1123/post/de72c2f1-72c0-4c22-931a-c75bb8fee536/image.png)


### Global users for our application ###

![](https://velog.velcdn.com/images/xodbs1123/post/3932ec94-efd4-4aba-a098-02c6d4717f10/image.png)

- 다른 region에 있는 애플리케이션에 접근할 때 공용 인터넷을 통하게 되는데 라우터를 거치는 동안 수 많은 홉으로 인해 상당한 지연이 발생할 수 있음
- 따라서 지연 시간을 최소화하기 위해 AWS 네트워크인 Global Accelerator 사용하는 것이 좋다!!
- Global Accelerator는 Anycast IP 개념 사용
  - 사용자와 가장 가까운 엣지 로케이션으로 트래픽을 직접 전송
  - 훨씬 안정적이고 지연 시간이 적은 사설 AWS 네트워크를 거쳐 ALB로 트래픽을 전송
- 어떤 애플리케이션에 대해서도 전 세계의 유저들에게 두 개의 고정 IP 주소를 제공
- 무엇과 함께 작동하는가?
  - Elastic IP, EC2 instances, ALB, NLB, public or private
- 네트워크 사용으로 안정적인 성능
  - 지능형 라우팅으로 지연 시간이 가장 짧은 엣지 로케이션으로 연결
  - 잘못된 경우 신속한 리전 장애 조치 이루어짐
  - 아무것도 캐시하지 않기에 클라이언트 캐시와도 문제가 없음
- Health Checks
  - 애플리케이션에 대한 상태 확인을 실행
  - 애플리케이션이 글로벌한지 확인 ( 한 리전에 있는 한 ALB에 대해 상태 확인을 실패하면 자동화된 장애 조치가 1분 안에 정상 엔드 포인트로 실행 ) 
- 보안
  - 단 두 개의 외부 IP만 존재하므로 보안 측면에서도 매우 안전
  - AWS Shield 덕분에 DDoS 보호도 자동으로 받음
### Global Accelerator VS CloudFront ###
- 둘 다 글로벌 네트워크 사용, AWS가 생성한 전 세계의 엣지 로케이션 사용
- DDos 보호를 위해 AWS Shield와 통합<br/><br/>
- CloudFront
  - 이미지나 비디오처럼 캐시 가능한 내용과 API 가속 및 동적 사이트 전달 같은 동적 내용 모두에 성능을 향상
  - 엣지 로케이션으로부터 제공
  - 캐시된 내용을 엣지로부터 가져와서 전달<br/><br/>
- Global Accelerator
  - TCP나 UDP 상의 다양한 애플리케이션 성능을 향상
  - 패킷은 엣지 로케이션으로부터 하나 이상의 AWS 리전에서 실행되는 애플리케이션으로 프록시됨
    - 이 경우 모든 요청이 애플리케이션 쪽으로 전달
  - 캐싱 불가능
  - 게임이나 IoT, Voice over IP 같은 non-HTTP를 사용할 경우 적합
  - 글로벌하게 고정 IP를 요구하는 HTTP 사용할 경우 적합
  - 결정적이고 신속한 리전 장애 조치가 필요할 때도 적합
#### AWS Global Accelerator + ALB ###
  - 정적 IP 주소를 할당하고 전 세계에 짧은 지연 시간으로 서비스를 제공하는 데 도움이 될 만한 AWS 서비스
  
#### Unicast IP vs Anycast IP ####

![](https://velog.velcdn.com/images/xodbs1123/post/006bee7d-26aa-4ed3-9c13-df696b47a274/image.png)

- Unicast IP : 하나의 서버가 하나의 IP 주소를 가진다, 따라서 참조하는 IP에 따라 해당하는 서버에 접근
- Anycast IP : 모든 서버가 동일한 IP 주소를 가지며 클라이언트는 가장 가까운 서버로 라우팅됨

` 실습은 Udemy 강의 참조!! `
