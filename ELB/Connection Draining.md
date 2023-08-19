### Connection Draining (시험 출제 !! ) ###
- Deregistration Delay - for ALB & NLB
- 인스턴스가 등록 취소, 혹은 비정상 상태에 있을 때 인스턴스에 어느 정도의 시간을 주어 활성 요청( in-flight requests )를 완료할 수 있도록 하는 기능
- Connection Draining되면 ELB는 등록 취소 중인 EC2 인스턴스로 새로운 요청을 보내지 않음

![](https://velog.velcdn.com/images/xodbs1123/post/8c7b5568-c25a-4e29-9634-f478dd1c0ca8/image.png)

- Connection Draining 파라미터는 매개변수로 표시 가능
  - 1 to 3600 second (default : 300 seconds )
  - 이 값을 0으로 설정하면 비활성화
  - 짧은 요청의 경우 낮은 값으로 설정하면 좋음
  - 그래야 EC2 인스턴스가 빠르게 드레이닝되고, 오프라인 상태가 되어 교체 작업을 할 수 있음
