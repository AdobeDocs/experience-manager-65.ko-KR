---
title: Maven을 사용하여 패키지 관리
seo-title: Maven을 사용하여 패키지 관리
description: Content Package Maven 플러그인을 사용하여 패키지 관리 작업을 Maven 프로젝트에 통합
seo-description: Content Package Maven 플러그인을 사용하여 패키지 관리 작업을 Maven 프로젝트에 통합
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Maven을 사용하여 패키지 관리{#managing-packages-using-maven}

Content Package Maven 플러그인을 사용하여 패키지 관리 작업을 Maven 프로젝트에 통합할 수 있습니다. 플러그인 목표 및 매개 변수를 사용하면 패키지 관리자 페이지 또는 FileVault 명령줄을 사용하여 일반적으로 수행하는 많은 작업을 자동화할 수 있습니다.

* 파일 시스템의 파일에서 새 패키지를 만듭니다.
* CRX 또는 CQ 서버에서 패키지를 설치하고 제거합니다.
* 서버에 이미 정의된 패키지를 빌드합니다.
* 서버에 설치된 패키지 목록을 확인합니다.
* 서버에서 패키지를 제거합니다.

## POM 파일에 Content Package Maven 플러그인 추가 {#adding-the-content-package-maven-plugin-to-the-pom-file}

Content Package Maven 플러그인을 사용하려면 POM 파일의 빌드 요소 내에 다음 플러그인 요소를 추가하십시오.

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Maven이 플러그인을 다운로드할 수 있도록 하려면 이 페이지의 Obtaining the Content Package Maven [Plugin](#obtaining-the-content-package-maven-plugin) 섹션에 제공된 프로필을 사용하십시오.

## Content Package Maven Plugin의 목표 {#goals-of-the-content-package-maven-plugin}

Content Package 플러그인이 제공하는 목표 및 목표 매개 변수는 다음에 나오는 섹션에 설명되어 있습니다. 공통 매개변수 섹션에 설명된 매개 변수는 대부분의 목표에 사용할 수 있습니다. 한 목표에 적용되는 매개 변수는 해당 목표에 대한 섹션에 설명되어 있습니다.

**플러그인 접두사**

플러그인 접두사는 content-package입니다. 다음 예와 같이 명령줄에서 목표를 실행하려면 이 접두사를 사용합니다.

```shell
mvn content-package:build
```

**매개 변수 접두사**

별도로 명시되지 않는 한, 다음 예와 같이 플러그인 목표와 매개 변수는 vault 접두사를 사용합니다.

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**프록시**

CRX 또는 CQ 서버의 프록시를 사용하는 목적은 Maven 설정에 있는 첫 번째 유효한 프록시 구성을 사용합니다. 프록시 구성을 찾을 수 없으면 프록시가 사용되지 않습니다. 일반 설정 섹션에서 useProxy 매개 변수를 참조하십시오.

### 공통 매개 변수 {#common-parameters}

다음 표의 매개 변수는 목표 열에 언급된 경우를 제외하고 모든 목표에 공통입니다.

<table>
 <tbody>
  <tr>
   <th>이름</th>
   <th>유형</th>
   <th>필수</th>
   <th>기본 값</th>
   <th>설명</th>
   <th>목표</th>
  </tr>
  <tr>
   <td>failOnError</td>
   <td>부울</td>
   <td>아니오</td>
   <td>false</td>
   <td>값이 <code>true</code> 있으면 오류가 발생할 때 빌드가 실패합니다. 값이 값을 <code>false</code> 지정하면 빌드가 오류를 무시합니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
  <tr>
   <td>이름</td>
   <td>문자열</td>
   <td>빌드:예<br /> 설치:rm 없음<br /> :예</td>
   <td>빌드:기본값은 없습니다.<br /> 설치:Maven 프로젝트의 artifactId 속성 값입니다.</td>
   <td>작동할 패키지의 이름입니다.</td>
   <td>Ls를 제외한 모든 목표.</td>
  </tr>
  <tr>
   <td>암호</td>
   <td>문자열</td>
   <td>예</td>
   <td>admin</td>
   <td>CRX 서버와의 인증에 사용되는 암호입니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>문자열</td>
   <td>아니오</td>
   <td></td>
   <td>인증을 위해 사용자 이름과 암호를 검색할 서버 ID입니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>문자열</td>
   <td>예</td>
   <td>http://localhost:4502/<br /> crx/packmgr/<br /> service.jsp</td>
   <td>CRX 패키지 관리자의 HTTP 서비스 API의 URL입니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
  <tr>
   <td>timeout</td>
   <td>int</td>
   <td>아니오</td>
   <td>5</td>
   <td>패키지 관리자 서비스와 통신하는 데 필요한 연결 시간(초)입니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>부울</td>
   <td>아니오</td>
   <td>true</td>
   <td>Maven 설정 파일의 프록시 구성을 사용할지 여부를 결정합니다. 의 <code>true</code> 값으로 인해 패키지 관리자에 대한 프록시 요청에 검색된 첫 번째 활성 프록시 구성이 사용됩니다. false 값을 지정하면 프록시가 사용되지 않습니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>문자열</td>
   <td>예</td>
   <td>admin</td>
   <td>CRX 서버에 인증할 사용자 이름입니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
  <tr>
   <td>verbose</td>
   <td>부울</td>
   <td>아니오</td>
   <td>false</td>
   <td>자세한 로깅을 활성화하거나 비활성화합니다. 에 대한 값은 자세한 로깅을 <code>true</code> 활성화합니다.</td>
   <td>패키지를 제외한 모든 목표</td>
  </tr>
 </tbody>
</table>

### build {#build}

AEM 인스턴스에 이미 정의된 콘텐츠 패키지를 빌드합니다.

>[!NOTE]
>
>이 목표는 Maven 프로젝트 내에서 실행할 필요가 없습니다.

#### 매개 변수 {#parameters}

빌드 목표에 대한 모든 매개 변수는 공통 매개 변수 [섹션에 설명되어](#common-parameters) 있습니다.

#### 예 {#example}

다음 예에서는 IP 주소 10.36.79.223을 사용하여 AEM 인스턴스에 설치된 workflow-mbean 패키지를 만듭니다.목표는 다음 명령을 사용하여 실행됩니다.

```shell
mvn content-package:build
```

다음 POM 파일은 명령줄 도구의 현재 디렉토리에 있습니다. POM 파섹

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### install {#install}

메모리에 패키지를 설치합니다. 이 목표를 실행해도 Maven 프로젝트가 필요하지 않습니다. 목표는 Maven 빌드 라이프사이클의 설치 단계에 바인딩됩니다.

#### 매개 변수 {#parameters-1}

다음 매개 변수 외에 공통 매개 변수 [섹션의 설명을 참조하십시오](#common-parameters) .

<table>
 <tbody>
  <tr>
   <th>이름</th>
   <th>유형</th>
   <th>필수</th>
   <th>기본 값</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>아티클</td>
   <td>문자열</td>
   <td>아니오</td>
   <td>Maven 프로젝트의 artifactId 속성 값입니다.</td>
   <td>groupId:artifactId:version[:packaging] 형식의 문자열입니다.</td>
  </tr>
  <tr>
   <td>artifactId</td>
   <td>문자열</td>
   <td>아니오</td>
   <td></td>
   <td>설치할 아티팩트의 ID</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>문자열</td>
   <td>아니오</td>
   <td></td>
   <td>설치할 아티팩트의 groupId</td>
  </tr>
  <tr>
   <td>install</td>
   <td>부울</td>
   <td>아니오</td>
   <td>true</td>
   <td>패키지가 업로드될 때 패키지를 자동으로 압축 해제할지 여부를 결정합니다. true로 설정하면 패키지의 압축을 풀고 false로 설정하면 패키지 압축을 풀지 않습니다.</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven.<br /> 아티팩트를 만듭니다. 저장소.<br /> ArtifactRepository</td>
   <td>아니오</td>
   <td>localRepository 시스템 변수의 값입니다.</td>
   <td>로컬 Maven 저장소입니다. 플러그인 구성을 사용하여 이 매개 변수를 구성할 수 없습니다. system 속성은 항상 사용됩니다.</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>아니오</td>
   <td>Maven 프로젝트에 대해 정의된 주요 아티팩트입니다.</td>
   <td>설치할 패키지 파일의 이름입니다.</td>
  </tr>
  <tr>
   <td>패키징</td>
   <td>문자열</td>
   <td>아니오</td>
   <td>zip</td>
   <td>설치할 아티팩트의 패키징 유형</td>
  </tr>
  <tr>
   <td>pomRemoteRepository</td>
   <td>java.util.List</td>
   <td>예</td>
   <td>Maven 프로젝트에 대해 정의된 remoteAtivityRepository 속성의 값.</td>
   <td>이 값은 플러그인 구성을 사용하여 구성할 수 없습니다. 프로젝트에 값을 지정해야 합니다. </td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>예</td>
   <td>플러그인이 구성된 프로젝트입니다.</td>
   <td>Maven 프로젝트. 프로젝트에 플러그인 구성이 포함되어 있으므로 프로젝트는 암시적입니다.</td>
  </tr>
  <tr>
   <td>repositoryId <i>(POM)</i><br /> repoID <i>(명령줄)</i></td>
   <td>문자열</td>
   <td>아니오</td>
   <td>temp</td>
   <td>객체가 검색되는 저장소의 ID입니다. POM 파섹 명령줄에서 repoID를 사용합니다.</td>
  </tr>
  <tr>
   <td>repositoryUrl <i>(POM)</i><br /> repoURL <i>(명령줄)</i></td>
   <td>문자열</td>
   <td>아니오</td>
   <td></td>
   <td>객체가 검색되는 저장소의 URL입니다. POM 파섹 명령줄에서 repoURL을 사용합니다.</td>
  </tr>
  <tr>
   <td>version</td>
   <td>문자열</td>
   <td>아니오</td>
   <td></td>
   <td>설치할 아티팩트의 버전.</td>
  </tr>
 </tbody>
</table>

#### 예 {#example-1}

다음 예제에서는 workflow-mbean OSGi 번들을 포함하는 패키지를 생성한 후( [빌드](#build) 목표 예 참조) 패키지를 설치합니다. 설치 목표는 패키지 설치 단계에 바인딩되므로 다음 명령은 설치 목표를 실행합니다.

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

패키지 관리자에 배포된 패키지를 나열합니다.

#### 매개 변수 {#parameters-2}

ls 목표에 대한 모든 매개 변수는 공통 매개 변수 [섹션에 설명되어](#common-parameters) 있습니다.

#### 예 {#example-2}

다음 예는 IP 주소 10.36.79.223을 사용하여 AEM 인스턴스에 설치된 패키지를 나열합니다.목표는 다음 명령을 사용하여 실행됩니다.

```shell
mvn content-package:ls
```

다음 POM 파일은 명령줄 도구의 현재 디렉토리에 있습니다. POM 파섹

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

패키지 관리자에서 패키지를 제거합니다.

#### 매개 변수 {#parameters-3}

rm 목표의 모든 매개 변수는 공통 매개변수 [섹션에 설명되어](#common-parameters) 있습니다.

#### 예 {#example-3}

다음 예에서는 IP 주소가 10.36.79.223인 AEM 인스턴스에 설치된 workfow-mbean 패키지를 제거합니다.목표는 다음 명령을 사용하여 실행됩니다.

```shell
mvn content-package:rm
```

다음 POM 파일은 명령줄 도구의 현재 디렉토리에 있습니다. POM 파섹

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### uninstall {#uninstall}

패키지를 제거합니다. 패키지가 제거된 상태의 서버에 남아 있습니다.

#### 매개 변수 {#parameters-4}

제거 목표에 대한 모든 매개 변수는 공통 매개 변수 [섹션에 설명되어](#common-parameters) 있습니다.

#### 예 {#example-4}

다음 예에서는 IP 주소 10.36.79.223을 사용하여 AEM 인스턴스에 설치된 workflow-mbean 패키지를 제거합니다.목표는 다음 명령을 사용하여 실행됩니다.

```shell
mvn content-package:uninstall
```

다음 POM 파일은 명령줄 도구의 현재 디렉토리에 있습니다. POM 파섹

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

콘텐츠 패키지를 만듭니다. 패키지 목표의 기본 구성에는 컴파일된 파일이 저장되는 디렉토리의 컨텐츠가 포함됩니다. 패키지 목표를 실행하려면 컴파일 빌드 단계가 완료되어야 합니다. 패키지 목표는 Maven 빌드 라이프사이클의 패키지 단계에 바인딩됩니다.

#### 매개 변수 {#parameters-5}

다음 매개 변수 외에 공통 매개 변수 섹션에서 `name` 매개 변수의 [설명을 참조하십시오](#common-parameters) .

<table>
 <tbody>
  <tr>
   <th>이름</th>
   <th>유형</th>
   <th>필수</th>
   <th>기본 값</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>아카이브</td>
   <td>org.apache.maven.<br /> archiver.<br /> MavenArchiveConfiguration</td>
   <td>아니오</td>
   <td></td>
   <td>사용할 아카이브 구성 Maven <a href="https://maven.apache.org/shared/maven-archiver/index.html">Archiver 설명서를 참조하십시오</a>.</td>
  </tr>
  <tr>
   <td>builtContentDirectory</td>
   <td>java.io.File</td>
   <td>예</td>
   <td>Maven 빌드의 출력 디렉토리 값.</td>
   <td>패키지에 포함할 컨텐츠가 들어 있는 디렉토리.</td>
  </tr>
  <tr>
   <td>종속성</td>
   <td>java.util.List</td>
   <td>아니오</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddedTarget</td>
   <td>java.lang.String</td>
   <td>아니오</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>임베드</td>
   <td>java.util.List</td>
   <td>아니오</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failOnMissingEmbed</td>
   <td>부울</td>
   <td>예</td>
   <td>false</td>
   <td>true 값은 포함된 아티팩트가 프로젝트 종속성에서 없으면 빌드가 실패합니다. 값을 사용할 경우 빌드가 오류를 무시합니다.</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>아니오</td>
   <td></td>
   <td>작업 영역 필터의 소스를 지정하는 파일입니다. 구성에 지정된 필터와 임베드 또는 하위 패키지를 통해 주입된 필터는 파일 컨텐츠와 병합됩니다.</td>
  </tr>
  <tr>
   <td>필터</td>
   <td>com.day.jcr.<br /> vault.maven.pack.impl.<br /> DefaultWorkspaceFilter</td>
   <td>아니오</td>
   <td></td>
   <td>패키지 컨텐츠를 정의하는 필터 요소를 포함합니다. 필터를 실행하면 filter.xml 파일에 필터가 포함됩니다. 아래의 필터 사용 섹션을 참조하십시오.</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>예</td>
   <td>Maven 프로젝트에 정의된 finalName(빌드 단계).</td>
   <td>생성된 패키지 ZIP 파일의 이름이며 .zip 파일 확장자가 없습니다.</td>
  </tr>
  <tr>
   <td>그룹</td>
   <td>java.lang.String</td>
   <td>예</td>
   <td>Maven 프로젝트에 정의된 groupID입니다.</td>
   <td>생성된 콘텐츠 패키지의 groupId입니다. 이 값은 콘텐트 패키지에 대한 대상 설치 경로의 일부입니다.</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>예</td>
   <td>Maven 프로젝트에 정의된 빌드 디렉터리입니다.</td>
   <td>컨텐츠 패키지가 저장되는 로컬 디렉토리입니다.</td>
  </tr>
  <tr>
   <td>접두사</td>
   <td>java.lang.String</td>
   <td>아니오</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>예</td>
   <td></td>
   <td>Maven 프로젝트.</td>
  </tr>
  <tr>
   <td>속성</td>
   <td>java.util.Map</td>
   <td>아니오</td>
   <td></td>
   <td>properties.xml 파일에서 설정할 수 있는 추가 속성입니다. 이러한 속성은 다음과 같은 사전 정의된 속성을 덮어쓸 수 없습니다.
    <ul>
     <li>그룹:그룹 매개 변수를 사용하여</li>
     <li>name:name 매개 변수를 사용하여 설정</li>
     <li>버전:버전 매개 변수를 사용하여</li>
     <li>description:프로젝트 설명에서 설정</li>
     <li>groupId:maven 프로젝트 설명자의 groupId</li>
     <li>artifactId:maven 프로젝트 설명자의 artifactId</li>
     <li>종속성:종속성 매개 변수를 사용하여</li>
     <li>createdBy:user.name 시스템 속성의 값</li>
     <li>생성됨:현재 시스템 시간</li>
     <li>requiresRoot:requiresRoot 매개 변수를 사용하여</li>
     <li>packagePath:그룹 및 패키지 이름에서 자동으로 생성</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requiresRoot</td>
   <td>부울</td>
   <td>예</td>
   <td>false</td>
   <td>패키지에 루트가 필요한지 여부를 정의합니다. 이렇게 하면 properties.xml 파일의 &lt;code&gt;requiresRoot&lt;/code&gt; 속성이 됩니다.</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.List</td>
   <td>아니오</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>version</td>
   <td>java.lang.String</td>
   <td>예</td>
   <td>Maven 프로젝트에 정의된 버전</td>
   <td>컨텐츠 패키지의 버전입니다.</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>예</td>
   <td>Maven 프로젝트에 정의된 디렉토리(빌드 단계).</td>
   <td>패키지에 포함할 컨텐츠가 들어 있는 디렉토리.</td>
  </tr>
 </tbody>
</table>

#### 필터 사용 {#using-filters}

필터 요소를 사용하여 패키지 컨텐츠를 정의합니다. 필터는 패키지의 `META-INF/vault/filter.xml` 파일에서 workspaceFilter 요소에 추가됩니다.

다음 필터 예제에서는 사용할 XML 구조를 보여 줍니다.

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**가져오기 모드**

이 `mode` 요소는 패키지를 가져올 때 저장소가 영향을 받는 방식을 정의합니다. 다음 값을 사용할 수 있습니다.

* **** 병합:저장소에 아직 없는 패키지의 컨텐츠가 추가됩니다. 패키지와 저장소 모두에 있는 컨텐츠는 변경되지 않습니다. 저장소에서 제거된 컨텐츠가 없습니다.
* **** 바꾸기:저장소에 없는 패키지의 컨텐츠가 저장소에 추가됩니다. 저장소의 컨텐츠는 패키지의 일치하는 컨텐츠로 대체됩니다. 컨텐츠가 패키지에 없을 때 저장소에서 제거됩니다.
* **** 업데이트:저장소에 없는 패키지의 컨텐츠가 저장소에 추가됩니다. 저장소의 컨텐츠는 패키지의 일치하는 컨텐츠로 대체됩니다. 기존 컨텐츠가 저장소에서 제거됩니다.

필터에 `mode` 요소가 없으면 기본값이 `replace` 사용됩니다.

#### 예 {#example-5}

다음 예제에서는 workflow-mbean OSGi 번들을 포함하는 패키지를 만듭니다. POM 파일은 jcr_root 디렉토리를 builtContentDirectory 속성의 값으로 식별합니다. jcr_root 디렉토리에는 저장소를 미러링하는 디렉토리 구조에 있는 번들 JAR 파일이 포함되어 있습니다.

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

목표는 패키지 빌드 단계에 바인딩되므로 다음 명령은 패키지 목표를 실행합니다.

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

플러그인 `package` 섹션에서 목표를 표현하는 대신 프로젝트 `executions` 요소의 `content-package` `packaging` 값으로 사용할 수 있습니다.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### 도움말 {#help}

#### 매개 변수 {#parameters-6}

| 이름 | 유형 | 필수 | 기본 값 | 설명 |
|---|---|---|---|---|
| 세부 정보 | 부울 | 아니오 | false | 각 목표에 대해 모든 설정 가능한 속성을 표시할지 여부를 결정합니다. true 값은 모든 설정 가능한 속성을 표시합니다. |
| 목표 | 문자열 | 아니오 |  | 도움말을 표시할 목표의 이름입니다. 값을 지정하지 않으면 모든 목표에 대한 도움말이 표시됩니다. |
| indentSize | int | 아니오 | 2 | 각 수준의 들여쓰기에 사용할 공백의 수입니다. 값을 지정하는 경우 이 값은 양수여야 합니다. |
| lineLength | int | 아니오 | 80 | 표시 라인의 최대 길이입니다. 값을 지정하는 경우 이 값은 양수여야 합니다. |

## Content Package Maven Plugin 얻기 {#obtaining-the-content-package-maven-plugin}

이 플러그인은 공개 Adobe 저장소에서 사용할 수 있습니다. 플러그인을 다운로드하려면 다음 Maven 프로필을 Maven 설정 파일에 추가하고 활성화하십시오. Maven 명령을 사용하면 필요한 경우 플러그인이 로컬 리포지토리로 다운로드됩니다.

>[!NOTE]
>
>Adobe Public Releases 저장소가 검색 가능하지 않으므로 웹 브라우저를 사용하여 저장소 URL로 이동하면 찾을 수 없음 오류가 발생합니다. 그러나 Maven은 저장소 디렉토리에 액세스할 수 있습니다.

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```

## 컨텐츠 패키지에 OSGi 번들 포함 {#embedding-osgi-bundles-in-a-content-package}

Content Package Maven Plugin을 사용하여 OSGi 번들을 컨텐츠 패키지에 포함합니다. 번들을 포함하려면 다음 구성을 구현합니다.

* 번들은 Maven 프로젝트의 종속성으로 선언되어야 합니다.
* 플러그인 구성은 패키지에 있는 번들의 원하는 경로를 사용하여 번들을 참조합니다.

다음 POM은 Apache Sling JCR UserManager 번들을 포함하는 패키지를 만듭니다. 패키지에서 번들 JAR는 `jcr_root/apps/myapp/install` 폴더에 있습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## 패키지에 축소판 이미지 또는 속성 파일 포함 {#including-a-thumbnail-image-or-properties-file-in-the-package}

기본 패키지 구성 파일을 대체하여 패키지 속성을 사용자 정의합니다. 예를 들어 축소판 이미지를 포함하여 패키지 관리자 및 패키지 공유에서 패키지를 구별할 수 있습니다.

패키지에서 FileVault 관련 파일은 /META-INF/vault 폴더에 있습니다. 소스 파일은 파일 시스템의 어느 위치에서나 찾을 수 있습니다. POM 파일에서 빌드 리소스를 정의하여 패키지에 포함할 소스 파일을 대상/vault-work/META-INF에 복사합니다.

다음 POM 코드는 프로젝트 소스의 META-INF 폴더에 있는 파일을 패키지에 추가합니다.

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

다음 POM 코드는 축소판 이미지만 패키지에 추가합니다. 축소판 이미지의 이름은 thumbnail.png여야 하며 패키지의 META-INF/vault/definition 폴더에 있어야 합니다. 이 예에서 소스 파일은 프로젝트의 /src/main/content/META-INF/vault/definition 폴더에 있습니다.

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## AEM 프로젝트 생성을 위해 원형 사용 {#using-archetypes-to-generate-aem-projects}

AEM 프로젝트를 생성하는 데 몇 가지 Maven 원형을 사용할 수 있습니다. 개발 목표에 맞는 원형을 사용하십시오.

* AEM 응용 프로그램용 리소스를 설치하는 콘텐츠 패키지: [simple-content-package-tranype](#simple-content-package-archetype)
* 타사 객체를 포함하는 컨텐츠 패키지: [simple-content-package-with-embedded-tranype](#simple-content-package-with-embedded-archetype).
* Java 클래스 및 단위 테스트 개발을 지원하는 다중 모듈 응용 프로그램: [multimodule-content-package-tranype](#multimodule-content-package-archetype).

>[!NOTE]
>
>Apache Sling 프로젝트는 AEM 개발에 유용한 원형도 제공합니다. 이러한 내용은 https://sling.apache.org/site/maven-archetypes.html에 [설명되어 있습니다](https://sling.apache.org/documentation/development/maven-archetypes.html).

각 원형은 다음 항목을 생성합니다.

* 프로젝트 폴더 구조.
* POM 파일.
* FileVault 구성 파일.

Adobe Public Maven 보관소에서는 원형 객체에 대한 정보를 확인할 수 있습니다. 원형형을 다운로드하고 실행하려면 Maven 전형(generate command)의 매개 변수를 사용하여 원형 및 Adobe 저장소를 식별합니다.

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

Maven 원형 플러그인은 셸이나 명령 프롬프트에서 대화형 모드를 사용하여 프로젝트에 대한 정보를 수집합니다. 제공하는 정보는 폴더 이름 및 객체 ID와 같은 다양한 프로젝트 속성을 구성하는 데 사용됩니다.

**POM 파일**

생성된 POM 파일에는 코드를 컴파일하고 번들을 만들고 패키지에서 AEM에 배포하는 명령이 포함되어 있습니다. Maven 프로젝트의 `groupID`속성, `artifactId``version`및 `name` 속성은 `archetype:generate` 대화형 프롬프트에 제공하는 값을 사용하여 자동으로 채워집니다.

생성된 pom.xml 파일에서 다음 기본값을 변경할 수 있습니다.

* CQ 서버 이름 또는 IP 주소:기본값은 `localhost`입니다. 아래 `crx.host` 요소에는 이 값이 `project/properties` 포함되어 있습니다.

* CQ 서버의 포트 번호:기본값은 `4502`입니다. 아래 `crx.port` 요소에는 이 값이 `project/properties` 포함되어 있습니다.

* Content Package Maven Plugin의 버전:최신 버전을 와 함께 플러그인의 `version` 요소 컨텐츠로 `artifactId` 사용합니다 `content-package-maven-plugin`. 기본값은 `0.0.24`입니다.

**원형 사용**

1. 셸 창이나 명령 프롬프트에서 Maven `archetype:generate` 명령을 입력합니다. 메시지가 표시되면 나머지 매개 변수에 대한 값을 제공합니다.

   각 매개 변수에 대한 자세한 내용은 사용 중인 원형의 섹션을 참조하십시오.

1. 텍스트 편집기를 사용하여 pom.xml 파일을 열고 요구 사항에 따라 기본값을 편집합니다.
1. 생성된 폴더를 리소스로 채웁니다.
1. 명령을 `mvn clean install` 입력합니다.

### simple-content-package-tranype {#simple-content-package-archetype}

간단한 AEM 응용 프로그램에 대한 리소스를 설치하는 데 적합한 마스터 프로젝트를 만듭니다. 폴더 구조는 AEM 저장소의 `/apps` 폴더 아래에 사용됩니다. POM 파섹

**원형 아티팩트 속성:**

* 그룹 ID: `com.day.jcr.vault`
* 아티팩트 ID: `simple-content-package-archetype`
* 버전: `1.0.2`
* 보관소: `adobe-public-releases`

**Maven 명령:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**원형 매개변수:**

* groupId:Maven이 생성하는 콘텐츠 패키지의 groupId입니다. 이 값은 POM 파일에서 자동으로 사용됩니다.
* artifactId:컨텐츠 패키지의 이름입니다. 이 값은 프로젝트 폴더의 이름으로도 사용됩니다.
* 버전:컨텐츠 패키지의 버전입니다.
* 패키지:이 값은 simple-content-package-tranype에 사용되지 않습니다.
* appsFolderName:/apps 아래의 폴더 이름.
* artifactName:컨텐츠 패키지에 대한 설명입니다.
* packageGroup:컨텐츠 패키지 그룹의 이름입니다. 이 값은 Content Package Maven 플러그인의 Package 목표에 대한 그룹 매개 변수를 구성합니다.

**폴더 구조:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### simple-content-package-with-embedded-tranype {#simple-content-package-with-embedded-archetype}

단순 컨텐츠 패키지 전원과 동일한 작업을 수행하고 공개 Maven 저장소의 아티팩트를 다운로드하고 포함합니다.

**원형 번들 속성:**

* 그룹 ID: `com.day.jcr.vault`
* 아티팩트 ID: `simple-content-package-with-embedded-archetype`
* 버전: `1.0.2`
* 보관소: `adobe-public-releases`

**Maven 명령:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**원형 매개변수:**

* groupId:Maven이 생성하는 콘텐츠 패키지의 groupId입니다. 이 값은 POM 파일에서 자동으로 사용됩니다.
* artifactId:컨텐츠 패키지의 이름입니다. 이 값은 프로젝트 폴더의 이름으로도 사용됩니다.
* 버전:컨텐츠 패키지의 버전입니다.
* 패키지:이 매개 변수는 사용되지 않습니다.
* appsFolderName:/apps 아래의 폴더 이름.
* artifactName:컨텐츠 패키지에 대한 설명입니다.
* embeddedArtifactId:컨텐츠 패키지에 포함할 아티팩트의 ID입니다.
* embeddedGroupId:포함할 아티팩트의 그룹 ID입니다.
* embeddedVersion:포함할 아티팩트의 버전.
* packageGroup:컨텐츠 패키지 그룹의 이름입니다. 이 값은 Content Package Maven 플러그인의 Package 목표에 대한 그룹 매개 변수를 구성합니다.

**폴더 구조:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### multimodule-content-package-tranype {#multimodule-content-package-archetype}

AEM 애플리케이션을 개발하고 서버에 리소스를 설치하기 위한 폴더 구조가 포함된 마스터 프로젝트를 만듭니다.

이 `bundle` 폴더에는 사용자가 개발한 Java 및 JUnit 소스 파일을 저장하는 폴더 구조가 들어 있습니다. 이 폴더의 pom.xml 파일은 OSGi 번들을 만듭니다. POM의 다음 값은 가공물과 번들을 식별합니다.

* artifactID: `${artifactID}-bundle`Adobe
* 번들-기호 이름: `${groupId}.${artifactId}-bundle`Adobe

`${artifactID}` 원본은 `${groupId}` 실행할 때 이러한 매개 변수에 대해 제공하는 값입니다.

이 `content` 폴더에는 AEM 인스턴스에 설치된 리소스가 포함되어 있습니다. artifactID의 값은 `${artifactID}multimodule-bundle`입니다.

상위 폴더에는 Maven 플러그인 및 종속성을 관리하는 부모 POM이 포함되어 있습니다.

**원형 번들 속성:**

* 그룹 ID: `com.day.jcr.vault`
* 아티팩트 ID: `multimodule-content-package-archetype`
* 버전: `1.0.2`
* 보관소: `adobe-public-releases`

**Maven 명령:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**원형 매개변수:**

* groupId:Maven이 생성하는 콘텐츠 패키지의 groupId입니다. 이 값은 POM 파일에서 자동으로 사용됩니다.
* artifactId:컨텐츠 패키지의 이름입니다. 이 값은 프로젝트 폴더의 이름으로도 사용됩니다.
* 버전:컨텐츠 패키지의 버전입니다.
* 패키지:이 값은 다중 모듈-content-package-tranype에 사용되지 않습니다.
* appsFolderName:/apps 아래의 폴더 이름.
* artifactName:컨텐츠 패키지에 대한 설명입니다.
* packageGroup:컨텐츠 패키지 그룹의 이름입니다. 이 값은 Content Package Maven 플러그인의 Package 목표에 대한 그룹 매개 변수를 구성합니다.

**폴더 구조:**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

