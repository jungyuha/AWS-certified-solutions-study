# \[실습] Application Load Balancer 생성

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-29 Thu

#### last modified : 2023-07-03 Mon

## \[1] Application Load Balancer의 특징

* HTTP/HTTPS 요청(웹서비스 요청)을 로드 밸런싱 해야 하는 경우 사용
* 웹 애플리케이션 처리에 적합
* 리스너 규칙을 기반으로 라우팅 설정이 가능함
* 데이터 전송 보안을 위한 HTTPS 프로토콜 사용시 SSL/TLS 인증서를 배포해야 함(로드발란서와 연결)
  * 인증서는 ACM(AWS Certificate Manager) 사용
  * 또는 클라이언트 인증서 사용 가능

## \[2] 리스너 규칙

<figure><img src="../.gitbook/assets/image (10) (3).png" alt=""><figcaption><p> 리스너 규칙</p></figcaption></figure>

* 특정 조건값에 따라 특정 타겟 그룹으로 라우팅하는 것(트래픽을 전달)

### Host header : 각 요청의 호스트 이름을 기반으로 라우팅

#### 예시

* aaa.example.com로 접속한 클라이언트는 aaa.example.com과 연결된 타겟 그룹으로 라우팅이 된다.
* ddd.example.com로 접속한 클라이언트는 ddd.example.com과 연결된 다른 타겟 그룹으로 라우팅이 된다.

### Path : 요청의 URL 의 경로 패턴을 기반으로 라우팅

#### 예시

* www.example.com/audio => audio에 해당하는 타겟그룹을 따로 지정
* www.example.com/video => video에 해당하는 타겟그룹을 따로 지정

### Http header : 각 요청의 HTTP 헤더를 기반으로 라우팅

### Http request method : 각 요청의 HTTP 요청 매서드를 기반으로 라우팅

### Query string: 쿼리 문자열의 키 값 페어 또는 값을 기반으로 라우팅

### Source IP : 각 요청의 소스 IP 주소를 기반으로 라우팅

## \[3] Application Load Balancer 생성 실습

이전 시간에 만든 TG-ALB라는 타깃 그룹을 대상으로 애플리케이션 로드 발란서를 생성한다.

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 생성 > Applicaion Load Balancer 선택

<figure><img src="../.gitbook/assets/image (40) (3).png" alt="" width="172"><figcaption><p> Applicaion Load Balancer</p></figcaption></figure>

* ![](<../.gitbook/assets/image (44) (2).png>)
  * 로드 밸런서 이름 : ALB
  * 체계 : 인터넷 경계
  * IP 주소 유형 : IPv4
* ![](<../.gitbook/assets/image (49) (2).png>)
  * 네트워크 매핑 : 이 로드발란서가 위치할 가용영역을 선택 > 전부 다 선택한다.
* 보안 그룹&#x20;
  * ![](<../.gitbook/assets/image (42) (2).png>)
    * default는 웹 트래픽이 허용되지 않은 상태이므로 삭제한다.
    * 웹서버 생성 때 만든 web\_accss\_sg 를 선택한다.
* 리스너 및 라우팅 : HTTP / 80 으로 전달이 될 때 대상그룹 TG-ALB로 전달하기로 설정한다.
  *

      <figure><img src="../.gitbook/assets/image (33) (3).png" alt=""><figcaption><p>  HTTP / 80 으로 전달이 될 때 대상그룹 TG-ALB로 전달하기로 설정</p></figcaption></figure>
* 나머지는 그대로 두고 로드밸런서를 생성한다.

### 로드발란서에 접속하는 방법

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 'DNS이름' 복사 > 브라우저에 복사

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption><p>  'DNS이름' 복사</p></figcaption></figure>

![](<../.gitbook/assets/image (70).png>)![](<../.gitbook/assets/image (12) (1).png>)

*   172-31-35-68 과 172.31.42.104라는 웹서버로 번갈아 접속이 된다.

    * 이 주소는 이전 시간에 만들었던 인스턴스 웹서버의 private IP주소이다.&#x20;

    <figure><img src="../.gitbook/assets/image (65).png" alt="" width="563"><figcaption><p> 172.31.42.104 인스턴스 접속</p></figcaption></figure>



    <figure><img src="../.gitbook/assets/image (11) (1).png" alt="" width="563"><figcaption><p> 172.31.35.68 인스턴스 접속</p></figcaption></figure>
* 즉, 2개의 웹서버가 로드밸런싱을 통해 번갈아가며 접속됨을 알 수 있다.

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 선택 > 아래 '리스너' 탭

<figure><img src="../.gitbook/assets/image (59).png" alt="" width="563"><figcaption><p> HTTP/80 에는 TG-ALB 대상그룹이 있다.</p></figcaption></figure>

* HTTP/80 에는 TG-ALB 대상그룹이 있다. 이 대상그룹엔 2개의 인스턴스가 연결되어 있다.

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 선택 > 대상 그룹 선택(TG-ALB)

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

* 아래 '상태검사'탭의 설정값에 따라 '대상' 탭에 있는 인스턴스의 '상태 확인' 값이 반영된다.
*   \- 비정상인 경우 해당 로드밸런싱은 인스턴스에 트래픽을 전달하지 않는다.

    (정상적인 인스턴스에만 트래픽을 전달한다.)

### HTTPS로 접속하기

#### 첫번째 방법 : 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 선택 > 아래 '리스너'탭 > '리스너' 추가

* HTTPS / 443 선택
* 기본 SSL 인증서 : ACM에서 인증서 만들어서 가져오기
  * ACM 기능은 AWS 콘솔에서 'ACM' 검색 > 인증서 요청 > 생성 후 도메인 주소에 연결하면 된다.

#### 두번째 방법 : 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 선택 > 아래 '리스너'탭 > '리스너' 추가

* HTTP / 80 선택
* 기본 작업 > '리디렉션' 선택
  * HTTPS / 443 추가
  * HTTP로 접속해도 HTTPS로 접속된다.
