# Instance Store

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-07-17 Mon

#### last modified : 2023-07-14 Mon



## \[1] Instance Store

* EC2의 블록 수준의 임시 스토리지
  *   때문에 인스턴스를 중지하거나 최대 절전 모드로 전환하거나 종료하면 인스턴스 스토어의

      모든 스토리지 블록이 리셋된다.
* EC2의 특정 인스턴스 유형은 Instance Store 라고 하는 스토리지를 가지고 있음
* Instance Store 는 서버에 직접 장착되어 있는 물리적 SSD 또는 HDD 스토리지
  * AWS 데이터 센터에 서버가 있고 서버에 EC2 가상머신이 생성된다.
  * 이 가상머신에 생성되는 서버에 직접 장착되어있는 SSD 또는 HDD 스토리지이다.
* Instance Store 는 서버에 직접 장착되어 있어 IOPS 성능이 매우 높은 고성능 스토리지이다.
* 임시 파일을 보관하는 가장 빠른 성능의 저장 옵션
*   Instance Store 는 EC2 인스턴스가 종료되면 데이터가 삭제되므로 영구적인 저장소가 아닌 고성능을 요구하는

    애플리케이션의 임시 저장소로 적합하다.

    *   예시 : 초당 수백 만개의 트랜잭션을 지원하는 I/O 처리량이 높은 데이터 베이스의 데이터의

        임시 스토리지 옵션으로 사용된다.
*   만약 중요한 장기 데이터의 경우에는 Instance Store 가 아닌 Amazon S3, Amazon EBS, Amazon EFS

    등의 데이터 스토리지를 사용한다.

## \[2] AWS Console에서 Instance Store 확인하기

#### 왼쪽 메뉴 '인스턴스' > '인스턴스 유형' 클릭 > '스토리지' 항목

* 인스턴스 스토리지가 연결되어있다는 의미이다.

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption><p> 스토리지</p></figcaption></figure>

#### 왼쪽 메뉴 '인스턴스' > '인스턴스 유형' 클릭 > 특정 인스턴스 유형 선택 (c5d.large) > 오른쪽 상단 '작업' > '인스턴스 시작'

<figure><img src="../.gitbook/assets/image (62).png" alt=""><figcaption><p> 특정 인스턴스 유형 선택 (c5d.large) </p></figcaption></figure>

* c5d.large의 인스턴스를 시작하게 된다.

#### '인스턴스 시작' 화면 > '스토리지 구성' 탭 > 오른쪽 상단 '어드밴스드' > '인스턴스 스토어 볼륨' > '세부정보 표시'

<figure><img src="../.gitbook/assets/image (48).png" alt="" width="563"><figcaption><p> 오른쪽 상단 '어드밴스드'</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (61).png" alt="" width="563"><figcaption><p> '인스턴스 스토어 볼륨' > '세부정보 표시'</p></figcaption></figure>

* ephemeral0 라는 인스턴스 스토어 볼륨이 추가된 것을 확인할 수 있다.

<figure><img src="../.gitbook/assets/image (49).png" alt="" width="563"><figcaption><p> ephemeral0 라는 인스턴스 스토어 볼륨이 추가된 것을 확인할 수 있다.</p></figcaption></figure>

