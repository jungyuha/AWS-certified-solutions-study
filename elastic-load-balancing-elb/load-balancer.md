# Load Balancer 개요

<figure><img src="../.gitbook/assets/image (33).png" alt="" width="375"><figcaption><p>고가용성 구현</p></figcaption></figure>

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-26 Mon

#### last modified : 2023-06-26 Mon

## Load Balancer 개요

* 트래픽을 분산하는 서비스
  * 예시 1.
    * 인터넷에 연결되어있는 클라이언트들이 있다.
    * 인터넷이 마주치는 로드 발란서 : External 로드 발란서
      * 인터넷을 통해 접속하는 클라이언트가 EC2 인스턴스에 골고루 접속되게 분산시킨다.
    * AWS 내부에서 동작하는 로드발란서 : Internal 로드 발란서
      * EC2 인스턴스가 하나의 데이터베이스에 모두 연결되는 게 아니라 Internal 로드 발란서를 통해서 적절하게 트래픽을 라우팅 해준다.
  * 만약에 로드발란서가 없는 경우 여러 클라이언트가 동일한 서버로 접속을 하여 트래픽이 과부하 될 수 있다.
* EC2 인스턴스 , 컨테이너 , IP 주소 등 여러 대상으로 자동으로 분산 가능
* 비정상 대상을 감지하면 , 해당 대상으로 트래픽 라우팅을 중단하고 대상이 다시 정상으로 감지되면 트래픽을 해당 대상으로 다시 라우팅
  * 예시 : 만약 제일 위에 있는 PC가 로드 발란서를 통해 제일 위에 있는 EC2 인스턴스에 연결하고있다고 가정할 때
    * 이 인스턴스가 문제가 생겨서 접속이 안되거나 다운이 된 경우 로드발란서가 자동으로 트래픽을 정상적인 인스턴스로 라우팅을 시킨다.
* 고가용성 구현 : 로드발란서가 분산시키는 대상(EC2 인스턴스 ..등등)울 원하는 모습으로 묶어 가용영역에 배치할 수 있다.

## AWS에서의 Load Balancer 종류 4가지

1. Application Load Balancer

* 시험에 나오는 부분(기출)
* Layer 7
  * Application Layer에서 동작한다.
* HTTP, HTTPS 트래픽을 다룬다.
* HTTP Header Content를 사용해 라우팅 요청을 처리
* 웹 애플리케이션 , 서비스에 적합
* 웹 서비스를 구축하는 경우 Application Load Balancer룰 사용한다고 생각하면 된다.

2. Network Load Balancer

* 시험에 나오는 부분(기출) Layer 4 • TCP, UDP, TLS • Protocol, Port Number 를 사용해 라우팅 요청 처리 • 수백만의 대용량 트래픽 처리에 적합

3. Gateway Load Balancer Layer 3 Gateway Load Balancer Endpoint • Layer 4 Gateway Load Balancer • GENEVE protocol 을 사용 하여 encapsulation 트래 픽 전송 • Transparency 한 네트워크 게이트웨이를 제공하므로 보안 검사를 위한 방화벽 , IPS, IDS 등의 원본 패킷 의 데이터가 중요한 가상 어플라이언스에 적합
4. classic Load Balancer

* 이전 세대 로드발란서라서 더 이상 사용하지 않는다. Layer 4 , Layer 7 • HTTP, HTTPS, TCP, TLS • Protocol, Port Number 를 사용해 라우팅 요청 처리 • 이전 세대 EC2 Classic 네 트워크에서 사용
