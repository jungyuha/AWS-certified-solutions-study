# 실습

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-09 Fri

#### last modified : 2023-06-09 Fri



IAM 대시보드 > 메뉴 > "역할" 클릭

#### 역할 만들기

오른쪽 상단의 "역할 만들기" 버튼 클릭

<figure><img src="../../.gitbook/assets/image (13) (1).png" alt=""><figcaption><p> 역할 만들기</p></figcaption></figure>

#### 엔터티 유형 : AWS 서비스 선택

여기서의 "역할"은 특정 AWS서비스(EC2..)가 다른 AWS 서비스에 접속해 작업을 수행할 때 필요한 권한

<figure><img src="../../.gitbook/assets/image (29) (2).png" alt=""><figcaption><p> 엔터티 유형 : AWS 서비스 선택</p></figcaption></figure>

#### 역할에 권한 부여하기

권한에 S3를 검색한 뒤 **AmazonS3FullAccess** 권한을 추가한다.

상단에 "필터 지우기" 버튼을 클릭하고 RDS를 검색하여 **AmazonRDSFullAccess** 권한을 추가한다.

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (2).png" alt=""><figcaption><p> 권한 부여하기</p></figcaption></figure>

#### 역할 생성하기

S3andRDS\_Full\_Access라는 이름을 가진 역할을 생성한다.

<figure><img src="../../.gitbook/assets/image (12) (1) (1) (1).png" alt=""><figcaption><p> 역할 생성하기</p></figcaption></figure>

#### 생성된 역할 조회

<figure><img src="../../.gitbook/assets/image (30) (2).png" alt=""><figcaption><p> 생성된 역할 목록</p></figcaption></figure>

역할을 클릭하면 연결된 권한 정책을 볼 수 있다.또한 역할에도 권한 경계 설정이 가능하다.

<figure><img src="../../.gitbook/assets/image (9) (2) (2).png" alt=""><figcaption><p> 권한 정책 , 권한 경계 설정</p></figcaption></figure>

#### 신뢰 정책&#x20;

신뢰 정책 편집을 통해서 이 역할을 다른 계정에 위임할 수도 있다.

<figure><img src="../../.gitbook/assets/image (17) (1) (2).png" alt=""><figcaption><p> 신뢰 정책</p></figcaption></figure>

#### EC2 인스턴스에 해당 역할 부여하기

EC2 대시보드 접속 > 인스턴스 시작 버튼 클릭

![](<../../.gitbook/assets/image (27) (1) (2).png>)

고급 세부정보 클릭 > IAM 인스턴스 프로파일 클릭해서 아까 만든 역할을 설정한다.

<figure><img src="../../.gitbook/assets/image (11) (2) (1) (1).png" alt=""><figcaption><p> EC2 인스턴스에 해당 역할 부여하기</p></figcaption></figure>

만들어진 EC2인스턴스에서 실행되는 애플리케이션은 S3와 RDS에 대해 FullAccess 권한을 갖게되어

데이터를 읽고 쓰거나 RDS데이터 베이스에 접속에서 데이터를 읽고 쓸수 있게 된다.
