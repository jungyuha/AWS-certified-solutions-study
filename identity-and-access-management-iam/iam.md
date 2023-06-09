# IAM 개요

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-02 Fri

#### last modified : 2023-06-02 Fri

## \[1] IAM 개요

* AWS 계정 및 권한 관리 서비스
* AWS 서비스와 리소스에 대한 액세스 관리
* 사용자, 그룹 , 역할 , 정책으로 구성되어 있다.
* 리전에 속하는 서비스가 아닌 글로벌 서비스

### 계정 보안 강화를 위해 해야할 것

* 루트 계정 (AWS 회원가입시 만들어지는 계정) : 최초 사용자 계정 생성 이후 가능하면 사용하지 말 것
* 사용자 계정 (IAM 계정 으로 서비스를 사용하고 사용자) : 필요한 최소한의 권한만 부여한다. => 최소권한의 원칙
* 루트계정과 개별 사용자 계정에 강력한 암호 정책과 멀티팩터 인증 (MFA) 적용
  *   **멀티팩터 인증 (MFA)** : 아이디와 패스워드 이외에 다른 인증 방법을 적용하는 것

      ( 예시 : 특정 웹사이트나 애플리케이션을 로그인 할 때 모바일 폰의 OTP 코드 사용, 문자메시지 추가 인증)
* 사용자의 암호에 대한 복잡성 요구 사항과 의무 교체 주기를 정의한다.

## \[2] IAM 액세스 관리

<figure><img src="../.gitbook/assets/image (10) (1) (2).png" alt=""><figcaption><p>액세스 관리</p></figcaption></figure>

* 정책은 각 사용자,그룹,역할에 대한 권한을 정의한다.
