### Amazon EFS - Elastic File System ###
- 네트워크 파일 시스템
- 여러 EC2 인스턴스에 마운트될 수 있음
  - 해당 EC2 인스턴스들은 여러 AZ에 있을 수 있음
- 가용성이 높고 확장성이 높다
- 가격이 비싸다, gp2 EBS 볼륨의 3배
- 사용량만큼 지불, 미리 용량을 프로비저닝하지 않아도 됨

![](https://velog.velcdn.com/images/xodbs1123/post/d15280a7-ef0d-4469-9b7b-b35153807420/image.png)

- 콘텐츠 관리에 사용
- 웹서버에 사용
- 데이터 공유 Wordlpress에 사용
- EFS에 대한 엑세스 제어를 위해 보안 그룹 설정해야함
- Linux기반 AMI와 호환됨
- 내부적으로 NFS 프로토콜 사용
- KMS를 사용해 EFS 드라이브에 저장 데이터 암호화 가능
- POSIX(이식 가능 운영체제 인터페이스) 시스템 사용, 표준 파일 API 가짐

### EFS 성능 (시험 출제!! ) ###
- 수천 개의 NFS 클라이언트에서 EFS에 동시 엑세스할 수 있게 확장됨
- 처리량 초당 10GB
- 용양을 미리 프로비저닝하지 않아도 NFS가 PB 규모로 자동 확장
- '범용 모드'
  - 기본설정
  - 지연 시간에 민감한 웹 서버, CMS와 같은 곳에 사용
- '최대 I/O'
  - 지연 시간, 처리량, 병렬 처리 성능 향상
  - 빅데이터나 미디어 처리 작업에 유용
- '처리량 모드'
  - 버스팅 모드가 기본값
  - 사용 공간 많을수록 버스팅 용량과 처리량 늘어남
  - 1TB 파일 시스템 데이터 전송 속도는 초당 50MiB, 최대 100MiB까지 버스트 가능
  - '프로비저닝 모드'로 설정 가능
    - 스토리지 크기 상관 없이 처리량 설정 가능
  ### EFS 스토리지 클래스 ###
  - 일정 기간 후 파일을 다른 계층으로 옮기는 기능
  - Standard 계층
    - 엑세스가 빈번한 파일 저장
  - EFS-IA( Infrequent Access )
    - 파일을 검색할 경우 검색에 대한 비용 발생
    - 파일을 저장하는 비용은 낮음
    - 수명 주기 정책 사용해야함

     ![](https://velog.velcdn.com/images/xodbs1123/post/e256c19c-e738-4c6c-b377-e32f139c3a23/image.png)

    EFS Standard 계층에 자주 사용하는 파일과
    60일 이상 액세스하지 않은 파일이 있다고 가정
	우리가 설정한 수명 주기 정책에 따라
	파일은 다른 계층인 EFS-IA로 옮겨짐
	비용은 낮아진다
- 가용성과 내구성
  - Standard
    - EFS를 다중 AZ에 설정
    - 프로덕션 사용 사례에 적합
    - 한 AZ가 중단되어도 EFS 파일 시스템에 영향 없음
  - One Zone
    - EFS 파일 시스템으로 개발 가능
    - 개발할 때 좋은 옵션
    - 하나의 AZ, 기본적으로 백업 활성화
    - EFS-IA 스토리지 계층과 호환, EFS One Zone-IA
    - 요금이 큰 폭으로 할인됨, 약 90% 절감 가능
    

@ 시험에서는 언제 EFS를 사용하는지, 유효성 검사와 요구 사항 준수를 위해 EFS 네트워크 파일 시스템에 설정해야 할 옵션을 물어볼 수 있음 
    

### EFS 실습 ###
1. EFS 콘솔 > 파일 시스템 생성

![](https://velog.velcdn.com/images/xodbs1123/post/e137589a-ee83-4230-a7ab-28da7d323c97/image.png)

2. 네트워크 엑세스 설정

![](https://velog.velcdn.com/images/xodbs1123/post/de68f03f-5738-4260-a102-bf9e2fe2017c/image.png)

3. 파일 시스템 정책 (고급 설정임)

![](https://velog.velcdn.com/images/xodbs1123/post/34fa5c6f-9966-4b03-be1c-0bd90b8cd111/image.png)

4. 검토 및 생성

![](https://velog.velcdn.com/images/xodbs1123/post/1a823f7e-10dd-4edf-8c7f-ccb3e2bad892/image.png)

- EC2에 마운트 하기
1. 인스턴스 생성 ( 네트워크 설정 > 서브넷 설정 > 파일 공유 시스템 추가 ... 등 세부 설정 )

2. EC2 콘솔이 보안 그룹을 생성해서 EFS 파일 시스템에 연결한 것 확인 가능

![](https://velog.velcdn.com/images/xodbs1123/post/d588bc61-82a6-46f5-8e66-9c40e8ef78e1/image.png)

3. efs-sg-2라는 보안 그룹이 인스턴스B EFS 파일 시스템에 연결 된 것 확인
   - 해당 보안 그룹이 인스턴스B의 EFS 파일 시스템 접근 제어

    ![](https://velog.velcdn.com/images/xodbs1123/post/2c8fa8e3-23fd-4b8b-82e4-f70f507a64df/image.png)

4. 가용영역 "ap-northeast-2a" 인스턴스 연결 후 파일 생성 명령어 입력

![](https://velog.velcdn.com/images/xodbs1123/post/1192669d-ff02-41a2-83e1-fc6a807e0c69/image.png)

5. 가용영역 "ap-northeast-2c" 인스턴스에서 해당 파일 찾을 수 있음

![](https://velog.velcdn.com/images/xodbs1123/post/4a6254a4-8be8-4085-b801-bb7141f88faa/image.png)
