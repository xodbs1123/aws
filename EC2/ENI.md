## Elastic Network Interfaces ( ENI )
- VPC의 논리적 구성 요소, 가상 네트워크 카드를 나타냄
- EC2 인스턴스가 네트워크에 엑세스할 수 있게 해줌
- EC2 인스턴스 외부에서도 사용

### ENI 속성 ###
- 주요 사설 IPv4와 하나 이상의 보조 공용 IPv4를 가질 수 있음
- 하나 이상의 보안 그룹을 연결할 수 있음
- EC2 인스턴스와 독립적으로 ENI를 생성하고 즉시 연결하거나 장애 조치를 위해 EC2 인스턴스에서 이동 가능
  - 장애 조치에 유용

![](https://velog.velcdn.com/images/xodbs1123/post/62715e2e-469b-447a-a77c-2dfd86333601/image.png)

- 가용 영역(AZ)에 바인딩 됨

### ENI 실습 ###
- 각 인스턴스에는 하나의 네트워크 인터페이스가 존재
- eni로 시작하는 ID, 퍼플릭 IPv4, 프라이빗 IPv4, IPv4 DNS가 있음

![](https://velog.velcdn.com/images/xodbs1123/post/9918e719-0f15-404f-a89c-abf48382cfbe/image.png)

- 인스턴스 생성 시 2개로 하면 그 2개는 Network interfaces로 연결 됨

![](https://velog.velcdn.com/images/xodbs1123/post/bde20894-8247-4f8d-9679-7116a93d7e0f/image.png)

- 새로운 네트워크 인터페이스 생성 가능
- 이름, 서브넷, 보안 그룹 선택 후 생성

![](https://velog.velcdn.com/images/xodbs1123/post/87d290c4-ee7a-444a-b34f-3eda01dbcabb/image.png)

- Actions 메뉴에서 Attach를 클릭하고 연결하려는 인스턴스 클릭

![](https://velog.velcdn.com/images/xodbs1123/post/44f9a427-2f1a-47ed-a487-2a4435e2cd70/image.png)

- 인스턴스에서 Networking 탭을 보면 두 개의 인터페이스 표시 확인 가능
- 하나는 퍼블릭, 프라이빗 IPv4가 있는 기본 인스턴스
- 다른 이스턴스인 DemoENI에는 보조 프라이빗 IPv4 주소가 있음

![](https://velog.velcdn.com/images/xodbs1123/post/0492b4a4-a158-45a7-adac-e07bc8536ad8/image.png)

- 해당 ENI를 제어할 수 있으므로 이 ENI를 통해 EC2 인스턴스에서 다른 인스턴스로 이동시키는 것
  - ex) 같은 애플리케이션을 가동 중인 EC2 인스턴스 두 개가 있다
    프라이빗 IPv4를 통해 다른 인스턴스로 접근하려면
    ENI를 다른 EC2 인스턴스쪽으로 옯겨주면 됨
    다른 방법보다 빠르고 간편하게 네트워크 장애 조치 수행 가능

![](https://velog.velcdn.com/images/xodbs1123/post/62715e2e-469b-447a-a77c-2dfd86333601/image.png)

- 인스턴스를 종료하면 직접 만든 ENI는 남고 인스턴스와 함께 생성 된 ENI는 자동으로 삭제됨( 네트워크 인터페이스 연결 사진과 비교 )

![](https://velog.velcdn.com/images/xodbs1123/post/734f572e-4c1b-4f0d-874d-8aef90a5be89/image.png)
