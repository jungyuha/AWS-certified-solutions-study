# AWS 글로벌 인프라

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-02 Fri

#### last modified : 2023-06-02 Fri

## \[1] 인프라 구성

리전 , 가용영역 , 데이터센터 , 엣지 네트워크로 구성

* 리전 : 전 세계 수십개의 국가에 '리전'을 운영
* 가용영역 : 하나 이상의 데이터 센터의 모음&#x20;

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption><p>안프라 구성</p></figcaption></figure>

## \[2] 리전 : 전 세계 수십개의 국가에 '리전'을 운영

<figure><img src="../../.gitbook/assets/image (9) (2) (1) (1).png" alt=""><figcaption><p>리전</p></figcaption></figure>

* 데이터 센터를 클러스터링 하는 물리적 위치 (서울리전 , 홍콩리전 등)
*   전세계 주요국가에 위치 1개 AWS 리전 => 2 개이상의 가용영역으로 구성

    즉, 리전 안에 가용영역이 존재한다.
* 대부분의 AWS 서비스는 리전을 선택 하여 시작 (예 : EC2 서비스)
*   리전을 선택하지 않는 글로벌 서비스도 있음&#x20;

    (예 : IAM 서비스 => 계정관리 서비스이다. 계정관리는 리전별로 운영할 필요가 없다.)
* 재해복구(DR) 설계에 '리전'을 사용함 => 2개이상의 리전에 시스템을 배치.&#x20;

## \[3] 가용영역  (Availability Zone – AZ)

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption><p>가용영역의 구성</p></figcaption></figure>

* 가용영역 = 하나 이상의 개별 데이터 센터로 구성됨
* 1개의 리전은 2개이상의 가용영역으로 구성 (보통 3\~4개의 가용영역으로 구성)
* 가용영역끼리는 물리적으로 떨어져 있고 고속 네트워크로 연결됨
* **고가용성 설계** = 다중 AZ (Multi-AZ)
  * &#x20;2개이상의 가용영역에 시스템을 배치하는 것을 고강용성 설계라고 한다.
  * (예: EC2를 가용영역1과 가용영역3에 각각 배치할 때)

## \[4] 엣지 로케이션  (Availability Zone – AZ)

<figure><img src="../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption><p>엣지 로케이션</p></figcaption></figure>

* 데이터 센터 안에 있는 물리적인 서버
* 엣지 로케이션에 콘텐츠(데이터)를 캐싱하여 사용자에게 더 짧은 지연 시간으로 콘텐츠를 전송
* 엣지 로케이션은 사용자의 지리적인 근처에 있는 서버이다.(리전에 있는 서버가 아님)
* 글로벌 배포서비스인 AWS CloudFront, Global Accelerator에서 대표적으로 사용 전세계 수백개의 엣지 로케이션을 운영 중
  * 아프리카는 리전이 없지만 엣지 로케이션은 있다.
* 엣지로케이션과 AWS 리전 , 가용영역끼리는 고속 네트워크로 연결되어 있음

#### 엣지 로케이션을 사용하지 않은 전송

<figure><img src="../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

#### 엣지 로케이션을 사용한 전송

<figure><img src="../../.gitbook/assets/image (17) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
