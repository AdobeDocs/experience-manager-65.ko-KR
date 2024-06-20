---
title: 새로운 기능 요약 | AEM 6.5 Forms
description: 세계에서 가장 고급 디지털 경험 관리 솔루션인 AEM 양식 및 문서에 대한 최신 기능과 개선 사항입니다.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
solution: Experience Manager, Experience Manager Forms
feature: Release Information
role: Admin, User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 39%

---

# 새로운 기능 요약 | AEM 6.5 Forms{#new-features-summary-aem-forms}

| 제품 | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.19.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2023년 12월 8일 토요일 |

## Adobe Experience Manager 6.5 Forms 서비스 팩 19에 포함된 제품(6.5.19.0)

Experience Manager 6.5.19.0에는 2019년 4월 6.5의 초기 출시 이후 릴리스된 새로운 기능, 주요 고객 요청 개선 사항, 버그 수정 사항 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html) Experience Manager 6.5에서.

### 새로운 기능

#### 새로운 적응형 양식 핵심 구성 요소

양식의 확장성을 높이기 위해 세로 탭, 약관 및 확인란이 추가됩니다.

* **[확인란 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식에 확인란 구성 요소를 포함할 수 있습니다. 이를 통해 사용자는 특정 옵션을 선택하거나 선택 취소하는 이진 선택을 할 수 있습니다. 확인란은 일반적으로 클릭하거나 탭하여 두 가지 상태(선택됨 및 선택 취소됨) 사이를 전환할 수 있는 작은 상자 형태입니다. 확인란은 예/아니요 또는 참/거짓 선택을 표시하는 데 사용되는 일반적인 양식 요소입니다.

* **[약관 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식에 약관 구성 요소를 포함함 수 있습니다. 이를 통해 양식 작성자는 양식 내에 특정 섹션을 도입하여 여기에서 사용자에게 서비스, 제품 또는 플랫폼 사용과 관련된 약관 또는 법적 계약을 표시할 수 있습니다. 이 구성 요소는 양식을 제출하면 동의하는 것으로 간주되는 규칙, 규정 및 의무에 대해 사용자에게 알리도록 설계되었습니다.

  ![세로 탭, 약관 및 확인란 구성 요소](/help/forms/using/assets/forms-components.png)

* **[세로 탭 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식은 양식 콘텐츠를 세로 탭 목록으로 구성하여 체계적이고 탐색 가능한 레이아웃을 제공할 수 있습니다. 양식에서 세로 탭을 사용하면 특히 양식에 여러 섹션이나 복잡한 정보가 포함되어 있을 때 탐색을 단순화하고 양식 콘텐츠 구성을 개선하여 전반적인 사용자 경험을 향상시킬 수 있습니다.

#### 64비트 버전의 AEM Forms Designer

다음 [64비트 버전의 AEM Forms Designer](/help/forms/using/installing-configuring-designer.md) 향상된 성능, 확장성 및 메모리 관리를 제공하여 양식 작성 환경을 향상시킵니다. 64비트 아키텍처를 사용하면 더 크고 복잡한 프로젝트를 간단하게 처리하여 원활한 워크플로 디자인과 최적화된 효율성을 보장할 수 있습니다. 이 혁신적인 릴리스를 통해 양식 디자인 기능을 개선하고 AEM Forms Designer를 진전시킬 수 있습니다.

#### Microsoft® SharePoint 목록과 적응형 Forms 연결

AEM Forms은 다음과 같은 기본 제공 통합을 제공합니다. [양식 데이터를 SharePoint 목록에 직접 제출](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list))을 클릭하여 SharePoint의 목록 기능을 사용할 수 있습니다. Microsoft® SharePoint 목록을 양식 데이터 모델에 대한 데이터 소스로 구성하고 양식 데이터 모델을 사용하여 제출 제출 액션을 사용하여 적응형 양식을 SharePoint 목록과 연결할 수 있습니다.

#### 적응형 양식 조각에 대한 기록 문서 속성 구성 지원

이제 쉽게 [적응형 양식 편집기에서 적응형 양식 단편 및 해당 필드 사용자 지정](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

#### 64비트 버전의 XMLFM 포함

XMLFM의 64비트 반복은 향상된 성능, 확장성 및 정교한 메모리 관리를 제공합니다. 서버측에 배포된 최초의 64비트 네이티브 서비스입니다. XMLFM 64비트는 32비트보다 훨씬 더 큰 메모리 리소스에 액세스할 수 있는 고유한 기능을 활용함으로써 더 큰 렌더링 워크로드를 원활하게 처리할 수 있도록 지원합니다. 이 이정표는 성능 향상을 나타낼 뿐만 아니라 AEM Forms 서버 내의 기본 서비스 프레임워크에 대한 주요 개선 사항을 소개합니다. 이 업데이트는 AEM Forms 서버가 모든 64비트 기본 서비스를 원활하게 지원할 수 있도록 합니다.



## 버그 수정

이 릴리스에는 고객이 보고한 20개 이상의 문제에 대한 수정 사항도 포함되어 있습니다. 서비스 팩에 포함된 수정 사항의 자세한 목록은 을 참조하십시오. [릴리스 정보](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ko-KR#forms-6519)


## 서비스 팩 설치

서비스 팩은 JEE의 AEM Forms과 OSGi의 AEM Forms 모두에 대한 새로운 기능과 버그 수정 사항을 제공합니다. 설치 지침에 이전 서비스 팩과 비교하여 변경된 사항이 있습니다. 설치 지침은 다음을 참조하십시오. [AEM Forms 서비스 팩 설치 지침](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en).






<!-- 
## Transaction Reports {#transaction-reports}



Transaction reports lets you capture and track the number of submitted forms, processed documents, and rendered documents. The objective behind tracking these transactions is to make an informed decision about the product usage and rebalancing investments in hardware and software. Some examples of transactions include:

* Submission of an Adaptive Form, an HTML5 Form, or a Form Set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For information about configuring and using transaction reports, see [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md).

![A sample transaction report](assets/surface_transaction_reporting.png)

## Interactive Communications {#interactive-communications}

**Define data display patterns**

Interactive Communication authors can now define [data display patterns](create-interactive-communication.md#datadisplaypatterns) for fields, variables, and form data model elements. For example, date, currency, or phone formats.

**Use new types of charts**

You can now add [Quadrant charts and charts with multiple series](../../forms/using/chart-component-interactive-communications.md) to Interactive Communications.

**Sort columns in a table**

You can now [sort columns of a table](../../forms/using/create-interactive-communication.md#sortcolumns) in the Interactive Communication. You can bind and sort table columns with static text or data model objects.

**Use new components in a web channel**

You can now add Button and Separator components to the web channel. For more information, see [Add Button component to the web channel](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) and [Separator component in web channel](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Layout mode to resize components**

You can now switch to [Layout mode](../../forms/using/resize-using-layout-mode.md) to resize components in the Web channel using a WYSIWYG interface.

**Usability improvements**

Interactive Communication authors can now utilize various easy-to-use operations while creating correspondences. The list of operations includes:

* [Perform undo-redo actions in print and web channels](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Add variables in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Add data model elements in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Delete or add a web channel to an existing Interactive Communication](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Bind data source elements with fields and variables using drag-and-drop actions](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Highlight unbound fields and variables while authoring Interactive Communication](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Perform additional actions such as copy, group, or more on inherited components in a web channel](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Improvements in sync process**

There are several improvements in the Web channel layout auto-generated using the Print channel.

![Interactive Communications Charts](assets/interactive-communication-charts.png)

## Adaptive Forms {#adaptive-forms}

### Use Adobe Sign's cloud-based digital signatures in Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Cloud-based digital signatures](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) or remote signatures are a new generation of digital signatures that work across desktop, mobile, and the web — and meet the highest levels of compliance and assurance for signer authentication. You can now [sign an Adaptive Form](../../forms/using/working-with-adobe-sign.md) with Cloud-based digital signatures.

#### Embed an Adaptive Form or Interactive Communication in AEM Sites Single Page Applications {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms lets you [seamlessly embed an Adaptive Form](../../forms/using/embed-adaptive-form-aem-sites-spa.md) or Interactive Communication in an AEM Sites single page application (SPA). The embedded Adaptive Form and Interactive Communication is fully functional and users can fill and submit the form without leaving the page. It helps user remain in context of other elements on the web page and simultaneously interact with the adaptive form or Interactive Communication.

#### Sort columns of Adaptive Form tables {#sort-columns-of-adaptive-form-tables}

You can [sort any column of an Adaptive Form table](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) in an ascending or descending order. You can apply sorting to table columns with static text, data model object properties, or a combination of static text and data model object properties.

#### Restrict the availability of Adaptive Forms templates to specific paths {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Adaptive forms has added support for the cq:allowedPaths property. The property [restricts availability of Adaptive Forms templates to specific paths](creating-adaptive-form.md#adaptive-form-templates).

#### Add check boxes to the Adaptive Form dynamically {#add-check-boxes-to-the-adaptive-form-dynamically}

You can now define rules to [add checkboxes to the Adaptive Form dynamically](../../forms/using/rule-editor.md#setpropertyrule) based on custom function, a form object, or an object property.

## AEM Workflows {#aem-workflows}

### Use variables in AEM Workflows {#use-variables-in-aem-workflows}

Variables enable workflow steps to hold and pass metadata across workflow steps at runtime. You can create different types of variables for storing different types of data. For example, integers, strings, documents, or form data model instances. Typically, you use a variable or a collection of variables when you need to make a decision based on the value that it holds or to store information that you need later in a process.

Variables are an extension of [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interface available in the previous version. It helps save time spent in developing custom ECMAScript code used to retrieve and update metadata values. You continue using MetaDataMap interface and ECMAScript code to manipulate metadata. Some benefits of using variables over MetaDataMap and ECMAScript are:

* Dynamically store, update, and use values stored in a variable across the workflow without relying on custom code
* Retrieve and update values directly to a form data model and data file (XML/JSON ) of a submitted form
* Store complete documents in a variable to perform document processing

The Go To step, OR Split step, and all AEM Forms workflow steps support variables. You can use MetaDataMap interface to access variables in workflow steps that do not have a native support for variables. For more information, see [Variables in AEM Workflows](../../forms/using/variable-in-aem-workflows.md).

![Setting a variable for in a workflow](assets/variable.png)

#### Use a workflow with different Adaptive Forms  {#use-a-workflow-with-different-adaptive-forms}

You can [specify an Adaptive Form for the assign task](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) and document of record step of form-centric workflows on the runtime. It allows a workflow to work with different Adaptive Forms. You can decide the method to select an Adaptive Form while designing the workflow. The Adaptive Form can be located at an absolute path, submitted as payload to the workflow, or available at a path calculated using a variable.

#### Use enhanced logging capabilities of forms-centric workflow steps {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Logging capabilities of forms-centric workflow steps are standardized. Now, all form-centric workflow steps produce similarly standardized logs. It helps improve debugging speed.

## Data Integration {#data-integration}

You can now:

* [Validate input data](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) based on a list of constraints. It helps ensure that only valid data is submitted to data source.
* [Override default endpoint](../../forms/using/configure-data-sources.md#configure-soap-web-services) defined in a WSDL (Web Services Description Language) file.

* [Override default](../../forms/using/configure-data-sources.md#configure-restful-web-services) [scheme, host, and base path](../../forms/using/configure-data-sources.md#configure-restful-web-services) defined in Swagger definition file.

## Platform and Security updates {#platform-and-security-updates}

### Major platform updates {#major-platform-updates}

AEM Forms can be set up using any combination of supported operating systems, application servers, databases, database drivers, JDK, LDAP servers, and email servers. The following are the major changes in [supported platforms](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Component</td>
   <td>Support Removed</td>
  </tr>
  <tr>
   <td>Operating systems</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Application servers<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty profile</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Databases</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP servers</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Email servers</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Connectors</td>
   <td>
    <ul>
     <li>Connector for Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1 support</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; Contact Adobe Support for information on migrating to a different platform

#### New HTML5-based UIs {#new-html-based-uis}

In line with planned EOL of Adobe Flash Player and overall direction of migrating Flash-based content to open standards, AEM 6.5 Forms has replaced Flash-based UI of Health Monitor, Process Management, Reader Extension, and Category Management UI of AEM Forms on JEE Administration Console with HTML5-based UI.

#### Security improvements {#security-improvements}

* AEM 6.5 Forms on JEE administration console UI is now based on Apache Struts 2.5.
* AEM 6.5 Forms now uses jQuery to 3.2.1 and jQuery UI 1.12.1. See, [upgrade documentation](/help/forms/using/introduction-aem-forms.md) for the impact of the change.

#### Accessibility improvements {#accessibility-improvements}

AEM 6.5 Forms has improved accessibility of AEM Forms Workspace. 
!-->

