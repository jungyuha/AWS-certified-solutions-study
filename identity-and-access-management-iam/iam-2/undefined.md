# 실습

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-08 Thu

#### last modified : 2023-06-08 Thu

일전에 등록한 사용자를 사용자 그룹에서 삭제한다.

<figure><img src="../../.gitbook/assets/image (24) (1) (1).png" alt=""><figcaption><p>사용자 삭제</p></figcaption></figure>

해당 사용자는 아무런 권한도 없게된다.

<figure><img src="../../.gitbook/assets/image (12) (1) (1) (1) (1).png" alt=""><figcaption><p>권한이 없는 사용자</p></figcaption></figure>

## \[1] 사용자에게 권한 추가하기

권한 추가 > 직접 정책 연결 클릭

<figure><img src="../../.gitbook/assets/image (16) (1) (2) (1) (1).png" alt=""><figcaption><p> 직접 정책 연결</p></figcaption></figure>

EC2 검색 > EC2FullAccess 권한 ( EC2에 대한 모든 권한을 가짐 )&#x20;

<figure><img src="../../.gitbook/assets/image (30) (1) (1).png" alt=""><figcaption><p> EC2FullAccess 권한</p></figcaption></figure>

정책을 부여한다.

<figure><img src="../../.gitbook/assets/image (33) (1) (1) (1).png" alt=""><figcaption><p> 정책 부여</p></figcaption></figure>

## \[2] IAM 사용자로 로그인하여 부여받은 권한 확인하기

IAM 사용자 접속시 크롬의 시크릿창 모드로 들어가 로그인하면 편하다.

EC2에 대한 권한만 받았으므로 IAM 대시보드에 들어가면 다음과 같이 권한이 거부된 화면이 뜬다.

<figure><img src="../../.gitbook/assets/image (20) (1) (2).png" alt=""><figcaption><p>IAM 권한이 거부됨</p></figcaption></figure>

EC2는 권한이 있으므로 이용이 가능하다.

<figure><img src="../../.gitbook/assets/image (25) (1).png" alt=""><figcaption><p> EC2</p></figcaption></figure>

### 인스턴스 만들기

인스턴스 시작 클릭

![](<../../.gitbook/assets/image (17) (1) (2) (1).png>)

인스턴스 생성시 설정값은 다음과 같이 임의로 설정한다.

* OS 이미지 : Amazon Linux
* 인스턴스 유형 :  t2.micro
* 네트워크 설정은 디폴트 그대로
* 나머지 설정값도 그대로 !

인스턴스가 생성된 모습

<figure><img src="../../.gitbook/assets/image (5) (2) (1).png" alt=""><figcaption><p> 인스턴스가 생성된 모습 </p></figcaption></figure>

## \[3] 권한 경계 기능으로 최대 권한 제한하기

루트 사용자 계정에서 IAM 사용자의 권한 경계를 설정한다.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p> IAM 사용자의 권한 경계를 설정</p></figcaption></figure>

EC2 검색 > AmazonEC2ReadOnlyAccess 선택

<figure><img src="../../.gitbook/assets/image (13) (1) (2).png" alt=""><figcaption><p> AmazonEC2ReadOnlyAccess</p></figcaption></figure>

&#x20;권한 경계가 설정된 모습이다.

<figure><img src="../../.gitbook/assets/image (8) (3) (1).png" alt=""><figcaption><p> 권한 경계가 설정된 모습</p></figcaption></figure>

## \[4] IAM 사용자로 로그인하여 설정된 권한 경계 확인하기

인스턴스 시작 버튼을 선택한다.

<figure><img src="../../.gitbook/assets/image (18) (2) (1).png" alt=""><figcaption><p> 인스턴스 시작 버튼을 선택</p></figcaption></figure>

키페어 설정값을 바꿔 변경을 시도한다.

<figure><img src="../../.gitbook/assets/image (29) (1).png" alt=""><figcaption><p> 키페어 설정값을 바꿔 변경을 시도</p></figcaption></figure>

인스턴스 시작을 누르면 다음과 같은 권한 제한 안내 문구가 뜬다.

\=> 권한경계에서 ReadOnlyAceess가 부여되었기 때문이다.

<figure><img src="../../.gitbook/assets/image (21) (2) (1) (1).png" alt=""><figcaption><p> 권한 제한 </p></figcaption></figure>

인스턴스를 선택해 인스턴스 종료 버튼을 누르면 마찬가지로 오류가 뜬다.

<figure><img src="../../.gitbook/assets/image (28) (1) (2).png" alt=""><figcaption><p> 인스턴스 종료 버튼</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11) (1) (2).png" alt=""><figcaption><p> 인스턴스 종료 제한</p></figcaption></figure>

루트 사용자 계정으로 들어가 다시 권한 경계를 제거한다.

<figure><img src="../../.gitbook/assets/image (31) (1) (1).png" alt=""><figcaption><p> 권한 경계를 제거</p></figcaption></figure>

다시 IAM 사용자에서 인스턴스 종료를 누르면 정상적으로 종료된다.

<figure><img src="../../.gitbook/assets/image (23) (2) (1).png" alt=""><figcaption><p> 인스턴스 종료</p></figcaption></figure>

## \[5] 정책을 직접 생성할 수도 있다.

IAM  > 정책 > 정책 생성 클릭

<figure><img src="../../.gitbook/assets/image (26) (2).png" alt=""><figcaption><p> 정책 생성</p></figcaption></figure>

시각적 편집기를 통해 직접 원하는 서비스를 추가하거나 JSON을 통해 직접 서비스를 명시할 수 있다.

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1).png" alt=""><figcaption><p> 시각적 편집기</p></figcaption></figure>

#### 시각적 편집기로 EC2FullAccess 정책 만들기

EC2 검색 > 모든 EC2 작업 선택 > 모든 리소스 선택

<figure><img src="../../.gitbook/assets/image (32) (1) (1).png" alt=""><figcaption><p> 시각적 편집기로 EC2FullAccess 정책 만들기</p></figcaption></figure>
