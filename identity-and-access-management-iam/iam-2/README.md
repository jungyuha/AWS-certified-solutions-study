# IAM 정책

**기록 ✍️**

#### author : jung yuha

#### first registered : 2023-06-08 Thu

#### last modified : 2023-06-08 Thu

## \[1] IAM 정책

* AWS 리소스에 대한 액세스 권한을 정의 한 것
* **사용자 , 그룹 , 역할**에 정책을 연결하여 사용함
* JSON 문서 형식으로 이루어짐
  * 정책이 명시되지 않는 경우 기본적으로 모든 요청이 거부됨

## \[2] IAM 정책 JSON

### (1) IAM 정책 JSON 문서 구조

<figure><img src="../../.gitbook/assets/image (34) (1) (1).png" alt=""><figcaption><p>JSON 문서 구조</p></figcaption></figure>

* **Effect** : Statement 에 대한 Access 또는 Deny
* **Action** : 권한에 대한 작업 목록
* **Resource** : 권한이 적용되는 리소스
* **Condition** : 정책이 적용되는 세부 조건 옵션사항 ( ex : 특정 이더넷에만 적용 , 특정 IP에서만 적용 )

### (2) IAM 정책 JSON 문서 예시

#### --예시1

<figure><img src="../../.gitbook/assets/image (4) (2) (1).png" alt=""><figcaption><p>IAM 정책 JSON 예시1</p></figcaption></figure>

#### 정책 명시 사항

* Lambda 서비스에 대한 정책이 명시
* 기본적으로 모든 권한을 허용
* 220.100.16.0/20 IP 네트워크로부터의 함수 생성과 함수 삭제는 권한이 거부됨.

#### --예시2

<figure><img src="../../.gitbook/assets/image (7) (2) (1).png" alt=""><figcaption><p>IAM 정책 JSON 예시2</p></figcaption></figure>

#### 정책 명시 사항

* EC2 서비스에 대한 정책이 명시
* 사용자 소스 IP 대역이 10.100.100.0/24 인 경우에만 ec2 인스턴스를 종료할 수 있음
* us esast 1 리전이 아닌 경우에는 다른 리전 에서 발생하는 모든 작업이 거부 됨
* 사용자 소스 IP 가 10.100.100.0/24 대역인 경우에만 us east 1 리전의 ec2 인스턴스를 종료할 수 있음

## \[3] IAM 권한 경계 (Permission Boundary)

* IAM 사용자 또는 역할에 최대 권한을 제한 하는 기능
  * Ex  :  IAM 사용자에게 Amazon S3, Amazon CloudWatch 및 Amazon EC2 만 관리할 수 있게 하려면 아래와 같은 정책을 적용한다.
  * ![](<../../.gitbook/assets/image (19) (1) (1).png>)
* 예를 들어 2개의 정책이 적용된 경우 ( AWS 전체 권한 + 권한 경계 정책 )
  * \=>AWS 전체 권한을 가지고 있어도 권한 경계에 대한 권한 범위로 축소되어 적용 된다.(중첩된 부분만 적용)
  * 여기서 최대 권한은 AWS 전체 권한이 된다.
  * ![](<../../.gitbook/assets/image (27) (1) (2) (1).png>)

