### Auto Scaling Group (ASG) ###
- 증가한 로드에 맞춰 EC2 인스턴스 추가 (Scale out)
- 감소한 로드에 맞춰 EC2 인스턴스 제거 (Scale in)
- 따라서 ASG 크기는 시간이 지나면서 변함
- 또한 ASG에서 실행되는 EC2 인스턴스의 최소 및 최대 개수를 설정할 수도 있음
- 로드 밸런서와 페어링하는 경우 ASG에 속한 모든 EC2 인스턴스가 로드 밸런서에 연결 됨

![](https://velog.velcdn.com/images/xodbs1123/post/c3a6c181-d6d0-4bf6-b73a-0cacb63817d2/image.png)

- 한 인스턴스가 비정상이면 종료하고 대체할 새 인스턴스를 생성
- ASG는 무료..!!, EC2 인스턴스와 같은 하위 리소스에 대한 비용만 지불하면 됨

![](https://velog.velcdn.com/images/xodbs1123/post/c083cb21-f88e-49ae-b6d9-05f61d50fee3/image.png)

- Launch Template

![](https://velog.velcdn.com/images/xodbs1123/post/8399028b-2e88-45d9-9312-084fa4dd2477/image.png)

- +Min / Max Size / Initial Capacity
- +Scaling Policies

### CloudWatch Alarms & Scaling ###
- Cloudwatch 경보 기반으로 ASG를 Scale in&out 가능
  - 사용자 정의 지표(Custom Metric)을 통해 경보가 울림
    - 평균 CPU 등을 지표로 설정
    - 경보에 의해 내부적으로 자동적인 스케일링(in&out) 이루어짐

![](https://velog.velcdn.com/images/xodbs1123/post/7b47f02f-868f-4c6e-97ea-e165f8df6593/image.png)

### Auto Scaling Group (ASG) 실습 ###    
1. 모든 인스턴스 종료
2. EC2 > Auto Scaling 그룹 > Auto Scaling 그룹 생성
3. 각 단계별 설정 후 생성

![](https://velog.velcdn.com/images/xodbs1123/post/6a99083e-dfc4-45af-b629-a34b792590ae/image.png)

4. 새로운 인스턴스가 스케일 아웃 (생성) 됨을 확인할 수 있다
   - ASG 생성시 설정 용량에 맞게 생성 됨
 
 ![](https://velog.velcdn.com/images/xodbs1123/post/304a2369-7dcd-4f13-a461-36a9e4a6cda2/image.png)

![](https://velog.velcdn.com/images/xodbs1123/post/964e95e1-7196-4c14-b9bb-7cdcdb66fe11/image.png)

5. Target Group에서 ASG에 의해 생성된 EC2인스턴스가 ALB에 등록되어 있음을 확인 가능

![](https://velog.velcdn.com/images/xodbs1123/post/2254b589-55fb-48f6-9bdf-d9de2625cee6/image.png)

6. 만약 인스턴스가 계속 비정상 상태면 해당 인스턴스 종료 후 새 인스턴스 생성, (생성시 ASG가 비정상 인스턴스 종료하도록 설정했음)
7. 생성후에도 편집을 통해 용량을 조정할 수 있음

![](https://velog.velcdn.com/images/xodbs1123/post/c2955b7c-1d1c-4cf0-a238-052a873c4886/image.png)

### Auto Scaling Group (ASG) 정책 ### 
- Dynamic Scaling Policies
  - Target Tracking Scaling
    - 가장 단순하고 설정하기 쉬움
    - ex) 평균 CPU 사용률 추적하여 40%에 머물수 있게함 
    - 기본 기준선을 세우고 상시 가용이 가능하도록 하는것
  - Simple / Step Scaling
    - CloudWatch 경보를 설정, 한 번에 추가할 유닛의 수와, 제거할 유닛의 수를 단계별 설정 필요
    - ex) 전체 ASG에 대한 CPU 사용률이 70% 초과하는 경우 2개의 유닛을 추가하도록 설정 가능, 그 반대도 가능하다
   - Scheduled Actions
     - 나와 있는 사용 패턴을 바탕으로 스케일링을 예상
     - ex) 금요일 오후 5시 큰 이벤트가 예정되어 있다
       따라서, ASG 최소 용량을 매주 금요일 오후 5시마다 자동으로 10까지 늘리도록 설정하는 것
    - Predictive Scaling
      - load를 보고 다음 스케일링을 예상하는 것
      - 예측을 기반으로 스케일링 작업이 예약됨

![](https://velog.velcdn.com/images/xodbs1123/post/f1573ac0-ca7e-4485-9db4-5d9b14549d28/image.png)

### Good metrics to scale on ###

![](https://velog.velcdn.com/images/xodbs1123/post/504c6290-7b01-49a3-9828-15acace2336b/image.png)

### Scaling Cooldown ###
- 스케일링 작업이 끝날 때 마다 (추가 삭제 상관 없이) Cooldown period를 가짐 ( default 300 seconds )
- cooldown 기간에는 ASG가 추가 인스턴스를 실행 또는 종료할 수 없음
- 스케일링 작업 발생시 기본적으로 설정된 Cooldown이 있는지 확인 필요
### Auto Scaling Group (ASG) 정책 실습 ### 
- 스케일링 종류 3가지 확인

![](https://velog.velcdn.com/images/xodbs1123/post/2e83d9b9-9d9e-46d6-98ec-6afecbb0b6ee/image.png)

- Scheduled Actions

![](https://velog.velcdn.com/images/xodbs1123/post/c46241e3-d6eb-4ae3-a722-50bfea2cdd5d/image.png)
- Predictive Scaling
  - 머신러닝 기반 스케일링

![](https://velog.velcdn.com/images/xodbs1123/post/806ff42d-bd24-4da4-8477-4af9e26a3364/image.png)
  
  - 지표 선택 종류
 
  ![](https://velog.velcdn.com/images/xodbs1123/post/c330e7cf-375b-47c3-b880-89e631df0828/image.png)

- Dynamic Scaling Policies

![](https://velog.velcdn.com/images/xodbs1123/post/0e942635-2a57-468d-8e3c-78184321382c/image.png)
  
  - Target Tracking Policy 생성한 모습
 
 ![](https://velog.velcdn.com/images/xodbs1123/post/a9ff9ef4-63c9-47ad-8b17-e523bcb707e8/image.png)
-------------
- CPU 사용률 100% 되도록 Stress 주어 스케일링 작동 상태 확인
1. Google에 'install stress Amazon Linux2' 입력
2. 깃헙에 들어가 두 번째 명령 복사해서 인스턴스에 입력, stress 설치 (2023 ver 부터는 두 번째 명령만 설치하면 됨)
  - ' sudo yum install stress -y '

![](https://velog.velcdn.com/images/xodbs1123/post/ca7c24e7-c61f-4171-8338-39f630538026/image.png)

3. ' stress -c 4 ' 명령 실행으로 4개의 vCPU 사용하게끔 동작 (사용률 100 %)

![](https://velog.velcdn.com/images/xodbs1123/post/b10bc111-3469-4351-8a64-fb4754b8e9f0/image.png)

4. 경보 발생 확인

![](https://velog.velcdn.com/images/xodbs1123/post/b46e6fc5-40ac-4cf7-b03d-349d49d2461e/image.png)

5. Target Tracking Policy에 따른 추가 인스턴스 생성 확인

![](https://velog.velcdn.com/images/xodbs1123/post/8eb27080-e22f-4dc1-9adf-245fa19efdd5/image.png)
6. CloudWatch > 경보에서 동작 상태 확인 가능
7. 인스턴스 재부팅 후(CPU 동작 정상화) 인스턴스 삭제 되는 모습

![](https://velog.velcdn.com/images/xodbs1123/post/fa93352a-1b4a-475a-8dd2-bd987a733615/image.png)
