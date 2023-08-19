### EC2 절전 모드(Hibernate) ###
- 인스턴스 중지
  - EBS 디스크 데이터는 다시 시작할 때까지 그대로 유지
- 인스턴스 종료
  - 루트 불륨이 삭제되게 했다면 인스턴스도 삭제
  - 그렇게 설정하지 않은 다른 볼륨은 그대로 남음
  - 인스턴스 다시 시작하면 운영 체제 먼저 부팅, EC2 사용자 데이터 스크립트 실행, 그 뒤 애플리케이션 실행, 캐시 구성되는 과정이 오래 걸림
- 인스턴스 절전(Hibernate)
  - RAM에 있던 In-memory는 그대로 보존
    - 루트 경로의 EBS 볼륨에 기록 됨
    - 루트 EBS 볼륨을 암호화 필수, 볼륨 용량도 RAM을 저장하기 충분해야 함
  - 인스턴스 부팅이 더 빨라짐
  - 인스턴스 RAM 크기는 최대 150GB
  - 오래 실행되는 프로세스를 갖고 있고 중지하지 않을 때
  - RAM 상태를 저장하고 싶을 때
  - 빠르게 재부팅을 하고 싶을 때
  - 서비스 초기화가 시간을 많이 잡아먹어 중단 없이 절전 모드로 전환하고 싶을 때
  - 절전 모드는 최대 60일까지 가능( 변경 가능성 있음 )
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/2fbb6e7e-2d8c-417d-b494-1345797b4199/image.png)

### EC2 절전 모드(Hibernate) 실습 ###
- 인스턴스 생성에서 고급 설정 > 최대 절전 중지 방식 > 활성화

![](https://velog.velcdn.com/images/xodbs1123/post/7448cfe1-5ebe-4e8a-a719-8a2ee1c771f3/image.png)

- 충분한 루트 불륨 공간, EBS 볼륨 암호화가 필요하다고 나옴
- 스토리지 구성 > 어드밴스드 > EBS 볼륨 > 암호화됨
- KMS키는 기본값인 awg/ebs 설정
- t2.micro 인스턴스는 1GB 사용하므로 8GB면 충분

![](https://velog.velcdn.com/images/xodbs1123/post/dadec316-2077-46cc-a53a-a01704f3ad26/image.png)

- 절전 모드 생긴 것  확인 가능

![](https://velog.velcdn.com/images/xodbs1123/post/da3c052d-dfd4-4953-8196-b5f023e7a688/image.png)
