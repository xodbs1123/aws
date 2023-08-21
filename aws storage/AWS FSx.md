### Amazon FSx ###
- 완전 관리형 서비스로 타사의 고성능 파일 시스템을 실행시킴
- 제공하는 파일 시스템 종류
- FSx File System Deployment OPtions
  - Scratch File System
    - 임시 스토리지
    - 데이터 복제가 안됨
    - 오작동하면 파일이 모두 날라감
    - 최적화로 초과 버스트 가능 ( 200MBps per Tib )
    - 단기 처리 데이터에 사용
    - 데이터 복제가 없어 비용 최적화 가능
  - Persistent(영구) File System
    - 장기 스토리지
    - 동일한 AZ 내에서 복제 가능
    - 민감한 데이터에 적합

![](https://velog.velcdn.com/images/xodbs1123/post/2c203779-6a82-4b57-b3c6-054049567363/image.png)

#### FSx for Windows File Server ####
  - 완전 관리형 Windows 파일 서버 공유 드라이브
  - SMB 프로토콜과 Windows NTFS 지원
  - Microsoft Active Directory 통합을 지원
    - 사용자 보안 추가, ACL로 사용자 할당량 추가로 액세스 제어 가능
  - Linux EC2 인스턴스에도 마운트 가능
  - DFS 기능을 사용하여 파일 시스템 그룹화 가능 ( 온프레미스의 Windows 파일 서버와 FSx for Windows File Server 결합 가능 )
  - Scale up to 10s of GB/s, millions of IOPS, 100s PB of data
  - Storage Options
    - SSD : 지연 시간이 짧아야하는 워크로드 저장
      - 데이터베이스, 미디어 처리 데이터 분석 등
    - HDD : 넓은 스펙트럼의 워크로드 저장
      - 홈 디렉터리나 CMS 등
   - 프라이빗 연결로 온프레미스 인프라에서 액세스 가능
   - 고가용성 다중 AZ에 대해 구성 가능
   - 모든 데이터는 재해 복구 목적으로 S3에 매일 백업
#### FSx for Lustre ####
- 동영상 처리, 금융 모델링, 전자 설계 자동화 등의 애플리케이션에서 쓰임
- 확장성이 높음
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- Storage Options
    - SSD : 지연 시간이 짧아야하는 워크로드
    - IOPS : 크기가 작은 무작위 파일 작업
    - HHD : 처리량이 많거나 크기가 큰 시퀀스 파일 작업
 - S3와 무결성 통합 가능
   - 파일 시스템처럼 S3를 읽고 S3에 출력하는 것이 가능
 - VPN과 직접 연결을 통해 온프레미스 서버에 사용 가능

#### FSx for NetApp ONTAP ####
- NFS, SMB, iSCSI 프로토콜과 호환
- 온프레미스 시스템의 ONTAP이나 NAS에서 실행 중인 워크로드를 AWS로 옮길 수 있음
- Linux, Windows, MacOS, VMware Cloud on AWS, Amazon Workspaces & AppStream 2.0, Amazon EC2, ECS and EKS 에서 사용 가능 = 호환 가능한 폭이 넓다
- 스토리지는 자동으로 확장 및 축소 = 오토 스케일링
- 복제오 스냅샷 기능 지원
- 데이터 압축 및 데이터 중복제거 가능
- 지정 시간 복제 기능이 있음
- 비용 저렴

### FSx for OPenZFS ###
- 여러 버전에서의 NFS 프로토콜과 호환 가능
- 주로 ZFS에서 실행되는 워크로드를 내부적으로 AWS로 옮길 때 사용
- Linux, MacOS, Windows 등에서 사용  가능
- Up to 1,000,000 IOPS with < 0.5ms latency
- 스냅샷, 압축 지원, 지정 시간 동시 복제 기능 지원
- 비용 저렴
