# Amazon Machine Image(AMI)

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-22 Thu

#### last modified : 2023-06-22 Thu



## \[1] Amazon Machine Image(AMI)이란 ?

* OS,애플리케이션 , 서버 프로그램 설정 등이 미리 구성된 이미지
* EC2 인스턴스 생성시 가장 먼저 선택한다.
*   AMI를 사용하면 EC2 인스턴스를 시작시 OS를 따로 설치한다거나 서버 소프트웨어 등을

    별도로 설정할 필요가 없다.
* 이미지를 로딩만 시켜 빠르게 인스턴스를 실행할 수 있다

## \[2] AMI 3가지 유형

### 1. AWS에서 제공하는 AMI

* 리눅스나 윈도우 인스턴스를 생성할 떄

### 2. AWS 마켓 플레이스 AMI

* thirdParty 즉 , AWS가 아닌 소프트웨어 회사에서 만들어 놓은 것을 판매하는 마켓 플레이스 AMI

### 3. AWS 커스텀 AMI

* 사용자가 직접 만드는 AMI
*   예시1 : 사용자가 웹서버를 구축한 경우 그 웹서버를 이미지로 만들어 그 이미지로 쉽게 다른 인스턴스를

    생성할 수 있게 한다.
* 운영중인 EC2 인스턴스를 커스텀 AMI 로 만들어서 동일한 환경으로 구성된 EC2를 빠르게 시작할 수 있다.

## 4. 콘솔에서 AMI 둘러보기

#### EC2 대시보드 > '인스턴스 시작' 클릭 > '애플리케이션 및 OS 이미지' 탭 > '더 많은 AMI 찾아보기' 클릭

<figure><img src="../.gitbook/assets/image (41).png" alt="" width="375"><figcaption><p>애플리케이션 및 OS 이미지 탭</p></figcaption></figure>

#### quickstart ami : aws에서 일반적으로 제공하고 또 많이 사용하는 ami

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p> quickstart ami</p></figcaption></figure>

#### &#x20;내 ami : 사용자가 직접 인스턴스에서 ami를 만들어서 업로드하여 사용할 수 있다.

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption><p> 내 ami</p></figcaption></figure>

#### 마켓플레이스 ami&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p> 마켓플레이스 ami </p></figcaption></figure>

#### 커뮤니티 ami : 누구나 공유와 게시가 가능한 ami

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption><p> 커뮤니티 ami</p></figcaption></figure>

### 내 인스턴스의 스냅샷 만들기 (백업 개념과 동일)

#### 왼쪽 메뉴 'Elastic Block Store' > '스냅샷' 클릭

* **왼쪽 메뉴 'Elastic Block Store' > 볼륨** 탭 내에 있는 EBS 볼륨을 백업을 해서 스냅샷을 만들어준다.
* 이 스냅샷을 AMI 이미지로 컨버팅을 하면 이 이미지를 가지고 인스턴스를 새로 만들 때 사용할 수 있다.
