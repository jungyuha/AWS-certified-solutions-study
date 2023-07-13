# \[실습] Elastic Block Store (EBS)

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-07-12 Wed

#### last modified : 2023-07-13 Thu

## \[1] EC2 인스턴스 생성하기

#### EC2 대시보드 > '인스턴스 생성' 클릭

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="182"><figcaption><p>인스턴스 생성</p></figcaption></figure>

* 이름 : EC2\_Linux
*   인스턴스 개수 : 1

    <figure><img src="../.gitbook/assets/image (16).png" alt="" width="279"><figcaption><p> 인스턴스 개수 : 1</p></figcaption></figure>
*   AMI : Linux2

    <figure><img src="../.gitbook/assets/image (18).png" alt="" width="368"><figcaption><p> AMI : Linux2</p></figcaption></figure>
* 인스턴스 유형 : t2.micro
* 키 페어 : EC2\_key
* 네트워크나 서브넷은 그대로 놔둔다.
*   보안그룹 : 기존 보안그룹 선택 > 'ssh web access' 선택

    <figure><img src="../.gitbook/assets/image (19).png" alt="" width="375"><figcaption><p> 기존 보안그룹 선택 > 'ssh web access' 선택</p></figcaption></figure>
*   &#x20;스토리지 구성 <- 이 부분이 EBS 볼륨이다.

    * 다음과 같이 설정한다.

    <figure><img src="../.gitbook/assets/image (10).png" alt="" width="563"><figcaption><p>EBS 볼륨 설정]</p></figcaption></figure>


*   세부정보 > 사용자 데이터 : 웹서버 생성 스크립트 작성



    <figure><img src="../.gitbook/assets/image (21).png" alt="" width="563"><figcaption><p> 웹서버 생성 스크립트 작성</p></figcaption></figure>

### EC2 인스턴스 생성시 EBS 볼륨 설정값 종류

*   디폴트로 그대로 놔둔다. > '편집' 클릭

    <figure><img src="../.gitbook/assets/image (15).png" alt="" width="375"><figcaption><p>'편집' 클릭</p></figcaption></figure>

    1.  EBS 볼륨의 크기(용량) 설정 가능

        <figure><img src="../.gitbook/assets/image (14).png" alt="" width="375"><figcaption><p> EBS 볼륨의 크기(용량)</p></figcaption></figure>
    2.  EBS 볼륨 유형 설정 가능



        <figure><img src="../.gitbook/assets/image (13).png" alt="" width="375"><figcaption><p> EBS 볼륨 유형 설정 가능</p></figcaption></figure>
    3.  EBS 볼륨 암호화 설정 가능

        <figure><img src="../.gitbook/assets/image (27).png" alt="" width="375"><figcaption><p> EBS 볼륨 암호화 설정1</p></figcaption></figure>



        <figure><img src="../.gitbook/assets/image (12).png" alt="" width="173"><figcaption><p> EBS 볼륨 암호화 설정2</p></figcaption></figure>



## \[2] 생성된 인스턴스 확인

#### EC2 대시보드 > '인스턴스'  클릭 > 생성된 인스턴스 확인

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p> 생성된 인스턴스 확인</p></figcaption></figure>

퍼블릭 IP주소를 통해 웹서버가 잘 생성됐는지 확인한다.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption><p> 웹서버가 잘 생성됐는지 확인</p></figcaption></figure>

#### 생성된 인스턴스 클릭 > '스토리지' 탭

*   EC2 인스턴스의 EBS 볼륨을 확인할 수 있다.

    *

        <figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>EC2 인스턴스의 EBS 볼륨을 확인할 수 있다. </p></figcaption></figure>





#### 왼쪽 메뉴 'Elastic Block Store' > 볼륨 메뉴

*   인스턴스에 연결된 EBS 볼륨을 확인할 수 있다.

    <figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption><p> 인스턴스에 연결된 EBS볼륨</p></figcaption></figure>


*   볼륨에 연결된 인스턴스 정보

    <figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>볼륨에 연결된 인스턴스 정보</p></figcaption></figure>


*   EBS 볼륨 이름을 변경한다.

    이름 : EC2\_Linux\_EBS

    <figure><img src="../.gitbook/assets/image (5).png" alt="" width="375"><figcaption><p> EBS 볼륨 이름을 변경한다.</p></figcaption></figure>



## \[3] 볼륨을 추가하여 동일한 인스턴스에 연결하기

EBS 볼륨은 동일한 가용영역 내에서만 연결이 가능하기 때문에 동일한 가용영역에 생성해야 한다.&#x20;

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption><p> 동일한 가용영역에 생성</p></figcaption></figure>

#### 왼쪽 메뉴 'Elastic Block Store' > 볼륨 메뉴 > '볼륨 생성' 클릭

1.  가용영역을 선택한다.

    <figure><img src="../.gitbook/assets/image (6).png" alt="" width="563"><figcaption></figcaption></figure>


2. 나머지 속성
   * 볼륨 유형 : 범용 SSD(gp 2)
   * 볼륨 크기 : 5 Gb
   *   이 볼륨 암호화 체크 + KMS 키 설정

       <figure><img src="../.gitbook/assets/image (23).png" alt="" width="375"><figcaption><p> 이 볼륨 암호화 체크</p></figcaption></figure>

#### 생성된 볼륨 선택 > 오른쪽 상단 '작업' > '볼륨 연결' 클릭

이름 : EC2\_Linux\_EBS2

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption><p> 생성된 볼륨 선택</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image.png" alt="" width="207"><figcaption><p> '볼륨 연결' 클릭</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="563"><figcaption><p> 연결할 인스턴스 선택</p></figcaption></figure>

#### EC2 대시보드 > '인스턴스'  클릭 > 인스턴스 선택 > 아래 '스토리지' 탭 > 연결된 볼륨 확인

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption><p> 연결된 볼륨 확인</p></figcaption></figure>

## \[4] EBS 볼륨에 데이터를 백업하는 스냅샷 만들기

#### 왼쪽 메뉴 'Elastic Block Store' > 볼륨 메뉴 > 볼륨 선택 > 오른쪽 상단 '작업' > '스냅샷 수명 주기 정책 생성' 클릭

<figure><img src="../.gitbook/assets/image (40).png" alt="" width="367"><figcaption><p>  '스냅샷 수명 주기 정책 생성' 클릭</p></figcaption></figure>

*   스냅샷을 일정에 따라 만들어줄 수 있다.

    <figure><img src="../.gitbook/assets/image (33).png" alt="" width="375"><figcaption><p> 스냅샷을 일정에 따라 만들어줄 수 있다.</p></figcaption></figure>

#### 왼쪽 메뉴 'Elastic Block Store' > 볼륨 메뉴 > 볼륨 선택 > 오른쪽 상단 '작업' 클릭 > '스냅샷 생성' 클릭

*   이름을 'EC2\_Linux\_Snapshot'으로 설정한다.

    <figure><img src="../.gitbook/assets/image (32).png" alt="" width="375"><figcaption><p>  '스냅샷 생성'</p></figcaption></figure>

#### 왼쪽 메뉴 'Elastic Block Store' > 스냅샷 메뉴 > 생성된 스냅샷 확인

*   원본 볼륨이 암호화되어있지 않았었기 때문에 이 스냅샷도 암호화 되어있지 않다.

    <figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption><p> 암호화 되어있지 않다.</p></figcaption></figure>

#### 왼쪽 메뉴 'Elastic Block Store' > 스냅샷 메뉴 > 스냅샷 선택 > 오른쪽 상단 '작업' > '스냅샷에서 볼륨 생성' 클릭

*   암호화된 EBS 볼륨을 생성시킨다.

    <figure><img src="../.gitbook/assets/image (46).png" alt="" width="367"><figcaption><p>암호화된 볼륨 생성</p></figcaption></figure>


* 이 암호화된 볼륨을 EC2 인스턴스에 연결하면 암호화된 볼륨으로 변경이 될 것이다.

#### 왼쪽 메뉴 'Elastic Block Store' > 스냅샷 메뉴 > 스냅샷 선택 > 오른쪽 상단 '작업' > '스냅샷에서 이미지 생성' 클릭

* 생성 속성
  * 이름 : EC2\_Linux\_AMI
  * 나머지는 그대로

#### 왼쪽 메뉴 '이미지' > 'AMI' > 생성된 AMI 이미지 확인

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption><p> 생성된 AMI 이미지 확인</p></figcaption></figure>

* 우리가 만든 EC2 인스턴스의 볼륨을 스냅샷으로 만들어서 이미지로 만들었다. 즉 , 리눅스 웹서버가 만들어졌을 것이다.

### 생성된 AMI 이미지를 사용하는 방법

스냅샷에서 웹서버의 이미지를 가지고 EC2 인스턴스를 생성할 수 있다.

#### 방법 1 : 왼쪽 메뉴 '이미지' > 'AMI' > 이미지 선택 > 오른쪽 상단  'AMI로 인스턴스 시작' 클릭 > EC2가 생성된다.

<figure><img src="../.gitbook/assets/image (31).png" alt="" width="563"><figcaption><p> 'AMI로 인스턴스 시작</p></figcaption></figure>

#### 방법 2 : 왼쪽 메뉴 '인스턴스' > '인스턴스 생성' > '애플리케이션 및 OS 이미지' > '내 AMI' 선택 > 생성했던 이미지 선택

<figure><img src="../.gitbook/assets/image (36).png" alt="" width="563"><figcaption><p> '내 AMI' 선택</p></figcaption></figure>

### 스냅샷 복사하기&#x20;

#### 왼쪽 메뉴 'Elastic Block Store' > 스냅샷 메뉴 > 스냅샷 선택 > 오른쪽 상단 '작업' > '스냅샷 복사'

*   스냅샷을 다른 리전으로 복사할 수 있다.



    <figure><img src="../.gitbook/assets/image (45).png" alt="" width="563"><figcaption><p> 스냅샷 복사하기</p></figcaption></figure>

### 스냅샷 복원하기&#x20;

#### 왼쪽 메뉴 'Elastic Block Store' > 스냅샷 메뉴 > 스냅샷 선택 > 오른쪽 상단 '휴지통' > '보존 규칙 생성'

<figure><img src="../.gitbook/assets/image (42).png" alt="" width="563"><figcaption></figcaption></figure>

*   휴지통에 규칙을 만들어서 보존 기간을 지정하게 되면 실수로 스냅샷을 삭제해도 보존 기간 내에서는 스냅샷 복원이 가능하다.



    <figure><img src="../.gitbook/assets/image (9).png" alt="" width="375"><figcaption><p> 보존 기간 내에서는 스냅샷 복원이 가능하다.</p></figcaption></figure>



