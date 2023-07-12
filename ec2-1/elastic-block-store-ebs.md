# Elastic Block Store (EBS) 개요

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-07-12 Wed

#### last modified : 2023-07-12 Wed

## \[1] Elastic Block Store (EBS) 개요

* EC2 인스턴스에 연결되는 가상 블록 스토리지
* EC2인스턴스 시작 시 AMI 가 설치 되는 EBS에 루트 부트 볼륨이 생성됨
*   여러개의 EBS 볼륨을 생성하여 하나의 EC2 에 추가 연결 가능

    * 하나만 생성하는 게 아니라 볼륨을 여러개 생성해서 하나의 EC2에 연결할 수 있다.

    <figure><img src="../.gitbook/assets/image (1).png" alt="" width="291"><figcaption><p> 하나만 생성하는 게 아니라 볼륨을 여러개 생성해서 하나의 EC2에 연결할 수 있다.</p></figcaption></figure>
* EBS와 EC2 는 동일한 가용영역에 있어야 연결 가능
* 스냅샷 기능을 통해 EBS 볼륨을 백업할 수 있다.
* 수명주기 관리자 (Data Life Cycle Manager) 정책을 통해 스냅샷 생성 일정을 자동화 가능
  * 매일/주별 백업 설정 등 백업을 자동화할 수 있다.
* AWS Key Management Service (KMS)를 이용해 EBS 볼륨 암호화 가능

## \[2] Elastic Block Store (EBS) 유형

* 성능에 따라 여러가지 볼륨 유형이 있다.
* 볼륨 유형에 따라 제공되는 용량 ( 크기 ), IOPS, 최대 처리량이 다르다.
* EBS에 AMI가 설치되는 부트볼륨은 범용 SSD, 프로비저닝 된 SSD 만 지원한다.
* 여러개 EBS 볼륨을 하나의 EC2인스턴스에 연결하는 기능을 EBS 다중 연결이라고 한다.
  * 이 다중 연결은 프로비저닝 된 SSD 만 지원한다.

#### 1) SSD TYPE

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="380"><figcaption></figcaption></figure>

* 일반적으로 속도가 빠르다.
* IOPS : 디스크를 읽고 쓰는 속도
* 범용 SSD
  * 일반적인 용도로 범용 SSD를 사용한다.
* 프로비저닝된 SSD
  * IOPS가 더 상대적으로 빠르다.
  * 고성능 처리에 사용된다.

#### 2) HDD TYPE

<figure><img src="../.gitbook/assets/image.png" alt="" width="383"><figcaption></figcaption></figure>

* 일반적으로 속도가 느리다. 비용이 상대적으로 저렴하다.
* 처리량 최적화 HDD
  * IOPS 속도가 느리다.
  * 저 비용이다.
* 콜드 HDD
  * IOPS 속도가 제일 느리다.
  * 최저 비용이다.

## \[3] EBS 다중연결 (EBS Multi-Attach)

* 일반적으로 하나의 EC2인스턴스에 여러 개의 EBS 볼륨을 연결한다.
*   특정한 조건 아래서 하나의 EBS 볼륨이 여러개의 EC2인스턴스와 동시에 연결할 수 있는 기능이다.

    <figure><img src="../.gitbook/assets/image (3).png" alt="" width="375"><figcaption><p> 하나의 EBS 볼륨이 여러개의 EC2인스턴스와 동시에 연결</p></figcaption></figure>

#### 제약 조건

* 다른 EBS와 마찬가지로 동일한 가용 영역 내에서만 연결이 가능하다.
  * EC2인스턴스들이 동일한 가용 영역 내에 있어야 한다.
* 모든 EC2 유형을 연결할 수는 없고 Nitro 기반의 Linux 인스턴스만 연결이 가능하다.
  * Nitro라는 기능을 지원하는 인스턴스 유형만 연결이 가능하다.
* 모든 EBS 유형을 지원하지는 않고 프로비저닝 된 IOPS SSD 만 지원한다.
* 동시에 최대 16대의 EC2 인스턴스 연결이 가능하다.
* 쓰이는 경우&#x20;
  *   여러 EC2 인스턴스가 하나로 클러스터링된 Linux Application에서 하나의 EBS 볼륨에 동시에

      읽기 쓰기 작업이 필요한 경우

## \[4] EBS Snapshots 기능

* EBS 볼륨의 데이터를 백업하는 기능
* 이 백업된 스냅샷을 다른 가용영역이나 다른 리전에 복사가 가능하다.
* 이 백업된 스냅샷을 커스텀 AMI 이미지로 만들어서 EC2 인스턴스를 생성할 때 이 AMI 이미지를 생성할 수 있다.
* 백업된 스냅샷을 가지고 EC2 인스턴스를 새로 생성할 수 있다.

### 1) EBS 스냅샷 아카이브 (EBS Snapshot Archive)

* 일반적으로 스냅샷을 백업하면 표준 저장소에 저장되는데 백업이니까 자주 액세스하지 않는 경우가 있을 것이다.
* 자주 액세스 하지 않는 스냅샷을 저렴한 아카이브 스토리지 계층에 보관
*   이 아카이브 계층은 최소 과금 기간이 90일이기 때문에 90 일 이상 저장할 계획인 경우에

    그리고 액세스할 필요가 거의 없는 스냅샷의 경우에 사용한다.
* 최대 75% 비용이 더 저렴하다.

### 2) EBS 스냅샷 휴지통 (Recycle Bin for EBS Snapshot )

* 실수로 삭제한 스냅샷을 휴지통에 보관해서 복구 가능
* 삭제된 파일을 1 일 부터 365 일까지 보관 기간 설정 가능

### 3) EBS 빠른 스냅샷 복원 (EBS Fast Snapshot Restore-FSR)

* 지연시간을 최소화 하여 빠르게 스냅샷으로부터 EBS 볼륨을 복원하는 기능
* 이 기능의 경우 추가적인 비용이 부과된다.

## \[5] 암호화 되지 않은 EBS 볼륨 암호화

* 일반적으로는 암호화하는 것을 추천한다.
* 사용중인 EBS 볼륨을 바로 암호화할 수는 없다.

### 암호화 순서

1. EBS 볼륨 스냅샷 생성
2.  이 볼륨을 암호화한 후 암호화된 스냅샷으로부터 새 EBS 볼륨을 생성

    또는

    암호화 되지 않는 스냅샷에서 새 EBS 볼륨을 생성할 때 암호화 선택
3. 새 EBS 볼륨을 EC2 인스턴스에 연결\


\


