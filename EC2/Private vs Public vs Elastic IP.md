# Private vs Public vs Elastic IP

- IPv4 : ex) 1. 160. 10. 240
    - 온라인에서 가장 널리 사용되는 형식
    - 공용 공간에서 37억 개의 서로 다른 주소 허용, 거의 고갈
    - [0-255].[0-255].[0-255].[0-255]
- IPv6 : ex) 3ffe: 1900 : 4545 : 3 : 200 : f8ff : fe21 : 67cf
    - IoT에서 많이 쓰임
    
    ![Untitled](Private%20vs%20Public%20vs%20Elastic%20IP%2045641b6804fb42b9ad49ac814cc457e2/Untitled.png)
    
- 각 서버들은 공용 IP를 통해서 서로 통신(인터넷 전역에 접근 가능)
- 사설 IP는 사설 네트워크 내의 컴퓨터끼리만 통신
- 사설 IP도 공용 게이트웨이인, 인터넷 게이트웨이를 이용하면 다른 서버들에 접근 가능 (AWS의 일반적인 패턴)
- 두 개 이상의 기기가 같은 공용 IP를 가질 수 없음
- 사설 IP는 사설 네트워크 안에서만 유일하면 됨
- 즉, 네이버와 카카오가 같은 사설 IP를 가질 수 있음
- NAT 장치와 프록시 역할을 할 인터넷 게이트웨이를 통해 외부 인터넷 연결
    - 프록시 : 프록시 서버는 클라이언트가 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해 주는 컴퓨터 시스템이나 응용 프로그램
- 사설 IP는 **지정된 범위**의 IP만 지정 가능

- Elastic IP (탄력적 IP)
    - 인스턴스를 시작하고 중지할 때 public IP가 바뀌므로 고정적 IP를 사용하기 위해 탄력적 IP를 사용하는 것
    - 최대 5개만 사용 가능
    - **사용하지 않는 것이 좋음**
    - **대신 임의의(랜덤) 공용 IP를 사용하여 DNS 이름을 할당하는 것이 좋음**
    
    <aside>
    💡 도메인 이름 시스템(DNS)은 사람이 읽을 수 있는 도메인 이름(예: [www.amazon.com](http://www.amazon.com/))을 머신이 읽을 수 있는 IP 주소(예: 192.0.2.44)로 변환
    
    </aside>
    

- 기본적으로 EC2는 내부 AWS 네트워크엔 사설 IP사용
- World Wild Web(WWW) 에서는 공용 IP 사용
- EC2 기기에 SSH 할 때는 사설 IP 사용 불가능
    - VPN을 쓰지 않는 이상 같은 네트워크에 있는 것이 아니기 때문

### 인스턴스 재시작시 Public IP유지하는 방법

1. Elastic IP사용
    - EC2콘솔 → 인스턴스 → Elastic IP
2. Allocate Elastic IP address 누른 후 Allocate

![스크린샷 2024-03-05 오후 9.10.17.png](Private%20vs%20Public%20vs%20Elastic%20IP%2045641b6804fb42b9ad49ac814cc457e2/image1.png)

- Elastic IP는 특정 EC2 인스턴스에 할당되며 연결이 유지되는 한 Elastic IP 유지
- Elastic IP를 갖고있는데 사용하지 않으면 요금이 부과되므로 빠르게 인스턴스에 연결해야 한다.
1. Action → Associate Elastic IP address (탄력적 IP주소 할당)
    
    ![스크린샷 2024-03-05 오후 9.13.44.png](Private%20vs%20Public%20vs%20Elastic%20IP%2045641b6804fb42b9ad49ac814cc457e2/image2.png)
    
2. 인스턴스와 Private IP선택 후 Associate
    
    ![스크린샷 2024-03-05 오후 9.14.24.png](Private%20vs%20Public%20vs%20Elastic%20IP%2045641b6804fb42b9ad49ac814cc457e2/image3.png)

3. 터미널에서 탄력적 IP로 접속 가능해진다.