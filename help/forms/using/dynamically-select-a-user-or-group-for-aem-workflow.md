---
title: AEM Forms 중심의 워크플로우 단계를 위해 사용자 또는 그룹을 동적으로 선택
seo-title: AEM Forms 중심의 워크플로우 단계를 위해 사용자 또는 그룹을 동적으로 선택
description: '런타임 시 AEM Forms 워크플로우의 사용자 또는 그룹을 선택하는 방법을 알아봅니다. '
seo-description: '런타임 시 AEM Forms 워크플로우의 사용자 또는 그룹을 선택하는 방법을 알아봅니다. '
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 1%

---


# AEM Forms 중심 워크플로우 단계 {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}에 대한 사용자 또는 그룹을 동적으로 선택

런타임 시 AEM Forms 워크플로우의 사용자 또는 그룹을 선택하는 방법을 알아봅니다.

대기업은 프로세스를 위해 사용자를 동적으로 선택해야 하는 요구 사항이 있습니다. 예를 들어, 상담원이 고객과의 근접 거리를 기반으로 고객에게 서비스를 제공할 필드 에이전트를 선택합니다. 이러한 시나리오에서 에이전트는 동적으로 선택됩니다.

OSGi](/help/forms/using/aem-forms-workflow.md)에서 [Forms 중심 워크플로우의 작업 및 Adobe Sign 단계를 할당하면 사용자를 동적으로 선택할 수 있는 옵션이 제공됩니다. ECMAScript 또는 OSGi 번들을 사용하여 작업 할당 단계에서 할당자를 동적으로 선택하거나 문서 서명 단계의 서명자를 선택할 수 있습니다.

## ECMAScript를 사용하여 사용자 또는 그룹 {#use-ecmascript-to-dynamically-select-a-user-or-group}을(를) 동적으로 선택

ECMAScript는 스크립팅 언어입니다. 클라이언트측 스크립팅 및 서버 응용 프로그램에 사용됩니다. ECMAScript를 사용하여 사용자나 그룹을 동적으로 선택하려면 다음 단계를 수행합니다.

1. CRXDE Lite 열기 URL은 `https://'[server]:[port]'/crx/de/index.jsp`입니다.
1. 다음 경로에서 확장명이 .ecma인 파일을 만듭니다. 경로(노드 구조)가 없는 경우 다음을 만듭니다.

   * (작업 할당 단계 경로) `/apps/fd/dashboard/scripts/participantChooser`
   * (서명 단계 경로) `/apps/fd/workflow/scripts/adobesign`

1. 사용자를 동적으로 선택하는 논리가 있는 ECMAScript를 .ecma 파일에 추가합니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   샘플 스크립트는 사용자 또는 그룹](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group)을 동적으로 선택하려면 [샘플 ECMAScript를 참조하십시오.

1. 스크립트의 표시 이름을 추가합니다. 이 이름은 워크플로우 단계에 표시됩니다. 이름을 지정하려면:

   1. 스크립트 노드를 확장하고 **[!UICONTROL jcr:content]** 노드를 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 혼합]**&#x200B;을 클릭합니다.
   1. [혼합 편집] 대화 상자에 `mix:title` 속성을 추가하고 **확인**&#x200B;을 클릭합니다.
   1. 스크립트의 jcr:content 노드에 다음 속성을 추가합니다.

      | 이름 | 유형 | 값 |
      |--- |--- |--- |
      | jcr:title | 문자열 | 스크립트 이름을 지정합니다. 예를 들어 가장 가까운 필드 에이전트를 선택합니다. 이 이름은 작업 지정 및 문서 서명 단계에 표시됩니다. |

   1. **모두 저장**&#x200B;을 클릭합니다. 이 스크립트는 AEM Workflow 구성 요소에서 선택할 수 있게 됩니다.

      ![스크립트](assets/script.png)

### 사용자 또는 그룹 {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}을 동적으로 선택하는 샘플 ECMAScript

다음 샘플 ECMAScript에서는 작업 할당 단계의 담당자를 동적으로 선택합니다. 이 스크립트에서 사용자는 페이로드 경로를 기반으로 선택됩니다. 이 스크립트를 사용하기 전에 스크립트에 언급된 모든 사용자가 AEM에 있는지 확인합니다. 스크립트에 언급된 사용자가 AEM에 없는 경우 관련 프로세스가 실패할 수 있습니다.

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

다음 샘플 ECMAScript는 Adobe Sign 단계의 담당자를 동적으로 선택합니다. 아래 스크립트를 사용하기 전에 스크립트에 언급된 사용자 정보(이메일 주소 및 전화 번호)가 올바른지 확인하십시오. 스크립트에 언급된 사용자 정보가 잘못된 경우 관련 프로세스가 실패할 수 있습니다.

>[!NOTE]
>
>Adobe Sign용 ECMAScript를 사용할 때 스크립트는 /apps/fd/workflow/scripts/adobesign/의 crx-repository에 있어야 하며 getAdobeSignRecipients라는 함수가 있어야 사용자 목록을 반환합니다.

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Java 인터페이스를 사용하여 사용자 또는 그룹 {#use-java-interface-to-dynamically-choose-a-user-or-group}을 동적으로 선택합니다.

[RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java 인터페이스를 사용하여 Adobe Sign 및 작업 할당 단계에 대한 사용자 또는 그룹을 동적으로 선택할 수 있습니다. [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java 인터페이스를 사용하는 OSGi 번들을 만들고 AEM Forms 서버에 배포할 수 있습니다. 이 옵션을 AEM Workflow의 작업 할당 및 Adobe Sign 구성 요소에서 선택할 수 있게 합니다.

아래 나열된 코드 샘플을 컴파일하려면 [AEM Forms Client SDK](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) jar 및 [granite jar](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) 파일이 필요합니다. 이러한 jar 파일을 OSGi 번들 프로젝트에 외부 종속성으로 추가합니다. Java IDE를 사용하여 OSGi 번들을 만들 수 있습니다. 다음 절차에서는 Eclipse를 사용하여 OSGi 번들을 만드는 단계를 제공합니다.

1. Eclipse IDE를 엽니다. **[!UICONTROL 파일]** **[!UICONTROL 새 프로젝트]**&#x200B;로 이동합니다.
1. 마법사 선택 화면에서 **[!UICONTROL 마비프로젝트]**&#x200B;를 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. New Maven 프로젝트에서 기본값을 유지하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다. 원형 유형을 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다. 예: maven-tranype-quickstart. 프로젝트에 대해 **[!UICONTROL 그룹 ID]**, **[!UICONTROL 아티팩트 ID]**, **[!UICONTROL 버전]** 및 **[!UICONTROL 패키지]**&#x200B;를 지정하고 **[!UICONTROL 완료]**&#x200B;를 클릭합니다. 프로젝트가 만들어집니다.
1. 편집할 pom.xml 파일을 열고 파일의 모든 내용을 다음과 같이 바꿉니다.

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java 인터페이스를 사용하여 할당 작업 단계의 사용자 또는 그룹을 동적으로 선택하는 소스 코드를 추가합니다. 샘플 코드는 [Java 인터페이스](#-sample-scripts-for)를 사용하여 사용자 또는 그룹을 동적으로 선택하는 샘플을 참조하십시오.
1. 명령 프롬프트를 열고 OSGi 번들 프로젝트가 포함된 디렉토리로 이동합니다. 다음 명령을 사용하여 OSGi 번들을 만듭니다.

   `mvn clean install`

1. AEM Forms 서버에 번들을 업로드합니다. AEM Package Manager를 사용하여 AEM Forms 서버로 번들을 가져올 수 있습니다.

번들을 가져온 후 동적으로 사용자 또는 그룹을 선택할 수 있는 Java 인터페이스 선택 옵션은 Adobe Sign 및 작업 할당 단계에서 사용할 수 있습니다.

### 사용자 또는 그룹 {#sample-java-code-to-dynamically-choose-a-user-or-a-group}을 동적으로 선택하는 샘플 Java 코드

다음 샘플 코드는 Adobe Sign 단계의 담당자를 동적으로 선택합니다. OSGi 번들에서 코드를 사용합니다. 아래 나열된 코드를 사용하기 전에 코드에 언급된 사용자 정보(이메일 주소 및 전화 번호)가 올바른지 확인하십시오. 코드에 언급된 사용자 정보가 잘못된 경우 관련 프로세스가 실패할 수 있습니다.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```

