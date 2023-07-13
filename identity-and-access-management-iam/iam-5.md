# IAM 정책 시뮬레이터

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-09 Fri

#### last modified : 2023-06-09 Fri



## \[1] IAM Policy Simulator

AWS 계정의 IAM 사용자 , 그룹 또는 역할에 연결된 정책을 테스트한다.

### 접속 링크&#x20;

{% embed url="https://policysim.aws.amazon.com/" %}

## \[2] IAM Policy Simulator 예시 : 사용자

#### 사용자 , 그룹 , 역할 중 1개 선택

![](<../.gitbook/assets/image (16) (1) (2).png>)

사용자 yuha.jung 선택한다. 이 사용자는 EC2에 대한 FullAccess권한만을 가진다.

#### 테스트하려는 서비스 선택 : EC2

<figure><img src="../.gitbook/assets/image (7) (2).png" alt=""><figcaption><p> 테스트하려는 서비스 선택 : EC2</p></figcaption></figure>

#### 시뮬레이션 실행

EC2에 대한 FullAccess 권한이 있으므로 모두 allowed가 뜬다.

<figure><img src="../.gitbook/assets/image (3) (1) (2).png" alt=""><figcaption><p> 시뮬레이션 실행</p></figcaption></figure>

#### 테스트하려는 서비스 선택 : S3

<figure><img src="../.gitbook/assets/image (4) (2) (2) (1).png" alt=""><figcaption><p> 테스트하려는 서비스 선택 : S3</p></figcaption></figure>

#### 시뮬레이션 실행

S3에 대한 권한은 없으므로 denied가 뜬다.

<figure><img src="../.gitbook/assets/image (17) (1).png" alt=""><figcaption><p> 시뮬레이션 실행</p></figcaption></figure>
