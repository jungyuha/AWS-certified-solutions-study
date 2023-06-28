# 탄력적 IP (Elastic IP)

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-20 Tue

#### last modified : 2023-06-20 Tue

## \[1] Public IP vs. Private IP

### 퍼블릭 IP

* 인터넷 연결에 사용하는 IP이다.
* 공용 IP라고도 한다.

### 프라이빗 IP

* 회사나 집의 내부에서만 사용하는 IP이다.
  * 회사 내부에서 컴퓨터가 연결될 떄 사용하는 IP
  * 집에 인터넷 공유기를 연결하고 공유기에 연결된 모바일 폰이나 PC 등
* 직접적으로 인터넷 연결이 안되며 인터넷 게이트웨이를 통해야 인터넷에 연결할 수 있다.

### 예시 1. 인터넷,웹서버,기업 내부 사설망으로 구성될 때

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p> 인터넷,웹서버,기업 내부 사설망으로 구성될 때</p></figcaption></figure>

#### **기업 내부 사설망**

* **기업 내부 사설망** 안에 서버나 컴퓨터 등이 있다.
* 이 사설망에서 인터넷과 연결하기 위해서는 '**인터넷 게이트웨이**'라는 것이 존재한다.
* 가정 등 에서는 '**인터넷 모뎀**' 이 인터넷 게이트웨이 역할을 한다.

#### 웹서버

* 웹서버에서는 인터넷에서 연결이 되어야 하니 퍼블릭 IP를 가지게된다.

#### 인터넷

* 퍼블릭 IP는 전세계에 하나밖에 없는 고유한 IP주소 값을 가진다.
* 인터넷 게이트웨이도 인터넷에서 연결이 되어야 하니 퍼블릭 IP를 가지게된다.
* 내부 사설망은 프라이빗 IP를 사용하게 된다.

#### Public IP vs. Private IP의 차이점

*   프라이빗 IP는 다른 기업이나 다른 가정에서 동일한 주소로 사용해도 서로 연결이 되지 않으니

    중복해서 사용이 가능하다.

## \[2] 탄력적 IP (Elastic IP)

* 기본 인스턴스는 Public IP 주소가 변경된다.
  * 인스턴스 생성시 자동으로 할당 받은 Public IP는 인스턴스를 재시작하면 다른 IP 로 재할당 받으면서 Public IP 주소가 변경된다.
* Elastic IP는 인터넷에 연결 가능한 고정적(정적)인 퍼블릭 IP 주소이다.
*   인스턴스를 재시작해도 동일한 IP를 사용하고 싶다면 이 Elastic IP를 생성해서 인스턴스에 연결된 네트워크

    인터페이스에 할당을 하면 된다.
* EC2 인스턴스의 ENI 에 탄력적 IP 주소를 연결하면 EC2 인스턴스를 다시 시작해도 동일한 IP 주소로 접속할 수 있다.

## \[3] 콘솔창에서 탄력적 IP (Elastic IP) 실습하기

### &#x20;1) public ip 주소 확인하기

#### EC2 인스턴스 대시보드 > 특정 인스턴스 클릭 > '네트워킹 탭' > public ip 주소 확인

<figure><img src="../.gitbook/assets/image (14) (3).png" alt=""><figcaption><p> public ip 주소 확인</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 특정 인스턴스 클릭 > 오른쪽 상단 '작업' 클릭 > 네트워킹 > 인스턴스 설정 > '중지 방지 변경' 클릭 > 활성화 'disable' >  &#x20;

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption><p> 중지 방지 비활성화</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 특정 인스턴스 클릭 > 오른쪽 상단 '인스턴스 상태' 클릭 > '인스턴스 중지'

public ip 주소를 보면 보이지 않는다.

<figure><img src="../.gitbook/assets/image (15) (2).png" alt=""><figcaption><p> 인스턴스 중지</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 특정 인스턴스 클릭 > '네트워킹 탭' > 네트워크 인터페이스 확인

간혹 네트워크 인터페이스가 2개 이상이면 public IP가 부여되지 않으므로 1개를 지운다.

<figure><img src="../.gitbook/assets/image (4) (3).png" alt=""><figcaption><p> 간혹 네트워크 인터페이스가 2개 이상이면 public IP가 부여되지 않는다.</p></figcaption></figure>

#### 네트워크 인터페이스 분리 및 삭제

인스턴스에 연결되어있던 EC2\_Linux2 네트워크 인터페이스를 인스턴스로부터 분리시키고 삭제한다.

<figure><img src="../.gitbook/assets/image (9) (3).png" alt=""><figcaption><p> 인스턴스로부터 분리</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11) (4).png" alt=""><figcaption><p>네트워크 인터페이스 삭제</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 특정 인스턴스 클릭 > 오른쪽 상단 '인스턴스 시작'&#x20;

다시 public ip 주소 확인하면  IP 주소가 바뀌어있다.

<figure><img src="../.gitbook/assets/image (51) (2).png" alt=""><figcaption><p> 다시 public ip 주소 확인하면  IP 주소가 바뀌어있다.</p></figcaption></figure>

### 2) 탄력적 IP 설정하기(유료 서비스)

#### 왼쪽 메뉴 '네트워크 및 보안' > 탄력적IP > 오른쪽 상단 '탄력적IP 주소 할당' 클릭

기본 설정 그래도 두고 '할당'을 클릭한다.

<figure><img src="../.gitbook/assets/image (42) (1).png" alt="" width="375"><figcaption><p> 탄력적 IP 설정 </p></figcaption></figure>

#### 탄력적IP 주소 목록 > 오른쪽 상단 '작업' 클릭 > '탄력적IP 주소 연결' 클릭

<figure><img src="../.gitbook/assets/image (38) (2).png" alt=""><figcaption><p> 탄력적IP 주소 연결</p></figcaption></figure>

#### 연결할 유형 '인스턴스' 선택 > 특정 인스턴스 선택 > 프라이빗 IP 주소 선택

<figure><img src="../.gitbook/assets/image (44) (1).png" alt="" width="375"><figcaption><p> 탄력적IP 주소 연결</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 특정 인스턴스 클릭 > '네트워킹 탭' > 탄력적 ip 주소 확인

이 때 이전에 할당받았던 public ip는 비활성화된다.

이 IP 주소는 인스턴스를 재시작해도 동일한 주소로 인터넷에 연결할 수 있다.

<figure><img src="../.gitbook/assets/image (34) (3).png" alt=""><figcaption><p> 탄력적 ip 주소 확인</p></figcaption></figure>

