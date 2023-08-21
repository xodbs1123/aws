### AWS Snow 제품군 ###
- 보안성이 뛰어난 휴대용 장치 모음
- 엣지에서 데이터를 수집하고 처리하기 위해 사용 or AWS 안팎으로 데이터를 마이그레이션 할 때 사용

### Data Migrations with AWS Snow Family ###
- 네트워크를 통해서 많은 데이터를 전송하려면 아주 오래 걸림
- 빠르게 접속하려면 데이터의 양, 제한된 대역폭, 대역폭 공유, 네트워크 비용, 불안정한 연결 문제가 발생함
- 이를 해결하기위해 Snow 제품군을 사용
  - 데이터를 마이그레이션함
  - AWS가 우편으로 물리적 장치를 보내주면 거기에 데이터를 끌어오고 다시 AWS로 배송하는 것
  - 일반적으로 네트워크 사용시 데이터 전송이 일주일이 넘으면 Snowball 장치를 사용하는 것이 좋음
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/4452ac0d-df23-43cb-8939-c421b4810d6c/image.png)
  
#### Snowball ####
- Snowball Edge는 TB 혹은 PB 데이터를 저장 가능
  - 데이터 전송 건마다 비용 청구
  - 인터페이스는 블록 스토리지 혹은 Amazon S3 호환 객체 스토리지 제공
  - Snowball Edge Storage Optimized는 80TB HDD 제공
  - Snowball Edge Compute Optimized는 42TB HDD 제공
  - 대량의 데이터 클라우드 마이그레이션이나 AWS에 데이터 백업을 통해 재해 복구하는 경우 사용
  
#### Snowcone ####
- snowball보다 크기 작음
- 이더넷 포트가 있어 어디서나 컴퓨팅이 가능
- 극악의 환경에서도 사용 가능
- 엣지 컴퓨팅, 스토리지 및 데이터 전송에 사용
- 8TB 저장 가능
- 드론 위에도 설치 가능!!
- 온/오프라인 전송 둘다 가능 ( 온라인은 AWS DataSync 사용 )

#### Snowmobile ####
- 진짜 트럭임
- EB 데이터 전송 가능
- 각 snowmobile 용랑은 100PB
- 보안성 뛰어나고 온도 조절 가능
- GPS 추적 및 비디오 감시로 안전한 데이터 전송 가능

![](https://velog.velcdn.com/images/xodbs1123/post/9094de47-07ec-44c5-9936-784898f1eca4/image.png)


### Edge Computing ###
- 데이터가 엣지 로케이션에서 생성될 때 실시간으로 처리하는 방식
- 엣지 로케이션
  - 인터넷이 없는 곳이나, 클라우드에서 멀리 있는 곳
- Snowball Edge나 Snowcone을 주문해서 엣지 로케이션에 장착시키면 엣지 컴퓨팅 가능
- 데이터 전처리, 클라우드로 보내지 않고 엣지에서 머신 러닝, 사전 미디어 스트림 트랜스코딩 등에 엣지 컴퓨팅 사용

### AWS OpsHub ###
- 컴퓨터나 노트북에 설치하는 소프트웨어
- 그래픽 인터페이스를 통해 snow 장치에 연결해서 구성 및 사용 가능

### Snowball을 통해 데이터를 직접 Glacier에 불러올 수 있는지? ###
- snowball은 Glacier에 데이터를 직접 끌어올 수 없음
- 단, Amazon S3를 먼저 사용하여 수명주기 정책 생성을 통해 Amazon Glacier로 객체를 전환할 수 있음

![](https://velog.velcdn.com/images/xodbs1123/post/6d92a773-73c1-464a-9c14-f016b5b6e4ce/image.png)
