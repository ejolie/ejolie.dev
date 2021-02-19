---
title: 웹 서버, 서블릿 컨테이너, 웹 애플리케이션 서버
date: '2021-02-19'
template: 'post'
draft: false
slug: 'web-server-and-others'
category: 'Dev'
tags:
  - 'Web Architecture'
description: ''
socialImage: ''
---

자바로 웹 개발을 할 때 자주 헷갈리는 개념인 웹 서버, 서블릿 컨테이너, 웹 애플리케이션 서버에 대해 간단히 정리해 보았다.

# 웹 서버(Web Server)

- 웹 서버는 **HTTP 프로토콜을 통해 클라이언트(브라우저)의 요청을 받아 응답으로 HTML 문서와 같은 정적 콘텐츠를 제공**해주는 소프트웨어 또는 하드웨어를 말한다.

- 예시
  - Apache HTTP Server
  - Nginx
  - Internet Information Services (IIS)



# 서블릿 컨테이너(Servlet Container) = 웹 컨테이너(Web Container)

- 서블릿 컨테이너는 **JSP/Servlet과 같은 서버 사이드 기술을 이용해 동적 콘텐츠를 제공**해주기 위한 웹 서버의 구성 요소다.

- **Java EE 명세 중 Servlet API만 구현한 것**을 서블릿 컨테이너라 한다. Java EE의 다른 기술을 서블릿 컨테이너에서 사용하기 위해서는 classpath에 jar 파일을 추가해야 한다.
- 웹 애플리케이션 서버 중에서 HTTP 요청을 받아 처리하는 기초 역할을 맡는다.

- 서블릿의 생명 주기를 관리하고, URL과 특정 서블릿을 맵핑하며 요청과 응답 객체를 생성 및 관리한다.
- 대부분의 웹 프레임워크가 제공하는 기능은 서블릿 컨테이너 위에서 동작하는 서블릿, 필터, 이벤트 리스너 등을 적절히 조합해 구현한 것이다. 따라서 사용자가 웹 프레임워크로 작성한 웹 애플리케이션은 결국 서블릿 컨테이너 위에서 동작한다.
- 예시
  - Apache Tomcat
  - Eclipse Jetty



## 서블릿(Servlet)

- 서블릿은 **자바로 웹 서비스를 제공하는 서버측 프로그램(서버에서 실행되는 자바 클래스)**이다.
- 클라이언트의 요청에 따라 동적으로 웹 페이지를 제공한다.
- `javax.servlet.Servlet` 인터페이스를 구현해야 한다.
- 스레드 방식으로 실행된다.
- 서블릿 vs. 일반적인 자바 프로그램
  - 일반적인 자바 프로그램: `public static void main(String[] args)` 메서드가 있어야 한다. main 메서드가 프로그램의 시작점이며 main 메서드가 끝나면 프로그램도 종료된다.
  - 서블릿: 서블릿 컨테이너에 등록된 후 서블릿 컨테이너에 의해 생성, 호출, 소멸이 이뤄진다. 즉, 서블릿은 독립적으로 실행되지 않고, main 메서드가 필요하지 않으며, 서블릿 컨테이너에 의해 서블릿의 상태가 바뀐다.



## JSP(JavaServer Pages)

- JSP는 HTML 문서 안에 자바 코드를 넣어 동적 웹 페이지를 만드는 기술이다.
- JSP에는 HTML, CSS, JavaScript 뿐만 아니라 다른 JSP 구성 요소들이 포함된다.
- JSP 파일 자체를 브라우저로 전송하게 되면 브라우저는 JSP 요소들을 해석하지 못한다. 따라서, JSP는 브라우저로 전송되기 전에 서블릿 컨테이너에 의해 변환 과정을 거친다.
  1. Translation: `*.jsp` -> `*.java` (서블릿으로 변환)
  2. Compile: `*.java` -> `*.class`
  3. Interpret: `*.class` 실행 -> 결과(HTML, CSS, JavaScript 코드) 응답



# 웹 애플리케이션 서버(WAS, Web Application Server)

- 좁은 의미
  - 웹 애플리케이션 서버는 **Java EE의 모든 명세를 구현한 자바 구현체**를 말한다.
  - 서블릿 컨테이너 + EJB 컨테이너
- 넓은 의미
  - 웹 애플리케이션 서버는 <u>**동적 웹 프로그래밍을 위한 미들웨어**</u>의 한 종류이다.
- 예시
  - Oracle Glassfish
  - IBM Websphere
  - Oracle Web Logic
  - RedHat Wildfly



## Apache Tomcat

**과거에는 Java EE의 일부만 지원하는 Tomcat을 서블릿 컨테이너 또는 웹 서버로 분류했다.** 하지만 최근에 EJB의 대안으로 Spring과 같은 경량 프레임워크를 사용하게 되면서 classpath에 필요한 라이브러리의 jar 파일을 추가하는 것만으로도 웹 애플리케이션 서버 대신 서블릿 컨테이너를 사용할 수 있게 되었고 그래서 **넓은 의미로 Tomcat을 웹 애플리케이션 서버라고 한다.**

참고로 Tomcat은 하나의 거대한 자바 애플리케이션이기도 하다. Tomcat을 기동하기 위해서는 JRE 환경의 JVM 상에서 `org.apache.catalina.startup.Bootstrap` 클래스를 실행해야 하기 때문이다. 따라서 Tomcat 실행을 위해 자바는 필수적이며 이는 자바 베이스의 모든 WAS에 해당되는 사항이다.



## 웹 서비스 구성: WEB-WAS?

과거에는 웹 소스 내 각종 이미지, CSS, JavaScript 등 정적 콘텐츠를 처리하기 위해 WEB-WAS를 분리 구성하는 경우가 많았다고 한다. **즉, 정적 콘텐츠 서빙을 위해 웹 서버(예: Apache HTTP Server)를, 동적 콘텐츠 생성을 위해 웹 애플리케이션 서버(예: Apache Tomcat)를 사용하는 것이다.** 이렇게 하면 웹 서버가 정적 콘텐츠 처리 역할을 담당하게 되어 Tomcat의 처리 부하가 줄어들게 된다.

하지만 최근에는 APR/Native를 사용하면서 Tomcat I/O 성능이 더욱 향상되었으며 **Tomcat 8.0 부터는 URL Rewrite와 같은 웹 서버 특유의 기능들까지 제공하고 있다.** 또한 CDN을 구성하는 사이트가 늘어나고 있어 단지 정적 컨텐츠 처리를 위해서 WEB-WAS를 분리 구성하는 경우는 예전만큼 많지 않다고 한다.



# 참고자료

- https://javajee.com/web-server-web-container-and-application-server

- https://ducmanhphan.github.io/2020-04-01-The-difference-between-web-server-web-container-application-server/

- 최진식, 《자바고양이 Tomcat 이야기》, 좋은땅

- 최희탁, 《웹 프로그래머를 위한 서블릿 컨테이너의 이해》, 한빛미디어

- 이병승, 《자바 웹을 다루는 기술》, 길벗