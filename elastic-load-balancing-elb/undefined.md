# 가용성과 확장성

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-26 Mon

#### last modified : 2023-06-26 Mon

## \[1] 확장성

### 1) 수직적 확장

<figure><img src="../.gitbook/assets/image (36) (2).png" alt="" width="375"><figcaption><p> 수직적 확장</p></figcaption></figure>

* 자원을 추가하는 방식
* 예시 1
  *   &#x20;EC2 인스턴스 중 CPU나 메모리 사양이 낮은 인스턴스가 있는 경우 이 인스턴스의 메모리나 CPU를

      증가시켜서 더 큰 인스턴스 사양으로 만드는 것
* 예시 2
  * &#x20;EC2 인스턴스를 t2.mirco 에서 t2.large 로 변경하는 것

### 2) 수평적 확장

<figure><img src="../.gitbook/assets/image (29) (3).png" alt="" width="375"><figcaption><p> 수평적 확장</p></figcaption></figure>

* 노드를 **추가**하는 방식
* **EC2 인스턴스 개수**를 늘리는 것(자원을 안 쓰면 다시 줄임)
  * **탄력성**이라고도 함
* 애플리케이션의 확장 방법으로 주로 사용됨
* 클라우드에서 많이 사용하는 확장 방식이다.
  * AWS의 auto scailing (오토 스케일링)

## \[2] 고 가용성 (High Availability)

* 지속적으로 정상 운영이 가능한 상태를 유지하는 것

### 이중화

#### 예시&#x20;

*

    <figure><img src="../.gitbook/assets/image (12) (2).png" alt="" width="375"><figcaption><p> 이중화</p></figcaption></figure>
* 각 가용영역 안에 시스템이 2개씩 있다.
* 가용영역끼리 연결하면 하나의 가용영역에 문제가 생긴경우 다른 가용영역을 사용하여 지속적으로 정상적인 운영이 가능하다.
