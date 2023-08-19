### Amazon RDS ###
- Relational Database Service
- SQL을 쿼리 언어로 사용하는 데이터베이스용 관계 데이터베이스 서비스
- 클라우드의 RDS 서비스에 DB 생성 가능, AWS가 DB 관리
  - ex) PstgreSQL, MySQL, MariaDB, Oracle, Microsoft SQL Server, Aurora
- 데이터베이스 프로비저닝과 기본 운영체제 패치가 자동화되어 있음  
- 지속적으로 백업 생성, 특정 시점으로 복원 가능
- 데이터베이스의 성능을 대시보드에서 모니터링 가능
- 읽기 전용 복제본을 활용해 읽기 성능 개선 가능
- 재해 복구 목적 다중 AZ 설정 가능
- 인스턴스 수직 및 수평 확장 가능
- EBS에 파일 스토리지 구성, gp2와 io1 볼륨
- RDS 인스턴스에 SSH 엑세스 불가능
- 기본 EC2 인스턴스에는 엑세스 불가능
#### RDS - Stroage Auto Scaling (시험 !!) ####
- 스토리지 용량을 20GB로 설정했는데 경우에 따라 공간 부족해질 수 있음
  - 이때, RDS 스토리지 오토 스케일링이 자동으로 스토리지 확장해줌
- 할당된 용량에서 은 공간이 10% 미만이 되면 스토리지를 자동으로 수정
  스토리지 부족 상태가 5분 이상 지속되거나 지난 수정으로부터 6시간이 지났을 경우에 오토 스케일링이 활성화되어 있다면 스토리지가 자동 확장  
  
### RDS Read Replicas for read scalabilty ###
- 읽기를 스케일링함

![](https://velog.velcdn.com/images/xodbs1123/post/1c1c6194-9624-4641-80b4-8ecd2e435b3e/image.png)

- 사용 사례
   - 새로운 팀이 우리의 데이터를 기반으로 분석 하고자 함
   - 메인 RDS 데이터베이스 인스턴스에 연결하면 오버로드 발생 및 속도가 느려지므로, 읽기 전용 복제본 생성해서 연결 시켜줌
   
 ![](https://velog.velcdn.com/images/xodbs1123/post/b7555936-ccb1-4592-adb0-a9284461ae9a/image.png)

- 읽기 전용 복제본에 있는 경우 SELECT 명령문만 사용
- AWS에서 데이터 이동은 비용 발생, 하지만 보통 관리형 서비스는 비용이 발생하지 않는다
  - RDS는 관리셩 서비스
- 읽기 전용 복제본이 다른 AZ지만 동일한 Region에 있으면 데이터 이동 비용 발생하지 않음
#### RDS Multi AZ (Disaster Recovery)
- 마스터 데이터베이스의 인스턴스 또는 스토리지에 장애가 발생할 때 스탠바이 데이터베이스가 새로운 마스터가 될 수 있도록 하는 것 (자동)
- 스탠바이 데이터베이스는 단지 대기 목적만 수행, 읽거나 쓸 수 없음

![](https://velog.velcdn.com/images/xodbs1123/post/1dc38861-c722-4172-a530-ac59fc259fbb/image.png)

- 재해 복구 대비 읽기 전용 복제본을 다중 AZ로 설정할 수 있음 (시험 자주 출제!!!)
- 단일 AZ에서 다중 AZ로 RDS 데이터베이스 전환
  - 다운 타임이 전혀 없음, 데이터베이스 중지가 필요 없다는 뜻
  - 데이터베이스 수정 클릭 후 다중 AZ 기능 활성화시키면 됨
  - 내부적으로 기본 데이터베이스의 RDS가 자동으로 스냅샷 생성
    - 새로운 스텐바이 데이터베이스에 복원됨
    - 두 데이터베이스 간 동기화 설정이 되어 다중 AZ 설정 상태가 됨

![](https://velog.velcdn.com/images/xodbs1123/post/76968f61-b09f-4bab-b063-060bfa26eeab/image.png)


### RDS 실습 ###
1. RDS > 데이터베이스 > 데이터베이스 생성 > 각 옵션 선택

![](https://velog.velcdn.com/images/xodbs1123/post/1440cebe-7404-4996-ad20-5f8da23cb2d3/image.png)
 
  - MySQL은 포트 3306 씀, 보안그룹 인바운드 규칙 확인하면 포트 범위 3306임을 확인할 수 있음
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/d0252bd4-5657-48c0-a0ee-4fb76eecf1f3/image.png)

2. SQL Electron Download, google 검색
3. Endpoint & Port 복사해서 SQL Electron을 통해 연결
  - 새 데이터베이스 추가
  - 서버 주소 붙여 넣고 포트 3306 선택
  - 연결 테스트 후, save

![](https://velog.velcdn.com/images/xodbs1123/post/3242338d-928a-4ae0-824c-38791fe89a42/image.png)

4. 데이터베이스에서 TABLE 생성
5. 생성 후 테이블에 각종 데이터 삽입 가능

![](https://velog.velcdn.com/images/xodbs1123/post/69bdf31d-a44b-4886-b68f-e922133436e1/image.png)
-------------
#### RDS 각종 기능 #### 
- 읽기 전용 복제본 만들기
- 모니터링
- 스냅샷 생성
- 특정 시점 복원
- 다른 Region으로 스냅샷 마이그레이션

![](https://velog.velcdn.com/images/xodbs1123/post/ab048672-d713-4f74-9b6f-76a073e947e2/image.png)

#### RDS Custom ####
- Oracle과 Microsoft SQL Server 다룸
- OS 및 데이터베이스 사용자 지정 기능에 엑세스 가능
- RDS : AWS에서의 데이터베이스 자동화 설정, 운영, 스케일링 장점 모두 챙길 수 있음
- Custom : 기저 데이터베이스와 운영 체제에 엑세스 가능
  - 내부 설정 구성, 패치 적용, 네이티브 기능 활성화 가능
  - SSH 또는 SSM 세션 관리자를 사용해 RDS 뒤에 있는 기저 EC2 인스턴스에 엑세스 가능
  - 사용자 지정 설정을 적용 및 검색 추가 가능
     - 해당 기능 사용시 RDS가 자동화, 유지관리, 스케일링 작업 자동화 꺼두는 게 좋음
     - 데이터베이스 스냅샷 만들어 두는 것이 좋음
- RDS vs RDS Custom 
  - RDS : 데이터베이스 전체 관리, 운영 체제와 나머지는 AWS에서 관리
  - RDS Custom : Oracle 및 Microsoft SQL Server에서만 사용 가능
      - 기저 운영 체제와 데이터베이스에 대한 관리자 권한 전체를 갖게 됨
