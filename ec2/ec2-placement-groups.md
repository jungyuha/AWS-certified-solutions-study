# EC2 배치그룹(Placement Groups)

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-22 Thu

#### last modified : 2023-06-22 Thu

## \[1] EC2 배치그룹(Placement Groups)

* EC2 인스턴스 배치를 구성하는 방법
*   EC2 인스턴스를 생성하게 되면 AWS의 데이터 센터에 있는 물리적인 서버에 가상머신이 생성이 된다.

    이 가상머신을 물리적인 어떤 서버에 어떤 방법으로 배치할지를 배치그룹을 통해서 구성할 수 있다.
* 일반적으로 배치그룹을 사용하지 않게 되면 EC2 인스턴스가 랜덤하게 할당된다.

### 기본 AWS 서버 구조도

#### 가용영역 > 서버랙 > 서버

<figure><img src="../.gitbook/assets/image (51).png" alt="" width="483"><figcaption><p> 기본 AWS 서버 구조도</p></figcaption></figure>

## \[2] 3가지 유형의 배치 그룹

### 1) 클러스터 배치그룹

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="563"><figcaption><p> 클러스터 배치그룹</p></figcaption></figure>

* 고성능 네트워크 연결로 이루어진 인스턴스 묶음
* 근접한 서버를 고속 네트워크로 연결하여 그룹화하는 것
*   클러스터 배치그룹을 사용하게 되면 가까운 거리에 있는 물리적 서버에 EC2 서버가 할당이 되고

    이 EC2 물리적 서버끼리는 고속 네트워크로 연결이 된다.
* 가까운 거리에 있는 물리적 서버의 EC2 인스턴스가 할당되므로 네트워크 지연 시간이 매우 짧다.
* 짧은 대기시간이 필요한 고성능 컴퓨팅 (HCP) 등에 적합하다.
*   일반적으로 배치그룹을 사용하지 않게 되면 EC2 인스턴스가 랜덤하게 할당되므로 네트워크 지연 시간이

    클러스터 배치그룹에 비해 길다.

### 2) 파티션 배치그룹

<figure><img src="../.gitbook/assets/image (1) (2).png" alt="" width="375"><figcaption><p> 파티션 배치그룹</p></figcaption></figure>

* 인스턴스 그룹을 하드웨어를 공유하지 않는 파티션 단위로 분할
* 배치그룹을 파티션으로 나눈다. 이 파티션 안에 인스턴스를 할당하게 된다.
* 하드웨어를 파티션으로 그룹화해서 배치그룹을 만드는 방식이다.
*   이 파티션끼리는 서버랙에 있는 서로 다른 하드웨어를 사용하게 된다.

    즉, 하드웨어를 다른 파티션끼리 공유하지 않는다.
*   하나의 하드웨어에 장애가 발생해도 다른 파티션에 있는 하드웨어에는 영향이 없다.

    즉, 파티션 간의 장애의 영향을 분리할 수 있다.
* 하둡 등의 빅데이터 분산처리 시스템에 사용된다.

### 3) 분산형 배치그룹

<figure><img src="../.gitbook/assets/image (6) (2).png" alt="" width="375"><figcaption><p> 분산형 배치그룹</p></figcaption></figure>

* 인스턴스 그룹을 별개의 서버랙 단위로 분할
* **예시 :** 3개의 서버렉이 있으면 서버렉 단위로 분산그룹을 만든다.
* 같은 서버렉의 서버를 그룹화하는 방식이다.
*   서버가 서로 다른 서버렉에 있기 때문에 EC2 인스턴스를 서로 다른 분산 그룹에 생성하면

    다른 서버렉에서 생성된다.
*   분산그룹끼리 서버렉을 공유하지 않기 때문에 서버렉 단위로 장애가 발생하는 경우

    다른 분산 그룹에 영향을 주지 않는다.
* 매우 중요하고 고가용성이 필요한 애플리케이션에 적합

## \[3] 배치그룹 생성하기

#### EC2 대시보드 > 왼쪽 메뉴 '네트워크 및 보안' > '배치그룹' > '배치그룹 생성' 클릭

아래 옵션으로 3개의 배치그룹을 생성한다.

* 이름 : Cluster / 배치전략 : 클러스터

<figure><img src="../.gitbook/assets/image (8) (4).png" alt="" width="563"><figcaption><p>클러스터 배치그룹</p></figcaption></figure>

* 이름 : Partition / 배치전략 : 파티션 / 파티션수 : 4

<figure><img src="../.gitbook/assets/image (53).png" alt="" width="563"><figcaption><p>파티션 배치그룹</p></figcaption></figure>

* 이름 : Spread / 배치전략 : 분산

<figure><img src="../.gitbook/assets/image (64).png" alt="" width="563"><figcaption><p>분산 배치그룹</p></figcaption></figure>

#### 왼쪽 메뉴 '인스턴스' > '인스턴스 시작' 클릭 > '고급 세부 정보' 탭 > '배치그룹' 선택

* 오른쪽 인스턴수 개수를 10개로 설정한다.

<figure><img src="../.gitbook/assets/image (7) (1).png" alt="" width="375"><figcaption><p> 인스턴수 개수를 10개로 설정</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4) (2).png" alt=""><figcaption><p> '배치그룹' 선택</p></figcaption></figure>

1. Cluster 선택
2. Partition 선택 > 파티션수 설정
3. Spread 선택
