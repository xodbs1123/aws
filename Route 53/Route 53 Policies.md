### Route 53 - Routing Policies ###
- Route 53이 DNS 쿼리에 응답하는 것을 도움
- Route 53이 지원하는 라우팅 정책
  - simple

   ![](https://velog.velcdn.com/images/xodbs1123/post/896c4230-b982-457f-9495-a66b68c3b8cb/image.png)

    - 트래픽을 단일 리소스로 보내는 방식
    - 예로, 클라이언트가 foo.example.com으로 가고자 한다면 Route 
       53이 IP 주소 ( A 레코드 주소 ) 알려주는 것
    - 동일한 레코드에 여러 개의 값을 지정하는 것도 가능
   
    ![](https://velog.velcdn.com/images/xodbs1123/post/36d4d6d2-2227-47c2-ad41-20f478003991/image.png)

    - DNS에 의해 다중 값을 받은 경우는 client 쪽에서 하나를 무작위로 고름
    - 단순 라우팅 정책에 별칭 레코드를 함께 사용하면 하나의 AWS 리소스만을 대상으로 지정 가능
    - 상태 확인은 불가능
  - weighted
  ![](https://velog.velcdn.com/images/xodbs1123/post/bfdbfd02-a98a-445e-bf99-acae06aaf4ab/image.png)

    - 가중치를 활용해 요청의 일부 비율을 특정 리소스로 보내는 식의 제어가 가능
  
    ![](https://velog.velcdn.com/images/xodbs1123/post/38a3fee1-0e01-4a46-ba33-2e1685d76003/image.png)

    - DNS 레코드들은 동일한 이름과 유형을 가져야함
    - 상태 확인과도 관련될 수 있음
    - 서로 다른 지역들에 걸쳐 로드 밸런싱을 할 때나 적은 양의 트래픽을 보내 새 애플리케이션을 테스트하는 경우에도 사용
    - 가중치 0의 값을 보내게 되면 특정 리소스에 트래픽 보내기를 중단해 가중치를 바꿀 수 있음
    - 모든 리소스 레코드 가중치 값이 0인 경우는 모든 레코드가 다시 동일한 가중치를 갖게 됨
  - Failover ( Active - Passive )

  ![](https://velog.velcdn.com/images/xodbs1123/post/bffeed32-f42b-4471-a72f-d293b61c0821/image.png)

   - Latency based
    - 지연 시간이 가장 짧은, 가장 가까운 리소스로 리다이렉팅 하는 정책
    - 지연 시간은 유저가 레코드로 가장 가까운 AWS 리전에 연결하기까지 걸리는 시간
    - VPN으로 위치 변경하면 해당 리전에서 가장 가까운 곳으로 연결
  - Geolocation
    - 사용자 실제 위치를 기반으로 함
    - 일치하는 위치가 없는 경우는 기본 레코드 생성, 레코드와 일치하지 않는 위치에서 접속하면 기본 레코드로 접속 됨
    - 콘텐츠 분산을 제한하고 로드 밸런신 등을 실행하는 웹사이트 현지화에 사용
    - 상태 확인과 연결 가능
  - Multi-Value Answer

   ![](https://velog.velcdn.com/images/xodbs1123/post/8e5a236b-5f9e-45d0-b89f-460300228d2b/image.png)
    - 트래픽을 다중 리소스로 라우팅할 때 사용
    - Route 53은 다중 값과 리소스 반환
    - 상태 확인과 연결 가능 ( 정상 리소스만 반환 )
    - 각각의 다중 값 쿼리에 최대 8개의 정상 레코드 반환
    - ELB를 대체할 수 없음, 클라이언트 측면의 로드 밸런싱일 뿐
  - Geoproximity ( using Route 53 Traffic Flow feature )
  
   ![](https://velog.velcdn.com/images/xodbs1123/post/b3c570ce-7982-4c06-8b1d-5bd56f0a0538/image.png)

   ![](https://velog.velcdn.com/images/xodbs1123/post/f12058a5-0e5f-49cd-a14c-7a0fae3cf997/image.png)

    - 사용자와 리소스의 지리적 위치를 기반으로 트래픽을 리소스로 라우팅하도록 함
    - 편향값을 사용해 특정 위치를 기반으로 리소스에 더 많은 트래픽을 이동
    - 지리적 위치를 변경하려면 편향값을 지정해야 함
    - 편향값 ( 1 to 99 ), more traffic to the resource
    - 편향값 ( -1 to -99 ), less traffic to the resource
    - Resources can be :
      - AWS resource ( specify AWS region )
      - Non-AWS resources ( specify Latitude and Longitude )
    - 편향 활용을 위해 고급 Route 53 트래픽 플로우 사용  
- IP based Routing

![](https://velog.velcdn.com/images/xodbs1123/post/c83f6052-130f-4a63-a516-5df93f3518bd/image.png)
  
  - 클라이언트 IP 주소를 기반으로 라우팅을 정의
  - Route 53에서 CIDR 목록을 정의
    - CIDR에 따라 트래픽을 어느 로케이션으로 보내야 하는지 정함
  - Use cases :
    - Optimize performance ( IP를 미리 알고 있으므로 )
    - reduce network costs ( IP가 어디에서 오는지 아니까 )
    
  ### Route 53 - Health Checks ###
  - 주로 공용 리소스에 대한 상태를 확인하는 방법
  - 개인 리소스 상태를 확인하는 방법도 있음

  ![](https://velog.velcdn.com/images/xodbs1123/post/151be31a-5b5c-44e0-81bd-54fbd2ba44cd/image.png)

- Health Check => Automated DNS Failover
  1. 공용 엔드 포인트 모니터링 ( application, server, other AWS resource )

      ![](https://velog.velcdn.com/images/xodbs1123/post/e72a81aa-1a1b-475b-9f29-d912261769f5/image.png)
    
    - 전 세계에서 온 15개의 상태 확인이 엔드포인트의 상태를 확인
     - 그 임계값을 정상 혹은 비정상으로 설정
     - 간격도 설정 가능, 30초 or 10초 ( 비용이 더 든다 )
     - HTTP, HTTPS 와 TCP 등 많은 프로토콜 지원
     - 18% 이상의 상태 확인이 엔드 포인트를 정상이라고 판단하면 Route 53도 정상이라고 간주
     - 상태 확인에 사용될 위치도 선택 가능
     - 상태 확인은 로드 밸런서로부터 2xx 나 3xx의 코드를 받아야 통과
     - 텍스트 기반 응답일 경우 응답의 첫 5,120 byte 확인 ( 텍스트가 있는지 확인하기 위해 )
     - 상태 확인이 ALB나 엔드 포인트에 접근 가능해야 함 ( Route 53의 상태 확인 IP 주소 범위에 들어오는 모든 요청 허용 )


   2. 다른 Health Check를 모니터링 ( Calculated Health Checks )

        ![](https://velog.velcdn.com/images/xodbs1123/post/1c648b9f-e069-4105-b543-3750bb4141a8/image.png)

       - 여러 개의 상태 확인 결과를 하나로 합쳐주는 기능
       - OR, AND, NOT 으로 상태 확인 합칠 수 있음
       - 상위 상태 확인이 통과하기 위해 몇 개의 상태 확인을 통과해야 하는지 지정 가능
       - 상태 확인이 실패하는 일 없이 상위 상태 확인이 웹사이트를 관리 유지하도록 하는 경우 사용
     
  4. CloudWatch 경보 상태 모니터링 ( 제어가 쉽고 개인 리소스들에 유
  용 )

   ![](https://velog.velcdn.com/images/xodbs1123/post/8ce9e4a0-8298-42ce-a82e-a4b4eeebac10/image.png)
    
    - CloudWatch의 지표에서 각 Health Check 확인 가능
    - CloudWatch Metric을 이용해 개인 서브넷 안에 있는 EC2 인스턴스를 모니터 하는 것
    - Metric이 침해되는 경우 ClowdWatch 알람 생성
    - 알람 상태가 되면 상태 확인은 자동으로 비정상 됨
    - 즉, 개인 리소스에 대한 상태 확인을 만든 것이나 다름 없음
