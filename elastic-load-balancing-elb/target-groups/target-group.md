# \[실습] Target Group 생성

## \[실습] Target Group 생성

**기록 ✍️**

**author : jung yuha**

**first registered : 2023-06-28 Wed**

**last modified : 2023-06-29 Thu**

### 타겟 그룹 뒤에 EC2 웹서버 생성하기

#### 1) EC2 웹서버 생성하기

**인스턴스 생성 > 고급세부정보 > 사용자 데이터(User Data)에 아래 웹서버를 생성하는 스크립트 추가**

* \*User Data는 인스턴스가 시작 될 때 실행되는 명령어 또는 스크립트
* 따라서 이 사용자 데이터에 웹서버 생성 스크립트를 넣으면 인스턴스를 런칭할 때 웹서버가 구축이 된다.

**EC2 대시보드 > 왼쪽 메뉴 '인스턴스' > '인스턴스 시작' 클릭**

* **인스턴스 개수** : 2개
  * ![](<../../.gitbook/assets/image (23).png>)
  * 2개의 인스턴스에 로드발란싱 처리를 할 것이다.
* **태그 이름** : EC2\_WEB
  * ![](<../../.gitbook/assets/image (25).png>)
* **애플리케이션 및 OS 이미지** : Amazon Linux 2 AMI <<<<<<< HEAD
  * <img src="../../.gitbook/assets/image (1).png" alt="" data-size="original">

\=======

* <img src="../../.gitbook/assets/image (1) (4).png" alt="" data-size="original">

> > > > > > > 7852428b5ec9e01ba27d77925f3752b5e23ba21b

* **인스턴스 유형** : t2.micro
  * ![](<../../.gitbook/assets/image (46).png>)
* **키페어(로그인)** : 이전시간에 지정한 EC2\_KEY
  * ![](<../../.gitbook/assets/image (31).png>)
* **네트워크 설정** : 그대로 설정
*   **보안그룹** : '보안그룹생성' 선택 > '편집' 클릭 \*

    ```
    <figure><img src="../../.gitbook/assets/image (20).png" alt="" width="563"><figcaption><p> '편집' 클릭</p></figcaption></figure>
    ```

    *   기존 ssh 제거

        <figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p>기존 ssh 제거</p></figcaption></figure>
    * **보안그룹이릅** : web\_access\_sg
    * **설명** : web\_access\_sg <<<<<<< HEAD
    * ![](<../../.gitbook/assets/image (4).png>) =======
    *

        ![](<../../.gitbook/assets/image (4) (4).png>)

> > > > > > > 7852428b5ec9e01ba27d77925f3752b5e23ba21b \* **보안그룹규칙1** 추가 \* 유형 : HTTP \* source type : Anywhere \* ![](<../../.gitbook/assets/image (15).png>) \* **보안그룹규칙2** 추가 \* 유형 : HTTPS \* source type : Anywhere \* ![](<../../.gitbook/assets/image (22).png>)

* **스토리지** : 그대로 설정
* **고급세부정보** \*
  *   \*\*사용자 데이터(User Data)\*\*에 웹서버를 생성하는 스크립트 추가

      ```
      #!/bin/bash
      yum update -y
      yum install httpd -y
      systemctl enable httpd.service
      systemctl start httpd.service
      cd /var/www/html
      echo "안녕하세요 . AWS EC2 입니다 . $(hostname -f)" > index.html
      ```

**EC2 대시보드 > 왼쪽 메뉴 '인스턴스' 클릭**

*   EC2\_WEB 인스턴스가 2개가 생성이 된 모습 \*

    ```
    <figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p> EC2_WEB 인스턴스가 2개</p></figcaption></figure>
    ```
* public IP 주소를 복사하여 확인해본다. \*

## <<<<<<< HEAD

```
  <figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p> public IP 주소 접속</p></figcaption></figure>
```

> > > > > > > 7852428b5ec9e01ba27d77925f3752b5e23ba21b

#### 2) 타겟그룹 생성하기

**만들 타겟그룹 목록 : 이 타겟그룹에 위에서 생성한 2개의 EC2 인스턴스를 연결하고자한다.**

* **TG-ALB** : application 로드발란스 전용
* **TG-NLB** : network 로드발란스 전용

**EC2 대시보드 > 왼쪽 메뉴 '로드밸런싱' > '대상그룹' 클릭 > 오른쪽 상단 'create target group' 클릭**

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption><p>타겟그룹 생성하기</p></figcaption></figure>

* **application 로드발란스** 전용
  * **target** : instance
  * **target group name** : TG-ALB
  * **protocol** : HTTP / 80
  * 나머지는 그대로
  * **Health Checks** : HTTP
  * 'Next' 선택 > 등록할 인스턴스 선택 > 위에서 생성된 2개의 인스턴스 모두 추가

**EC2 대시보드 > 왼쪽 메뉴 '로드밸런싱' > '대상그룹' 클릭 > 오른쪽 상단 'create target group' 클릭**

* **Network 로드발란스** 전용
  * **target** : instance
  * **target group name** : TG-NLB
  * **protocol** : TCP / 80
  * 나머지는 그대로
  * **Health Checks** : TCP
    *   TCL 프토로톨 80번이 HTTP 프로토콜이므로 HTTP를 선택해주어도 된다.

        HTTP가 TCP 프로토콜에 포함되기 때문이다.
  * 'Next' 선택 > 등록할 인스턴스 선택 > 위에서 생성된 2개의 인스턴스 모두 추가

**EC2 대시보드 > 왼쪽 메뉴 '로드밸런싱' > '대상그룹' 클릭 > 특정 대상그룹 클릭(TG-ALB)**

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption><p>타겟그룹에 등록된 인스턴스 목록</p></figcaption></figure>

#### 3) 로드밸런싱 속성 변경하기

**EC2 대시보드 > 왼쪽 메뉴 '로드밸런싱' > '대상그룹' 클릭 > 아무 대상 그룹 클릭 > 아래 탭 'Attribute' > 'Edit'**

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption><p>로드밸런싱 속성 변경하기</p></figcaption></figure>
