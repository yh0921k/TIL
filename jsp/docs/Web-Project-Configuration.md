# JSP 프로젝트 구성

**방법 01**

GraalVM(JDK) + Eclipse + Tomcat 환경에서 Hello World를 작성해본다.



### 이클립스에서 프로젝트 준비

- [File] - [New] - [Project]로 이클립스에서 프로젝트를 생성할 수 있다.
- 항목 중 [Web]에서 [Dynamic Web Project]를 선택하고 JSP 개발을 위한 프로젝트를 만든다.
- 프로젝트 이름을 설정하고, 필요에 따라 [Target Runtime]과 [Configuration]을 설정한다.
  - 현재는 `<None>`, `<custum>`으로 진행
- 다음 단계는 소스 폴더를 설정하는 것인데, [src] 디렉토리를 사용한다.
  - 자바 소스코드는 [src]에 존재하며, 컴파일된 바이트 코드는 [build\classes]에 존재함을 알 수 있다.

- Web Module 설정에서는 Context Root와 Content Directory를 볼 수 있다.

  - Context Root는 어플리케이션의 접속 경로를 설정한다.
    - 만약 test라고 지정할 경우 웹에서의 접속 경로는 https://localhost:8080/test 가 된다.

  - Context Directory는 JSP, HTML, 이미지 등의 파일이 위치할 디렉터리이다.
    - 기본값을 사용한다.
  - 마지막으로 아래의 web.xml 생성은 체크를 하도록 한다.
    - 추후에 다시 다루겠지만, 어플리케이션과 관련된 설정 내용을 저장하는 파일이다.

- 추가적으로 프로젝트 생성 도중 이클립스 레이아웃을 JavaEE로 변경할 것인지를 선택하는 상자가 나온다. 
  - JavaEE Perspective는 웹 개발에 적합하므로 변경하도록 한다.



### Hello World 프로그램 작성

- [Web Content] - [New] - [Folder] - [Test]
- [Test] - [New] - [JSP File]
  - 파일이름은 HelloWorld.jsp이며 템플릿은 New Jsp File(html 5)를 사용한다.
- jsp 파일을 만들고 나면 코드 왼쪽 상단에 `<%` 부분에 빨간줄이 그이면서 에러를 명시한다.

###### Error 해결방법

- 프로젝트에 오른쪽 버튼을 클릭하면 Properties 항목이 있다. 
- 해당 항목에서 왼쪽 탭에 Project Facets를 누른다.
- 이후 [Java] - [Runtime]에서 설치한 Tomcat 디렉토리를 지정하면 에러가 사라진다.

```jsp
<!-- 아래는 page 지시어로, JSP 페이지 형식을 지정한다. JPS 파일에 기본적으로 들어가 있어야 하며 추후에 다시 설명한다. -->
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>HelloWorld</h1>
    <!-- 아래는 간단한 JSP 표현식이다. -->
	new java.util.Date() : <%=new java.util.Date()%>
</body>
</html>
```



### 서버 설정

- JSP 파일을 선택하고 [Run As] - [Run on Server]를 선택해 설치한 톰캣을 선택한다.
- [Next]를 선택하면 다음 화면에서는 톰캣이 설치된 폴더를 지정한다.
- [Next]를 선택하면 다음 화면에서는 실행에 포함시킬 프로젝트를 선택한다.
- 실행 확인을 위한 다른 방법은, http://localhost:8080/project_name/jsp_file_name 에 연결할 수 있다.

---



**방법 02**

GraalVM(JDK) + Eclipse + Tomcat + gradle 환경에서  HelloWorld.jsp를 작성해본다.

- webstudy라는 폴더를 만든 후 gradle init으로 초기화
  - Application, Java, Groovy, JUnit4 순서로 선택
- 프로젝트 폴더에서 build.gradle 파일을 열어 수정

``` groovy
plugins {    
    id 'java'
    
    // 기존의 application 삭제 하고 아래 두 줄 추가
    id 'eclipse-wtp'
    id 'war'
}
repositories {
    jcenter()
}
dependencies {
    // 이 내용은 mvnrepository.com/ 에서 Java Servlet API를 선택하고 Gradle에 있는 내용 복사
    providedCompile group: 'javax.servlet', name: 'javax.servlet-api', version: '4.0.1'
    
    implementation 'com.google.guava:guava:28.0-jre'
    testImplementation 'junit:junit:4.12'
}
// 아래의 application { ... } 삭제
```

- gradle eclipse 수행
- src/main/webapp 추가
  - 아래에 index.html 추가
- src/main/java/App.java 삭제
- src/test/java/AppTest.java 삭제

- 이클립스에 프로젝트 추가
  - [File] - [Import] - [Existing Projects into Workspace] 에서 프로젝트 폴더 추가
- 아래의 Servers에서 Tomcat 실행
  - Tomcat v9.0 Server at localhost 오른쪽버튼 - Add and Remove - 프로젝트 추가
- 웹 브라우저에서 http://localhost:8080/project-name/index.html

---

