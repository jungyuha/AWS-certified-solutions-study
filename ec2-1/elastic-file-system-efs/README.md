# Elastic File System (EFS)

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-07-17 Mon

#### last modified : 2023-07-17 Mon



## \[1] Elastic File System (EFS)

* 리눅스 환경의 EC2 인스턴스에서 연결하기 위한 네트워크 파일 스토리지
  * 리눅스 OS에서만 연결이 가능하다.
* Network File System(NFS) 프로토콜을 지원한다.
* 여러 가용영역에 있는 수십 수백대의 EC2를 연결할 수 있다.
* EFS는 보안그룹을 통해 인스턴스에 연결한다.
  * 보안 그룹에서 인파운드 트래픽이나 아웃바운드 트래픽을 필터링할 수 있다.
* EC2 외에 Linux 방식의 온 프레미스 서버에서도 연결이 가능하다.

#### 그림 예시

여러 가용영역이 있는 상태 및 회사의 데이터 센터인 온프레미스도 있다고 가정한다.

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption><p> 그림 예시</p></figcaption></figure>

* NFS 프로토콜을 통해서 EFS에 연결할 수 있다.

## \[2] 성능 및 스토리지 클래스

### (1) 스토리지 클래스의 여러가지 유형

위에서부터 아래로 내려갈수록 비용이 저렴해진다.

* 표준 스토리지(standard)
  * 3개의 가용영역에 데이터를 중복해서 저장 -> 고가용성을 달성할 수 있다.
  * 자주 액세스하는 파일을 저장하는 데 사용
* 표준 IA (Standard Infrequent Access)
  * 3개의 가용영역에 데이터를 중복해서 저장&#x20;
  * 자주 액세스하지 않는 파일을 저장하는 데 사용
  * 표준보다 비용이 더 저렴하다.
* One Zone 스토리지 클래스
  * 1 개의 가용영역에 데이터 저장
    * 1개의 가용영역에 문제가 생기면 데이터가 손실될 수 있다.
  * 자주 액세스하는 파일을 저장하는 데 사용
* One Zone IA (One Zone Infrequent Access)
  * 1 개의 가용영역에 데이터 저장
  * 자주 액세스하지 않는 파일을 저장하는 데 사용&#x20;

데이터 비용을 절약하기 위해서 EFS는 수명주기 관리 정책 또는 EFS 지능형 계층화 (Intelligent Tiering) 을 사용해 자주 사용하지 않는 데이터를 다른 스토리지 클래스로 자동 전환이 가능하다.

* 자주 사용하지 않는 데이터를 표준 스토리지에 저장했다가 30일이나 60일 뒤에 표준 IA나 원존 IA로 이동하는 자동 전환 기능을 이용할 수 있다.

## \[3] 성능 모드 : I/O 읽기 쓰기 속도

* ### 높은 성능의 처리가 필요한 빅데이터 분석 애플리케이션 등에 사용
  * 일반적인 I/O 성능
* 최대 I/O 성능 모드 (Max I/O performance mode)
  * 높은 성능의 처리가 필요한 빅데이터 분석 애플리케이션 등에 사용

### \[4] 처리량 모드 : 파일 시스템의 처리량 MiB

• 기본 버스팅 처리량 모드 파일 용량이 커짐에 따라 자동으로 처리량을 확장

• 프로비저닝된 모드 저장된 데이터의 양과 상관없이 고정으로 처리량을 지정
