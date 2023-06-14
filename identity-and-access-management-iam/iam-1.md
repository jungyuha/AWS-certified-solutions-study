# \[실습] IAM 유저 , 그룹



**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-07 Wed

#### last modified : 2023-06-07 Wed

## \[1] 계정 보안 강화

IAM의 리전은 **글로벌**로 설정되어있다.

## ![](<../.gitbook/assets/image (1).png>)&#x20;

* 계정 설정 메뉴 클릭 > 암호 정책 편집&#x20;
*

    <figure><img src="../.gitbook/assets/image (24) (1) (1).png" alt=""><figcaption><p>암호정책</p></figcaption></figure>


*

    <figure><img src="../.gitbook/assets/image (20) (1).png" alt=""><figcaption><p>다양한 암호정책 설정</p></figcaption></figure>


*

    <figure><img src="../.gitbook/assets/image (23) (1).png" alt=""><figcaption><p>대시보드 > 보안권장 사항 > MFA 추가</p></figcaption></figure>


* 보안 자격증명 > MFA 할당
* ![](<../.gitbook/assets/image (21) (1).png>)
*

    <figure><img src="../.gitbook/assets/image (25) (1).png" alt=""><figcaption><p>내 보안자격증명 > MAF 할당</p></figcaption></figure>
* MFA 디바이스 관리&#x20;
* 인증 관리 앱 ( 가상 MFA 디바이스 ) (ex : 모바일 앱에서 구글 authentication 나 MS의 otp 서비스 같은 패스코드를 만들고 그 패스코드를 사용하여 로그인할 때 사용함 )
* MFA 디바이스 선택
*

    <figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>MFA 디바이스 선택 > 인증 관리자 앱</p></figcaption></figure>


* QR 코드 표시 선택
* 암호를 설정하면 AWS 로그인시 직접 치지 않고 해당 MFA코드로 로그인이 가능하다.
*

    <figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>디바이스 설정 > QR 코드 보이기 > 암호 설정</p></figcaption></figure>



## \[2] 사용자

* 사용자 메뉴 > 사용자 추가
*

    <figure><img src="../.gitbook/assets/image (22) (1).png" alt=""><figcaption><p>사용자 메뉴 > 사용자 추가</p></figcaption></figure>


*

    <figure><img src="../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption><p>사용자 추가 > 사용자 세부 정보</p></figcaption></figure>


*   그룹이 없으니 그룹을 생성함

    <figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>사용자 권한 설정 : 그룹에 사용자 추가</p></figcaption></figure>


* AWS에서 미리 만들어놓은 정책들 : 852개
*

    <figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>
* 다음 예시는 모든 Resource와 모든 Action을 허용하는 권한의 예시임(AWS 전체에 대한 권한)
* Full 권한이나 읽기 권한같은 다양한 권한들이 있음
* 실습에서는 해당 권한(AdministratorAccess)로 그룹을 생성한다.
*

    <figure><img src="../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption><p>그룹 생성</p></figcaption></figure>


*   사용자 추가

    <figure><img src="../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>


*

    <figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>사용자 생성 완료</p></figcaption></figure>


*   사용자 그룹

    <figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## \[3] 새로운 사용자로 Access 하기

* IAM 대시보드 > 오른쪽 상단의 AWS 계정 박스 > 이 계정 IAM 사용자를 위한 로그인 URL&#x20;
  * 기본 별칭을 바꿔 URL을 커스터마이징 할 수 있음
  * ![](<../.gitbook/assets/image (19) (1).png>)
* 해당 URL로 들어가 해당 사용자의 계정으로 로그인 한다.
  * ![](<../.gitbook/assets/image (12) (1) (1) (1) (1).png>)
  * 루트 사용자 계정이 아니므로 IAM 사용자라고 표시된다.
  * ![](<../.gitbook/assets/image (28) (1) (1).png>)
* 로그인 종류 : IAM 사용자 / root 사용자 선택
* ![](<../.gitbook/assets/image (26) (1).png>)

