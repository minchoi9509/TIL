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
[form 데이터 처리](#form-데이터-처리)  
[JSP 스크립트](#JSP-스크립트)  
[JSP request, response](#JSP-requset,-response)  
[JSP내장객체](#JSP-내장객체)  
[Servlet 데이터 공유](#Servlet-데이터-공유)  
[Cookie](#Cookie)  
[Session](#Session)  
[한글처리](#한글처리)  
[JDBC](#JDBC)  
[DAO와 DTO](#DAO와-DTO)     
[Connection Pool](#Connection-Pool)  

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

---
### form 데이터 처리
사용자의 form 데이터를 Servlet에서 처리하는 방법
* 사용자가 requset 했을 때 서버에서 response하기 위해서 JSP&Servlet을 배우기 때문에 중요한 파트
* 서버에서 doGet/doPost 두 가지 방식으로 받을 수 있음
#### :fire: form 태그
* request 객체를 통해서 브라우저에서 데이터를 서버로 날릴 수 있음
* form 태그의 속성 __method__에서 POST/GET 설정 가능
#### :fire: doGet
* 설정하지 않은 경우 디폴트 값
* 데이터가 웹 브라우저 URL에 노출되어 웹 서버로 전송, 사용자 정보가 URL에 노출 될 수 있음 > 보안에 취약함
* 정보 전달의 한계가 존재함
#### :fire: doPost
* 맵핑 정보만 노출됨 
* 사용자의 데이터가 헤더 파일에 암호화되서 전송이 됨(ex: 로그인, 회원가입, 설문조사..)

:heavy_check_mark: requset.getParameterValues()를 통해서 여러가지 값을 받을 수 있음   
:heavy_check_mark: request.getParameterNames() > while문을 통해서 서버 쪽에 보내진 객체를 확인 가능

---

### JSP 스크립트
html 파일에 java 관련 코드를 삽입하여 jsp 파일을 만드는 방법   

#### :fire: Servlet <-> JSP
* __servlet__ : 순수 자바 파일   
xxx.java -> xxx.class   
* __Jsp__ : jsp 파일 + HTML 파일   
xxx.jsp -> xxx_jsp.java -> xxx_jsp.class   

#### :fire: JSP 주요 스크립트
* 선언 태그 : JSP 페이지에서 Java의 멤버변수 또는 메서드 선언
```java
	<%!
		int num = 10;
		public exampleMethod() {
			System.out.println("exaple");
		}
	%>
```
* 주석 태그 : 
```html
	<!-- --> html 주석 태그
	<%-- --%> JSP 주석 태그
```
* 스크립트릿 태그 : JSP 페이지에서 Java 코드를 넣기 위한 태그
```java
	<%
	if(num > 0) {
	%>
		<p>if</p>
	<% } else { %>
		<p>else</p>
	<%>} <%>
```
* 표현식 태그 : Java의 변수 및 메서드의 반환값을 출력하는 태그
```java
	<%=number%>
```
* 지시어 : 서버에서 jsp 페이지를 처리하는 방법에 대한 정의
	* page : 페이지 기본 설정 > 거의 변하지 않음 
	* :heavy_check_mark: __include__ : 다른 JSP 파일을 사용하고 싶은 경우
	```java
	<%@ include file="header.jsp"%>
	```
	* taglib : 외부 라이브러리 태그 설정
	```java
	<%@ taglib url = "외부 라이브러리 url" prefix="c" %>
	```
----

### JSP request, response
사용자의 요청과 웹 서버의 응답을 담당하는 객체  
* Servlet과 내용이 비슷함 > 같은 request, response 객체를 사용하기 때문

#### :fire: response 객체
response.sendRedirect("example.js"); 
바로 리다이렉트로 보내버리는 메소드

--- 
### JSP 내장객체
requset, response 외 JSP에서 기본적으로 제공하는 객체들
#### :fire: config 객체
web.xml에 데이터를 저장해놓고 __getInitParameter()__ 메소드를 통해서 JSP에서 데이터를 사용 할 때 이용하는 객체
__web.xml__
```xml
	<servlet-name>servletEx</servlet-name>
	<jsp-file>/jspEx.jsp</jsp-file>
	<init-param>
		<param-name>adminId</param-name>
		<param-value>admin</param-value>
	</init-param>
	<init-param>
		<param-name>adminPw</param-name>
		<param-value>1234</param-value>
	</init-param>
	<servlet-mapping>servletEx</servlet-mapping>
	<url-pattern>/jspEx.jsp</url-pattern>
```
__jspEx.jsp__
```java
	String adminId = config.getInitParameter("adminId");
	String adminPw = config.getInitParameter("adminPw");
```
#### :fire: application 객체
하나의 jsp가 아니라 어플리케이션 전체에서 사용하기 위해서 사용. 어플리케이션 전체 공유를 위해 사용.
__web.xml__
```xml

	<context-param>
		<param-name>imgDir</param-name>
		<param-value>/upload/img</param-value>
	</context-param>
```
__jspEx.jsp__
```java
	String imgDir = application.getInitParameter("imgDir");   
	    
	appication.setAttibute("ex", "example");
	String ex = (String)application.getAttribute("ex"); // string으로 반환해서 저장 필요
```
#### :fire: out 객체
out.print(); 출력 객체   

#### :fire: exception 객체
* `<@ page errorPage="errorPage.jsp" %>`  
이 페이지에서 에러가 발생 한 경우는 errorPage.jsp로 이동한다는 의미 
* `<@ page isErrorPage="true" %>`   
이 페이지는 에러 페이지로 이용 하겠다는 
의미

exception.getMessage(); 메소드를 통해서 에러 메세지 확인 가능

---
### Servlet 데이터 공유
Servlet에서 데이터를 공유하는 방법   
JSP에서 사용했던 방식과 비슷하게 동일   

---
### Cookie
* 클라이언트와 서버의 연결을 유지시켜주는 방법
#### :fire: Cookie란?
* 서버와 클라이언트가 연결을 시도했던 흔적을 남기는 것 > 그 흔적을 가지고 과거에 연결이 되었다는 것을 알고 이용할 수 있음
* http 프로토콜은 브라우저와 서버의 연결이 requset, response 단계를 한 번 유지하고 난 뒤에는 바로 연결을 끊음/한번 요청, 한번 응답 후 자원 해지 > 서버 부하 방지   

ex) 쇼핑몰 : 물건을 여러개 구매 하는 경우에 여러개를 장바구니에 넣는 동안 로그인 정보는 계속 유지되어야 함.    

 :heavy_check_mark: 쿠키 : 해당 브라우저 클라이언트에 기존 연결정보를 저장함. 저장되어있는 데이터 정보 역시 클라이언트 쪽에 저장됨.
  
#### :fire: Cookie 구현
쿠키는 배열로 정의

Cookie[]  cookies = requset.getCookies();    
response.addCookie(cookie);
cookie.setMaxAge();   

http 프로토콜에서 많이 사용 될 기법이지만 보안에 취약 할 수 있음.  사용자의 정보가 로컬 pc에 저장되므로 중요한 정보의 경우에는 쿠키에 저장하지 않는 것이 바람직.

---
### Session
클라이언트와 서버의 연결을 유지시켜주는 Cookie와는 또 다른 방법    
쿠키 (클라이언트 생성 및 저장) <-> 세션(웹 컨테이너/서버에서 생성 및 저장)   
쿠키는 보안상 취약점이 있기 때문에 세션을 더 많이 사용 

#### :fire: Session이란?
공통점 : http 프로토콜을 사용하기 때문에 연결은 반드시 사용 후 끊기게 되는데 그 이후 재연결을 하기 위한 방식 

#### :fire: Session 구현
HttpSession session = request.getSession(); 
session.setAttribute(" ", xx);
session.invalidate(); // 세션 삭제 메소드

---
### 한글처리
한글이 정상적으로 출력될 수 있는 방법   

#### :fire: 한글처리
1) POST : 서블릿, jsp 파일에 `request.setCharacterEncoding("UTF-8");`
`response.setContentType("text/html; charset=UTF-8");` 
2) GET : server.xml에 `<Connector URIEncoding="UTF-8"/>` 추가   


#### :fire: Filter
* 웹 브라우저와 서버가 통신을 할 때 필터를 통해서 한 번 걸러내서 통신을 함. 
* Filter에 인코딩을 포함시켜주면 모든 파일에 일일히 추가 할 필요 없이 한 번에 해결 가능 
* Filter 인터페이스를 구현하는 클래스 생성(ex: 클래스명 : TempFilter)
```xml
<filter>
	<filter-name>tempFilter</filter-name>
	<filter-class>com.servlet.filter.TempFilter</filter-class>
</filter>
```
---
### JDBC   
자바와 오라클이 통신 할 수 있는 방법   
#### :fire: JDBC 설정
* __JDBC__ : 자바와 데이터베이스가 통신 할 수 있게 해주는 API 
* 오라클용 JDBC를 사용해줘야 함 
* __JDBC 설정__
	windows > preferences > java > build path > classpath variables > 사용하는 jre의 경로를 알 수 있음, 외부 라이브러리를 사용하는 경우 이 경로에서 추가해주면 됨   

#### :fire: JDBC를 통한 데이터관리
client -> jsp, servlet -> DataBase   
1. OracleDriver 로딩 : `Class.forName(driver);`
2. Java와 Oracle 연결(connection) : `con=DriverManager.getConnection(url, id, pw);`
3. Query 전송 객체(statement) : `stmt = con.createStatement();` 통신을 하기 위한 전송 객체 생성
4. Query 작성 : `String sql = "SELECT * FROM EMP";`
5. Query 전송 : `res = stmt.executeQuery(sql);` 

finally문에서 꼭 자원 해제를 해줘야 함   
```java
finally {
	try {
	if(stmt != null) stmt.close();
	if(con != null) con.close();
	}catch(Exception ex) {
		ex.printStackTrace();
	}
```
executeQuery(select문) <-> executeUpdate(update, insert문)

#### :fire: PrepareStatement
* 쿼리문을 전부 작성하는 것이 아니라 비워둠. 
* 코드의 중복 및 실수 방지

```java
	String sql = "update book set book_loc = ? where book_name = ?";
	pstmt = con.prepareStatement(sql); 
	pstmt.setString(1, "111-2212");
	pstmt.setString(2, "book2"); 
```

---
### DAO와 DTO
데이터 베이스와 통신하기 위한 기능을 모듈화하는 방법
#### :fire: DAO, DTO란?
DAO : Data Access Object , 데이터 베이스와 연결 해주는 역할
DTO : Data Transfer Object, 값 저장

#### :fire: DAO, DTO 구현
브라우저 <-> [ Servlet <-> DAO  ] <- DTO - 데이터베이스  
데이터 베이스와 관련된 내용을 DAO 객체로 구분해줌   

---
### Connection Pool
데이터 베이스와 통신하는 자원을 효율적으로 관리하기 위한 방법

#### :fire: 커넥션 풀이란?
브라우저 -> request -> 웹 서버 ---> DB Access -> 데이터베이스   
기존 DB Access 단계 1. DB Connection 2. Data Handling 3. DB connection close   
문제점 :  웹 서비스 사용 중에는 서버에 수차례 DB Connection이 필요한데  이렇게 사용하는 경우 계속 같은 작업을 반복함으로 작업에 부화가 될 수 있음. > Connection Pool이라는 경로를 통해서 rent, return을 통해서 사용 가능 (효율적) 

#### :fire: 커넥션 풀 설정
server > context.xml

```xml
	<Resource auth = "Container"
	driverClassName = "oracle.jdbc.driver.OracleDriver"
	url = "jdbc:oracle:thin:@localhost:1521:xe"
	username = "scott"
	password = "123456"
	name="jdbc/Oracle11g" // 커넥션 풀의 이름
	type="javax.sql.DataSource" // 커넥션 풀 생성 API
	maxActive="4" 
	maxWait="10000"
```

#### :fire: 커넥션 풀 구현
```java
	public BookDAO() {
		try {
			Context context = new InitialContext();
			DataSource dataSource = (DataSource)context.lookup("java:comp/env/jdbc/Oracle11g");
		}catch(Exception e) {
			e.printStackTarace();
		}
	}
```
