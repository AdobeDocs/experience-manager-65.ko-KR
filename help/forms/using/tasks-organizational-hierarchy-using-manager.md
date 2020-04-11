---
title: 관리자 보기를 사용하여 조직 계층 구조에서 작업 관리
seo-title: 관리자 보기를 사용하여 조직 계층 구조에서 작업 관리
description: 관리자 및 조직 헤드가 AEM Forms 작업 영역의 [할 일] 탭에서 직접 및 간접 보고서의 작업에 액세스하고 작업하는 방법.
seo-description: 관리자 및 조직 헤드가 AEM Forms 작업 영역의 [할 일] 탭에서 직접 및 간접 보고서의 작업에 액세스하고 작업하는 방법.
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 관리자 보기를 사용하여 조직 계층 구조에서 작업 관리{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

이제 관리자는 AEM Forms 작업 영역에서 계층 구조 내 모든 사람에게 할당된 작업(직접 또는 간접 보고서)에 액세스하여 다양한 작업을 수행할 수 있습니다. 작업은 AEM Forms 작업 영역의 할 일 탭에서 사용할 수 있습니다. 직접 보고서의 작업에 지원되는 작업은 다음과 같습니다.

**직접** 보고서에서 모든 사용자에게 작업을 전달합니다.

**클레임** 직접 보고서 작업을 요청합니다.

**청구 및** 열기 직접 보고서의 작업을 요청하고 관리자의 할 일 목록에서 자동으로 엽니다.

**거부** 다른 사용자가 직접 보고서로 전달된 작업을 거부합니다. 이 옵션은 다른 사용자가 직접 보고서로 전달하는 작업에 사용할 수 있습니다.

AEM Forms는 사용자가 ACL(액세스 제어)을 가진 작업에 대해서만 사용자의 액세스를 제한합니다. 이러한 검사를 통해 사용자는 액세스 권한이 있는 작업만 가져올 수 있습니다. 서드파티 웹 서비스와 구현을 사용하여 계층 구조를 정의하면 조직은 관리자의 정의를 사용자 정의하고 요구에 맞게 직접 보고서를 작성할 수 있습니다.

1. DSC를 만듭니다. 자세한 내용은 AEM Forms를 사용한 프로그래밍 [안내서의 &#39;AEM Forms용 구성 요소 개발&#39; 항목을](https://www.adobe.com/go/learn_aemforms_programming_63) 참조하십시오.
1. DSC 파섹 다음은 샘플 Java™ 코드 조각입니다.

   ```as3
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

1. component.xml 파일을 만듭니다. spec-id가 아래 코드 조각에 표시된 것과 동일해야 합니다. 다음은 재사용할 수 있는 샘플 코드 조각입니다.

   ```as3
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

1. 워크벤치를 통해 DSC를 배포합니다. 서비스를 다시 `ProcessManagementTeamTasksService` 시작합니다.
1. 브라우저를 새로 고치거나 로그아웃/사용자와 다시 로그인해야 할 수 있습니다.

다음 화면은 직접 보고서의 작업 및 사용 가능한 작업에 액세스하는 방법을 보여줍니다.

![cu_manager_view](assets/cu_manager_view.png)

직접 보고서의 작업에 액세스하여 작업 수행
