# Load Balancer 개요

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-26 Mon

#### last modified : 2023-06-27 Tue

## Load Balancer 개요

* 트래픽을 분산하는 서비스

#### 예시 : Load Balancer

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption><p>Load Balancer</p></figcaption></figure>

* 인터넷에 연결되어있는 클라이언트들이 있다.
*   인터넷이 마주치는 로드 발란서 : **External 로드 발란서**

    * 인터넷을 통해 접속하는 클라이언트가 EC2 인스턴스에 골고루 접속되게 분산시킨다.

    <figure><img src="../.gitbook/assets/image (27).png" alt="" width="249"><figcaption><p>External 로드 발란서</p></figcaption></figure>
*   AWS 내부에서 동작하는 로드발란서 : **Internal 로드 발란서**

    *   EC2 인스턴스가 하나의 데이터베이스에 모두 연결되는 게 아니라 Internal 로드 발란서를 통해서

        적절하게 트래픽을 라우팅 해준다.

    <figure><img src="../.gitbook/assets/image (51).png" alt="" width="235"><figcaption><p><strong>Internal 로드 발란서</strong></p></figcaption></figure>
* 만약에 로드발란서가 없는 경우 여러 클라이언트가 동일한 서버로 접속을 하여 트래픽이 과부하 될 수 있다.
* EC2 인스턴스 , 컨테이너 , IP 주소 등 여러 대상으로 자동으로 분산 가능
* 비정상 대상을 감지하면 , 해당 대상으로 트래픽 라우팅을 중단하고 대상이 다시 정상으로 감지되면 트래픽을 해당 대상으로 다시 라우팅한다.

#### 예시 : 만약 제일 위에 있는 PC가 로드 발란서를 통해 제일 위에 있는 EC2 인스턴스에 연결하고있다고 가정할 때

<figure><img src="../.gitbook/assets/image (67).png" alt="" width="563"><figcaption><p>고가용성 구현</p></figcaption></figure>

*   이 인스턴스가 문제가 생겨서 접속이 안되거나 다운이 된 경우 로드발란서가 자동으로 트래픽을 정상적인

    인스턴스로 라우팅 시킨다.
*   **고가용성 구현** : 로드발란서가 분산시키는 대상(EC2 인스턴스 ..등등)울 원하는 모습으로 묶어 가용영역에

    배치할 수 있다.

## AWS에서의 Load Balancer 종류 4가지

### 1) Application Load Balancer

<figure><img src="../.gitbook/assets/image (8) (1) (2).png" alt="" width="296"><figcaption><p>Application Load Balancer</p></figcaption></figure>

* 시험에 나오는 부분(기출)
* Layer 7 에서 동작한다.
  * Application Layer에서 동작한다.
* HTTP, HTTPS 트래픽을 다룬다.
* HTTP Header Content를 사용해 라우팅 요청을 처리
* 웹 애플리케이션 , 서비스에 적합
* 웹 서비스를 구축하는 경우 Application Load Balancer룰 사용한다고 생각하면 된다.

### 2) Network Load Balancer

<figure><img src="../.gitbook/assets/image (36).png" alt="" width="293"><figcaption><p>Network Load Balancer</p></figcaption></figure>

* 시험에 나오는 부분(기출)
* Layer 4 에서 동작한다.
* 네트워크 레이어이기 떄문에 TCP, UDP, TLS을 다룬다.
* Protocol, Port Number를 사용해 라우팅 요청처리
*   Application Layer와는 달리 네트워크 레이어이기 떄문에 동작 속도가 빨라 수백만의 대용량 트래픽 처리에

    적합하다.(게임 애플리케이션 등 ..)

### 3) Gateway Load Balancer

<figure><img src="../.gitbook/assets/image (2) (2).png" alt="" width="292"><figcaption><p>Gateway Load Balancer</p></figcaption></figure>

* Layer 3 에서 동작한다.
  * Gateway Load Balancer Endpoint
* Layer 4 에서 동작한다.
  * Gateway Load Balancer
* GENEVE protocol을 사용하여 encapsulation 트래픽 전송
* GENEVE protocol은 암호화되어서 트래픽을 전송한다.
* Gateway Load Balancer 뒤에 IPS나 IDS 등의 보안 검사를 위한 애플리케이션이 위치한다.
  * 따라서 보안 검사를 위한 용도로 해당 로드 발란서를 사용한다.
* 보안 검사를 위한 방화벽이나 IPS ,IDS 등에 사용하는 로드발란서이다.
* Transparency한 네트워크 게이트웨이를 제공하므로 보안 검사를 위한 방화벽 , IPS, IDS 등의 원본 패킷의 데이터가 중요한 가상 어플라이언스에 적합

### 4) classic Load Balancer

<figure><img src="../.gitbook/assets/image (16).png" alt="" width="291"><figcaption><p>classic Load Balancer</p></figcaption></figure>

* 이전 세대 로드발란서라서 더 이상 사용하지 않는다.
* Layer 4 , Layer 7 에서 동작한다.
* HTTP, HTTPS, TCP, TLS
* Protocol, Port Number를 사용해 라우팅 요청 처리
* 이전 세대 EC2 Classic 네트워크에서 사용

## Elastic Load Balancer 구성 (Gateway Load Balancer 제외 )

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption><p>Elastic Load Balancer 구성</p></figcaption></figure>

* **클라이언트**가 있고 **Listener(로드 발란서)**와 **Target Group**이 있다.

### Listener(로드 발란서)

* 연결 요청을 확인하는 프로세스이다.
* 클라이언트에서 로드 발란서에 연결을 요청하면 리스너가 확인을 한다.
* 리스너가 클라이언트와 로드밸런스 간의 연결을 위한 프로토콜 및 포트 번호를 확인한다. 즉 , 클라이언트와 로드밸런스 간의 프로토콜 및 포트 번호로 구성되어 있다.
* 또한 로드밸런스와 Target간의 연결을 위한 프로토콜 및 포트 번호를 확인한다. 즉, 로드밸런스와 Target간의 프로토콜 및 포트번호로 구성되어있다.
* 이 리스너는 Target 그룹과 연결이 된다.

### Target Group

* 대상(targer)의 모임
  * EC2 인스턴스 , auto scailing(EC2 인스턴스의 모임) , ip 주소 , 애플리케이션 로드발란서.. 등등
* 로드 발란서가 리소스(EC2 인스턴스..)와 연결이 되어야한다.
