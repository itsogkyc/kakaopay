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



----------
실행방법
-------------

>어플리케이션의 서비스 포트는 "1234"를 사용   
>도메인 ( www.petclinic.com ) 으로 서비스에 접속 가능

1. 깃 다운로드
<pre>
<code>
$ git clone https://github.com/itsogkyc/kakaopay.git
</code>
</pre>

2. 어플리케이션 도커 이미지 생성
<pre>
<code>
$ cd kakaopay
$ docker build -t petclinic:v1 .
</code>
</pre>

3. 쿠버네티스 오브젝트 선언
<pre>
<code>
$ kubectl apply -f mysql.yaml
$ kubectl apply -f ingress.yaml
$ kubectl apply -f apps.yaml
</code>
</pre>


### 문의사항
기타 궁금하신 사항은 아래 메일로 연락 주세요.
itsogkyc@gmail.com

