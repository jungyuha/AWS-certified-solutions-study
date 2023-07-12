# \[실습] Elastic Block Store (EBS)

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-07-12 Wed

#### last modified : 2023-07-12 Wed

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



## \[2]

### 생성된 인스턴스 확인

#### EC2 대시보드 > '인스턴스'  클릭 > 생성된 인스턴스 확인

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p> 생성된 인스턴스 확인</p></figcaption></figure>

퍼블릭 IP주소를 통해 웹서버가 잘 생성됐는지 확인한다.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption><p> 웹서버가 잘 생성됐는지 확인</p></figcaption></figure>
