# \[실습] Network Load Balancer 생성

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-30 Fri

#### last modified : 2023-07-03 Mon

## \[1] Network Load Balancer의 특징

* TCP, UDP, TLS 요청을 로드 밸런싱 해야 하는 경우에 사용
*   동작이 Application Load Balancer보다 빠르기 때문에 고도의 성능이 요구되거나

    대기 시간이 낮아야 하는 애플리케이션에 적합
* 게임 등의 수백만의 동시 사용자 처리에 적합
* 고정 IP 주소 할당 가능
  * ALB에서는 불가능하다.
  *   인터넷 상의 특정 서비스가 IP주소로 필터링 하는 경우 고정 IP 주소를 사용해야 하므로

      이 때 네트워크 로드 밸런스를 사용하면 된다.
* 클라이언트 IP 주소 전달 가능 (Source IP Preservation)
  *   일반적으로 PC에서 로드밸런스에 접속해서 로드밸런스 뒤의 타겟그룹의 서비스에 접속하게 되면

      클라이언트 IP 주소를 전달하지 않는다.
  *   타겟그룹 안에 있는 서비스가 클라이언트 IP주소가 필요한 경우 NLB를 통해서

      클라이언트 IP 주소를 전달받을 수 있다.
* ALB처럼 리스너 규칙 설정 없음
* 리스너 프로토콜은 TCP, TCP/UDP, UDP, TLS 를 사용 할 수 있음
* ALB처럼 데이터 전송보안을 위한 TLS 프로토콜 사용시 SSL/TLS 인증서를 배포해야 함
* 인증서는 ACM(AWS Certificate Manager) 사용 또는 클라이언트 인증서 사용 가능

## \[2] Network Load Balance 생성 실습

이전 시간에 만든 TG-NLB라는 타깃 그룹을 대상으로 네트워크 로드 밸런서를 생성한다.

### TG-NLB 타겟그룹을 Network Load Balancer에 적용하기

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 생성 > Network Load Balancer 선택

<figure><img src="../.gitbook/assets/image (28).png" alt="" width="159"><figcaption><p> Network Load Balancer 선택 </p></figcaption></figure>

*

    <figure><img src="../.gitbook/assets/image (32).png" alt="" width="236"><figcaption><p>기본 구성</p></figcaption></figure>

    * 로드 밸런서 이름 :NLB
    * 체계 : 인터넷 경계
    * IP 주소 유형 : IPv4
* ![](<../.gitbook/assets/image (49).png>)
  * 네트워크 매핑 : 이 로드발란서가 위치할 가용영역을 선택 > 전부 다 선택한다.
*

    <figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption><p> 리스너 및 라우팅</p></figcaption></figure>

    * 리스너 및 라우팅 : TCP / 80 프로토콜이 들어올 때 TG-NLB 타겟그룹에 전달하는 리스너를 만든다.
      * 타겟그룹이 TCP이므로..
* 나머지는 그대로 두고 로드밸런서를 생성한다.

### 로드발란서에 접속하는 방법

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 'DNS이름' 복사 > 브라우저에 복사

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption><p>  'DNS이름' 복사</p></figcaption></figure>

![](<../.gitbook/assets/image (70).png>)![](<../.gitbook/assets/image (12).png>)

* 172-31-35-68 과 172.31.42.104라는 웹서버로 번갈아 접속이 된다.
  * 이 주소는 이전 시간에 만들었던 공용 IP의 웹서버이다.&#x20;
    *

        <figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption><p> 172-31-35-68</p></figcaption></figure>
    *

        <figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption><p>172.31.42.104</p></figcaption></figure>
* 즉, 2개의 웹서버가 로드밸런싱을 통해 번갈아가며 접속됨을 알 수 있다.

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 선택 > 아래 '리스너' 탭 > 리스너 조회

#### 왼쪽 메뉴 '로드 밸런싱' > 로드밸런서 > 로드밸런서 선택 > 아래 '설명'탭 > '가용영역' 부분 >ipv4 조회 > 'AWS에서 할당'

### 고정 IP 주소 할당하기

#### 왼쪽 메뉴 '네트워크 및 보안' > '탄력적 IP' 클릭 > 오른쪽 상단 '탄력적 IP 주소 할당' 선택 > 오른쪽 아래 '할당' 클릭

<figure><img src="../.gitbook/assets/image (9) (4).png" alt=""><figcaption><p> 탄력적 IP 주소 할당</p></figcaption></figure>

* 이름 : NLB\_IP

#### 왼쪽 메뉴 '로드밸런싱' > '로드밸런서 생성' 클릭 > 'network Load Balancer' 클릭

#### '네트워크 매핑' 탭 > 가용영역 > ipv4 설정 > ipv4 주소 > '탄력적 IP 주소 사용' 클릭

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="563"><figcaption><p> '네트워크 매핑' 탭 > 가용영역 > ipv4 설정 > ipv4 주소 > '탄력적 IP 주소 사용' 클릭</p></figcaption></figure>



{% hint style="danger" %}
**로드밸런스와 탄력적 IP는 과금서비스이므로 실습 후 삭제한다.대상그룹도 삭제한다.**
{% endhint %}



####
