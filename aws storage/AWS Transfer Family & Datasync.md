### AWS Transfer Family ###
- FTP 프로토콜 전송 지원
- FTPS ( FTP의 암호화된 형태 ) SSL을 통한 파일 전송 프로토콜 지원
- SFTP 보안 파일 전송 프로토콜 지원
- 완전 관리형 인프라이며 확장성, 안정성이 높고 가용성도 높음
- 시간당 프로비전이된 엔드 포인트 비용 + 전송된 데이터의 GB당 요금 청구
- 서비스 내에서 사용자 자격 증명을 저장 및 관리 가능
- 기존의 외부 인증 시스템과 통합 가능 ( Microsoft Actie Directory, LDAP, Okta, Amazon Cognito, custom )
- 사용 사례
  - 파일 공유, 공개 데이터셋 공유, CRM, ERP 등

   ![](https://velog.velcdn.com/images/xodbs1123/post/82393f43-aa7a-4c73-bcaa-bb8b28a30b5e/image.png)

### AWS DataSync ###

![]
(https://velog.velcdn.com/images/xodbs1123/post/784df7a9-d477-4c54-8c38-a8d622e40f8c/image.png)

![](https://velog.velcdn.com/images/xodbs1123/post/f96d4789-7474-4e5c-8b86-7f5df2114f97/image.png)

- 데이터를 동기화하여 대용량 데이터를 옮길 수 있음
  - 온프레미스나 AWS의 다른 클라우드로 옮길 수 있음
  - 이때 서버를 NFS, SMB HDFS 또는 다른 프로토콜에 연결해야함
  - 옮길 위치인 온프레미스나 연결할 다른 클라우드에 에이전트가 있어야함
  - AWS의 서비스에서 다른 AWS 서비스로 데이터를 옮기는 등, 다른 유형의 마이그레이션도 가능
  - 복제 작업은 매 시간, 매일 혹은 매주 실행되도록 가능
  - 파일 권한과 메타데이터 저장 기능이 있음 ( NFS POSIX, SMB )
  - 에이전트 하나의 태스크가 초당 10Gb까지 사용 가능
  - 네트워크 대역폭에 제한을 걸 수 있음
  - AWS Snowcone 사용을 통해 네트워크 용량 해결 가능

#### DataSync 동기화 가능 목록 ####
  - Amazon S3 ( any storage classes - including Glacier )
  - Amazon EFS
  - Amazon FSx ( All OS )
