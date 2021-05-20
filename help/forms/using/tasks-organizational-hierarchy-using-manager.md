---
title: 관리자 보기를 사용하여 조직 계층 구조에서 작업 관리
seo-title: 관리자 보기를 사용하여 조직 계층 구조에서 작업 관리
description: AEM Forms 작업 공간의 할 일 탭에서 관리자 및 조직 책임자가 직접 및 간접 보고서의 작업에 액세스하고 작업하는 방법입니다.
seo-description: AEM Forms 작업 공간의 할 일 탭에서 관리자 및 조직 책임자가 직접 및 간접 보고서의 작업에 액세스하고 작업하는 방법입니다.
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
exl-id: e50974a7-01ac-4a08-bea2-df9cc975c69e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# 관리자 보기{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}를 사용하여 조직 계층 구조에서 작업 관리

이제 AEM Forms 작업 공간에서 관리자는 계층 구조의 모든 사람에게 할당된 작업(직접 또는 간접 보고서)에 액세스하여 다양한 작업을 수행할 수 있습니다. 작업은 AEM Forms 작업 영역의 할 일 탭에서 사용할 수 있습니다. 직접 보고서의 작업에 지원되는 작업은 다음과 같습니다.

**** 전달: 직접 보고서에서 모든 사용자에게 작업을 전달합니다.

**** 청구직접 보고서의 작업을 청구합니다.

**청구 및** 열기직접 보고서의 작업을 생성하여 관리자의 할 일 목록에서 자동으로 엽니다.

**** 거부일부 다른 사용자가 직접 보고서에 전달된 작업을 거부합니다. 이 옵션은 다른 사용자가 직접 보고서에 전달하는 작업에 사용할 수 있습니다.

AEM Forms은 사용자가 ACL(액세스 제어)을 가진 작업에만 사용자의 액세스를 제한합니다. 이러한 검사는 사용자가 액세스 권한이 있는 작업만 가져올 수 있도록 해줍니다. 서드파티 웹 서비스 및 구현을 사용하여 계층을 정의하면 조직은 관리자의 정의를 사용자 지정하고 요구에 맞게 보고서를 직접 정의할 수 있습니다.

1. DSC를 만듭니다. 자세한 내용은 [AEM Forms을 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63) 안내서의 &#39;AEM Forms용 구성 요소 개발&#39; 항목을 참조하십시오.
1. DSC에서 계층 관리를 위한 새 SPI를 정의하여 AEM Forms 사용자 내에서 직접 보고서와 계층 구조를 정의합니다. 다음은 샘플 Java™ 코드 조각입니다.

   ```java
   public class MyHierarchyMgmtService
   {
        /*
       Input : Principal Oid for a livecycle user
       Output : Returns true when the user is either the service invoker OR his direct/indirect report.
       */
       boolean isInHierarchy(String principalOid) {
   
       }
   
       /*
       Input : Principal Oid for a livecycle user
       Output : List of principal Oids for direct reports of the livecycle user
       A user may get direct reports only for himself OR his direct/indirect reports.
       So the API is functionally equivalent to -
       isInHierarchy(principalOid) ? <return direct reports> : <return empty list>
       */
       List<String> getDirectReports(String principalOid) {
   
       }
   
       /*
       Returns whether a livecycle user has direct reports or not.
       It's functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. component.xml 파일을 만듭니다. 아래 코드 조각에 표시된 것과 spec-id가 동일해야 합니다. 다음은 재사용할 수 있는 샘플 코드 조각입니다.

   ```xml
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.SampleDSC</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
         <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
         <services>
           <service name="MyHierarchyMgmtService" title="My hierarchy management service" orchestrateable="false">
           <auto-deploy service-id="MyHierarchyMgmtService" category-id="Sample DSC" major-version="1" minor-version="0" />
           <description>Service for resolving hierarchy management.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.HierarchyManagementProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.hierarchymanagement.MyHierarchyMgmtService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="true" name="isInHierarchy" method="isInHierarchy">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               <operation anonymous-access="true" name="getDirectReports" method="getDirectReports">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.util.List"/>
               </operation>
               <operation anonymous-access="true" name="isManager" method="isManager">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               </operations>
               </service>
         </services>
   </component>
   ```

1. Workbench를 통해 DSC를 배포합니다. `ProcessManagementTeamTasksService` 서비스를 다시 시작합니다.
1. 브라우저를 새로 고치거나 사용자와 로그아웃/로그인해야 할 수 있습니다.

다음 화면에서는 직접 보고서의 작업 및 사용 가능한 작업에 액세스하는 방법을 보여줍니다.

![cu_manager_view](assets/cu_manager_view.png)

직접 보고의 작업에 액세스하고 작업에 대해 수행합니다
