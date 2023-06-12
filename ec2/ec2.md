# EC2 개요 및 인스턴스 생성

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-12 Mon

#### last modified : 2023-06-12 Mon

## \[1] EC2 개요

* AWS 클라우드 컴퓨팅 서비스 = 클라우드 가상 서버 (Virtual
* EC2 클라우드 가상 서버를 인스턴스 라고 부름

## \[2] EC2 인스턴스 생성 실습1 : Linux 인스턴스

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Linux 인스턴스 생성</p></figcaption></figure>

1. 이름 및 태그
2. 애플리케이션 및 OS 이미지
3. 인스턴스 유형
4. 키 페어 (원격 접속을 위한)
5. 네트워크 설정
6. 스토리지 구성
7. 고급 세부 정보

### (1) EC2 대시보드

#### 리전 확인

![](<../.gitbook/assets/image (24).png>)

#### 현재 형성된 리소스 확인

해당 리전(서울)에 현재 형성된 리소스들을 볼 수 있다.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption><p>현재 형성된 리소스</p></figcaption></figure>

#### 현재 리전(서울)의 가용영역

<figure><img src="../.gitbook/assets/image (8).png" alt="" width="375"><figcaption><p>해당 리전(서울)의 가용영역</p></figcaption></figure>

#### 인스턴스 시작

첫번째 방법 , 대시보드 > 인스턴스 시작

![](<../.gitbook/assets/image (6).png>)

두번째 방법 , 메뉴 > 인스턴스 > 인스턴스 시작

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

#### 인스턴스 설정 1 : 이름 및 태그

* 태그 추가 : 부서별, 리소스 별 등등 태그를 설정할 수 있다.
  *

      <figure><img src="../.gitbook/assets/image (34).png" alt="" width="375"><figcaption><p> 태그 추가 : 부서별, 리소스 별 등등 태그를 설정</p></figcaption></figure>

#### 인스턴스 설정 2 : 애플리케이션 및 OS 이미지(AMI)

* 인스턴스 시작할 때 필요한 OS 나 운영체제 애플리케이션 등이 모두 포함된 이미지
* 이 이미지를 인스턴스에 로드하여 빠르게 인스턴스를 실행시킬 수 있다.
* 디폴트값 : **Amazon Linux**
* **더 많은 API 찾아보기** 클릭
  * **내 AMI** : 사용자가 AMI를 직접 생성해서 그 AMI를 가지고 인스턴스를 만들 수 있다.
  * **AWS Marketplace AMI** : AWS의 협력업체들이 소프트웨어 구성을 해서 이미지를 런칭하여 손쉽게 서버를 구현하도록 함
  * **커뮤니티 AMI** : 누구나 개시가 가능하다.
  * **Quickstart AMI** : AWS에서 많이 사용하는 AMI 리스트들을 볼 수 있음
    *

        <figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p> <strong>Amazon Linux 2 AMI 선택</strong></p></figcaption></figure>


    *

        <figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p> <strong>Amazon Linux 2 AMI 선택</strong></p></figcaption></figure>


    *

        <figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption><p>Quick Start > Amazon Linux 선택</p></figcaption></figure>

#### 인스턴스 설정 3 : 인스턴스 유형&#x20;

인스턴스 유형은 머신의 하드웨어 사양이라고 생각하면 된다.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption><p> 인스턴스 유형</p></figcaption></figure>

#### 인스턴스 설정 4 : 키페어

인스턴스에 원격 접속시 보안 접속을 위해 사용되는 키유형이다.

* 새 키페어 생성 클릭 > RSA 선택 , pem 선택 > 키페어 생성
  *

      <figure><img src="../.gitbook/assets/image (12).png" alt="" width="375"><figcaption><p>  RSA 선택 , pem 선택 , 이름 설정</p></figcaption></figure>


* 키 페어를 생성하고 나면 키페어가 다운로드 된다.(잘 보관하고 있어야한다.)

#### 인스턴스 설정 5 : 네트워크 설정

#### 인스턴스 설정 6 : 방화벽(보안 그룹)

인스턴스에 대한 트레픽을 제어하는 방화벽이다.

* 보안그룹 규칙1 : 모든 위치로 부터 들어온 ssh를 허용해준다.
  *

      <figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>


  * 보안그룹 규칙2 : 모든 위치로 부터 들어온 http를 허용해준다.
    *

        <figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

#### 인스턴스 설정 7 : 스토리지 구성

스토리지에 OS,이미지 등의 AMI가 설치된다.

* 오른쪽 상단의 어드밴스드 클릭

**볼륨 유형 선택**&#x20;

![](<../.gitbook/assets/image (10).png>)

**인스턴스 삭제 여부**

![](<../.gitbook/assets/image (28).png>)

* 종료 시 삭제가 '예'이면   해당 인스턴스를 삭제할 때 스토리지도 같이 삭제가 된다.
* 아니오를 하게 되면 해당 인스턴스가 삭제될 때 스토리지도 삭제되지 않는다.
* 따라서 데이터를 삭제하기를 원하지 않는 경우 "아니오"로 설정해야 한다.

**스토리지 암호화 설정**

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="375"><figcaption></figcaption></figure>

**볼륨 추가**

<figure><img src="../.gitbook/assets/image (21).png" alt="" width="205"><figcaption></figcaption></figure>

**파일 시스템 연결**

<figure><img src="../.gitbook/assets/image (15).png" alt="" width="563"><figcaption></figcaption></figure>



#### 인스턴스 설정 1 : 고급 세부정보

**스팟 인스턴스 요청**

![](<../.gitbook/assets/image (23).png>)-

스팟 인스턴스 요청을 체크하지 않으면 온디맨드 구매 옵션을 선택하게 된다.

**도메인 조인 디렉터리**

* 컴퓨터나 계정을 관리하는 액티브 디렉토리 기능 이 액티브 디렉토리를 조인할건지 말건지에 대한 설정

**IAM 인스턴스 프로파일**

* 설정할 IAM 인스턴스 프로파일을 선택

**호스트 이름 유형**

* 인스턴스가 생성될 때의 컴퓨터 이름
* 사용하려면 네트워크 설정에서 서브넷을 설정해주어야한다.

**인스턴스 자동 복구**

* 인스턴스가 작동하는지 시스템이 확인할 때 상태 확인에 실패하는 경우 자동으로 복구해주는 기능

**종료 동작**

* 만약에 윈도우를 종료한다거나 리눅스를 소프트웨어에서 종료하는 경우 중지를 할건지 종료를 할건지 선택
* 일반적으로 중지를 한다.
* 종료를 하게 되면 인스턴스가 삭제된다.

**최대 절전 중지 방식**

* 노트북의 최대 절전 모드 기능과 동일함

**종료 방지**

* 인스턴스를 실수로 종료하는 것을 방지하는 기능
* 종료할 때 종료방지를 Disable 시켜야 종료가 된다.
* 활성화 체크
  *

      <figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

**중지 방지**

* 인스턴스를 실수로 중지하는 것을 방지하는 기능
* 중지할 때 중지방지를 Disable 시켜야 종료가 된다.
* 활성화 체크

**세부 CloudWatch 모니터링**

* 인스턴스 메모리나 CPU 등의 사용량을 측정하게 되는데 조금 더 세부적으로 측정하게 됨
* 활성화를 하게되면 추가요금 발생&#x20;

**Elastic Inference**

* 머신러닝 관련된 추가적인 기능

**크레딧 사양**

* 인스턴스의 CPU가 고정된 리소스만 사용 가능한데 할당량을 넘기면 Credit을 사용함 이 떄 이 크레딧을 할당량 만큼만 사용할 것인지 또는 무제한으로 사용할 것인지에 대한 선택
* 무제한 사용인경우 할당량이 넘어가게 되면 추가요금 부과

**배치 그룹**

* 인스턴스를 어떻게 물리적으로 배치할것인지에 대한 조합

**용량 예약**

* 인스턴스를 미리 구매해놓을수가 있는데 미리 구매해놓은 인스턴스를 사용하는 기능

**Tenancy**

* 공유된 전용 하드웨어를 사용할 수 있음
* 사용하지 않으면 AWS 데이터센터에 있는 무작위로 비어잇는 물리적인 서버를 사용

**메타데이터**

* 인스턴스와 관련된 정보들을 갖고있는 데이터
* 이 메타데이터값으 ㄹ사용자가 프로그래밍하여 사용할 수 있다.

**사용자데이터**

* 사용자 데이터 아래에 스크립트를 작성해 인스턴스를 시작할 때 사용자가 원하는 스크립트를 실행할 수 잇게 한다.





