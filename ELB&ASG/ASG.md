# ASG (Auto Scailing Group)

- 증가한 로드에 맞춰 EC2 인스턴스 추가 (Scale out)
- 감소한 로드에 맞춰 EC2 인스턴스 제거 (Scale in)
- 따라서 ASG 크기는 시간이 지나면서 변함
- 또한 ASG에서 실행되는 EC2 인스턴스의 최소 및 최대 개수를 설정할 수도 있음
- 로드 밸런서와 페어링하는 경우 ASG에 속한 모든 EC2 인스턴스가 로드 밸런서에 연결 됨

- 한 인스턴스가 비정상이면 종료하고 대체할 새 인스턴스를 생성
- ASG는 무료, EC2 인스턴스와 같은 하위 리소스에 대한 비용만 지불하면 됨

- Launch Template

- +Min / Max Size / Initial Capacity
- +Scaling Policies

**CloudWatch Alarms & Scaling**

- Cloudwatch 경보 기반으로 ASG를 Scale in&out 가능
    - 사용자 정의 지표(Custom Metric)을 통해 경보가 울림
        - 평균 CPU 등을 지표로 설정
        - **경보에 의해 내부적으로 자동적인 스케일링(in&out) 이루어짐**

**Auto Scaling Group (ASG) 정책**

- Dynamic Scaling Policies
    - Target Tracking Scaling
        - 가장 단순하고 설정하기 쉬움
        - ex) 평균 CPU 사용률 추적하여 40%에 머물수 있게함
        - 기본 기준선을 세우고 상시 가용이 가능하도록 하는것
    - Simple / Step Scaling
        - CloudWatch 경보를 설정, 한 번에 추가할 유닛의 수와, 제거할 유닛의 수를 단계별 설정 필요
        - ex) 전체 ASG에 대한 CPU 사용률이 70% 초과하는 경우 2개의 유닛을 추가하도록 설정 가능, 그 반대도 가능
    - Scheduled Actions
        - 나와 있는 사용 패턴을 바탕으로 스케일링을 예상
        - ex) 금요일 오후 5시 큰 이벤트가 예정되어 있다 따라서, ASG 최소 용량을 매주 금요일 오후 5시마다 자동으로 10까지 늘리도록 설정하는 것
    - Predictive Scaling
        - load를 보고 다음 스케일링을 예상하는 것
        - 예측을 기반으로 스케일링 작업이 예약됨

**Scaling Cooldown**
- 스케일링 작업이 끝날 때 마다 (추가 삭제 상관 없이) Cooldown period를 가짐 (default 300 seconds)
- cooldown 기간에는 ASG가 추가 인스턴스를 실행 또는 종료할 수 없음
- 스케일링 작업 발생시 기본적으로 설정된 Cooldown이 있는지 확인 필요