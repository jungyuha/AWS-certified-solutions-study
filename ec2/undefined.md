# 네트워크 인터페이스

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-16 Fri

#### last modified : 2023-06-16 Fri



## \[1] 네트워크 인터페이스

AWS의 EC2 인스턴스는 가상머신이다.

이 가상머신도 하나의 개별 서버이기 때문에 인터넷이나 다른 AWS 리소스와 통신을 하기 위해서 네트워킹을 이용한다.

이 네트워킹을 이용하기 위해서 '**네트워크 인터페이스**'를 사용하게 된다.

기본적으로 EC2를 생성할 때 하나의 네트워크 인터페이스가 생성되고 이 네트워크 인터페이스에 IP 주소가 부여되서 EC2 인스턴스는 네트워크 인터페이스를 통해 통신할 수 있게된다.

### AWS의 네트워크 인터페이스 : Elastic Network Interface (ENI)

* 가상 머신에 연결되는 네트워크 인터페이스이다.
* IP 주소 , MAC 주소 등이 부여된다.
* 인스턴스에 연결되어 네트워크 통신을 하는 역할을 한다.
* 인스턴스 생성시 기본 네트워크 인터페이스가 IP 주소 등의 정보 할당과 함께 생성된다.
* EC2에 추가로 여러 개의 네트워크 인터페이스 연결 가능하다.
  * &#x20;서로 다른 IP값을 가지며 서로 다른 네트워크 라우팅도 가능하다.
  * ![](<../.gitbook/assets/image (60).png>)

## \[2] 특정 인스턴스의 네트워크 인터페이스 확인하기

#### EC2 대시보드 > 왼쪽 메뉴 > 인스턴스&#x20;

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption><p> EC2 대시보드 > 왼쪽 메뉴 > 인스턴스 </p></figcaption></figure>

#### 특정 인스턴스를 클릭 > 네트워킹 탭 > 네트워크 인터페이스 확인

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption><p> 특정 인스턴스를 클릭 > 네트워킹 탭 > 네트워크 인터페이스 확인</p></figcaption></figure>

**VPC ID**  : 이 네트워크 인터페이스가 AWS의 가상 네트워크인 VPC에 연결이 되어있다.

**서브넷 ID** : VPC와 관련된 서브넷 정보이다.

**보안그룹** : 들어가고 나가는 트래픽을 제어한다.

## \[2] 네트워크 인터페이스 목록 확인하기

#### EC2 대시보드 > 왼쪽 메뉴 > 네트워크 및 보안 > 네트워크 인터페이스

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption><p> EC2 대시보드 > 왼쪽 메뉴 > 네트워크 및 보안 > 네트워크 인터페이스</p></figcaption></figure>

**가용영역** : 이 네트워크 인터페이스가 생성된 곳이며 해당 EC2 인스턴스의 가용영역과 동일하다.

오른쪽 상단 '작업' > 분리 선택시 인스턴스가 분리가 되고 해당 인스턴스는 인터넷이나 내부적으로 통신할 수 없게된다.

## \[3] 네트워크 인터페이스 생성하기

#### 오른쪽 상단 '네트워크 인터페이스 생성' 을 통해 네트워크 인터페이스를 새로 만들 수도 있다.

<figure><img src="../.gitbook/assets/image (74).png" alt="" width="563"><figcaption><p> 오른쪽 상단 '네트워크 인터페이스 생성' 을 통해 네트워크 인터페이스를 새로 만들 수도 있다.</p></figcaption></figure>

#### 네트워크 인터페이스 생성 정보&#x20;

<figure><img src="../.gitbook/assets/image (57).png" alt="" width="563"><figcaption><p> 네트워크 인터페이스 생성 정보 </p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (77).png" alt="" width="563"><figcaption><p> 네트워크 인터페이스 생성 정보 </p></figcaption></figure>

**설명** : EC2\_Linux2

**서브넷** : 인터페이스가 사용될 인스턴스와 동일한 서브넷이어야한다.(동일한 가용영역에 있는)

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption><p> 인스턴스의 가용영역 : ap-northeast-2a</p></figcaption></figure>

**private ip 주소** : 자동할당

**보안 그룹** 설정

#### 네트워크 인터페이스 연결

인터페이스가 만들어지면 오른쪽 상단 '작업' > '연결'을 선택하여 특정 인스턴스를 클릭한다.

여기서는 EC\_Linux 인스턴스를 선택했다.

![](<../.gitbook/assets/image (54).png>)

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption><p>인스턴스로 EC_Linux를 선택</p></figcaption></figure>

#### 특정 인스턴스를 클릭 > 네트워킹 탭 > 네트워크 인터페이스 확인

하나의 인스턴스에 여러개의 네트워크 인터페이스가 설정되어있음을 확인할 수 있다.

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption><p>나의 인스턴스에 여러개의 네트워크 인터페이스가 설정됨</p></figcaption></figure>

