카카오페이 Devops 사전과제
===================

----------

개발환경 및 요구사항
-------------
>Note :
>웹 어플리케이션 spring-petclinic-data-jdbc을 kubernetes 환경에서 실행

#### Develop Environment

>- OS : ubuntu 18.04
>- JDK : Java 1.8.0_275
>- Docker(client/server) : 19.03.13
>- Kubernetes : 1.15.4


#### Requirements
>- gradle을 사용하여 어플리케이션과 도커이미지를 빌드한다.   
   => 
>- 어플리케이션의 log는 host의 /logs 디렉토리에 적재되도록 한다.   
   => application.properties에 "logging.file.path"를 추가해 어플리케이션의 로그를 남게 설정   
   => 어플리케이션 파드에 hostpath볼륨을 마운트해 로그를 호스트에 저장하게 구현   
>- 정상 동작 여부를 반환하는 api를 구현하며, 10초에 한번 체크하도록 한다. 3번 연속 체크에 실패하면 어플리케이션은 restart 된다.   
   => 정상 동작 여부를 확인하기 위해 "livenessprobe" tcp socket 체크를 구현
   => 10초에 한번 체크 = periodSeconds: 10   
   => 3번 연속 체크 실패시 재시작 = failureThreshold: 3   
>- 종료 시 30초 이내에 프로세스가 종료되지 않으면 SIGKILL로 강제 종료 시킨다.   
   => 30초 이내 미종료시 강제 종료 = terminationGracePeriodSeconds: 30   
>- 배포 시와 scale in/out 시 유실되는 트래픽이 없어야 한다.   
   => 배포 시 유실되는 트래픽이 없게 하기위해 디플로이먼트로 배포
>- 어플리케이션 프로세스는 root 계정이 아닌 uid:1000으로 실행한다.   
   => 도커 이미지 생성 시 계정을 생성하고, 추가한 신규계정이(kakaopay(uid:1000)) 어플리케이션 실행하도록 구현
>- DB도 kubernetes에서 실행하며 재 실행 시에도 변경된 데이터는 유실되지 않도록 설정한다.   
   => DB파드의 상태저장과 관리를 위해 statefulset으로 배포, 데이터는 hostpath (/home/kakaopay/logging)에 저장
>- 어플리케이션과 DB는 cluster domain을 이용하여 통신한다.   
   => service type ClusterIP로 설정, 어플리케이션 빌드할 때 DB URL에 도메인 입력 함
>- nginx-ingress-controller를 통해 어플리케이션에 접속이 가능하다.   
   => "www.petclinic.com" 도메인을 사용해 접속이 가능하도록 구현
>- namespace는 default를 사용한다.   
   => 기본 네임스페이스를 default로 오브젝트 생성   
>- README.md 파일에 실행 방법을 기술한다.   
 

----------
실행방법
-------------

>어플리케이션의 서비스 포트는 "1234"를 사용   
>도메인 ( www.petclinic.com ) 으로 서비스에 접속 가능


본 프로젝트는 Spring 프레임워크를 사용하여 MVC 디자인패턴으로 개발하였습니다. 
아래와 같이 프로젝트에 사용된 각 요소들은 다음과 같은 역할을 수행 합니다. 
#### **Model** 
 * boardService : 실질적인 비즈니스 로직을 담는 클래스로서 데이터베이스와 관련된 DATA가공을 책임지는 
 컴포넌트
<pre>
<code>
1. 깃 다운로드
$ 
$ docker build -t petclinic:v1 .
</code>
</pre>


### 문의사항
기타 궁금하신 사항은 아래 메일로 연락 주세요.
itsogkyc@gmail.com

