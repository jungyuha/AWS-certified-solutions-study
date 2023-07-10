# Page 1

<figure><img src="../.gitbook/assets/image (8).png" alt="" width="476"><figcaption><p> 인스턴스 1개가 생성이 되어있다.'</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (22).png" alt="" width="563"><figcaption><p> 용량 사이즈가 모두 1로 설정되어있기 때문이다.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (24).png" alt="" width="504"><figcaption><p> 2개가 런칭이 됐다가 인스턴스 사용량이 적어지면 최소용량인 1개로 런칭이 된다.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="375"><figcaption><p> 스케줄을 걸어 특정 시간대에 해당 용량으로 설정되게끔 한다.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="375"><figcaption><p> 단계 크기 조정 : 작업을 인스턴스의 용량 단위로 증가시키거나 / 백분율 단위로 증가시킬 수 있다.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (32).png" alt="" width="563"><figcaption><p> 지표값이 있다.(평균 CPU 사용률 , 네트워크 , Application Load Balancer 요청 수 등)</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (21).png" alt="" width="563"><figcaption><p> 평균 CPU 사용률이 50% 이상 초과했을 시 인스턴스를 늘리는 조정 정책을 생성한다.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (108).png" alt="" width="375"><figcaption><p>target tracking Policy 생성</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="329"><figcaption><p> target tracking Policy가 생성되고 왼쪽 '세부정보'탭에 따라 해당 용량이 조정된다.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (19).png" alt="" width="440"><figcaption><p> 최대 용량을 3으로 변경한다.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt="" width="563"><figcaption><p> '모니터링'탭 > 'EC2'탭 > CPU 사용률을 높여보기</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (31).png" alt="" width="563"><figcaption><p> 왼쪽 '인스턴스' 메뉴 > '인스턴스' 클릭 > 오토스케일링 그룹에 의해서 실행중인 인스턴스 </p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption><p>EC2 원격 접속</p></figcaption></figure>



\[EC2 Auto Scaling 실습2]

auto scailing 수동 크기 조절 왼쪽 메뉴 > auto scailing > auto scailing 그룹

> 'ASG' 오토스케일링그룹 클릭 > '인스턴스 관리 탭'

* 인스턴스 1개가 생성이 되어있다.
* '세부정보 탭'에 보면 용량 사이즈가 모두 1이기 때문이다.
  * 용량을 원하는 용량 2, 최대 용량을 2로 바꾸면 인스턴스 2개가 런칭이 됐다가 인스턴스 사용량이 적어지면 최소용량인 1개로 런칭이 된다.
  * 최대 용량을 3으로 늘리면 인스턴스 사용량이 많아질 때 3개까지 늘어난다.

auto scailing 자동 크기 조절 왼쪽 메뉴 > auto scailing > auto scailing 그룹

> 'ASG' 오토스케일링그룹 클릭 > '자동크기조절 탭' - 동적 크기 , 예측 크기 , 예약된 작업 3가지로 구성

1. 예약된 작업

* 제일 밑의 '예약된 작업 생성' 클릭
  * 이 '예측 크기'는 인스턴스의 사용률로 집계를 한다.
    * CPU나 네트워크 등의 지표값을 사용량으로 집계한 데이터를 가지고 머신러닝하여 자동으로 예측해서 크기를 조정한다.

2. 예측 크기 조정 영역

* 우측의 '예측 크기 조정 정책 생성' 클릭
  * 용량을 예약된 일정에 따라 작업을 할 수 있다.스케줄을 걸어 특정 시간대에 해당 용량으로 설정되게끔 한다.

3. 동적 크기 조정 영역

* 우측의 '동적 크기 조정 정책 생성' 클릭
  * 용량을 예약된 일정에 따라 작업을 할 수 있다.스케줄을 걸어 특정 시간대에 해당 용량으로 설정되게끔 한다.
* 동적 크기의 3가지 유형
  * 대상 크기 조정(실습 부분)
    * 지표값이 있다.(평균 CPU 사용률 , 네트워크 , Application Load Balancer 요청 수 등)
    * 이 지표 대상값이 임계값에 도달하면 인스턴스를 증가하고 임계값 이하인 경우에는 인스턴스를 줄인다.
    * 평균 CPU 사용률이 50% 이상 초과했을 시 인스턴스를 늘리는 조정 정책을 실습한다.
    * target tracking Policy가 생성되고 왼쪽 '세부정보'탭에 따라 해당 용량이 조정된다.
    * 최대 용량을 3으로 바꾸면 CPU사용량이 50% 넘어간 경우 최대 3개까지 인스턴스가 증가하게 된다.
  * 단계 크기 조정
    * 클라우드 watch 경보를 기반으로 크기를 조정한다.
    * 작업을 인스턴스의 용량 단위로 증가시키거나 / 백분율 단위로 증가시킬 수 있다.
  * 단순 크기
    * 클라우드 watch 경보를 기반으로 크기를 조정한다.
    * 작업을 인스턴스의 용량 단위로 증가시키거나 / 백분율 단위로 증가시킬 수 있다.

### 대상 크기 조정(실습 부분) - 평균 CPU 사용률이 50% 이상 초과했을 시 인스턴스를 늘리는 조정 정책을 실습한다. - 지표값이 있다.(평균 CPU 사용률 , 네트워크 , Application Load Balancer 요청 수 등) - 이 지표 대상값이 임계값에 도달하면 인스턴스를 증가하고 임계값 이하인 경우에는 인스턴스를 줄인다. - target tracking Policy가 생성되고 왼쪽 '세부정보'탭에 따라 해당 용량이 조정된다. - 최대 용량을 3으로 바꾸면 CPU사용량이 50% 넘어간 경우 최대 3개까지 인스턴스가 증가하게 된다. '모니터링'탭 > 'EC2'탭 > CPU 사용률을 높여보기 - 왼쪽 '인스턴스' 메뉴 > '인스턴스' 클릭 - 오토스케일링 그룹에 의해서 실행중인 인스턴스를 확인할 수 있따. - 해당 인스턴스 클릭 > 우측 상단 '연결' 클릭 > 인스턴스 커넥터를 통해 원격 접속
