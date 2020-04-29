## 실전 JSP - 신입 프로그래머를 위한 강좌

## :pushpin: 목차
### 오리엔테이션 및 소개
[웹 프로그램 개요](#웹-프로그램-개요)   
[JSP 맛보기](#JSP-맛보기)  
[Servlet 맛보기](#Servlet-맛보기)

### 본격 JSP 학습하기
[Servlet 맵핑](#Servlet-맵핑)  
[Servlet request, response](#Servlet-request,-response)  
[Servlet Life-Cycle](#Servlet-Life-Cycle)  
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

---- 
### Servlet 맵핑
#### :fire: Servlet 맵핑이란?  
ex) full path : http://localhost/projectname/servlet/com.servlet.servletEx 일때  
projectname부터를 contextpath라고 함 > 이런 식으로 url에 다 보이면 보안에 취약하므로 프로젝트명 이하를 간결한 URL로 맵핑 할 수 있음.   
__맵핑 방법__  1. web.xml 2. java Annotation

#### :fire: web.xml을 이용한 맵핑  
고전적 방법  
__web.xml 파일__
```xml
<servlet>
	<servlet-name>servletEx</servlet-name>
	<servlet-class>com.servlet.ServletEx</servlet-class>
</servlet>
<servlet-mapping>
	<servlet-name>servletEx</servlet-name>
</servlet-mapping>
```

[참고 링크 - 나의 티스토리](https://minchoi0912.tistory.com/78?category=909191)
#### :fire: Java Annotation을 이용한 맵핑  
해당 서블릿 위에 코드 추가 @webServlet("/SE")   
/SE로 url이 들어왔을 때 servlet 호출   
맵핑을 통해서 response를 할 수 있음

---
### Servlet request, response
사용자의 요청(request)과 웹 서버의 응답(response)을 담당하는 객체
#### :fire: HttpServlet  
servlet 객체를 만들기 위해서는 HttpServlet 클래스를 상속 받아서 사용해야함.   
로컬에서 작업하는 것이 아니라 웹 서버와의 통신이 필요하므로 많은 기능들이 필요하기 때문에 많은 클래스들이 상속 및 구현된 HttpServlet 상속 받아서 사용함.   
이런 이유로 개발자는 HttpServlet만 상속 받아서 사용 할 수 있게 됨. 
```java
@WebServlet("/testServlet")
public class testServlet extends HttpServlet {

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		doGet(request, response);
	}

}

```
#### :fire: HttpServletRequest
요청에 대한 정보를 가지고 있는 객체(사용자)
* 주요 메소드
request.getCookies();  
request.getSession();   
request.getAttribute(" "); / request.setAttribute(" ", " ")  
request.getParameter();
#### :fire: HttpServletResponse
응답에 대한 정보를 가지고 있는 객체
* 주요 메소드  
response.addCookie("");

#### :fire: 더하기
1.  사용자(클라이언트)가 URL을 클릭하면 HTTP Request를 Servlet Conatiner로 전송합니다.
    
2.  HTTP Request를 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 두 객체를 생성합니다.
    
3.  web.xml은 사용자가 요청한 URL을 분석하여 어느 서블릿에 대해 요청을 한 것인지 찾습니다.
    
4.  해당 서블릿에서 service메소드를 호출한 후 클리아언트의 POST, GET여부에 따라 doGet() 또는 doPost()를 호출합니다.
    
5.  doGet() or doPost() 메소드는 동적 페이지를 생성한 후 HttpServletResponse객체에 응답을 보냅니다.
    
6.  응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킵니다.

[참고 링크 - 망나니 개발자님 티스토리]([https://mangkyu.tistory.com/14](https://mangkyu.tistory.com/14))

---- 
### Servlet Life Cycle
#### :fire: Servlet 생명주기
@PostConstruct(준비 단계) --> [ init() -> service -> destroy() ]  --> @PreDestory(서블릿 종료 후 실행) : Servlet 생성 및 종료, 생명주기   

#### :fire: 생명주기 관련 메서드  
* Servlet의 단계 별로 필요한 과정이 있다면 메소드를 오버라이딩 해서 사용 할 수 있음.    
* Servlet 실행 부분은 service 메소드를 오버라이딩 해도 되지만 doGet/doPost를 보통 이용함
* init() : 생성 시점, 데이터 서버에 로그인 아이디나 패스워드를 담는 등의 공통적인 부분  
* destroy() : 데이터베이스 사용 뒤 자원 해제, 웹 서버 리소스 이용 뒤 반납시 이용   

웹 컨테이너(tomcat)가 적절한 시점에 메소드를 호출해줌.
