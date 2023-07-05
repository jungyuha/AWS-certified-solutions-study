# EC2 Auto Scailng 개요

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-07-04 Tue

#### last modified : 2023-07-04 Tue



## \[1] EC2 Auto Scaling

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>  최소 용량 , 원하는 용량 , 최대 용량을 설정한다.</p></figcaption></figure>

* EC2 인스턴스를 자동으로 확장하고 축소하는 기능
* 사용자가 정의한 조정 정책에 따라 인스턴스 수가 증가 되거나 축소된다.
  * **예시**
    * 서버의 로드가 증가하면 EC2 인스턴스 개수가 추가 됨 (Scale out)
    * 서버의 로드가 감소하면 EC2 인스턴스 개수 줄어 듬 (Scale in)
* 최소 용량 , 원하는 용량 , 최대 용량을 설정한다.
  * **예시**
    1. 처음에는 EC2가 3대가 생성이 된다.
    2. 사용량이 적어지면 최소 용량까지 EC2가 줄어든다.
    3. 사용량이 많아지면 최대 용량까지 EC2가 늘어난다.

## \[2] EC2 Auto Scaling 구성 요소

1. <img src="../.gitbook/assets/image (8).png" alt="" data-size="line"> 오토 스케일링 그룹
   * EC2의 인스턴스의 그룹
2. <img src="../.gitbook/assets/image (4).png" alt="" data-size="line"> 시작 템플릿 (런치 템플릿)
   * EC2 서버를 시작하기위한 AMI(Amazon Machine Image)
   *   이 Machine Image를 가지고 auto scailing에서 ec2 인스턴스를 추가하면서 늘려줄 때

       이 템플릿을 가지고 서버를 구성하게 된다.
   * 인스턴스 유형 정보를 가진 템플릿
3. <img src="../.gitbook/assets/image.png" alt="" data-size="line"> 조정 옵션 (조정 정책)
   * Auto Scaling을 실행하기 위한 조건

### EC2 Auto Scaling 설정 순서

1. 시작 템플릿 (런치 템플릿)을 가지고 오토 스케일링 그룹을 만든다.
2. 만들어진 오토 스케일링 그룹을 가지고 조정 정책을 통해서 오토 스케일링을 실행하기 위한 조건을 설정한다.

## \[3] EC2 Auto Scaling - 조정 옵션 (조정 정책)

1. 항상 현재 인스턴스 수준 유지 관리
   * 지정된 수의 실행 인스턴스를 항상 유지하도록 Auto Scaling 그룹을 구성
   * 인스턴스가 비정상 상태임을 확인하면 해당 인스턴스를 종료한 다음 새 인스턴스를 시작
2. 수동 조정
   * 최대, 최소 또는 원하는 용량의 변경 사항만 지정하는 경우 사용
3. 일정을 기반으로 조정
   * 확장 작업이 시간 및 날짜 함수에 따라 자동으로 수행됨
   * **예시**
     * 사용량이 많은 매주 일요일에는 인스턴스 4 대 , 다른 요일에는 2 대 실행
4. 온디맨드 기반 조정
   * 많이 사용함
   * 수요 변화에 맞춰 Auto Scaling 그룹의 크기를 동적으로 조정
   * 동적 조정(Dynamic Scailing) 이라고도 한다.
   * **예시**
     * CPU 사용량을 50% 기준으로 하고 사용량 기준에 따라 EC2 인스턴스 수를 증가하거나 감소시킨다.
5. 예측 조정 사용 (Predictive Scailing)
   * 머신러닝을 사용하여 CloudWatch의 기록 데이터를 기반으로 용량 필요량을 예측

## \[4] EC2 Auto Scaling-동적 조정(Dynamic Scailing)

### (1) 대상 추적 조정 (Target Tracking Scailing)

* 목표값을 지정한다.
* 지정한 지표가 목표값을 초과할 때 한해서 Auto Scaling 그룹을 확장 하는 방식
* **예시**
  * CPU 사용률 목표값을 50% 로 설정한 후 Auto Scaling 그룹이 목표값을 초과하면 EC2 인스턴스 증가
* 사용할 수 있는 지표들
  1. CPU 평균 사용률
  2. 네트워크 인터페이스에서 송 수신한 평균 바이트 수
  3. 로드발란서 요청 수 등

### (2) 단계 조정 (Step Scailing)

* CloudWatch alarm의 지표를 기반으로 Auto Scaling 그룹을 확장 하는 방식
* **예시**
  * CloudWatch alarm의 CPU 사용률이 60% 초과하면 Auto Scaling Group 10%(일정 퍼센테이지) 또는 2개(일정 갯수) 증가
  * CPU 사용률이 30% 이하면 Auto Scaling Group 10% 또는 2 개 감소
* 크기 조정 활동(Scailing 활동) 또는 상태 확인 교체가 진행 중인 동안에도 정책이 추가 경보에 계속 응답할 수 있다.

### (3) 단순 조정 (Simple Scailing)

* CloudWatch alarm의 지표를 기반으로 Auto Scaling 그룹을 확장 하는 방식
* **예시**
  * CloudWatch alarm의 CPU 사용률이 60% 초과하면 Auto Scaling Group 10%(일정 퍼센테이지) 또는 2개(일정 갯수) 증가
  * CPU 사용률이 30% 이하면 Auto Scaling Group 10% 또는 2 개 감소
* 크기 조정 활동(Scailing 활동)이 진행되는 기간에는 응답을 하지 않는다.
*   크기 조정 활동이 시작된 후 정책은 크기 조정 활동 또는 상태 확인 교체가 완료되고

    휴지 기간 (Cooldown Period)이 끝날 때까지 기다린 후 추가 경보에 응답한다.

### (4) Amazon SQS

* 메시징 서비스이다.
* Amazon SQS 대기열의 시스템 로드 변경에 따라 Auto Scaling 그룹을 조정하는 기능

## \[5] EC2 Auto Scaling-조정 휴지 (Scaling Cooldowns)

* EC2 가 증가 또는 감소하는 활동이 발생하면 조정 휴지 기간 (Cooldown Period)을 가짐
  *   이유 : EC2가 증가하게 되면 인스턴스를 런칭하는 데에 걸리는 부팅 시간 동안 CPU 사용량이 많아진다.

      즉, EC2가 부팅하는 시간 동안 Cooldown Period 시간을 가져서

      이 시간 동안 오토스케일링의 지표값을 측정하지 않게된다.
* Cooldown Period가 지나서도 CPU 사용량이 많게되면 그 땐 인스턴스를 증가시킨다.
* 디폴트 조정 휴지 기간(Cooldown Period)은 300 초
* 조정 휴지 기간 동안 Auto Scaling Group은 지표값을 측정하지 않기 때문에 EC2를 종료하거나 시작하지 않는다.
*   EC2 인스턴스가 처음 시작된 다음 안정적인 서비스 상태가 될 때까지 시간이 소요되기 때문에

    EC2가 안정적인 서비스 상태가 될 때까지 스케일링을 하지 않도록 차단하는 역할을 함
* 불필요한 EC2 인스턴스가 많이 생성되거나 갑자기 종료되는 것을 방지 하는 기능을 한다

## \[6] EC2 Auto Scaling-수명 주기 후크

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p> Auto Scaling-수명 주기</p></figcaption></figure>

* Auto Scaling 인스턴스 수명 주기의 이벤트를 인식한 다음 해당 수명 주기 이벤트가 발생할 때 사용자 지정 작업을 수행
* 수명 주기
  * 특정 지표값에 다다라서 Scale Out이 되는 경우 수명 주기에 따라 Pending 상태로 가고 이 Pending이 Proceed로 가게된다. 그리고 이 상태에서 새로운 인스턴스가 런칭된다.그 다음에 EC2는 서비스 상태가 된다.
  *   특정 지표값 이하로 떨어져 Scale In이 되는 경우 terminating 상태로 가고 terminating waiting 단계로

      간 다음에 인스턴스를 terminating한다.
* 인스턴스가 In Service 상태에 가기 전에 추가적인 작업을 수행할 수 있음 (Pending State)
* 인스턴스가 Terminated 상태에 가기 전에 추가적인 작업을 수행할 수 있음 (Terminating State)
* EC2 Auto Scaling 수명 주기 후크를 사용하여 인스턴스 시작 및 종료 시 감사 시스템에 데이터를 보내는 사용자 지정 스크립트 실행
  *   예 : 인스턴스를 시작하거나 종료하는 경우 로그 파일등의 데이터를 백업해야하는 경우 이 수명 주기 후크를

      이용해 인스턴스를 시작하거나 종료할 때 감사 시스템에 데이터를 보내는 사용자 지정 스크립트를 실행하도록 설정한다.
