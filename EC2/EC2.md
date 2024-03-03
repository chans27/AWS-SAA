# EC2

## EC2(Elastic Compute Cloud)

- AWS에서 제공하는 Infrastructure as a Service
- 주요 기능
    - Renting virtual Machine (EC2) - 가상머신을 ec2에서 빌림
    - Storing data on virtual drives (EBS)
    - Distributing load across machine (ELB)
    - Scaling the services using an auto-scaling group (ASG)
- EC2 사용법을 아는 것은 **클라우드 작동 방식을 이해할 때 필수적**
    - 클라우드는 필요할 때마다 가상 공간을 언제든지 활용 가능한데 EC2가 그 예시

**EC2 옵션**

- OS : Windos, Mac OS, **Linux**
- CPU : How much compute power & cores - 이 가상머신에 사용할 컴퓨팅 성능과 코어의 양(CPU갯수)
- RAM : How much random-access memory - 랜덤 액세스 메모리의 양
- Storage space - 네트워크를 통해 연결할 스토리지의 필요여부
    - Network-attached (EBS & EFS)
    - Hardware (EC2 Instance Store)
- Network card : Speed of the card, Public IP address - EC2 인스턴스에 연결할 네트워크의 종류
- Firewall rules : security group
- Bootstrap script (configure at first launch) : EC2 User Data

**EC2 Instance 생성**

1. EC2 > Instances > Launch instances
2. Instance 생성( 이름, OS, 이미지, 인스턴스 유형, 키 페어 등 선택 )
3. 하단에 있는 User data는 EC2를 첫 번째 생성할 때 실행되는 명령어를 입력할 수 있음

![스크린샷 2024-03-03 오후 6.15.41.png](image/image1.png)

1. Summary에서 EC2 스펙 확인
    
![image2.png](image%2Fimage2.png)
    
2. 인스턴스 생성까지 10~15초가 걸린다. (이것이 클라우드의 힘) 즉 서버를 보유하고 있지 않아도 바로 생성 가능하다.

## 인스턴스 정보

![image3.png](image%2Fimage3.png)

- 인스턴스 ID : 고유 식별자
- 퍼블릭 IPv4 : EC2 인스턴스에 접근하기 위해 사용할 주소
- 프라이빗 IPv4 : AWS 네트워크에서 내부적으로 인스턴스에 접근하는 주소

## 인스턴스 실행 및 중지

![image4.png](image%2Fimage4.png)

- 계속 실행하면 지불해야 하는 금액도 증가하므로 미사용시엔 중지할것
- 재실행 시 퍼블릭 IPv4 주소가 변경 됨, 프라이빗은 변경 X

## EC2 인스턴스 타입

- 각 조건에 맞는 EC2 인스턴스 확인 가능
- 각 스펙이나 요금 등을 비교할 수 있음

![image5.png](image%2Fimage5.png)

- AWS 제품 이름 설정 규칙
    - ex) m5.2xlarge
    - m : Instance class (general instance)
    - 5 : Generation
    - exlarge : Instance size, 클수록 인스턴스에 더 많은 메모리와 CPU를 가지게 됨
    
    ## 인스턴스 최적화 유형 (시험 관련)
    
    1. General Purpose (범용 인스턴스)
        - 웹 서버나 코드 저장소와 같은 다양한 작업에 적합
        - 컴퓨팅, 메모리, 네트워킹 간의 **균형이 잘 맞음**
            - ex) t2.micro
    2. Compute Optimized (컴퓨팅 최적화 인스턴스)
        - 컴퓨터 고성능 작업에 적합
        - 데이터 일괄 처리
        - 미디어 트랜스코딩
        - 고성능 웹 서버
        - HPC 작업
        - 머신 러닝
        - 전용 게임 서버 등
        - 인스턴스 이름이 ‘C’로 시작하는 이름을 가짐 ex) C5, C6
    3. Memory Optimized (메모리 최적화 인스턴스)
        - 메모리에서 대규모 데이터 셋을 처리하는 작업에 적합
        - 고성능의 관계형 또는 비관계형 데이터 베이스
        - 분산 웹스케일 캐시 저장소
        - BI (Business Inteligence) 에 최적화된 In-memory 데이터베이스
        - 대규모 비정형 데이터의 실시간 처리를 실행하는 어플리케이션
        - 인스턴스 이름이 주로 RAM을 나타내는 ‘R’로 시작 ex) R6g, R5, R5a
        - 하지만 X1이나 대용량 메모리인 Z1도 있다.
    4. Storage Optimized (스토리지 최적화 인스턴스)
        - 로컬 스토리지에서 대규모 데이터셋에 접근할 때 적합
        - High Frequency Online Transaction Processing(OLTP)시스템
        - 관계형과 비관계형 NoSQL 데이터베이스
        - 메모리 데이터베이스의 캐시 ex) Redis
        - 데이터 웨어하우징 어플리케이션
        - 분산 파일 시스템
        - ~~인스턴스 이름이 ‘I’, ‘G’, ‘H1’으로 시작~~
        
        ## 인스턴스 유형 별 비교
        ![image6.png](image%2Fimage6.png)
        - t2.micro에는 vCPU 1개, 1GB의 메모리
        - r5.10xlarge에는 vCPU 64개, 512GB 메모리
            - 상대적으로 메모리가 중요함 을 알 수 있음
        - cd5.4xlarge에는 vCPU 16개, 32GB 메모리
        - 메모리나 CPU 등 네트워크 성능에 따라 EBS 대역폭 등이 달라짐