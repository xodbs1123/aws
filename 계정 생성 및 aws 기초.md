1. AWS 계정 생성
![](https://velog.velcdn.com/images/xodbs1123/post/310530b7-c500-441d-b287-d2f7c128653e/image.png)

### Regions ###
  - 데이터 센터의 집합
  - 대부분의 서비스들은 특정 리전에 연결되어 국한
  - 한 리전에서 특정 서비스를 이용하다 다른 리전에서 그 서비스를 이용하료고 하면, 서비스를 처음 이용하게 되는 거나 다름없음
  
  Q) 새로운 애플리케이션을 출시하는 경우 어떤 리전을 선택하면 될까요? 미국, 유럽, 남아메리카 호주 중 어디가 좋을까요?
  
  A) 상황에 따라 다르다
  
- AWS 리전 선택에 영향을 미칠 수 있는 요인
  - 각 나라의 법률
  - 지연 시간
  - AWS를 지원하지 않는 리전
  - 요금, 리전마다 요금 다름
  
### Availabilty Zones ###
  - Region 내에 존재함
  - 보통 3개, 최소 2개, 최대 6개
  - 각각의 Availabgilty Zone은 여분의 전원 네트워킹, 통신 기능을 갖춘 1개 또는 2개의 개별적 데이터 센터로 구성
  - 재난 상황에 대비해 서로 분리 되어 있음, 문제에 대해 서로 영향 X
  
### AWS Regional Service ###
[aws regional service](https://aws.amazon.com/ko/about-aws/global-infrastructure/regional-product-services/)
- 각 리전에서 제공하는 서비스들이 어떠한 것이 있는지 확인 할 수 있음
- 모든 리전에 AWS의 모든 서비스가 있는 것은 아님

