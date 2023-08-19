### Elastic Beanstalk ###

![](https://velog.velcdn.com/images/xodbs1123/post/6f4662e8-8902-4b19-982f-0e96a2f6a560/image.png)

- Beanstalk는 AWS에서 애플리케이션을 배포하는 개발자 중심의 관리 서비스
- 단 하나의 인터페이스로 EC2, ASG, ELB, RDS 등의 모든 구성 요소를 재사용하는 것
- 즉, 용량 프로비저닝, 로드 밸런서 구성, 확장, 애플리케이션 상태 모니터링, 인스턴스 구성 등을 처리해줌
- Beanstalk 서비스는 무료, 단 구성 된 ASG와 ELB 등의 비용은 유료
#### Beanstalk 구성 ####
- Application Version
  - 애플리케이션 코드의 반복
- Environment
  - 특정 애플리케이션 버전을 실행하는 리소스의 모음
  - 환경 내에서는 한 번에 하나의 애플리케이션 버전만 존재
  - 환경 내에서 애플리케이션 버전을 업데이트 할 수 있음
  - 웹 서버 환경 티어와 작업자 환경 티어가 있음
  - dev, test, prod 등 다수의 환경을 만들 수 있음

 ![](https://velog.velcdn.com/images/xodbs1123/post/133dd321-8195-4149-8acc-4ef1eea19097/image.png)

- Supported Platforms

   ![](https://velog.velcdn.com/images/xodbs1123/post/f4bde9b8-7a32-452e-837d-10f0584809ab/image.png)

- Web Server Tier vs Worker Tier

![](https://velog.velcdn.com/images/xodbs1123/post/ac1922a8-b189-43db-b060-6541338000d8/image.png)
