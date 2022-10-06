---
title: Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법
seo-title: How to Develop AEM Projects Using Eclipse
description: 이 안내서에서는 AEM 기반 프로젝트 개발에 Eclipse를 사용하는 방법을 설명합니다
seo-description: This guide describes how to use Eclipse for developing AEM based projects
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 4%

---

# Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법{#how-to-develop-aem-projects-using-eclipse}

이 안내서에서는 AEM 기반 프로젝트를 개발하기 위해 Eclipse를 사용하는 방법을 설명합니다.

>[!NOTE]
>
>이제 Adobe이 다음을 제공합니다. [Eclipse용 AEM 개발 도구](/help/sites-developing/aem-eclipse.md) Eclipse를 사용하여 AEM 솔루션을 개발하는 데 도움이 되는 솔루션입니다.

## 개요 {#overview}

Eclipse에서 AEM 개발을 시작하려면 다음 단계가 필요합니다.

각 방법은 이 방법 설명서의 나머지 부분에서 더 자세히 설명합니다.

* Eclipse 4.3 설치(Kepler)
* Maven을 기반으로 AEM 프로젝트 설정
* Maven POM에서 Eclipse에 대한 JSP 지원 준비
* Maven 프로젝트를 Eclipse로 가져오기

>[!NOTE]
>
>이 안내서는 Eclipse 4.3(Kepler) 및 AEM 5.6.1을 기반으로 합니다.

## Eclipse 설치 {#install-eclipse}

Java EE 개발자용 Eclipse IDE를 [Eclipse 다운로드 페이지](https://www.eclipse.org/downloads/).

다음 단계에 따라 Eclipse 설치 [설치 지침](https://wiki.eclipse.org/Eclipse/Installation).

## Maven을 기반으로 AEM 프로젝트 설정 {#set-up-your-aem-project-based-on-maven}

다음으로, 다음에 설명된 대로 Maven을 사용하여 프로젝트를 설정합니다. [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md).

## Eclipse에 대한 JSP 지원 준비 {#prepare-jsp-support-for-eclipse}

Eclipse는 JSP 작업(예:

* 태그 라이브러리 자동 완성
* Eclipse 인식 &lt;cq:defineobjects /> 및 &lt;sling:defineobjects />

이를 수행하려면 다음을 수행하십시오.

1. 다음 지침을 따르십시오 [JSP 사용 방법](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md).
1. 다음 내용을 &lt;build /> 섹션을 참조하십시오.

   Eclipse의 Maven 지원 플러그인 m2e는 maven-jspc-plugin에 대한 지원을 제공하지 않으며, 이 구성은 m2e가 임시 컴파일 결과를 정리하는 플러그인 및 관련 작업을 무시하도록 지시합니다.

   문제가 아닙니다. 에 언급된 [JSP 사용 방법](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)를 지정하는 경우 이 설정의 maven-jspc-plugin은 빌드 프로세스의 일부로 해당 JSP가 컴파일되는지 확인하는 데만 사용됩니다. Eclipse는 이미 JSP의 문제를 보고하며 이 Maven 플러그인을 사용하여 문제를 해결할 수 없습니다.

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

### Maven 프로젝트를 Eclipse로 가져오기 {#import-the-maven-project-into-eclipse}

1. Eclipse에서 파일 > 가져오기.. 를 선택합니다.
1. 가져오기 대화 상자에서 Maven > Existing Maven Projects를 선택한 후 &quot;다음&quot;을 클릭합니다.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 프로젝트의 최상위 폴더에 대한 경로를 입력한 다음 &quot;모두 선택&quot; 및 &quot;마침&quot;을 클릭합니다.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 이제 Eclipse를 사용하여 JSP 자동 완성 등 AEM 프로젝트를 개발할 수 있도록 설정되었습니다.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >다음을 포함하는 경우 `/libs/foundation/global.jsp` 또는 기타 JSP `/libs`을 지정하면, Eclipse에서 포함 사항을 해결할 수 있도록 프로젝트에 복사해야 합니다. 동시에 Maven이 컨텐츠 패키지에 번들로 제공되지 않았는지 확인해야 합니다. 이를 수행하는 방법은 다음과 같습니다 [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md).
