스프링(Spring) 웹 개발 프로젝트 [게시판]
===================

----------

개발환경 및 기능소개
-------------
>Note :
>스프링 프레임워크를 사용한 MVC(Model-View-Control) 구조 게시판 개발

#### Develop Environment

>- OS : ubuntu 18.04
>- JDK : Java 1.8.0_275
>- Docker(client/server) : 19.03.13
>- Kubernetes : 1.15.4


#### Requirements
>-gradle을 사용하여 어플리케이션과 도커이미지를 빌드한다.
>-어플리케이션의 log는 host의 /logs 디렉토리에 적재되도록 한다.
>-정상 동작 여부를 반환하는 api를 구현하며, 10초에 한번 체크하도록 한다. 3번 연속 체크에 실패하
>-면 어플리케이션은 restart 된다.
>-종료 시 30초 이내에 프로세스가 종료되지 않으면 SIGKILL로 강제 종료 시킨다.
>-배포 시와 scale in/out 시 유실되는 트래픽이 없어야 한다.
>-어플리케이션 프로세스는 root 계정이 아닌 uid:1000으로 실행한다.
>-DB도 kubernetes에서 실행하며 재 실행 시에도 변경된 데이터는 유실되지 않도록 설정한다.
>-어플리케이션과 DB는 cluster domain을 이용하여 통신한다.
>-nginx-ingress-controller를 통해 어플리케이션에 접속이 가능하다.
>-namespace는 default를 사용한다.
>-README.md 파일에 실행 방법을 기술한다.



----------
MVC ( Model-View-Controller ) 
-------------
본 프로젝트는 Spring 프레임워크를 사용하여 MVC 디자인패턴으로 개발하였습니다. 
아래와 같이 프로젝트에 사용된 각 요소들은 다음과 같은 역할을 수행 합니다. 
#### **Model** 
 * boardService : 실질적인 비즈니스 로직을 담는 클래스로서 데이터베이스와 관련된 DATA가공을 책임지는 
 컴포넌트

#### **View**
* boardList.jsp : 게시판 목록과 관련된 사용자 인터페이스 요소를 나타내는 역할 수행
* boardOneView.jsp : 게시글 조회와 댓글관련 화면 인터페이스 요소를 나타내는 역할 수행
* boardRegisterForm.jsp : 게시글 등록과 관련된 인터페이스 요소를 나타내는 역할 수행

#### **Controller**    
* HomeController.java : View에 게시글 목록과 관련된 DATA 흐름을 제어하는 역할을 수행하는 Class
* PageMaker.java : 게시글 페이징 처리와 관련된 로직을 수행하는 Class
* ReplyController.java : 댓글과 관련된 DATA 흐름을 제어하는 Class


------------

게시판 동작화면
-------------

####  **게시판 목록**
게시글 목록을 보여주는 화면입니다. 기본값으로 1페이지 [ 글 10개, 페이징block 10개] 설정되어 있으며, 코드 수정을 통해 페이징과 글목록 수정이 가능하도록 지원하고 있습니다.
 댓글이 있는 글의 제목 옆에 댓글 갯수를 표시하도록 만들었습니다.
 
![enter image description here](https://github.com/itsogkyc/Spring_Board/blob/master/imgfile/img_01.png?raw=true)

####  **게시글 수정/삭제 , 댓글 입력/수정/삭제**
게시글 수정 / 삭제가 가능하고, 각 게시글에 댓글을 입력 / 수정 / 삭제 할 수 있도록 구현 하였습니다.

![enter image description here](https://github.com/itsogkyc/Spring_Board/blob/master/imgfile/img_04.png?raw=true)


OnsenUI 적용 게시판 동작화면 (Last Updated 2018.03.07)
-------------


![enter image description here](https://github.com/itsogkyc/Spring_Board/blob/master/imgfile/onsen1.png?raw=true)



![enter image description here](https://github.com/itsogkyc/Spring_Board/blob/master/imgfile/onsen2.png?raw=true)


![enter image description here](https://github.com/itsogkyc/Spring_Board/blob/master/imgfile/onsen3.png?raw=true)

----------


### 문의사항
기타 궁금하신 사항은 아래 메일로 연락 주세요.
itsogkyc@gmail.com

