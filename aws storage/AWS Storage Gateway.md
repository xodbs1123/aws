### AWS Storage Cloud Native Option ###

![](https://velog.velcdn.com/images/xodbs1123/post/2450ae24-7e43-4528-9726-ecc83e371cfa/image.png)

### AWS Storage Gateway ###

![](https://velog.velcdn.com/images/xodbs1123/post/703c1dec-fccc-4196-b316-c8d93fc23f81/image.png)
 
- 온프레미스 데이터와 클라우드 데이터간의 연결 역할
- 사용 예시
  - 재해 복구
  - 백업 및 복구
  - 클라우드 마이그레이션, 온프레미스에서 클라우드 간 스토리지 확장
  - 데이터 대부분을 AWS에 저장하고 파일 액세스 지연 시간을 줄이기위해 Storage Gateway를 온프레미스 캐시로 사용
 - Types of Storage Gateway
   - S3 File Gateway
  ![](https://velog.velcdn.com/images/xodbs1123/post/63b87e84-a131-4a44-94be-c0f8503575fa/image.png)

     - 모든 버킷을 NFS 및 SMB 프로토콜을 사용하여 액세스 가능
     - 사용된 데이터는 파일 게이트웨이에 캐시로 저장됨 ( 최근 사용된 파일만 파일 게이트웨이에 존재 )
     - S3 Standard, S3 Standard IA, S3 One Zone A, S3 Intellignet Tiering 지원
     - 생명 주기 정책 사용시 S3 Glacier로 이동 가능
     - 버킷에 액세스하기 위해 각 파일 게이트웨이마다 IAM Role 생성 필요
     - SMB 프로토콜 사용하는 경우 사용자 인증을 위해 Active Directory와 통합해야함
     
   - FSx File Gateway
   
   ![](https://velog.velcdn.com/images/xodbs1123/post/1d52cda2-4a96-42e3-830c-b60752457eb9/image.png)

     - Amazon FSx for Windows File Server에 네이티브 액세스 제공
     - 자주 액세스하는 데이터의 로컬 캐시 확보 가능
     - Window native와 호환 ( SMB, NTFS, Active Directory.. )
     - 그룹 파일 공유나 온프레미스를 연결할 홈 디렉토리로 사용 가능
   
   - Volume Gateway
   
   ![](https://velog.velcdn.com/images/xodbs1123/post/3297e156-1c9b-488a-8f8c-eccc342ac130/image.png)

     - 블록 스토리지로 Amazon S3가 백업하는 iSCSI 프로토콜 사용
     - 볼륨이 EBS 스냅샷으로 저장되어 온프레미스 볼륨 복구 가능
       - Cached volumes : 데이터 액세스 시 지연 시간이 낮음
       - Stored volumes : 전체 데이터 세트가 온프레미스에 있어 주기적으로 S3 백업이 있음
   
  
   - Tape Gateway
   
   ![](https://velog.velcdn.com/images/xodbs1123/post/84fb8c91-3b93-42e4-b21d-bea6b6cf174d/image.png)

     - 물리적으로 테이프를 사용하는 백업 시스템이 있는 회사가 클라우드를 활용해 데이터를 백업할 수 있게 해줌
     - 가상 테이프 라이브러리(VTL)는 S3와 Glacier을 이용
     - 테이프 기반 프로세스의 기존 백업 데이터를 iSCSI 인터페이스를 사용하여 백업
    
  - Hardward appliance
    - 온프레미스 서버가 없는 경우 사용
    - 미니 서버 역할을 함
    - 가상화가 없는 경우 유용
  
