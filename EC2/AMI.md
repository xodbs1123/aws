### AMI ( Amazon Machine Image ) ###
- EC2 인스턴스를 통해 만든 이미지
- 특정 AWS Region에 국한, 각 Region에는 고유 AMI가 있음
- AMI를 특정 지역에 구축한 후 다른 지역으로 복사해 글로벌 인프라로 활용 가능 
- AMI로 AWS 구축 가능 및 Customization 가능
- 원하는 소프트웨어 및 설정 파일 추가
- 별도의 운영 체제 설치
- 모니터링 툴 추가
- AMI 따로 구성시, 부팅 및 설정 시간 단축
  - AMI가 EC2 인스턴스에 설치해야할 모든 소프트웨어 패키징 해줌
- AWS에서 제공하는 Linux2 AMI 등을 활용 가능
   - 또는 직접 구축할 수도 있으나 유지, 관리도 직접 해야함
- AWS 마켓플레이스에서 다른 사람이 구축한 AMI 사용할 수도 있음   

![](https://velog.velcdn.com/images/xodbs1123/post/a9bbb5b8-7dbf-4c63-adb3-158edc00a884/image.png)


### AMI 실습 ###
1. 신규 인스턴스 생성
2. 인스턴스 우클릭 > 이미지 및 템플릿 > 이미지 생성

![](https://velog.velcdn.com/images/xodbs1123/post/d08ebb4a-ebfe-409e-a1bd-ba224b2a8f38/image.png)

3. 인스턴스 시작 > 나의 AMI 클릭

![](https://velog.velcdn.com/images/xodbs1123/post/e25b559b-8ba0-4d93-918d-a29ee7b4815e/image.png)

4. 코드 첫 번째 행과 마지막행만 복사
   - 인스턴스가 시작될 때 index.html 파일을 생성하는 메시지를 사용자 지정하고 EC2를 사용자 부팅했을 때 하나의 명령만 실행되도록 하는 것

![](https://velog.velcdn.com/images/xodbs1123/post/32fbd11b-b01c-4d84-b873-3c4448172eea/image.png)
  
   - 필요한 소프트웨어가 EC2 인스턴스에 설치되어 있으므로 부팅 시간이 단축됨
   - 일반적 소프트웨어나 보안 소프트웨어, 방화벽 또는 사용자 지정 구성 작업 시 유용
