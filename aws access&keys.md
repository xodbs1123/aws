### AWS 엑세스 방법 ###
1. AWS Management Console (protected by password + MFA)
   - 비밀번호 정책
2. AWS Command Line Interface(CLI) : protected by access keys
   - Access keys : 터미널에서 AWS 엑세스를 가능하도록 해주는 키
3. AWS Software Developer Kit(SDK) : for code : protected by access keys
   - AWS로부터 애플리케이션 코드 내에서 API 호출하고자 할 때 사용하는 방식

- Access keys
  - 비밀번호와 마찬가지로 암호
  - 본인의 Access keys 생성 후 공유 X
  - Access keys ID : 사용자 이름
  - Secret Access Keys : 비밀번호
  

- CLI(Command Line Interface)
   - 명령줄 인터페이스
   - 명령줄 셸에서 명령어를 사용하여 AWS 서비스들과 상호작용할 수 있도록 도와줌
   ![](https://velog.velcdn.com/images/xodbs1123/post/ad38de89-4082-471c-ac4c-e5d5b9ba4f1a/image.png)
  - AWS 서비스의 공용 API로 직접 엑세스 가능 
  - 리소스를 관리하는 스크립트 개발하여 일부 작업 자동화 가능
  - 오픈소스, GitHub에서 모든 소스 코드 찾을 수 있음
  - AWS 관리 콘솔 대신 사용되기도 함
  

- SDK(Software Development Kit) 
  - 특정 언어로 된 라이브러리 집합
  - 프로그래밍 언어에 따라 개별 SDK 존재
  - AWS 서비스의 공용 API로 직접 엑세스 가능 
  - 코딩을 통해 애플리케이션 내에 적용하는 것
  - JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++ 등을 지원
  - 안드로이드나 iOS를 쓰면 모바일 SDK도 사용 가능
  - IoT SDK 장치도 지원

### Windows에서 AWS CLI 설정 ###
1. AWS CLI install windows를 Google에 검색
2. version2(최신) 설치 페이지 접속 후 msi 다운로드 및 실행
![](https://velog.velcdn.com/images/xodbs1123/post/cec9af1b-a823-4f34-880a-cb88d1c7cb36/image.png)
3. 명령 프롬프트 실행
4. aws --version 명령어로 정상 설치 확인
![](https://velog.velcdn.com/images/xodbs1123/post/475c2b2a-f41a-433b-91e0-8525d9a08061/image.png)
		
        정상 설치 시, aws-cli/2.0.30 Python/3.7.7 Windows/10 botocore/2.0.0dev34
 
5. CLI 업그레이드 시 설치 페이지에서 재설치하면 됨
6. Mac Os 및 Linux에서 CLI 설치 방법은 상이


### Access keys 생성 방법 ###
1. 루트 계정이 아닌 사용자 계정으로 로그인
2. Users에서 해당 사용자 클릭
3. Security credentials(보안 자격 증명) 클릭
4. Access Keys 만들기 클릭
![](https://velog.velcdn.com/images/xodbs1123/post/4af26adc-e011-42f6-ab1e-ffb7f2124205/image.png)
5. CLI 사용 클릭
![](https://velog.velcdn.com/images/xodbs1123/post/b60e087b-914f-4241-a801-065d05d94668/image.png)
6. Access Keys는 기밀, 오직 생성 시에만 표시 및 다운로드 가능
7. 컴퓨터 보관용으로 .csv 파일 다운로드 가능


### Access Keys 구성 방법 ###
1. 명령 프롬프트 실행
2. aws configure 입력
3. 엑세스 키 ID 입력
4. 엑세스 암호 키 입력
5. 가까운 리전(서울, ap-northeast-2) 입력
6. 기본 출력 포맷 엔터(Enter) 입력

![](https://velog.velcdn.com/images/xodbs1123/post/756ba4f8-0a86-42b8-8788-c09e5c5f2469/image.png)

#### CLI 작동 확인 ####
- 계정 모든 사용자 목록 확인**(명령어 : aws iam list-users)**
![](https://velog.velcdn.com/images/xodbs1123/post/ae411921-c120-4dcc-ad50-d6795f26cec9/image.png)
   - 'xodbs1123' 이라는 유저 확인 가능
   - 콘솔 UI와 표시되는 내용이 비슷
   - CLI 권한은 IAM 콘솔과 같은 권한
