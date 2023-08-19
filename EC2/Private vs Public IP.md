### Private vs Public Ip (IPv4)
- IPv4 : ex) 1. 160. 10. 240
  - 온라인에서 가장 널리 사용되는 형식
  - 공용 공간에서 37억 개의 서로 다른 주소 허용, 거의 고갈
  - [0-255].[0-255].[0-255].[0-255]
- IPv6 : ex) 3ffe: 1900 : 4545 : 3 : 200 : f8ff : fe21 : 67cf
  - IoT에서 많이 쓰임
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/0b28c338-ee1c-4211-bf28-3935959e0c71/image.png)
  
- 각 서버들은 공용 IP를 통해서 서로 통신(인터넷 전역에 접근 가능)
- 사설 IP는 사설 네트워크 안 컴퓨터끼리만 통신
- 사설 IP도 공용 게이트웨이인, 인터넷 게이트웨이를 이용하면 다른 서버들에 접근 가능 (AWS의 일반적인 패턴) 
- 두 개 이상의 기기가 같은 공용 IP를 가질 수 없음
- 사설 IP는 사설 네트워크 안에서만 유일하면 됨
- 즉, 네이버와 카카오가 같은 사설 IP를 가질 수 있음
- NAT 장치와 프록시 역할을 할 인터넷 게이트웨이를 통해 외부 인터넷 연결
  - 프록시 : 프록시 서버는 클라이언트가 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해 주는 컴퓨터 시스템이나 응용 프로그램
- 사설 IP는 지정된 범위의 IP만 지정 가능  
- 탄력적 IP
  - 인스턴스를 시작하고 중지할 때 public IP를 바뀌므로 고정적 IP를 사용하기 위해 탄력적 IP를 사용하는 것
  - 최대 5개만 사용 가능
  - 사용하지 않는 것이 좋음
  - 대신 임의의 공용 IP를 사용하여 DNS 이름을 할당하는 것이 좋음
- 기본적으로 EC2는 내부 AWS 네트워크에서는 사설 IP사용
- World Wild Web( WWW ) 에서는 공용 IP 사용
- EC2 기기에 SSH 할 때는 사설 IP 사용 불가능
  - VPN을 쓰지 않는 이상 같은 네트워크에 있는 것이 아니기 때문
  
### 인스턴스 재시작시 공용 IP 유지 방법 ###  
1. 탄력적 IP 사용
   - EC2 콘솔 > 네트워크 및 보안 > 탄력적 IP > 탄력적 IP 주소 할당
     
  ![](https://velog.velcdn.com/images/xodbs1123/post/deccaa18-9a5d-4108-be6e-3121814b8a31/image.png)

   - 특정 EC2 인스턴스에 할당되며 연결이 유지되는 한 탄력적 IP 유지
   - 탄력적 IP주소 가지고 있는데 사용하지 않으면 요금 부과
    - 따라서 빠르게 인스턴스에 연결해야 함
2. 작업(Actions) > 탄력적 IP 주소 연결

![](https://velog.velcdn.com/images/xodbs1123/post/461a0787-8040-4524-944d-968ef1feb764/image.png)

3. 인스턴스와 사설 IP 선택

![](https://velog.velcdn.com/images/xodbs1123/post/8bdb7f3c-03ae-4555-8d3b-aae8e3ef17db/image.png)

4. 탄력적 IP로 접속 가능해짐

![](https://velog.velcdn.com/images/xodbs1123/post/9c1632f0-857c-443a-850b-3fe35d3683bb/image.png)

5. 탄력적 IP에서 연결 해제하면 인스턴스에서 제거 가능
6. 이후 탄력적 IP 릴리스 선택
