# Target Groups 개요

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-27 Tue

#### last modified : 2023-06-27 Tue

## Target의 유형 4가지

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption><p> Target의 유형 4가지</p></figcaption></figure>

1. **인스턴스**
   * 개별 인스턴스 (EC2 Instance)
   * 인스턴스 모음 (EC2 Auto Scailing Groups)
2. **ip 주소**
   * (private IP)Local VPC CIDR
   * Public IP 주소
3. **Lambda(서버리스 컴퓨팅)**
4. **Application Load Balancer**
   * 로드 발란서 뒤에 Application Load Balancer을 연결할 수도 있다.

## Target에 대한 프로토콜 지정

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption><p> Target에 대한 프로토콜 지정</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24).png" alt="" width="367"><figcaption><p>각 로드발란서의 프로토콜 설정</p></figcaption></figure>

#### ALB(Application Load Balancer)

* web 트래픽을 다루기 때문에 HTTP,HTTPS 프로토콜을 선택한다.

#### NLB(Network Load Balancer)

* TCP,TLS 등등 프로토콜을 선택한다.

#### GWLB(GateWay Load Balancer)

* GENEVE 프로토콜을 선택한다.

## 상태 검사 (Health Checks)

<figure><img src="../../.gitbook/assets/image (21).png" alt="" width="563"><figcaption><p> 상태 검사 (Health Checks)</p></figcaption></figure>

* 등록된 Target( 대상 ) 에게 상태 확인 메시지를 보내서 대상의 상태를 확인한다.

#### 예시 1 : EC2 인스턴스가 정상인지 비정상인지 확인한다.

#### 예시 2 : ALB에서 HTTP나 HTTPS 프로토콜을 서버에 보내게 되면 웹 접속이 잘 되고있는지 확인할 수 있다.

## 속성(Attributes)

ALB(Application Load Balancer)나 NLB(Network Load Balancer)에 타겟 그룹을 만들게 되면 속성값을 설정할 수 있다.

### 1) ALB(Application Load Balancer)의 HTTP/HTTPS 프로토콜에서 타겟그룹을 만든 경우

#### 1. 등록 취소 지연(Deregistration delay/Connecting Draining)

* Auto Scaling 축소 등으로 Deregistration 된 인스턴스에 더 이상의 요청을 보내지 않도록 하는 기능
* 해당 인스턴스에 진행중이 요청이 있을 경우 설정해 놓은 시간동안 연결이 유효상태가 되지 않으면 해당 인스턴스에 연결 요청을 하지 않음
*   만약 이 로드발란서 뒤에 오토 스케일링을 연결한 경우 오토 스케일링 뒤의 EC2가 증가하거나 축소를

    하게 될 것인데, 축소가 되면 로드 발란서과 연결된 EC2 인스턴스가 없어지게 된다.

    *   이 경우에 만약에 이 인스턴스에 클라이언트가 연결된 요청이 있을 경우 특정시간동안 연결이 진행되지 않은

        경우 인스턴스에 연결요청을 하지 않게 된다.

#### 2. 느린 시작 기간 (Slow start duration)

* 기본적으로 대상은 대상 그룹으로 등록되자 마자 전체 요청 공유를 받기 시작하고 초기 상태 확인을 전달
*   로드 발란서 뒤의 타겟 그룹이 바로 등록이 된 경우 트래픽을 한꺼번에 보내지 않고 점진적으로 보낼 수 있게 하는

    기능
* 느린 시작 모드에서는 로드 밸런서가 대상으로 보낼 수 있는 요청의 수를 선형으로 증가시킨다.
*   예를 들어 , 타겟 그룹에 인스턴스가 바로 생성된 경우 트래픽을 한꺼번에 바로 보내게 되면 시스템이 과부하

    걸릴 수도 있다. 따라서 점진적으로 시스템 가동이 완전히 된 이후에 트래픽을 받을 수 있도록 요청 수를 선형적으로 증가시킨다.

#### 3. 알고리즘

* 라운드 로빈 (Round Robin): 일정 시간마다 라우팅을 변경
  * 로드발란서 뒤에 인스턴스가 여러개 있으면 일정시간마다 서로 다른 인스턴스로 라우팅을 변경하는 것
* 최소 미해결 요청 (Least Outstanding Requests): 처리하고 있는 요청이 가장 적은 대상에게 라우팅

#### 4. 고정(Stickiness Sessions / Session Affinity)

* (클라이언트) - (로드발란서) - (서버들)
*   이 클라이언트가 로드발란서에 의해 특정 서버에 연결되어있는 경우 이 연결된 서버와 작업이 끝날 때까지 요청을

    계속 동일한 인스턴스로 연결해주는 기능
* 클라이언트가 세션을 유지한 상태라면 모든 요청을 동일한 인스턴스로 유지하는 기능
* 세션 유지를 위해 쿠키를 사용하기에 클라이언트에서 쿠키를 지원해야 함
* 세션 데이터를 잃지 않으려는 상태정보를 유지하는 서버에 적합
* 예 : 쇼핑몰의 장바구니 , 데이터 베이스에 연결한 경우 (다른 서버로 바뀌면 데이터를 잃게 된다.)

### 2) NLB(Network Load Balancer)의 TCP/UDP/TLS 프로토콜에서 타겟그룹을 만든 경우

#### 1. 등록 취소 지연 (Deregistration delay)

* ALB와 동일하다.
* Auto Scaling 축소 등으로 Deregistration 된 인스턴스에 더 이상의 요청을 보내지 않도록 하는 기능
*   해당 인스턴스에 진행중이 요청이 있을 경우 설정해 놓은 시간동안 연결이 유효상태가 되지 않으면

    해당 인스턴스에 연결 요청을 하지 않음

#### 2. 등록 해제 시 연결 종료 (Connection termination on deregistration)

* 등록 취소 지연(ex:300초)에 도달 했을 때 NLB가 활성 연결을 종료하는 기능

#### 3. 프록시 프로토콜 v2

#### 4. 클라이언트 IP 주소 보존 Preserve client IP addresses)

* 이 로드 발란서에 접속하는 모든 트래픽의 클라이언트 IP를 애플리케이션으로 전달하는 기능
  * 애플리케이션 : 로드 발란서 뒤에 있는 서버들

#### 5. 고정(Stickiness Sessions / Session Affinity)

* ALB와 동일하다.
* 클라이언트가 세션을 유지한 상태라면 모든 요청을 동일 한 인스턴스로 유지하는 기능
* 세션 유지를 위해 쿠키를 사용하기에 클라이언트에서 쿠키를 지원해야 함
* 세션 데이터를 잃지 않으려는 상태정보를 유지하는 서버에 적합
