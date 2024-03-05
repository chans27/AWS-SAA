# IAM | Users & Groups

## IAM : Identity and Access Management

- 디폴트로 루트계정이 생성되며 사용되거나 공유되면 안된다. (오직 계정을 생성할 때만 사용되어야 한다.)
- Users는 조직 내의 사람들이며 그룹화 될 수 있다.
- 한 사용자가 여러 그룹에 속할 수 있다.
- IAM users는 자신만의 자격 증명(사용자 이름 & 비밀번호, 혹은 액세스 키)을 통해 AWS 서비스에 액세스합니다.
- IAM User groups는 IAM user만 포함시킬 수 있다.
- IAM User를 작성한 직후엔, 아무런 권한도 갖고있지 않다. IAM 정책을 통해 권한을 부여할 필요가 있다.

### 사용자와 그룹을 생성하는 이유

- AWS 계정을 사용하도록 허용하기 위해.
- AWS계정사용의 허용을 위해서는 권한을 부여해야 한다.
- 이를 위해 사용자 또는 그룹에게 IAM정책이라 불리는 JSON문서를 지정할 수 있다.

## IAM 정책 (JSON)

![Untitled](IAM%20Users%20&%20Groups%205ec096f3f65b4a70991fb88d66b1ef1f/Untitled.png)

1. id : 정책을 식별하기 위한 ID (선택)
2. statement : 정책 요소의 컨테이너 역할을 한다. 단일 문 또는 개별 문의 배열을 포함할 수 있다. (필수)
- Sid : (statement id) : 설명문(statement)의 id (선 택)
- **Effect** : Statement가 특정 API에 대한 접근을 허용할지 거부할지를 정한다. (**필수**)
- **Principal** : 특정 정책이 적용될 보안 주체(사용제, 계정, 혹은 역할로 구성된다)를 지정한다. 강의에선 AWS 계정의 루트계정이 적용된다.
- **Action** : effect에 기반해 허용 및 거부된 API 호출의 목록
- **Resource** : IAM권한 정책을 생성하는 경우 작업이 적용될 action의 리소스의 목록
- Condition : Statement가 언제 적용될지를 결정 (선택)

## IAM Password Policy

- 비밀번호 정책(최소길이, 특정유형, 일정 주기 변경 등)
- MFA(Multi Factor Authentication) - 비밀번호와 보안장치를 함께 사용
- MFA 장치 종류
    1. Virtual MFA device
    - Google Authenticator (phone only)
    - Authy(Multi Device) 컴퓨터와 핸드폰에서 같이 사용 가능
    - 원하는 수만큼의 계정 및 사용자 등록 가능
    1. Universal 2nd Factor (U2F) Security Key
    - Yubico사의 YubiKey (AWS의 서드파티 회사)
    - 물리적인 장치
    - 하나의 보안키에서 여러 루트 계정과 IAM 사용자 지원
    1. Hardware Key Fob MFA Device
    - Gemelto의제품 (AWS의 서드파티 회사)
    1. Hardware Key Fob MFA Device for AWS GovCloud(US)
    - 미국 정부 클라우드인 AWS GovCloud 사용하는 경우 필요
    - SurePassID의 제품 (AWS의 서드파티 회사)
    

## AWS에 액세스하는 방법들

1. 관리 콘솔을 통해 액세스 (protected by password + MFA)
2. CLI을 통해 액세스 (protected by access keys) - 터미널에서의 AWS액세스를 가능하게 한다
3. SDK(Software Developer Kit)을 통한 액세스 (for code:protected by access keys)
- access key는 관리 콘솔을 통해 생성할 수 있다. (비밀번호와 같으므로 절대 공유해선 안된다)
    
    (루트계정의) IAM → 액세스키 만들기 → CLI → 생성하기
    
    ![Untitled](IAM%20Users%20&%20Groups%205ec096f3f65b4a70991fb88d66b1ef1f/Untitled%201.png)
    

iterm에서 aws configure로 정보 입력 후 aws iam list-users를 입력하면 계정 내 모든 사용자가 리스토로 보여진다.

![image3.png](IAM%20Users%20%26%20Groups%205ec096f3f65b4a70991fb88d66b1ef1f%2Fimage3.png)
### CloudShell

- AWS 클라우드에서 무료로 사용가능한 터미널같은 개념 (특정 리전에서만 사용 가능)

## IAM Role

- 일부 AWS 서비스를 사용하기 위해서는 루트 계정 활용
- 이때, IAM Role을 생성하여 권한을 부여 받아야한다.
- IAM Role은 사용자와 같지만 실제 사람이 사용하도록 만들어 진 것이 아니고 AWS서비스에 의해 사용되도록 만들어 졌다.
    - ex) EC2 Instance를 생성한다. EC2 Instance는 AWS에서 어떤 작업을 수행하려고 할 수 있는데, 이를 위해 EC2 Instance에 권한을 부여해야 한다. 권한부여를 위해 IAM Role을 만들고 만든 Role을 EC2 Instance와 묶어 하나의 개체로 만들어서 AWS의 특정 정보에 접근하도록 한다.
- Common Roles에는 ‘EC2 Instance Roles’, ‘Lamda Function Roles’, ‘Roles for CloudFormation’ 등이 있다.

- 선택된 AWS Service만 알아두도록 하자.
![image1.png](IAM%20Users%20%26%20Groups%205ec096f3f65b4a70991fb88d66b1ef1f%2Fimage1.png)

## IAM Security Tools

- IAM Credentials Report (루트 계정 레벨)
    - 유저와 다양한 Credentials(자격 증명) 포함
- IAM Access Advisor (유저 계정 레벨)
    - 사용자에게 부여된 서비스 권한과 마지막으로 Access한 시간 확인가능
    - 이 도구를 사용하여 어떤 권한이 사용되지 않는지 볼 수 있어서 최소권한의 원칙을 지킬 수 있다.

## Credential report

![Untitled](IAM%20Users%20&%20Groups%205ec096f3f65b4a70991fb88d66b1ef1f/Untitled%202.png)

- IAM > Access reports > Credential report > Download Report
- 어떤 사용자가 비밀번호를 변경하지 않았는지, 계정을 사용하는지 등 파악할 때 유용
- 보안 측면에서 어떤 사용자를 주목해야 하는지 발견하는 데 도움이 된다.

## IAM Access Advisor

- IAM > Users > User name > Acces Advisor
- 보통 최근 4시간 동안의 활동 내역을 보여줌
- 사용하지 않는 권한들을 확인 후 삭제할 때 도움이 됨
![image2.png](IAM%20Users%20%26%20Groups%205ec096f3f65b4a70991fb88d66b1ef1f%2Fimage2.png)

### Q_1) 다음 중 IAM 역할의 올바른 정의는?

```
 a. 다중 사용자 그루벵 속한 IAM 사용자
 b. IAM 사용자들을 위한 비밀번호 정책을 정의하는 IAM 개체
 c. AWS 서비스에 요청을 생성하기 위한 일련의 권한을 정의하고, AWS 서비스에 의해 사용 될 IAM 개체
 d. 특정 행동 수행을 위해 IAM 사용자에게 할당된 권한

```

### Q_2) 다음 중 IAM 보안 도구에 해당되는 것은?

```
a. IAM 자격 증명 보고서
b. IAM 루트 계정 관리자
c. IAM 서비스 보고서
d. IAM 보안 관리자

```

### Q_3) IAM 사용자에 대해 잘못 서술된 내용을 고르세요

```
a. IAM 사용자들은 다중 사용자 그룹에 속할 수 있다
b. IAM 사용자들이 사용자 그룹에 속할 필요는 없다
c. IAM 정책은 IAM 사용자들에게 직접 연걸될 수 있다
d. IAM 사용자들은 루트 계정 자격 증명을 통해 AWS 서비스에 엑세스한다

```

### Q_4) 다음 중 IAM 모범 사례에 해당하는 것은?

```
a. 한 사람에게 다수의 IAM 사용자 생성하기
b. 루트 계정 사용하지 않기
c. 동료들이 업무를 대신 수행할 수 있도록 AWS 계정 자격 증명 공유하기
d. 보다 쉬운 엑세스를 위해 MFA를 활성화하지 않기

```

### Q_5) IAM 정책은 무엇인가?

```
a. AWS 계정들이 상호작용하는 방법을 정의하는 일련의 정책
b. AWS 서비스에 요청을 생성하기 위한 일련의 권한을 정의, IAM 사용자, 사용자 그룹 및 IAM 역할에서 사용하게 될 JSON 문서
c. IAM 사용자들의 비밀번호를 정의하는 일련의 정책
d. 고객들이 AWS와 상호작용하는 방법을 보여주는, AWS에서 정의한 일련의 정책

```

### Q_6) IAM 권한에는 다음 중 어떤 원칙이 적용되어야 하는가?

```
a. 최대 권한 부여하기
b. 직원의 요청이 있을 경우, 더 많은 권한 부여하기
c. 최소 권한 부여하기
d. 루트 계정 권한 제한하기

```

### Q_7) 루트 계정 보안을 향상시키기 위해서는 어떤 작업을 수행해야 하는가?

```
a. 루트 계정에서 권한 제거하기
b. AWS 명령줄 인터페이스(CLI)를 통해서만 AWS 서비스에 엑세스하기
c. IAM 사용자를 생성하지 않고, 루트 계정으로만 AWS 계정에 엑세스하기
d. 다중 인증(MFA) 활성화하기

```

### Q_8) IAM 사용자 그룹은 IAM 사용자 및 기타 사용자 그룹을 포함할 수 있습니다.

```
a. 참
b. 거짓

```

### Q_9) IAM 정책은 하나 이상의 문장으로 구성됩니다. 다음 중 IAM 정책 내 문장의 구성 요소가 아닌 것을 고르세요.

```
a. 효과 (Side)
b. 원칙 (Principal)
c. 버전 (Version)
d. 조치 (Action)
e. 리소스 (Resource)

```

### 정답 및 해설

Q_1. (c)
일부 AWS 서비스는 여러분을 위해 특정 행동을 수행해야 합니다. IAM 역할은 이러한 권한을 할당하기 위해 사용됩니다.

Q_2. (a)
IAM 자격 증명 보고서에는 AWS 계정의 모든 IAM 사용자와 이들의 다양한 자격 증명 상태가 포함되어 있습니다.

Q_3. (d)
IAM 사용자들은 자신만의 자격 증명(사용자 이름 & 비밀번호, 혹은 액세스 키)을 통해 AWS 서비스에 액세스합니다.

Q_4. (b)
루트 계정은 최초 IAM 사용자 생성과 일부 계정/서비스 관리 업무에만 사용됩니다. 일상적인 업무에는 IAM 사용자를 사용하셔야 합니다.

Q_5. (b)

Q_6. (c)
사용자에게 필요 이상의 권한을 부여하지 마세요.

Q_7. (d)
MFA를 활성화할 경우, 보안에 하나의 층을 더 추가하게 됩니다. 비밀번호가 유출되었거나 도용을 당한 경우에도, 계정 보호 가능합니다.

Q_8. (거짓)
IAM 사용자 그룹은 IAM 사용자만을 포함할 수 있습니다.

Q_9. (c)
IAM 정책의 문장은 시드, 효과, 원칙, 조치, 리소스, 그리고 조건으로 구성됩니다. 버전은 IAM 정책 자체의 일부이지, 문장의 일부가 아닙니다.