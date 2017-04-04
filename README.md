# spring

Maven 기초 사용법
Maven-Gradle-Ant 2008.12.17 10:32 
본 글에서는 Maven을 이용해서 프로젝트를 생성하는 방법과, 디렉토리 구조, POM 파일 기본 구성, Maven 라이프 사이클 그리고 Maven 프로젝트를 이클립스 프로젝트로 생성하는 방법을 살펴보도록 하겠다.

본 글의 내용 중 일부를 현재 메이븐 버전인 3.2에 맞게 수정했다. - 2014년 12월

Maven 설치

http://maven.apache.org/ 사이트를 방문하면, 최신 버전의 메이븐을 다운로드 받을 수 있다. 이 글을 쓰는 시점에서 메이븐 최신 버전은 3.2.3이다. 바이너리 배포판을 다운로드 받은 아무 곳이나 원하는 디렉토리에 압축을 푼다. 설치 과정은 다음과 같다.
다운로드 받은 파일의 압축을 푼다. 예, apache-maven-3.2.3.zip 파일의 압축을 C:에 풀면 c:\apache-maven-3.2.3 디렉토리가 생성된다.
PATH 환경 변수에서 메이븐 bin 디렉토리를 추가한다. 
예) PATH=c:\apache-maven-3.2.3\bin;%PATH%
JAVA_HOME 환경 변수가 올바르게 설정되어 있는지 확인한다. 참고로, 메이븐 3.2 버전은 자바 1.6 이상을 요구한다.
설치를 끝냈으면, 다음 명령어를 실행해서 메이븐이 올바르게 동작하는지 확인한다.
환경 변수를 모두 설정해 주었다면 아래의 명령어를 사용해서 Maven이 제대로 실행되는 지 확인해보자.

C:\Users\madvirus>mvn -version
Apache Maven 3.2.3 (33f8c3e1027c3ddde99d3cdebad2656a31e8fdf4; 2014-08-12T05:58:10+09:00)
Maven home: C:\devtool\apache-maven-3.2.3
Java version: 1.8.0_20, vendor: Oracle Corporation
Java home: C:\Java\jdk1.8.0_20\jre
Default locale: ko_KR, platform encoding: MS949
OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"

Maven 프로젝트 생성하기
설치가 끝났다면 Maven 프로젝트를 생성해 보자. 명령 프롬프트에서 아래 명령어를 실행하면 된다. (아래 명령어를 처음 실행할 경우 꽤 오랜 시간이 걸리는데, 그 이유는 Maven이 필요한 플러그인과 모듈을 다운로드 받기 때문이다. Maven 배포판은 최초로 Maven을 사용하는 데 필요한 모듈만 포함하고 있고, 그 외에 archetype 플러그인, compiler 플러그인 등 Maven을 사용하는 데 필요한 모듈은 포함하고 있지 않다. 이들 모듈은 실제로 필요할 때 Maven 중앙 리포지토리에서 로딩된다.)

mvn archetype:generate

위 명령어를 실행하면 Maven 프로젝트를 생성하는 데 필요한 정보를 입력하라는 메시지가 단계적으로 뜨고, 각 항목별로 알맞은 값을 입력해주면 된다. 아래는 실행 화면 예이다. 붉은색으로 표시한 것은 입력한 값이다.

C:\Users\madvirus>mvn archetype:generate
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] ------------------------------------------------------------------------
[INFO]
...생략
Choose archetype:
1: remote -> br.com.ingenieux:elasticbeanstalk-service-webapp-archetype (A Maven Archetype Encompassing RestAssured, Jetty, Jackson, Guice and Jersey for Publishing JAX-RS-based Services on AWS' Elastic Beanstalk Service)
2: remote -> br.com.otavio.vraptor.archetypes:vraptor-archetype-blank (A simple project to start with VRaptor 4)
...생략
436: remote -> org.apache.maven.archetypes:maven-archetype-quickstart (An archetype which contains a sample Maven project.)
437: remote -> org.apache.maven.archetypes:maven-archetype-site (An archetype which contains a sample Maven site which demonstrates some of the supported document types like
    APT, XDoc, and FML and demonstrates how to i18n your site. This archetype can be layered
    upon an existing Maven project.)
...생략
1090: remote -> uk.ac.rdg.resc:edal-ncwms-based-webapp (-)
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 436: [엔터]
Choose version:
1: 1.0-alpha-1
2: 1.0-alpha-2
3: 1.0-alpha-3
4: 1.0-alpha-4
5: 1.0
6: 1.1
Choose a number: 6: [엔터]
Define value for property 'groupId': : net.madvirus
Define value for property 'artifactId': : sample
Define value for property 'version':  1.0-SNAPSHOT: : [엔터]
Define value for property 'package':  net.madvirus: :  [엔터]
Confirm properties configuration:
groupId: net.madvirus
artifactId: sample
version: 1.0-SNAPSHOT
package: net.madvirus
 Y: : [엔터]
 [INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Old (1.x) Archetype: maven-archetype-quickstart:1.1
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: groupId, Value: net.madvirus
[INFO] Parameter: packageName, Value: net.madvirus
[INFO] Parameter: package, Value: net.madvirus
[INFO] Parameter: artifactId, Value: sample
[INFO] Parameter: basedir, Value: C:\Users\madvirus
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] project created from Old (1.x) Archetype in dir: C:\Users\madvirus\sample

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 25:52 min
[INFO] Finished at: 2014-07-02T15:17:56+09:00
[INFO] Final Memory: 12M/111M
[INFO] ------------------------------------------------------------------------
C:\Users\madvirus>

위 과정에서 실제로 입력하는 값은 다음과 같다.
groupId - 프로젝트 속하는 그룹 식별 값. 회사, 본부, 또는 단체를 의미하는 값이 오며, 패키지 형식으로 계층을 표현한다. 위에서는 net.madvirus를 groupId로 이용하였다.
artifactId - 프로젝트 결과물의 식별 값. 프로젝트나 모듈을 의미하는 값이 온다. 위에서는 sample을 artifactId로 이용하였다.
version - 결과물의 버전을 입력한다. 위에서는 기본 값인 1.0-SNAPSHOT을 사용하였다.
package - 기본적으로 생성할 패키지를 입력한다. 별도로 입력하지 않을 경우 groupId와 동일한 구조의 패키지를 생성한다.
Maven 프로젝트의 기본 디렉토리 구조

archetype:generate 골이 성공적으로 실행되면, artifactId에 입력한 값과 동일한 이름의 디렉터리가 생성된다. 위 경우에는 현재 디렉터리에 sample 이라는 하위 디렉터리가 생성된다. 위 과정에서 선택한 archetype은 maven-archetype-quickstart 인데, 이 archetype을 선택했을 때 생성되는 디렉터리 구조는 다음과 같다.

sample
├─src
│   ├─main
│   │  └─java
│   │      └─net
│   │          └─madvirus
│   │              └─App.java
│   ├─test
│       └─java
│           └─net
│               └─madvirus
│                   └─AppTest.java
└─pom.xml

기본적으로 생성되는 디렉터리를 포함한 Maven 프로젝트의 주요 디렉터리는 다음과 같다.
src/main/java - 자바 소스 파일이 위치한다.
src/main/resources - 프로퍼티나 XML 등 리소스 파일이 위치한다. 클래스패스에 포함된다.
src/main/webapp - 웹 어플리케이션 관련 파일이 위치한다. (WEB-INF 디렉터리, JSP 파일 등)
src/test/java - 테스트 자바 소스 파일이 위치한다.
src/test/resources - 테스트 과정에서 사용되는 리소스 파일이 위치한다. 테스트 시에 사용되는 클래스패스에 포함된다.
기본적으로 생성되지 않은 디렉터리라 하더라도 직접 생성해주면 된다. 예를 들어, src/main 디렉터리에 resources 디렉터리를 생성해주면 Maven은 리소스 디렉터리로 인식한다.

컴파일 해보기/테스트 실행 해보기/패키지 해보기

이제 간단하게 컴파일과 테스트를 실행해보자. 소스 코드를 컴파일 하려면 다음과 같은 명령어를 실행해주면 된다.

C:\Users\madvirus\sample>mvn compile
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building sample 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ sample ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory C:\Users\madvirus\sample\src\main\resources
[INFO]
[INFO] --- maven-compiler-plugin:2.5.1:compile (default-compile) @ sample ---
[INFO] Compiling 1 source file to C:\Users\madvirus\sample\target\classes
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.205 s
[INFO] Finished at: 2014-07-03T09:51:15+09:00
[INFO] Final Memory: 11M/110M
[INFO] ------------------------------------------------------------------------

컴파일 된 결과는 target/classes 디렉터리에 생성된다.

테스트 클래스를 실행해보고 싶다면, 다음과 같은 명령어를 사용하면 된다.

$ mvn test
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building sample 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ sample ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/madvirus/sample/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.5.1:compile (default-compile) @ sample ---
[INFO] Compiling 1 source file to /Users/madvirus/sample/target/classes
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ sample ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/madvirus/sample/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.5.1:testCompile (default-testCompile) @ sample ---
[INFO] Compiling 1 source file to /Users/madvirus/sample/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ sample ---
...최초 실행시 관련 플러그인 파일 다운로드
-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running net.madvirus.AppTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.005 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 10.238 s
[INFO] Finished at: 2014-07-03T22:20:08+09:00
[INFO] Final Memory: 13M/228M
[INFO] ------------------------------------------------------------------------

그러면, 테스트 코드를 컴파일한 뒤 테스트 코드를 실행한다. 그리고 테스트 성공 실패 여부를 화면에 출력한다. 컴파일 된 테스트 클래스들은 target/test-classes 디렉터리에 생성되고, 테스트 결과 리포트는 target/surefire-reports 디렉터리에 저장된다.

(아무것도 한게 없으니 당연하지만) 모든 코드가 정상적으로 만들어지고 테스트도 통과했으니, 이제 배포 가능한 jar 파일을 만들어보자. 아래 명령어를 실행하면 프로젝트를 패키징해서 결과물을 생성한다.

$ mvn package
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building sample 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ sample ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/madvirus/sample/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.5.1:compile (default-compile) @ sample ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ sample ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/madvirus/sample/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.5.1:testCompile (default-testCompile) @ sample ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ sample ---
[INFO] Surefire report directory: /Users/madvirus/sample/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running net.madvirus.AppTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.005 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ sample ---
[INFO] Building jar: /Users/madvirus/sample/target/sample-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.783 s
[INFO] Finished at: 2014-07-03T22:21:59+09:00
[INFO] Final Memory: 8M/156M
[INFO] ------------------------------------------------------------------------

mvn package가 성공적으로 실행되면, target 디렉터리에 프로젝트 이름과 버전에 따라 알맞은 이름을 갖는 jar 파일이 생성된다. 위 예제의 경우에는 sample-1.0-SNAPSHOT.jar 파일이 생성된 것을 확인할 수 있다.

POM 파일 기본

Maven 프로젝트를 생성하면 pom.xml 파일이 프로젝트 루트 디렉터리에 생성된다. 이 pom.xml 파일은 Project Object Model 정보를 담고 있는 파일로서, 이 파일에서 다루는 주요 설정 정보는 다음과 같다.
프로젝트 정보 - 프로젝트의 이름, 개발자 목록, 라이센스 등의 정보를 기술
빌드 설정 - 소스, 리소스, 라이프 사이클 별 실행할 플러그인 등 빌드와 관련된 설정을 기술
빌드 환경 - 사용자 환경 별로 달라질 수 있는 프로파일 정보를 기술
POM 연관 정보 - 의존 프로젝트(모듈), 상위 프로젝트, 포함하고 있는 하위 모듈 등을 기술
archetype:create 골 실행시 maven-archetype-quickstart Archetype을 선택한 경우 생성되는 pom.xml 파일은 다음과 같다.

[기본으로 생성되는 pom.xml 파일]
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>net.madvirus</groupId>
  <artifactId>sample</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>sample</name>
  <url>http://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>

위 POM 파일에서 프로젝트 정보를 기술하는 태그는 다음과 같다.
<name> - 프로젝트 이름
<url> - 프로젝트 사이트 URL
POM 연관 정보는 프로젝트간 연관 정보를 기술하는데, 관련 태그는 다음과 같다.
<groupId> - 프로젝트의 그룹 ID 설정
<artifactId> - 프로젝트의 Artifact ID 설정
<version> - 버전 설정
<packaging> - 패키징 타입 설정. 위 코드의 경우 프로젝트의 결과 Artifact가 jar 파일로 생성됨을 의미한다. jar 뿐만 아니라 웹 어플리케이션을 위한 war나 JEE를 위한 ear 등의 패키징 타입이 존재한다.
<dependencies> - 이 프로젝트에서 의존하는 다른 프로젝트 정보를 기술한다.
<dependency> - 의존하는 프로젝트 POM 정보를 기술
<groupId> - 의존하는 프로젝트의 그룹 ID
<artifactId> - 의존하는 프로젝트의 artifact ID
<version> - 의존하는 프로젝트의 버전
<scope> - 의존하는 범위를 설정
의존 설정

<dependency> 부분의 설정에 대해서 좀 더 살펴보도록 하자.

Maven을 사용하지 않을 경우 개발자들은 코드에서 필요로 하는 라이브러리를 각각 다운로드 받아야 한다. 예를 들어, 아파치 commons DBCP 라이브러리를 사용하기 위해서는 DBCP 뿐만 아니라 common pool 라이브러리도 다운로드 받아야 한다. 물론, commons logging을 비롯한 라이브러리도 모두 추가로 다운로드 받아 설치해 주어야 한다. 즉, 코드에서 필요로 하는 라이브러리 뿐만 아니라 그 라이브러리가 필요로 하는 또 다른 라이브러리도 직접 찾아서 설치해 주어야 한다.

하지만, Maven을 사용할 경우에는 코드에서 직접적으로 사용하는 모듈에 대한 의존만 추가해주면 된다. 예를 들어, commons-dbcp 모듈을 사용하고 싶은 경우 다음과 같은 <dependency> 코드만 추가해주면 된다.

<dependency>
    <groupId>commons-dbcp</groupId>
    <artifactId>commons-dbcp</artifactId>
    <version>1.2.1</version>
</dependency> 

그러면, Maven은 commons-dbcp 뿐만 아니라 commons-dbcp가 의존하는 라이브러리를 자동으로 처리해준다. 실제로 1.2.1 버전의 commons-dbcp 모듈의 pom.xml 파일을 보면 의존 부분이 다음과 같이 설정되어 확인할 수 있다.

  <dependencies>
    <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
      <version>2.1</version>
    </dependency>
    <dependency>
      <groupId>commons-pool</groupId>
      <artifactId>commons-pool</artifactId>
      <version>1.2</version>
    </dependency>
    <dependency>
      <groupId>javax.sql</groupId>
      <artifactId>jdbc-stdext</artifactId>
      <version>2.0</version>
      <optional>true</optional>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>xml-apis</groupId>
      <artifactId>xml-apis</artifactId>
      <version>2.0.2</version>
    </dependency>
    <dependency>
      <groupId>xerces</groupId>
      <artifactId>xerces</artifactId>
      <version>2.0.2</version>
    </dependency>
  </dependencies>

Maven은 commons-dbcp 모듈을 다운로드 받을 때 관련 POM 파일도 함께 다운로드 받는다. (다운로드 받은 파일은 로컬 리포지토리에 저장되는데 이에 대한 내용은 뒤에서 다시 설명하겠다.) 그리고 POM 파일에 명시한 의존 모듈을 함께 다운로드 받는다. 즉, commons-dbcp 1.2.1 버전의 경우 commons-collections 2.1 버전과 commons-pool 1.2 버전 등을 함께 다운로드 받는다. 이런 식으로 반복해서 다운로드 받은 모듈이 필요로 하는 모듈을 다운로드 받고 이들 모듈을 현재 프로젝트에서 사용할 클래스패스에 추가해준다.

따라서, 개발자는 일일이 필요한 모듈을 다운로드 받을 필요가 없으며, 현재 코드에서 직접적으로 필요로 하는 모듈에 대해서만 <dependency>로 추가해주면 된다. 나머지 의존은 모두 Maven이 알맞게 처리해준다.

search.maven.org 사이트에서 POM 정보 찾기

Maven을 사용할 때 자주 찾게 되는 사이트가 search.maven.org 이다. search.maven.org는 Maven 중앙 리포지토리에 등록된 POM 정보를 검색해주는 기능을 제공해준다. 이 사이트를 통해서 추가할 라이브러리의 <dependency> 설정 정보를 구할 수 있다.

의존의 scope: compile, runtime, provided, test

앞의 pom.xml 파일에서 <dependency> 부분을 보면 <scope>를 포함하고 있는 것과 그렇지 않은 것이 존재한다는 것을 알 수 있다. <scope>는 의존하는 모듈이 언제 사용되는 지를 설정할 때 사용되며, <scope>에 올 수 있는 값은 다음의 네 가지가 존재한다.
compile - 컴파일 할 때 필요. 테스트 및 런타임에도 클래스패스에 포함된다. <scope>를 설정하지 않을 경우 기본 값은 compile 이다.
runtime - 런타임에 필요. JDBC 드라이버 등이 예가 된다. 프로젝트의 코드를 컴파일 할 때는 필요하지 않지만, 실행할 때 필요하다는 것을 의미한다. 배포시 포함된다.
provided - 컴파일 할 때 필요하지만, 실제 런타임 때에는 컨테이너 같은 것에서 기본으로 제공되는 모듈임을 의미한다. 예를 들어, 서블릿이나 JSP API 등이 이에 해당한다. 배포시 제외된다.
test - 테스트 코드를 컴파일 할 때 필요. Mock 테스트를 위한 모듈이 예이다. 테스트 시에 클래스패스에 포함되며, 배포시 제외된다.

원격 리포지토리와 로컬 리포지토리

Maven은 컴파일이나 패키징 등 작업을 실행할 때 필요한 플러그인이나 pom.xml 파일의 <dependency> 등에 설정한 모듈을 Maven 중앙 리포지토리에서 다운로드 받는다. 현재 중앙 리포지토리의 주소는 http://repo1.maven.org/maven2/ 이다.

원격 리포지토리에서 다운로드 받은 모듈은 로컬 리포지토리에 저장된다. 로컬 리포지토리는 [USER_HOME]/.m2/repository 디렉터리에 생성되며, 로컬 리포지토리에는 다음과 같은 형식의 디렉터리를 생성한 뒤 다운로드 받은 모듈을 저장한다.

[groupId]/[artifactId]/[version]

예를 들어, commons-dbcp 1.2.1 버전의 경우, 모듈 및 관련 POM 파일이 저장되는 디렉터리는 다음과 같다.

[USER_HOME]/.m2/repository/commons-dbcp/commons-dbcp/1.2.1

위 디렉터리에 저장되는 파일은 패키징 된 모듈 파일, pom 파일, 그리고 소스 코드 다운로드 옵션을 실행한 경우에는 소스 코드를 포함한 jar 파일이 포함된다.

일단 원격 리포지토리로부터 파일을 다운로드해서 로컬 리포지토리에 저장하면, 그 뒤로는 로컬 리포지토리에 저장된 파일을 사용하게 된다.

Maven 라이프사이클(Lifecycle)과 플러그인 실행

본 글의 서두에 Maven은 프로젝트의 라이프사이클 기반 프레임워크를 제공한다고 했다. 앞서 프로젝트를 생성한 뒤 컴파일하고(mvn compile), 테스트 하고(mvn test), 패키징 하는(mvn package) 과정을 정해진 명령어를 이용해서 실행했는데, 이때 compile, test, package는 모두 빌드 라이프사이클에 속하는 단계이다.

Maven은 clean, build (default), site의 세 가지 라이프사이클을 제공하고 있다. 각 라이프사이클은 순서를 갖는 단계(phase)로 구성된다. 또한, 각 단계별로 기본적으로 실행되는 플러그인(plugin) 골(goal)이 정의되어 있어서 각 단계마다 알맞은 작업이 실행된다. 아래 표는 디폴트 라이프사이클을 구성하고 있는 주요 실행 단계를 순서대로 정리한 것이다.

[표] 디폴트 라이프사이클의 주요 단계(phase)
 단계
설명 
단계에 묶인 플러그인 실행
generate-sources
컴파일 과정에 포함될 소스를 생성한다. 예를 들어,  DB 테이블과 매핑되는 자바 코드를 생성해주는 작업이 이 단계에서 실행된다.

process-sources
필터와 같은 작업을 소스 코드에 처리한다.
 
generate-resources
패키지에 포함될 자원을 생성한다. 
 
process-resources
필터와 같은 작업을 자원 파일에 처리하고, 자원 파일을 클래스 출력 디렉토리에 복사한다.
resources:resources 
compile
소스 코드를 컴파일해서 클래스 출력 디렉터리에 클래스를 생성한다.
compiler:compile
generate-test-sources
테스트 소스 코드를 생성한다. 예를 들어, 특정 클래스에서 자동으로 테스트 케이스를 만드는 작업이 이 단계에서 실행된다.

process-test-sources
필터와 같은 작업을 테스트 소스 코드에 처리한다.
resources:testResources 
generate-test-resources
테스트를 위한 자원 파일을 생성한다. 
 
process-test-resources
필터와 같은 작업을 테스트 자원 파일에 처리하고, 테스트 자원 파일을 테스트 클래스 출력 디렉터리에 복사한다.
 
test-compile
테스트 소스 코드를 컴파일해서 테스트 클래스 추력 디렉터리에 클래스를 생성한다.
compiler:testCompile
test
테스트를 실행한다.
surefire:test
package
컴파일 된 코드와 자원 파일들을 jar, war와 같은 배포 형식으로 패키징한다.
패키징에 따라 다름
jar - jar:jar
war - war:war
pom - site:attach-descriptor
ejb - ejb:ejb
install
로컬 리포지토리에 패키지를 복사한다.
install:install
deploy
생성된 패키지 파일을 원격 리포지토리에 등록하여, 다른 프로젝트에서 사용할 수 있도록 한다.
deploy:deploy

라이프사이클의 특정 단계를 실행하려면 다음과 같이 mvn [단계이름] 명령어를 실행하면 된다.


mvn test
mvn deploy

라이프사이클의 특정 단계를 실행하면 그 단계의 앞에 위치한 모든 단계가 실행된다. 예를 들어, test 단계를 실행하면 test 단계를 실행하기에 앞서 'generate-sources' 단계부터 'test-compile' 단계까지 각 단계를 순서대로 실행한다. 각 단계가 실행될 때는 각 단계에 묶인 골(goal)이 실행된다.

플러그인을 직접 실행할 수도 있다. mvn 명령어에 단계 대신 실행할 플러그인을 지정하면 된다.

mvn surefire:test

단, 플러그인 골을 직접 명시한 경우에는 해당 플러그인만 실행되기 때문에 라이프사이클의 단계가 실행되지는 않는다.

플러그인 골(Plugin Goal)

Maven에서 플러그인을 실행할 때에는 '플러그인이름:플러그인지원골'의 형식으로 실행할 기능을 선택한다. 예를 들어, compiler:compile은 'compiler'는 플러그인에서 'compile' 기능(goal)을 실행한다는 것을 뜻한다.

맺음말

이번 글에서는 Maven의 기본 사용법을 살펴봤다. Maven이 제공하는 의존 관리는 개발자를 jar 지옥(?)에서 구해준다는 것을 알 수 있었다. 또한, Maven은 표준화된 라이프사이클을 제공하고 있기 때문에 개발자가 컴파일-테스트-패키징 등의 과정을 손으로 정의하지 않아도 되며, 개발자는 Maven이 제공하는 단계 중 필요한 단계만 실행하면 된다. 그럼, 나머지 작업(컴파일, 테스트 실행, jar 파일 생성)은 모두 Maven이 처리해준다.

다음 글에서는 많이 사용되고 있는 개발툴인 이클립스에서 Maven 프로젝트를 import하는 방법과 컴파일러 버전을 명시하는 방법을 살펴보도록 하겠다.

관련 자료:
Maven 홈 페이지: http://maven.apache.org
Maven: The Definitive Guide (Sonatype, Oreilly)
Maven 컴파일러 버전 설정


출처: http://javacan.tistory.com/entry/MavenBasic [자바캔(Java Can Do IT)]
