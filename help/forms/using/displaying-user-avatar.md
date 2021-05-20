---
title: 사용자 아바타 표시
seo-title: 사용자 아바타 표시
description: 로그인한 사용자의 이미지를 표시하기 위해 AEM Forms 작업 영역을 사용자 지정하는 방법입니다.
seo-description: 로그인한 사용자의 이미지를 표시하기 위해 AEM Forms 작업 영역을 사용자 지정하는 방법입니다.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
exl-id: ee0708b0-b630-4a2b-84b6-3c0b92dd7777
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 사용자 아바타 표시 {#displaying-the-user-avatar}

로그인한 사용자의 아바타가 AEM Forms 작업 공간의 오른쪽 위 모서리에 표시됩니다. 또한 조직 계층 구조의 직접 보고서 아바타가 관리자 보기에 표시됩니다. LDAP 서버와 같이 데이터베이스에서 사용자 이미지를 선택하도록 AEM Forms 작업 영역을 구성할 수 있습니다.

>[!NOTE]
>
>사용자 이미지의 지원되는 종횡비는 1:1입니다.

1. 다음 단계에서 언급한 세부 사항을 사용하여 DSC를 만듭니다. 자세한 내용은 [AEM Forms을 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63) 안내서의 &#39;AEM Forms용 구성 요소 개발&#39; 항목을 참조하십시오.
1. DSC에서는 AEM Forms 사용자의 이미지 URL을 가져오기 위해 getCurrentUserImageUrl 및 getUserImageUrl 메서드를 노출하는 새 SPI를 정의합니다. 다음은 샘플 Java™ 코드 조각입니다.

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. component.xml 파일을 만듭니다. spec-id가 아래 코드 조각에 표시된 대로 표시되는지 확인합니다.

   다음 코드 조각은 샘플입니다. 특정 요구 사항에 맞게 사용자 정의합니다.

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Workbench를 통해 DSC를 배포합니다. `ProcessManagementClientSessionService` 서비스를 다시 시작합니다.
1. 브라우저를 새로 고치거나 사용자와 로그아웃/로그인해야 할 수 있습니다.
