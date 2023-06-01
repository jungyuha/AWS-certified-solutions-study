# AWS 결제 및 비용관리 1 : AWS budget

## AWS Budgets(예산)

### 1) 경로

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### 2) 예산 생성

![](<../.gitbook/assets/image (10).png>)

**정해진 비용 기준으로 추적하기**

<figure><img src="../.gitbook/assets/image (11).png" alt="" width="563"><figcaption></figcaption></figure>

### 3) 세부 정보 입력

<figure><img src="../.gitbook/assets/image (12).png" alt="" width="563"><figcaption><p>세부정보 입력</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

### 4) 알림 생성

_**알림 임계값 추가**_ 선택

설정한 금액의 80%를 초과할시 알림이 가도록 설정

&#x20;

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="563"><figcaption></figcaption></figure>

### 5) 작업 설정

특정 임계값에 도달한 경우 알림과 함께 특정 작업을 수행하도록 설정이 가능하다.

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="552"><figcaption></figcaption></figure>

* 알림이 옴과 동시에 EC2를 중지하는 작업
* EC2가 생성된 리전을 클릭한다.

지금은 작업이 없으니 그냥 작업없이 생성한다. 생성된 예산은 다음 메뉴에서 확인 가능

<figure><img src="../.gitbook/assets/image.png" alt="" width="375"><figcaption></figcaption></figure>

