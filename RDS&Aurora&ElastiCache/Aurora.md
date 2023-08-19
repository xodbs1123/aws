### Amazon Aurora ###
- 시험에 자주 나온다..!!
- AWS 고유 기술 ( not open sourced )
- Postgres 및 MySQL과 호환됨
- 클라우드에 최적화 되어 있음
- RDS의 MySQL보다 5배 좋은 성능
- RDS의 Postgres보다 3배 좋은 성능
- Aurora의 스토리지는 자동으로 확장
- 읽기 전용 복제본 15개까지 가능 ( MySQL은 최대 5개 )
- 비용이 RDS에 비해 20% 정도 높지만 스케일링 측면에서 훨씬 효율적
- 높은 가용성과 읽기 스케일링
  - 3개의 AZ에 걸쳐 기록할 때마다 6개의 사본 저장
  - Write에는 6개 사본 중 4개만 있으면 됨
  - Read에는 6개 사본 중 3개만 있으면 됨
- 자가 복구 기능
  - 일부 데이터가 손상되거나 문제가 있으면 백엔드에서 P2P 복제를 통한 자가 복구 진행
  - 수 백개의 볼륨을 사용함
- 쓰기를 받는 인스턴스는 하나 뿐 ( 마스터 인스턴스 )
- 마스터가 작동하지 않으면 평균 30초 이내로 장애 조치 시작
- 마스터에 문제가 생기면 읽기 전용 복제본 중 하나가 마스터가 되어 대체
- 리전 간 복제를 지원함 ( Global Aurora 생성 가능 )
- Aurora 작동 방식
- 라이터(Writer) 엔드폰인트를 통해 DNS 이름으로 항상 마스터를 가리킴
- 자동 스케일링을 통해 절적한 수의 읽기 전용 복제본 존재하도록 할 수 있음 ( 복제본 CPU 사용량 또는 복제본 접속 횟수에 기반해 복제본 스케일링 가능 )
- 리더(Reader) 엔드포인트를 통해 모든 읽기 전용 복제본과 자동으로 연결
  - 읽기 복제본 중 하나로 연결되어 로드 밸런런싱을 도와줌
  - 로드 밸런싱은 연결 레벨이서 이루어진다..!!

![](https://velog.velcdn.com/images/xodbs1123/post/5423d365-4224-4d4d-a5ad-929fff0050eb/image.png)

- Aurora 추가 기능

![](https://velog.velcdn.com/images/xodbs1123/post/01bef341-2087-4710-8a7c-2f4736867eef/image.png)

### Aurora 실습 ###
- RDS > 데이터베이스 생성 > Aurora > 각 옵션 선택

![](https://velog.velcdn.com/images/xodbs1123/post/e159540a-1440-4f0e-8951-87932f430ded/image.png)

- 데이터베이스를 생성하면 Region 클러스터와 그 안에 Writer 인스턴스, Reader 인스턴스가 나누어져 생성되어 있음 ( 서고 다른 AZ에 존재 )

### Aurora 심화 ###
- 복제본 자동 스케일링

![](https://velog.velcdn.com/images/xodbs1123/post/0781ba0a-2417-4f86-a0a8-5f9e2a9cd314/image.png)

- 사용자 지정 엔드포인트
  - 사용자 지정 엔드포인트가 있으면 일반적으로 Reader 엔드포인트는 사용하지 않음, 사라지는 것은 아님!!

![](https://velog.velcdn.com/images/xodbs1123/post/cee12c58-03de-4cd3-8f43-a6d1409b409d/image.png)

- Serverless 기능
  - 실제 사용량에 기반한 자동 데이터베이스 인스턴스화와 자동 스케일링 가능하게 해줌
  - 비정기적, 간헐적, 예측 불허한 워크로드에 유용
  - 용량 계획 세울 필요가 없음
  - 각 Aurora 인스턴스에 대해 매 초당 비용 지불하게 됨
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/5b2b36c2-a484-44e6-a68f-ef0d1f4b9d76/image.png)

- Multi-Master
  - Writer 노드에 대한 즉각적 장애 조치
  - Writer 노드에 높은 가용성을 갖추고자 할 때 사용
  - Aurora 클러스터의 모든 노드에서 읽기 및 쓰기 가능

   ![](https://velog.velcdn.com/images/xodbs1123/post/78d73a4b-6a66-4f68-9fa6-6ab0894b1c00/image.png)

- Global Aurora
  - 모든 쓰기 및 읽기가 진행되는 하나의 기본 리전이 존재
  - 복제 지연이 1초 미만인 보조 읽기 전용 리전 5개까지 설정 가능
  - 각 보조 지역마다 읽기 전용 복제본 16개까지 생성 가능
  - 한 리전의 데이터베이스가 작동 중단될 경우 재해 복구 목적으로 다른 지역을 승격하는데 필요한 복구 시간(RTO) 목표는 1분 미만

   - Auroroa Global 데이터베이스에서 Region에 걸쳐 데이터 복제에 걸리는 시간은 평균 1초 미만 ( 시험에 출제 !! )

   ![](https://velog.velcdn.com/images/xodbs1123/post/fb096ee1-0c0a-4c85-9f69-fda6970b1ca6/image.png)

- Aurora Machine Learning
  - ML 기반 예측을 SQL 인터페이스로 애플리케이션에 적용
  - SageMaker, Amazon Comprehend 서비스 지원
  - 맞춤 광고, 감정 분석 제품 추천 등이 있음

   ![](https://velog.velcdn.com/images/xodbs1123/post/0cfa4e3a-f60f-41d4-85b3-1fae1bbd6b0b/image.png)
