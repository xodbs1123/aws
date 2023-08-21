### AWS Storage Comparsion ###

- S3 : 객체 스토리지, 대부분의 AWS와 연결 가능
- S3 Glacier : 객체를 아카이브할 때 사용
- EBS volumes : 한 번에 한 개의 EC2 인스턴스에만 스토리지 연결할 때 사용, IO1과 IO2 볼륨에 다중 연결 기능 지원
- Instance STorage : 고성능 물리 스토리지가 필요한 경우 사용 ( high IOPS )
- EFS : 네트워크 파일 시스템이 필요하며 다중 가용 영역 간 마운트해야 하면서 POSIX 파일 시스템이 필요할 때 사용
- FSx for Windows : Windows 서버 파일 시스템이 필요한 경우
- FSx for Lustre : 고성능 연산 Linux 파일 시스템이며 Lustre 클라이언트와 호환 가능해야 하는 경우 사용
- FSx NetApp ONTAP : 높은 운영 체제 호환성과 네트워크 파일 시스템이 필요할 때 사용
- FSx for OpenZFS : 관리형 ZFS 파일 시스템이 필요한 경우 사용
- Storage Gateway : S3, FSx File Gateway, Volume Gateway ( cache & stored ), Tape Gateway 를 활용하여 온프레미스 및 클라우드, S3, FSx에 파일 동기화 가능
- Transfer Family : FTP, FTPS, SFTP 인터페이스를 필요로 하는 경우 사용
- DataSync : 온프레미스에서 AWS, AWS에서 AWS로 일정에 따라 데이터 동기화할 때 사용, 
- Snowcone / Snowball / Snowmobile : 물리적으로 대용량의 데이터를 옮겨야 할 때 사용, 온프레미스 설치 후 클라우드로 옮길 수 있음
- Database
