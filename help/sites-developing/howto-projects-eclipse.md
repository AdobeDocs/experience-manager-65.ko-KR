---
title: Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법
seo-title: Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법
description: 이 안내서에서는 AEM 기반 프로젝트를 개발하기 위해 Eclipse를 사용하는 방법에 대해 설명합니다
seo-description: 이 안내서에서는 AEM 기반 프로젝트를 개발하기 위해 Eclipse를 사용하는 방법에 대해 설명합니다
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16

---


# Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법{#how-to-develop-aem-projects-using-eclipse}

이 안내서에서는 AEM 기반 프로젝트를 개발하기 위해 Eclipse를 사용하는 방법에 대해 설명합니다.

>[!NOTE]
>
>Adobe는 이제 Eclipse [용 AEM 개발](/help/sites-developing/aem-eclipse.md) 도구를 제공하여 Eclipse를 사용하여 AEM 솔루션을 개발할 수 있도록 지원합니다.

## 개요 {#overview}

Eclipse에 대한 AEM 개발을 시작하려면 다음 단계가 필요합니다.

각각의 내용은 본 사용 방법(How-To)의 나머지 부분에서 더 자세히 설명합니다.

* Eclipse 4.3(Kepler) 설치
* Maven을 기반으로 AEM 프로젝트 설정
* Maven POM에서 Eclipse에 대한 JSP 지원 준비
* Eclipse로 Maven 프로젝트 가져오기

>[!NOTE]
>
>이 안내서는 Eclipse 4.3(Kepler) 및 AEM 5.6.1을 기반으로 합니다.

## Eclipse 설치 {#install-eclipse}

Eclipse 다운로드 페이지에서 &quot;Java EE 개발자를 위한 Eclipse [IDE&quot;를](https://www.eclipse.org/downloads/)다운로드하십시오.

설치 지침에 따라 Eclipse [를 설치합니다](https://wiki.eclipse.org/Eclipse/Installation).

## Maven을 기반으로 AEM 프로젝트 설정 {#set-up-your-aem-project-based-on-maven}

그런 다음 Apache Maven을 사용하여 AEM 프로젝트 [빌드 방법 설명에 따라 Maven을 사용하여 프로젝트를 설정합니다](/help/sites-developing/ht-projects-maven.md).

## Eclipse에 대한 JSP 지원 준비 {#prepare-jsp-support-for-eclipse}

또한 Eclipse는 JSP를 사용하여 작업할 수 있도록 지원합니다(예:

* 태그 라이브러리 자동 완성
* &lt;cq:defineObjects /> 및 &lt;sling:defineObjects />에 의해 정의된 개체의 Eclipse-award

이를 위해 다음을 수행합니다.

1. Apache Maven을 사용하여 [AEM 프로젝트](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 빌드 [방법 작성의 JSP 사용 방법에 대한 지침을 따르십시오](/help/sites-developing/ht-projects-maven.md).
1. 콘텐트 모듈의 POM에서 &lt;build /> 섹션에 다음을 추가합니다.

   Eclipse의 Maven 지원 플러그인 m2e는 maven-jspc-plugin에 대한 지원을 제공하지 않으며, 이 구성은 m2e가 임시 컴파일 결과를 정리하는 플러그인 및 관련 작업을 무시하도록 합니다.

   문제가 아닙니다.JSP를 [사용한 방법](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)작업에 설명된 바와 같이, 이 설정의 maven-jspc-plugin은 빌드 프로세스의 일부로 해당 JSP가 컴파일되었는지 확인하는 데만 사용됩니다. Eclipse는 이미 JSP의 문제를 보고하므로 이 Maven 플러그인을 사용할 수 없습니다.

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Eclipse로 Maven 프로젝트 가져오기 {#import-the-maven-project-into-eclipse}

1. Eclipse에서 파일 > 가져오기...를 선택합니다.
1. 가져오기 대화 상자에서 Maven > Existing Maven Projects를 선택한 다음 &quot;다음&quot;을 클릭합니다.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 프로젝트의 최상위 폴더 경로를 입력한 다음 &quot;모두 선택&quot; 및 &quot;마침&quot;을 클릭합니다.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 이제 JSP 자동 완성 기능을 포함하여 AEM 프로젝트를 개발하기 위해 Eclipse를 사용할 수 있습니다.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >에 `/libs/foundation/global.jsp` 또는 다른 JSP를 포함하는 `/libs`경우 Eclipse가 포함을 해결할 수 있도록 프로젝트에 복사해야 합니다. 동시에 Maven이 콘텐츠 패키지에 번들로 제공되지 않도록 해야 합니다. 이를 실현하는 방법은 Apache Maven을 [사용하여 AEM 프로젝트를 빌드하는 방법에 설명되어 있습니다](/help/sites-developing/ht-projects-maven.md).

