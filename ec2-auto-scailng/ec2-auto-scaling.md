# \[실습] EC2 Auto Scaling 생성

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-07-05 Wed

#### last modified : 2023-07-07 Fri

## 1) 시작 템플릿 생성하기

#### 왼쪽 메뉴 > auto scailing > auto scailing 그룹

* 인스턴스를 생성할 때 시작 템플릿을 이용한다.

### 시작 템플릿 지정하기

<figure><img src="../.gitbook/assets/image (100).png" alt="" width="563"><figcaption><p> 시작 템플릿 생성</p></figcaption></figure>

#### 왼쪽 '인스턴스' 메뉴 > '시작 템플릿' 클릭 > '시작 템플릿 생성' 클릭

*   **시작 템플릿** : auto scailing 그룹에서 ec2 인스턴스를 만들 때 어떠한 이미지를 사용하고

    어떠한 컴퓨팅 옵션이나 설정등을 사용해서 만들지에 대한 템플릿
* 생성 정보
  * 이름 : ASG\_EC2
    * ![](<../.gitbook/assets/image (101).png>)
  * 애플리케이션 및 OS 이미지 : Amazon Linux 2
  * 인스턴스 유형 : t2.micro
    * ![](<../.gitbook/assets/image (94).png>)
  * 키페어 : 이전 시간에 만든 거
    * ![](<../.gitbook/assets/image (82).png>)
  * 네트워크 설정 : 시작 템플릿에 포함하지 않음
  * 보안 그룹 : ssh\_web\_access(ssh,http 허용)
    * ![](<../.gitbook/assets/image (102).png>)
  * 고급 세부 정보
    * 사용자 데이터 : 웹서버를 생성하는 스크립트를 추가한다.
      *

          <figure><img src="../.gitbook/assets/image (83).png" alt="" width="474"><figcaption><p> 웹서버를 생성하는 스크립트</p></figcaption></figure>

## 2) auto scailing 그룹 만들기

<figure><img src="../.gitbook/assets/image (84).png" alt=""><figcaption><p> auto scailing 그룹 생성</p></figcaption></figure>

#### 왼쪽 메뉴 > auto scailing > auto scailing 그룹 > 'auto scailing 그룹 생성' 클릭

* 생성 정보
  * 이름 : ASG
  * 시작 템플릿 : ASG\_EC2(방금 전에 만든 거)
    * ![](<../.gitbook/assets/image (80).png>)
  * 네트워크
    * 시작 템플릿의 정보를 가지고 만든 인스턴스를 어디에 배치할 것인지에 대한 설정이다.
    * 가용영역 및 서브넷 : 서울 리전의 4개의 가용영역 중 어디에 배치할 것인지에 대한 선택을 할 수 있다.
      * 고 가용성을 구현하기 위해서 4개 모두 선택한다.
    * ![](<../.gitbook/assets/image (103).png>)
  * 로드밸런싱 : 오토스케일 그룹을 로드밸런서에 연결한다.
    * 실습에서는 '로드 밸런서 없음'을 선택
  * 상태 확인 : 오토 스케일 그룹에 연결된 EC2나 로드밸런서의 상태를 확인하는 것이다. 특정 인스턴스가 맛이 가면 해당 인스턴스를 종료하거나 자동으로 교체하는 기능을 한다.
    * 상태 확인 유예기간 : 인스턴스가 처음 런칭이 되면 부팅시간이 걸리기 때문에 상태 확인이 되질 않는데 이 상태 확인을 하지 않을 시간을 설정한다.
    * ![](<../.gitbook/assets/image (107).png>)
  * 기본 인스턴스 워밍업 : 인스턴스가 런칭이 되면 초기 부팅 시간이 있기 때문에 cloud Watch 모니터링을 해도 정상 데이터가 아니다.따라서 '기본 인스턴스 워밍업 활성화'를 누른뒤 '300초'를 설정하면 300초 동안은 CPU나 메모리 등 Cloud Watch 지표를 반영하지 않는다.
    * 실습에선 체크하지 않는다.
  * 그룹 크기
    * 원하는 용량 : 1 / 최소 용량 : 1 / 최대 용량 : 1
    * ![](<../.gitbook/assets/image (86).png>)
  * 크기 조정 정책 : 없음
  * 나머지는 모두 기본 설정

### auto scailing 기능 확인

#### 왼쪽  'auto scailing' 메뉴 > 만들어진 auto scailing 그룹 선택

* 인스턴스 관리 탭을 누르면 인스턴스가 1개 만들어진 것을 볼 수 있다.
  * 세부정보에서 원하는 용량 : 1 / 최소 용량 : 1 / 최대 용량 : 1 으로 설정되어 있기 때문이다.
  *

      <figure><img src="../.gitbook/assets/image (93).png" alt="" width="563"><figcaption><p> 인스턴스가 1개 만들어진 것을 볼 수 있다.</p></figcaption></figure>
* 모니터링 탭에서는 오토스케일링과 EC2에 관한 지표가 수집된다.

#### 왼쪽  '인스턴스' 메뉴 > auto scailing 그룹에서 생성된 인스턴스가 실행됨을 확인 > 해당 인스턴스를 클릭

* 하단 '네트워킹' 탭 > 퍼블릭 IP 주소 복사 > 새탭에 붙여넣으면 서버가 기동중임을 확인 할 수 있다.
  *

      <figure><img src="../.gitbook/assets/image (76).png" alt="" width="563"><figcaption><p> 퍼블릭 IP 주소 복사</p></figcaption></figure>


  *

      <figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption><p> 서버가 기동중임을 확인</p></figcaption></figure>

### 용량을 1에서 2로 변경하기

#### 왼쪽 'auto scailing'메뉴 > auto scailing 그룹 > 특정 그룹 클릭 > '세부정보' 탭 > '그룹 세부 정보'의 '편집' 클릭

* 그룹 크기 변경
  * 원하는 용량 : 2 / 최소 용량 : 1 / 최대 용량 : 2
    * ![](<../.gitbook/assets/image (81).png>)
* '활동' 탭 > '작업 기록'의 '새로고침' 클릭 - 인스턴스가 2개로 늘어난다.
  *

      <figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption><p> 인스턴스가 2개로 늘어난다.</p></figcaption></figure>


*



    <figure><img src="../.gitbook/assets/image (85).png" alt="" width="563"><figcaption><p> 인스턴스가 2개로 늘어난다.</p></figcaption></figure>
*

    <figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption><p> 인스턴스가 2개로 늘어난다.</p></figcaption></figure>

### 용량을 2에서 1로 변경하기

<figure><img src="../.gitbook/assets/image (104).png" alt="" width="375"><figcaption><p> 용량을 2에서 1로 변경</p></figcaption></figure>

#### 왼쪽 'auto scailing'메뉴 > auto scailing 그룹 > 특정 그룹 클릭

* '인스턴스 관리' 탭 - 인스턴스를 확인했을 때 1개가 종료되고 있음을 확인할 수 있다.
  *

      <figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption><p>인스턴스가 1개로 줄어든다.</p></figcaption></figure>


  *

      <figure><img src="../.gitbook/assets/image (98).png" alt="" width="375"><figcaption><p> 인스턴스가 1개로 줄어든다.</p></figcaption></figure>
  *

      <figure><img src="../.gitbook/assets/image (89).png" alt="" width="563"><figcaption><p> 인스턴스가 1개로 줄어든다.</p></figcaption></figure>

### 용량이 1인 상태에서 남은 1개의 인스턴스를 종료하기

#### 왼쪽 메뉴 '인스턴스' > 인스턴스 목록에서 실행중인 것을 종료시킨다.

![](<../.gitbook/assets/image (90).png>)

#### 왼쪽 'auto scailing' 메뉴 > 만들어진 auto scailing 그룹 선택

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption><p>인스턴스를 종료시킴</p></figcaption></figure>

* '활동' 탭을 누르면 남은 1개의 인스턴스가 다운이 됐기 때문에 인스턴스를 새로 런칭하는 모습을 확인할 수 있다.
  * 항상 1개의 인스턴스를 유지해야하기 때문이다.
  *

      <figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption><p>다시 인스턴스 1개가 런칭된다.</p></figcaption></figure>
  *

      <figure><img src="../.gitbook/assets/image (87).png" alt="" width="563"><figcaption><p> 다시 인스턴스 1개가 런칭된다.</p></figcaption></figure>



