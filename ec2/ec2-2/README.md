# EC2 인스턴스 원격 접속

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-13 Tue

#### last modified : 2023-06-13 Tue



아래 방법\[1] , 방법\[2]는 **AWS뿐만이 아니라 일반적으로 서버 관리하면서도 자주 사용하는 방식**이다.

## \[1] EC2 원격접속 방법 1 : SSH 연결 (Linux 인스턴스)

<figure><img src="../../.gitbook/assets/image (50) (1).png" alt=""><figcaption><p> SSH 연결 (Linux 인스턴스</p></figcaption></figure>

* SSH 프로토콜을 이용해 Linux 인스턴스에 원격으로 연결 및 파일 전송 가능
* SSH(Secure Shell Protocol)은 보안을 통해 원격으로 접속하기 위한 방식&#x20;
  * EC2 리눅스 인스턴스에서 public 키를 가지고 있고 우리가 다운받은 Private 키를 가지고 있는 상태에서 원격 접속 프로그램을 통해 SSH 프로토콜을 통하여 public 키와 Private 키를 비교한뒤 접속한다.
  * SSH를 사용하기 위해서는 EC2인스턴스에서 보안그룹을 생성할 때 TCP 22번 포트가 열려 있어야 한다.
* 아이디 , 패스워드 방식이 아닌 Public Key 와 Private Key 를 이용해 접속
* 원격 접속 방법 : MAC PC 의 Terminal, Windows Powershell , Windows Putty 프로그램 등을 사용한다.

## \[2] EC2 원격접속 방법 2 : RDP 연결 (Windows 인스턴스)

<figure><img src="../../.gitbook/assets/image (6) (1) (2).png" alt=""><figcaption><p> RDP 연결 (Windows 인스턴스)</p></figcaption></figure>

* RDP 프로토콜을 이용해 Windows 인스턴스에 원격으로 연결 및 파일 전송 가능
* RDP(Remote Desktop Protocol,원격 데스크탑 연결) 은 Windows OS 를 원격으로 접속하기 위한 방식
* 아이디, 패스워드를 이용해 접속
* 원격 접속 방법 : 윈도우의 원격 데스크톱 연결 프로그램 사용
  * 클라이언트에서 원격 접속을 할 때 RDP라는 프로토콜을 사용하여 아이디, 패스워드를 이용해 접속
  * RDP를 사용하기 위해서는 EC2인스턴스에서 보안그룹을 생성할 때 TCP 3389번 포트가 열려 있어야 한다.

**3번 방법은 AWS에서만 지원한다.**

## \[3] EC2 원격접속 방법 3 : Instance Connect 연결 (Linux 인스턴스)

<figure><img src="../../.gitbook/assets/image (33) (2).png" alt=""><figcaption><p> Instance Connect 연결 : 웹 브라우저를 이용해 EC2 인스턴스에 연결</p></figcaption></figure>

* 웹 브라우저를 이용해 EC2 인스턴스에 연결
* SSH 프로토콜을 사용하여 일회용 SSH 퍼블릭키를 인스턴스 메타데이터에 업로드해서 EC2 연결
  * 클라이언트에 퍼블릭 키가 없어도 된다. 일회용키를 AWS에서 인스턴스 메타데이터에 업로드해서 EC2 연결
  * SSH를 사용하기 위해서는 EC2인스턴스에서 보안그룹을 생성할 때 TCP 22번 포트가 열려 있어야 한다.
*   PowerShell 이나 Putty 를 이용한 SSH 연결처럼 프라이빗 키를 다운로드 받을 필요 없음

    \=> 즉 , 간단하게 연결이 가능하다.
* Linux 인스턴스만 연결 가능하다.
