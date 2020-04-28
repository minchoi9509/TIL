## 실전 JSP - 신입 프로그래머를 위한 강좌
:bulb: 실전 JSP (renew ver.) - 신입 프로그래머를 위한 강좌 / 인프런

## :pushpin: 목차
### 오리엔테이션 및 소개
[웹 프로그램 개요](#웹-프로그램-개요)   
[JSP 맛보기](#JSP-맛보기)  
[Servlet 맛보기](#Servlet-맛보기)

### 본격 JSP 학습하기
Servlet 맵핑  
Servlet request, response  
Servlet Life-Cycle  
form 데이터 처리  
JSP 스크립트  
JSP request, response  
JSP 내장객체  
Servlet 데이터 공유  
Cookie  
Session  
한글처리  
오라클 설치  
SQL  
JDBC  
DAO와 DTO     
Connection Pool  

----
  
### 웹 프로그램 개요
#### :fire:__웹 프로그램이란?__  
* 어떤 PC(브라우저)에서 어떤 다른 PC(서버)에게 정보를 요청(request)하고 응답(response) 받는 것  
* 인터넷 서비스를 이용해서 서로 다른 구성요소들(PC등)이 통신 할 수 있는 프로그램  

#### :fire: 프로토콜과 IP
* 프로토콜(Protocol) : 인터넷 객체가 웹 서버에 정보를 요청하고 응답 받는 __통신__을 하기위한 규약  
ex) __HTTP__, FTP(파일의 이동), SMTP(메일 관련), POP등이 있음  

* IP : 어떠한 컴퓨터의 특정한 주소  
DNS와 ip 주소의 맵핑을 통해서 사용자들의 접근 용이  
ex) http(protocol)://www(인터넷 서비스구분).google.com(도메인):80(port번호)/index.html(경로)  
port : 웹 서버에서 구동하고 있는 여러가지 프로그램을 찾아가는 경로, 기본 포트번호 80  

#### :fire: 웹 프로그램의 동작 원리
User <-> Web Server <-> Database  
정적 데이터(HTML)  
동적 데이터(Container) : 데이터를 새로 수집, 가공을 통해 새로운 데이터 생성   

----
### JSP 맛보기
#### :fire: __웹 컨테이너 구조__  
xxx.jsp (request) --> [xxx_jsp.java -> xxx_jsp.class -> xxx_jsp.obj] --> (respone) HTML   
WAS(Web Application Server)  
웹 컨테이너(tomcat) : 개발자가 생성한 jsp 파일을 기계어로 컴파일 해줌. 서버에서 구동 된 뒤 작업에 대한 
응답으로 HTML이 생성됨  

#### :fire: __java 파일 확인__  
웹 컨테이너는 서버 안에 존재 함  
위치 : C:\Program Files\Apache Software Foundation\Tomcat 8.5\work\Catalina\localhost\ROOT\org\apache\jsp  

----
### Servlet 맛보기
Servlet : 순수 자바 사용 <-> JSP : HTML안에 JSP 코드 삽입   
__공통점__ : 사용자의 요청에 의해서 동적인 작업을 하기 위한 프로그래밍  

