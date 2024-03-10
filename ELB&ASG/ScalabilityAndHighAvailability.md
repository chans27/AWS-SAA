- Scalability (확장성)
    - 애플리케이션 시스템이 조정을 통해 더 많은 양의 데이터를 처리할 수 있는 것
    - 수직 확장성
        - **인스턴스의 크기를 확장**하는 것
        - 데이터베이스와 같이 분산되지 않은 시스템에 사용
        - RDS나 ElastiCache 등의 하위 인스턴스의 유형을 업그레이드해 수직적으로 확장할 수 있는 시스템들에 사용
        - 확장의 한계가 있고 하드웨어 제한이 있음
    - 수평 확장성
        - 애플리케이션에서 **인스턴스나 시스템의 수를 늘리는 것**
        - 스케일 아웃 ( 인스턴스의 수가 늘어나는 것 )
        - 스케일 인 ( 인스턴스의 수가 줄어드는 것 )
- High Availabilty (고가용성)
    - 시스템을 **둘 이상의 AWS의 AZ나 데이터센터에서 가동**하는 것
    - 고가용성의 목표는 데이터 센터에서의 손실에서 살아남는것으로 센터 하나가 멈춰도 계속 작동이 가능하게끔 하는것
    - 다중 AZ가 활성화된 자동 스케일러 그룹이나 로드 밸런서에도 사용