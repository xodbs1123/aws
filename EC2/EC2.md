### EC2(Elastic Computer Cloud) ###
- AWS에서 제공하는 Infrastructure as a Service
- 포함하고 있는 주요 기능
  - Renting virtual Machine (EC2)
  - Storing data on virtual drives (EBS)
  - Distributing load across machine (ELB)
  - Scaling the services using an auto-scaling group (ASG)
- EC2 사용법을 아는 것은 **클라우드 작동 방식을 이해할 때 필수적**
  - 클라우드는 필요할 때마다 가상 공간을 언제든지 활용 가능한데 EC2가 그 예시

#### EC2 옵션 ####
- OS : Windos, Mac OS, **Linux** 
- CPU : How much compute power & cores
- RAM : How much random-access memory
- Storage space
  - Network-attached (EBS & EFS)
  - Hardware (EC2 Instance Store)
- Network card : Speed of the card, Public IP address
- Firewall rules : security group
- Bootstrap script (configure at first launch) : EC2 User Data
	
#### EC2 사용자 데이터 스크립트 ####
 - Bootstrap은 머신이 작동될 때 명령을 시작하는 것
 - 스크립트는 처음 시작할 때 한 번만 실행
 - 부팅 작업을 자동화하기 때문에 Bootstraping이라는 이름을 가짐
   - 업데이트, 소프트웨어 설치, 파일 다운로드 등의 사용자가 원하는 것을 자동화
- 사용자 데이터 스크립트에 작업을 추가할 수록 부팅 시 Instance의 작업이 많아짐
- 루트 계정에서 실행
  - 따라서, 모든 명령문은 sudo로 해야 함
- EC2 instance Types : example
![](https://velog.velcdn.com/images/xodbs1123/post/42492315-dc56-48b6-b988-ad7794660f51/image.png)

### EC2 Instance 생성 ###
1. EC2 > Instances > Launch instances
2. Instance 생성( 이름, OS, 이미지, 인스턴스 유형, 키 페어 등 선택 ) 
3. 하단에 있는 User data는 EC2를 첫 번째 생성할 때 실행되는 명령어를 입력할 수 있음

![](https://velog.velcdn.com/images/xodbs1123/post/804f0afe-7f1a-42c5-bc73-32fa7660ff46/image.png)

4. Summary에서 EC2 스펙 최종 점검

![](https://velog.velcdn.com/images/xodbs1123/post/ee6c87d1-bfb3-46ce-a8a0-fa0f46ec1b16/image.png)

5. 인스턴스 생성까지 10 ~ 15초 걸림..  이것이 클라우드의 힘!!
	즉, 서버를 보유하고 있지 않아도 바로 생성 가능..!!

- 인스턴스 정보
  - 인스턴스 ID : 고유 식별자
  - 공용 IPv4 : EC2 인스턴스에 접근하기 위해 사용할 주소
  - 사설 IPv4 : AWS 네트워크에서 내부적으로 인스턴스에 접근하는 주소
  ![](https://velog.velcdn.com/images/xodbs1123/post/b37e1783-a47a-4c20-b697-baf8f79df69a/image.png)
  - 그 외 세부 정보들을 포함하고 있음
  - 공용 Ipv4로 접속한 서버 모습
  ![](https://velog.velcdn.com/images/xodbs1123/post/73720855-41e3-4518-b7b2-336daeb8d685/image.png)
- 인스턴스를 중지 및 재실행 할 수 있음
  - 오래 실행시킬수록 지불해야 하는 금액이 커지므로 미사용시 중지
  - 재실행 시 공용 IPv4 주소가 변경 됨, 사설은 변경 X

![](https://velog.velcdn.com/images/xodbs1123/post/29842f1a-aff5-4af5-8522-c0d74923c2b2/image.png)


### EC2 Instance 종류 ###
[Amazon EC2 Instance Types](https://aws.amazon.com/ko/ec2/instance-types/)
 - 각 조건에 맞는 EC2 인스턴스 확인 가능
 - 각 스펙이나 요금 등을 비교 할 수 있음

 ![](https://velog.velcdn.com/images/xodbs1123/post/47b71e82-1dd3-463a-9095-724beb7ca93b/image.png)

### AWS 제품 이름 설정 규칙 ###
- ex) m5.2xlarge
  - m : Instance class, 범용의 인스턴스
  - 5 : Generation(세대)
  - exlarge : Instance size, 클수록 인스턴스에 더 많은 메모리와 CPU를 가지게 됨

### 인스턴스 최적화 유형 (시험 관련 숙지 사항) ###
- 범용 인스턴스( General Purpose )
  - 웹 서버나 코드 저장소와 같은 다양한 작업에 적합
  - 컴퓨팅, 메모리, 네트워킹 간의 균형이 잘 맞음
    - ex ) t2.micro

- 컴퓨팅 최적화 인스턴스( Compute Optimized )
  - 컴퓨터 고성능 작업에 적합
  - 데이터 일괄 처리
  - 미디어 트랜스코딩
  - 고성능 웹 서버
  - HPC 작업
  - 머신 러닝
  - 전용 게임 서버 등
  - 인스턴스 이름이 'C'로 시작하는 이름을 가짐
    - ex) C5, C6
    

- 메모리 최적화 인스턴스( Memory Optimized )
  - 메모리에서 대규모 데이터셋을 처리하는 작업에 적합
  - 고성능의 관계형 또는 비관계형 데이터베이스
  - 분산 웹스케일 캐시 저장소
  - BI에 최적화된 In-memory 데이터베이스
  - 대규모 비정형 데이터의 실시간 처리를 실행하는 어플리케이션
  - 인스턴스 이름이 RAM을 나타내는 'R'로 시작
    - ex) R6g, R5, R5a
  - 하지만, X1이나 대용량 메모리 Z1도 있음


- 스토리 최적화 인스턴스( Storage Optimized)
  - 로컬 스토리지에서 대규모 데이터셋에 접근할 때 적합
  - High Frequency Online Transcation Processing(OLTP) 시스템
  - 관계형과 비관계형 NoSQL 데이터베이스
  - 메모리 데이터베이스의 캐시,  ex) Redis
  - 데이터 웨어하우징 어플리케이션
  - 분산 파일 시스템
  - 인스턴스 이름이 'I', 'G', 'H1'으로 시작
  
  
  ### 인스턴스 유형 별 비교 ###
  ![](https://velog.velcdn.com/images/xodbs1123/post/da783cc6-38e2-4e63-8a8c-5b03c9c13ec2/image.png)
- t2.micro에는 vCPU 1개, 1GB의 메모리
- r5.10xlarge에는 vCPU 64개, 512GB 메모리
  - 상대적으로 메모리가 중요함 을 알 수 있음
- cd5.4xlarge에는 vCPU 16개, 32GB 메모리
- 메모리나 CPU 등 네트워크 성능에 따라 EBS 대역폭 등이 달라짐
