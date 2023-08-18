### windows 활용 EC2 인스턴스에 SSH ###
- SSH
  - 명령줄로 원격 머신을 제어할 수 있게 해주는 것
1. Window PowerShell or 명령 프롬프트에 'ssh' 입력
![](https://velog.velcdn.com/images/xodbs1123/post/d790c466-a0a9-4a45-b89f-ec148575b1bd/image.png)
2. EC2Tutorial.pem이 있는 디렉토리로 변경
   - 내 PC 기준 : cd .\desktop\AWS_SAA
![](https://velog.velcdn.com/images/xodbs1123/post/b257a513-b39b-427a-9afc-a28be138c5e9/image.png)

3. 보안 그룹에서 포트 22가 SSH에 대해 열려 있는지 확인
4. SSH 명령 입력
   -  ssh -i '.\EC2 Tutorial.pem' ec2-user@공용 IP
      - ec2-user라는 사용자를 허용 
      - EC2 Tutorial이라는 키를 사용
5. 호스트를 신뢰할 수없음, 계속 할 것인지? 'Yes'
6. 만약 권한 문제가 발생하면 키 권한 변경해야함
 - pem 키 파일 우클릭
 - 속성
 - 보안 탭

 - 권한 변경

    ![](https://velog.velcdn.com/images/xodbs1123/post/4880feb5-711c-4a37-a56e-292d113b8896/image.png)

 - 모든 상속된 권한 제거

 - 추가 > 보안 주체 선택 

![](https://velog.velcdn.com/images/xodbs1123/post/0550a3e0-83d1-4cb6-992b-69c2988e93e0/image.png)

- User name 입력 후 이름 확인

- 모든 권한 부여

![](https://velog.velcdn.com/images/xodbs1123/post/a192a982-4945-4944-94a9-b5199ea3ca2a/image.png)

- 보안 주체가 본인이 되어있음을 확인, 모든 권한 확인

![](https://velog.velcdn.com/images/xodbs1123/post/5cf1c42b-926b-4703-9d35-5a0953d336fd/image.png)

7. 다시 SSH 명령 입력

![](https://velog.velcdn.com/images/xodbs1123/post/4d69cf15-eba8-497b-bf4a-4eccbc067772/image.png)


### EC2 인스턴스 커넥트 ###
- 브라우저 기반으로 EC2 인스턴스에 대한 SSH 세션을 실행 가능
- 보이지 않는 부분에서 SSH에 의존하고 있음
- 인바운드 규칙에서 SSH 삭제하면 접속 안됨
1. 인스턴스 콘솔에서 연결( Connect) 클릭
![](https://velog.velcdn.com/images/xodbs1123/post/62445f8c-23ea-4a4d-8d83-52b33116ac4f/image.png)
2. 공용 IP, User name 확인
   - 'ec2-user'은 AWS에서 지정한 것, 변경하면 작동 안함
   - SSH 키 입력 안해도 자동으로 업로드해서 접속 가능
![](https://velog.velcdn.com/images/xodbs1123/post/99dbb6e9-8c50-476b-b262-fa6f9288d764/image.png) 
3. 연결 시 Amazon Linux2 AMI로 접속
   - 'whoami' or 'ping google.com' 명령어 실행 가능
   ![](https://velog.velcdn.com/images/xodbs1123/post/10d6a8c7-73da-4075-b619-6248e3dc518d/image.png)

### EC2 인스턴스를 위한 IAM 역할 ###
1. EC2 인스턴스에 연결
   - Amazon Linux AMI는 AWS CLI를 포함하고 있음
   - 'aws configure' 명령을 통해 EC 인스턴스에 상세 개인 정보( 엑세스 키 ID, PW 등) 입력하는 것은 좋지 않음
   - 해당 계정 사용자들이 EC2 인스턴스 커넥트를 통해 해당 정보를 확인할 수 잇기 때문
   - 대신 사용할 수 있는게 IAM
   ![](https://velog.velcdn.com/images/xodbs1123/post/41975703-c72b-42ef-92b0-6345ba74cfd7/image.png)
2. EC2 콘솔 > instance > Action > Security > Modify IAM role

![](https://velog.velcdn.com/images/xodbs1123/post/18375a7f-89fa-43ef-99a6-28c2b9f68e55/image.png)

3. 역할 선택 후 업데이트

![](https://velog.velcdn.com/images/xodbs1123/post/b17767d0-ccd7-4d6f-a7bc-9c0fbfd85191/image.png)

4. EC2 인스턴스에 'aws iam list-users' 입력
   - User에 관한 정보를 확인할 수 있음

 ![](https://velog.velcdn.com/images/xodbs1123/post/3f503970-e3a2-4fc3-a215-8849e656b5b3/image.png)

### EC2 인스턴스 구매 옵션 ###
- EC2 On Demend
  - 필요한 대로 인스턴스 실행 가능
  - 단기적인 워크로드에 사용하기 좋음
  - 사용한 대로 지불
  - 비용이 가장 많이 들지만 바로 지불하는 것이 아님
  - 중단 없는 워크로드가 필요할 때, 애플리케이션의 작동 상황을 에상할 수 없을 때  

- EC2 Reserved Instances( 1 & 3 )
  - 장기간 데이터베이스를 실행할 계획이라면 좋음
  - 온디맨드에 비해 약 70% 할인 제공
  - 인스턴스 타입, Region, Tenancy, OS 등을 예약
  - 부분 선결제 or 선셜제
  - 사용량이 일정한 애플리케이션 ( database ) 등에 사용
  - 마켓플레이스에서 사고 팔 수 있음
	
- 전환형 예약 인스턴스 
  - 인스턴스 타입, 인스턴스 패밀리, OS, 범위, Tenancy 변경 가능
  - 유연성이 크므로 할인이 적음, 최대 66%
  
- Saving Plans ( 1 & 3 )
  - 장기간 워크로드를 위한 것
  - 70% 할인 가능
  - 사용량이 한도를 넘어가면 온디맨드 가격으로 청구
  - 특정한 인스턴스와 패밀리, Region으로 고정
    - ex) M5 타입의 인스턴스 패밀리, us-east-1을 원한다면 인스턴스 사이즈는 유연하기 때문에 m5.xlarge, m5.2xlarge 등을 선택 가능
    	OS는 Linux나 Windows 등으로 전환 가능

- Spot Instance
  - 아주 짧고 저렴함, 하지만 인스턴스 손실 가능성이 있어 신뢰성이 낮음
  - 온디맨드에 비해 최대 90%까지 할인 가능
  - 지불하려는 최대 가격을 정의, 만약 그 가격을 넘어가게 되면 인스턴스 손실
  - 배치 작업
  - 데이터 분석
  - 이미지 처리
  - 분산형 워크로드
  - 시작과 종료 시간이 유연한 워크로드
  - 중요한 작업이나 데이터베이스에는 적절하지 않음 (시험에 출제)
  - 스팟 요청을 취소 후, 스팟 인스턴스 종료해야 함
  - 스팟 플릿, 한 세트의 스팟 인스턴스에 온디맨드 인스턴스를 조합해 사용하는 방식
    - LowestPrice, Diversfiled, CapacityOptimized
    -  사용하고자 하는 인스턴스의 유형과 가용 영역을 지정해서 		하게 되는 단순한 스팟 인스턴스 요청과 달리 
     - 스팟 플릿은 여러분의 요구 예를 들면 최저가의 선택 등등의 조건에 따라 인스턴스의 유형과 가용 영역을 선택하도록 한다는 데서 서로 차이가 있음

- Dedicated Host
  - 물리적 서버 전체를 예약, 인스턴스 배치를 제어 가능
  - 낮은 수준의 하드웨어까지 접근 가능
  - 실제 물리적 서버를 예약하므로 AWS에서 가장 비쌈
  - BYOL( Bring Your Own License )인 경우
  - 규정이나 법규를 준수해야하는 회사인 경우
 - Dedicated Instances
   - 다른 계정과 하드웨어를 공유하지 않는 것
   - 사용자 전용 하드웨어에서 실행되는 인스턴스
   - 같은 계정에서 다른 인스턴스와 함께 하드웨어 공유 가능
   - 인스턴스 배치에 대한 통제권이 없음
 
 - Capacity Reservations 
   - 원하는 기간 동안 특정한 AZ에 용량을 예약할 수 있음
   - 언제든 용량을 예약하고 취소할 수 있음
   - 용량을 예약하는 게 유일한 목적
   
   
   ### 상황에 맞는 EC2 인스턴스 구매 요약 ###
   
	첫 번째, 온디맨드
	리조트에 비유해보자
	온디맨드인 경우에 여러분은 리조트가 있고, 원할 때 언제나 리조트에 오고 전체 가격을 지불

	두 번째, 예약 인스턴스
	여러분은 미리 계획을 하고 그 리조트에
	아주 오래 체류할 것이라는 걸 알고 있다, 1년 내지 3년
	여러분은 오래 체류할 것이기 때문에 많은 할인을 받게 될 겁니다

	세 번째, 절약 플랜은 리조트에서 일정한 금액을 지출할 것임을 알고 있다고 말하는 것과 같다
	다음 12개월 동안에 매월 300달러를 지출할 예정
	그래서 여러분은 시간이 지나면 객실 타입을 변경 할 수 있다
	킹, 스위트, 바다 뷰 등을 변경할 수 있죠
	하지만 절약 플랜은 호텔에서 특정한 지출액을 약정하라고 말하게 되죠

	네 번째, 스폿 인스턴스는 빈 객실이 있고 사람들을 끌어 모으기 위해 
  	호텔이 마지막 할인을 제공하는 경우
  	빈 객실이 있고 사람들이 그 빈 객실을 얻기 위해 경매
  	그래서 아주 많은 할인을 얻게 됩니다
  	하지만 이 리조트에서 만일 다른 사람이 여러분보다 객실 요금을 더 많이 낼 의사가 있다면
	여러분은 언제라도 쫓겨 나갈 수 있다

	다섯 번째, 전용 호스트는 마치 리조트 건물 전체를 예약하려는 것과 같습니다
	그럼 여러분은 자신만의 하드웨어, 자신만의 리조트를 받게 된다
    
	여섯 번째, 용량 예약은 말하자면 객실을 예약할 건데
  	내가 체류할지 확실치 않다고 말하는 것과 같습니다
	체류할 수도 있겠지만, 체류하지 않는 경우에도
  	그 객실을 예약하는 전체 비용을 지불하게 됩니다

![](https://velog.velcdn.com/images/xodbs1123/post/6b3a4bc3-e0d4-471b-a68e-00c88079aae3/image.png)

- 시험에는 워크로드에 적합한 게 어떤 타입의 인스턴스인지 물어본다!!!

### 스폿 요청 ###
- EC2 콘솔 > Spot Requests > Spot Instance pricing histor에서 요금 확인 가능

![](https://velog.velcdn.com/images/xodbs1123/post/014ecabe-043a-4eb5-8e85-161f25bead1f/image.png)

1. Request Spot Instance
2. 각종 옵션 선택 후 요청

![](https://velog.velcdn.com/images/xodbs1123/post/17704ef3-1ecf-4927-877c-bed8dc71c8d0/image.png)

- 바로 스폿 인스턴스 생성 방법
  - Instances > Launch instances > Advanced details에서 스폿 인스턴스 요청 옵션 클릭
  
 - 그외 인스턴스 옵션

 ![](https://velog.velcdn.com/images/xodbs1123/post/fcc88414-d761-4935-9ddc-fa3b968ee890/image.png)

