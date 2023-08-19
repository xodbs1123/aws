### IAM(Identity and Access Management) ###
- 사용자를 생성하고 그룹에 배치하는 것
- 글로벌 서비스에 해당(모든 리전에 제공하는 서비스)
- 계정은 루트 계정으로 본인만 사용 가능
- 대신, 사용자를 추가하여 그룹 생성 가능
- 그룹에는 사용자만 배치할 수 있음
- 한 사용자가 여러 그룹에 속할 수 있음
- 루트 계정에 대한 특정 권한 부여를 위해 사용자와 그룹을 생성하는 것


### IAM 사용자 생성 ###
1. IAM 검색
2. Users 항목에서 ADD Users 선택
![](https://velog.velcdn.com/images/xodbs1123/post/4c5b36f2-4327-4dd2-8368-8464f7d098c9/image.png)
   - 보안 상의 이유로, 관리자 계정을 생성하여 되도록 루트 계정은 사용 안하는 것이 좋음
   
   

3. 사용자 정보 및 권한 설정
![](https://velog.velcdn.com/images/xodbs1123/post/7849c041-4a2e-4083-a42d-491034e4f23c/image.png)
4. 그룹 생성 및 그룹 권한(관리자 권한) 생성
![](https://velog.velcdn.com/images/xodbs1123/post/37098199-5569-422d-a0dd-7b55e7e0e7f3/image.png)
5. 계정 고유 별칭 생성
![](https://velog.velcdn.com/images/xodbs1123/post/db8a0e7f-1050-4b21-85b8-67e4ff6d47e9/image.png)
6. 생성 된 링크로 접속하여 IAM 사용자 계정으로 로그인
![](https://velog.velcdn.com/images/xodbs1123/post/28aeebc5-f895-457d-85fb-2495085ac382/image.png)


### IAM 정책 ###
![](https://velog.velcdn.com/images/xodbs1123/post/50c36212-3666-4f4c-86df-f7f41b1943d0/image.png)
- 각 그룹은 각자의 권한을 받음
- Fred와 같이 그룹이 없는 사용자는 인라인 권한을 생상할 수 있음
- 두 그룹에 속하여 각 권한을 적용받을 수 있음

### IAM 정책 구조 ###
![](https://velog.velcdn.com/images/xodbs1123/post/ae26bf18-8c15-4fdd-b18e-23b45a602948/image.png)

- Version : 정책 언어 버전 ( 문장의 일부 아님 )
- Id : 정책을 식별하는 ID, 선택 사항( 문장의 일부 아님 )
- Sid(시드) : 문장 ID로 식별자, 선택 사항
- **Effect(효과)** : 명시된 정책에 대한 허용 혹은 차단
- **Principal(원칙)** : 접근을 허용 혹은 차단하고자 하는 대상
- **Action(조치)** : 허용 혹은 차단하고자 하는 접근 타입
- **Resource(리소스)** : 요청의 목적지가 되는 서비스, 적용될 Action의 리소스의 목록
- Condition(조건) : 명시된 조건, 유효하다고 판단될 수 있는 조건, 정책이 언제 적용될지 결정함

#### 시험 대비 ####
- Effect, Principal, Action, Reosurce 개념은 확실히 이해하자

### IAM 그룹에서 사용자 삭제 ###
1. User Group에 들어간다(잘못봐서 user에서 삭제하면 다시 생성해야한다..)
2. 사용자 선택후 삭제!!
![](https://velog.velcdn.com/images/xodbs1123/post/1a40e581-3a0a-4676-ba4f-02e5c7a00068/image.png)

### IAM 그룹에서 사용자 재추가 ###
1. User에 들어가 다시 권한을 직접 연결한다
    - 권한을 부여하고 나서 새로 정책 생성 혹은 기존 정책을 이용
    - 인라인 정책을 추가해 권한을 사용자에게 직접 연결
  ![](https://velog.velcdn.com/images/xodbs1123/post/6416caf5-7040-4da3-88ee-d49775d92dc0/image.png)
	
  
#### 기존 정책을 바로 연결하는 방법 ####
![](https://velog.velcdn.com/images/xodbs1123/post/e7a78f8c-4b3b-46d7-b720-59c6508da250/image.png)

1. 권한 추가 클릭
2. 직접 정책 연결 클릭
3. IAM으로 검색 후 'IAMReadOnlyAccess' 클릭 후 권한 부여
4. 읽기 전용 권한만 부여했으므로 생성 권한은 없음

- 그룹에 여러개 속해있으면 각 그룹에서 어떤 권한을 받는 지 확인할 수 있음
![](https://velog.velcdn.com/images/xodbs1123/post/a1a68bb9-6505-4077-8649-f469cc3eeea2/image.png)


### 정책 생성 방법 ###
1. 정책 → 정책 생성 클릭
![](https://velog.velcdn.com/images/xodbs1123/post/e7dedac1-8282-48e2-bc7a-a93a455e4932/image.png)
2. Visual Editor 혹은 Json 방법으로 생성
![](https://velog.velcdn.com/images/xodbs1123/post/dbc48ed8-2b05-4cb1-afbd-8cc602ac3eda/image.png)

   - Visual Editor에서 정책 설정한 모습
   ![](https://velog.velcdn.com/images/xodbs1123/post/55f4489a-a42d-4259-b5f3-dd24f062564f/image.png)

   - Json에 적용 된 모습

  ![](https://velog.velcdn.com/images/xodbs1123/post/3aca4f2b-55e0-474a-be63-df7ecd8a0208/image.png)

- 그룹 제거는 User Groups에서 제거 할 그룹 선택, 그룹명 입력 후 제거
- 사용자 정책 제거는 Users에서 사용자 클릭, 삭제할 정책 클릭 후 삭제

## IAM 방어 매커니즘 ##
- 비밀번호 정책(최소 길이, 특정 유형, 일정 주기 변경 등)
- **MFA(다요소 인증)**  → 시험을 위해 숙지!!
  - 비밀번호와 보안 장치를 함께 사용하는 것
 - **MFA 장치 종류**
   - Virtual MFA device
     - Google Authenticator(Phone Only)
     - Authy(Multi-device), 컴퓨터와 핸드폰에서 같이 사용 가능
     - 원하는 수만큼의 계정 및 사용자 등록 가능
     
   - Universal 2nd Factor (U2F) Security Key
     - Yubico사의 YubiKey가 있음, AWS의 제3자회사
     - 물리적 장치
     - 하나의 보안 킨에서 여러 루트 계정과 IAM 사용자를 지원
   - Hardware Key Fob MFA Device
     - Gemalto의 제품, AWS의 제3자회사
   - Hardware Key Fob MFA Device for AWS GovCloud(US)
     - 미국 정부 클라우드인 AWS GovCloud 사용하는 경우 필요
     - SurePassID의 제품, AWS의 제3자회사
     

### IAM MFA 실습 ###
- 비밀번호 정책 변경
  - IAM > 계정 설정 > 암호 정책 편집 > 사용자 지정
- 루트 계정에 MFA 설정
	
	
1. 계정 이름 클릭 > 보안 자격 증명 클릭(My Security Credentials)
       
![](https://velog.velcdn.com/images/xodbs1123/post/0bb0744c-9284-47a0-ace8-337c538398a9/image.png)

2. MFA 활성화

![](https://velog.velcdn.com/images/xodbs1123/post/7791d4ec-99cc-4245-a1fe-2121e286a021/image.png)

3. Device 선택

![](https://velog.velcdn.com/images/xodbs1123/post/97fc7ef7-9e38-43a4-8f99-c6d784060e92/image.png)
	
4. 호환되는 애플리케이션 설치 ex) Authy
5. Authy 어플의 Add Account에 들어가서 QR 코드 스캔
6. 계정의 닉네임과 로고 선택 후 Save
7. MFA 코드1 확인 후 입력, 15초 후 MFA 코드2 확인 후 입력
8. MFA 추가 클릭

![](https://velog.velcdn.com/images/xodbs1123/post/e93e782f-a316-4d99-b8f1-6937206e2d20/image.png)


### IAM Role ###
- 일부 AWS 서비스를 사용하기 위해서는 루트 계정 활용
- 이때, IAM Role을 생성하여 권한을 부여 받아야함
   - ex) 'EC2' 가상 서버를 만들어 AWS에서 특정 작업을 수행 가능
      그러기 위해서는 ECE Instance에 권한을 부여해야 함
      이를 위해 IAM Role을 만들어 하나의 개채로 만들어 AWS에 특정 정보에 접근 가능하도록 함
  ![](https://velog.velcdn.com/images/xodbs1123/post/c339fc15-bf15-4350-8ea3-eb52d54f86d4/image.png)
- ' EC2 Instance Roles ',  ' Lambda Function Roles ',  ' Roles for CloudFormation ' 등 여러 Role이 존재      


### Role 생성 ###
1.  Access management > Roels > Create role
2. Trusted entity type과 Use case 선택 
   - 시험은 AWS service 관련해서만 나옴
   ![](https://velog.velcdn.com/images/xodbs1123/post/3bf02f2d-77b9-4482-8a85-5a8d1bdf79c7/image.png)
3. 권한 추가
4. Role 이름 설정
	                  
### IAM Security Tools ###
- IAM Credentials Report (루트 계정 수준에서 가능)
  - 사용자와 다양한 Credentials 포함
- IAM Access Advisor (사용자 계정 수준 가능)
  - 사용자에게 부여된 서비스 권한과 마지막으로 Access한 시간이 보임
  
  
### Credential report ###
- IAM > Access reports > Credential report > Download Report
- 어떤 사용자가 비밀번호를 변경하지 않았는지, 계정을 사용하는지 등 파악할 때 유용
- 보안 측면에서 어떤 사용자를 주목해야 하는지 발견하는 데 도움이 된다
![](https://velog.velcdn.com/images/xodbs1123/post/5435cb48-ab61-437a-b5dd-0b1179133b63/image.png)


### IAM Access Advisor ###
- IAM > Users > User name > Acces Advisor
- 보통 최근 4시간 동안의 활동 내역을 보여줌
- 사용하지 않는 권한들을 확인 후 삭제할 때 도움이 됨
![](https://velog.velcdn.com/images/xodbs1123/post/df3c70bc-3d08-497f-be4c-a4b00401db85/image.png)

  
