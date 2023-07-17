# \[실습] 콘솔창에서 보안그룹 확인하기

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-19 Mon

#### last modified : 2023-06-19 Mon



### 1) EC2 인스턴스의 보안 그룹 확인

#### EC2 인스턴스 대시보드 > 아래 '네트워킹' 탭 클릭 > 네트워크 인터페이스 > 오른쪽으로 쭉 보면 '보안그룹'이 연결되어있음

* 나가고 들어오는 트래픽을 '보안그룹'이 필터링함

<figure><img src="../../.gitbook/assets/image (47) (1).png" alt=""><figcaption><p> EC2 인스턴스의 보안 그룹</p></figcaption></figure>

### 2) 인바운드와 아웃바운드 규칙 확인

#### 왼쪽 메뉴 '네트워크 및 보안' > 보안 그룹 클릭 > 특정 보안그룹 선택 > 아래 탭에서 해당 보안그룹의 인바운드와 아웃바운드 규칙 확인 가능

<figure><img src="../../.gitbook/assets/image (13) (2).png" alt=""><figcaption><p> '네트워크 및 보안' > 보안 그룹 클릭 > 특정 보안그룹 선택</p></figcaption></figure>

#### 보안 그룹 대시보드 > 아래 탭 '인바운드 규칙 클릭'

<figure><img src="../../.gitbook/assets/image (2) (2) (1).png" alt=""><figcaption><p> 인바운드 규칙</p></figcaption></figure>

* 모든 IP로부터의 (0.0.0.0/0) 웹서버 접속을 위한 HTTP 80 프로토콜 허용
* 모든 IP로부터의 (0.0.0.0/0) SSH 접속을 허용

#### 보안 그룹 대시보드 > 아래 탭 '아웃바운드 규칙 클릭'

<figure><img src="../../.gitbook/assets/image (3) (3).png" alt=""><figcaption><p> 아웃바운드 규칙</p></figcaption></figure>

* 기본 설정으로 '전체 프로토콜'이 허용됨

### 3) 인바운드와 아웃바운드 접속 테스트

#### EC2 인스턴스 대시보드 > 퍼블릭 IPv4 주소 복사 > 브라우저에 붙여넣기 > 웹서버 접속 가능

HTTP 프로토콜이 보안그룹에서 허용이 되어있기 때문에 접속이 가능하다.

<figure><img src="../../.gitbook/assets/image (55) (1).png" alt="" width="375"><figcaption><p> 웹서버 접속 가능</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 오른쪽 상단 연결 클릭 > 아래 연결 클릭 > 원격 접속 가능

SSH 프로토콜이 보안그룹에서 허용이 되어있기 때문이다.

<figure><img src="../../.gitbook/assets/image (57) (1).png" alt="" width="375"><figcaption><p> 원격 접속 가능</p></figcaption></figure>

### 4) 인바운드와 아웃바운드 규칙 편집

#### 1. 인바운드 규칙 편집

#### 보안 그룹 대시보드 > 아래 탭 '인바운드 규칙 클릭' > '인바운드 규칙 편집' 클릭

* HTTP 80 프로토콜을 삭제한다.

<figure><img src="../../.gitbook/assets/image (9) (2).png" alt=""><figcaption><p> HTTP 80 프로토콜을 삭제</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 퍼블릭 IPv4 주소 복사 > 브라우저에 붙여넣기 > 웹서버 접속 불가능

HTTP 프로토콜이 보안그룹에서 삭제됐기 때문에 접속이 불가능하다.

#### 보안 그룹 대시보드 > 아래 탭 '인바운드 규칙 클릭' > '인바운드 규칙 편집' 클릭

* HTTP 80 프로토콜을 다시 추가한다.

#### 2. 아웃바운드 규칙 편집

#### 보안 그룹 대시보드 > 아래 탭 '아웃바운드 규칙 클릭' > '아웃바운드 규칙 편집' 클릭

* 아웃 바운드 규칙 삭제 => 나가는 모든 트래픽을 차단하게 된다.

<figure><img src="../../.gitbook/assets/image (62) (1).png" alt=""><figcaption><p> 아웃 바운드 규칙 삭제</p></figcaption></figure>

#### EC2 인스턴스 대시보드 > 퍼블릭 IPv4 주소 복사 > 브라우저에 붙여넣기 > 웹서버 접속 가능

<figure><img src="../../.gitbook/assets/image (55) (1).png" alt="" width="375"><figcaption><p> 웹서버 접속 가능</p></figcaption></figure>

* 상태저장 방화벽이기 떄문에 인바운드 규칙 허용시 아웃바운드 규칙은 체크하지 않는다.
* 아웃바운드 규칙이 없어도 리턴 트래픽은 나갈 수 있다.(인바운드에 규칙이 있으므로)

#### 보안 그룹 대시보드 > 아래 탭 '아웃바운드 규칙 클릭' > '아웃바운드 규칙 편집' 클릭

* 아웃 바운드 규칙 추가 : 유형은 '모든 트래픽' , 대상은 모든 IP(0.0.0.0/0)

