---
title: Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법
seo-title: Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법
description: 이 안내서에서는 AEM 기반 프로젝트를 개발하는 데 Eclipse를 사용하는 방법에 대해 설명합니다
seo-description: 이 안내서에서는 AEM 기반 프로젝트를 개발하는 데 Eclipse를 사용하는 방법에 대해 설명합니다
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---


# Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법{#how-to-develop-aem-projects-using-eclipse}

이 안내서에서는 AEM 기반 프로젝트를 개발하는 데 Eclipse를 사용하는 방법에 대해 설명합니다.

>[!NOTE]
>
>이제 Adobe은 Eclipse를 사용하여 AEM 솔루션을 개발하는 데 도움이 되는 [AEM Development Tools for Eclipse](/help/sites-developing/aem-eclipse.md)를 제공합니다.

## 개요 {#overview}

Eclipse에 대한 AEM 개발을 시작하려면 다음 단계가 필요합니다.

각 내용은 본 사용 방법(How-To)의 나머지 부분에서 더 자세히 설명되어 있습니다.

* Eclipse 4.3 설치(Kepler)
* Maven을 기반으로 AEM 프로젝트 설정
* Maven POM에서 Eclipse에 대한 JSP 지원 준비
* Eclipse로 Maven 프로젝트 가져오기

>[!NOTE]
>
>이 안내서는 Eclipse 4.3(Kepler) 및 AEM 5.6.1을 기반으로 합니다.

## Eclipse {#install-eclipse} 설치

[Eclipse 다운로드 페이지](https://www.eclipse.org/downloads/)에서 &quot;Java EE 개발자를 위한 Eclipse IDE&quot;를 다운로드하십시오.

[설치 지침](https://wiki.eclipse.org/Eclipse/Installation)에 따라 Eclipse를 설치합니다.

## Maven {#set-up-your-aem-project-based-on-maven}을(를) 기반으로 AEM 프로젝트 설정

다음으로, Apache Maven](/help/sites-developing/ht-projects-maven.md)을 사용하여 AEM 프로젝트를 빌드하는 방법[에 설명된 대로 Maven을 사용하여 프로젝트를 설정하십시오.

## Eclipse {#prepare-jsp-support-for-eclipse}에 대한 JSP 지원 준비

Eclipse는 JSP를 사용하여 작업하는 경우에도 지원합니다(예:

* 태그 라이브러리의 자동 완성
* &lt;cq:defineObjects /> 및 &lt;sling:defineObjects />에 의해 정의된 개체의 Eclipse-award

이를 실현하려면

1. [Apache Maven](/help/sites-developing/ht-projects-maven.md)을 사용하여 AEM 프로젝트를 빌드하는 방법[JSP를 사용한 작업 방법](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)의 지침을 따릅니다.
1. 컨텐츠 모듈의 POM에서 &lt;build /> 섹션에 다음을 추가합니다.

   Eclipse의 Maven 지원 플러그인 m2e는 maven-jspc-plugin에 대한 지원을 제공하지 않으며, 이 구성은 m2e가 임시 컴파일 결과를 정리하는 플러그인 및 관련 작업을 무시하도록 합니다.

   문제가 아닙니다.[JSP를 사용하여 작업 방법](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)에 명시된 대로, 이 설정의 maven-jspc-plugin은 해당 JSP가 빌드 프로세스의 일부로 컴파일되었는지 확인하는 데만 사용됩니다. Eclipse는 이미 JSP의 문제를 보고하므로 이 Maven 플러그인을 사용하지 않아도 됩니다.

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

### Eclipse {#import-the-maven-project-into-eclipse}로 Maven 프로젝트 가져오기

1. Eclipse에서 파일 > 가져오기...를 선택합니다.
1. [가져오기] 대화 상자에서 [Maven] > [기존 Maven 프로젝트]를 선택한 다음 &quot;다음&quot;을 클릭합니다.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 프로젝트의 최상위 폴더 경로를 입력한 다음 &quot;모두 선택&quot; 및 &quot;마침&quot;을 클릭합니다.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 이제 JSP 자동 완성 등 AEM 프로젝트를 개발하기 위해 Eclipse를 모두 사용할 수 있습니다.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >`/libs/foundation/global.jsp` 또는 다른 JSP를 `/libs`에 포함하는 경우 Eclipse가 포함을 해결할 수 있도록 해당 JSP를 프로젝트에 복사해야 합니다. 동시에 Maven이 콘텐츠 패키지에 번들로 제공되지 않는지 확인해야 합니다. 이를 달성하기 위한 방법은 [Apache Maven](/help/sites-developing/ht-projects-maven.md)을 사용하여 AEM 프로젝트를 빌드하는 방법에 설명되어 있습니다.

