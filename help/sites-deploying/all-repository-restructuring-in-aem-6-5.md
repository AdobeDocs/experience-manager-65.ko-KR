---
title: AEM 6.5의 공통 저장소 구조 변경
seo-title: Common Repository Restructuring in AEM 6.5
description: AEM의 모든 영역에 공통인 AEM 6.5의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 작업을 수행하는 방법을 알아봅니다.
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 that are common for all areas of AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
source-git-commit: 3f64bd7f5b4eb43aeefb9277a94e10ef1f0df59c
workflow-type: tm+mt
source-wordcount: '2693'
ht-degree: 3%

---

# AEM 6.5의 공통 저장소 구조 변경 {#common-repository-restructuring-in-aem}

상위에 설명된 대로 [AEM 6.5의 저장소 구조 변경](/help/sites-deploying/repository-restructuring.md) 페이지에서 AEM 6.5로 업그레이드하는 고객은 이 페이지에서 모든 솔루션에 영향을 줄 수 있는 저장소 변경 과 관련된 작업 작업을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업 노력이 필요한 반면, 다른 변경 사항은 향후 업그레이드될 때까지 지연될 수 있습니다.

**6.5 업그레이드**

* [ContextHub 구성](#contexthub-6.5)
* [워크플로 인스턴스](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [워크플로우 모델](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [워크플로 런처](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [워크플로우 스크립트](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**향후 업그레이드 전**

* [ContextHub 구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [클래식 Cloud Services 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Classic 대시보드 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [클래식 Reports 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [기본 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Adobe DTM JavaScript 끝점](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Adobe DTM 웹 후크 끝점](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [받은 편지함 작업](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [다중 사이트 관리자 블루프린트 구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM 프로젝트 대시보드 가젯 구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [복제 알림 전자 메일 템플릿](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [태그](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [번역 클라우드 서비스](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [번역 언어](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [번역 규칙](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [번역 위젯 클라이언트 라이브러리](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [트리 활성화 웹 콘솔](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [공급업체 번역 커넥터 Cloud Services](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [워크플로우 알림 이메일 템플릿](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 6.5 업그레이드 {#with-upgrade}

### ContextHub 구성 {#contexthub-6.5}

AEM 6.4 이상에서는 기본 ContextHub 구성이 없습니다. 따라서 사이트 a의 루트 수준에서 `cq:contextHubPathproperty` 어떤 구성을 사용해야 하는지를 나타내도록 설정해야 합니다.

1. 사이트의 루트로 이동합니다.
1. 루트 페이지의 페이지 속성을 열고 개인화 탭을 선택합니다.
1. Contexthub 경로 필드에 고유한 ContextHub 구성 경로를 입력합니다.

또한 ContextHub 구성에서는 `sling:resourceType` 절대적이지 않고 상대적이도록 업데이트해야 합니다.

1. CRX DE Lite에서 ContextHub 구성 노드의 속성을 엽니다(예: ). `/apps/settings/cloudsettings/legacy/contexthub`
1. 변경 `sling:resourceType` 변환 전: `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` to `granite/contexthub/cloudsettings/components/baseconfiguration`

전.. `sling:resourceType` ContextHub 구성의 경우 절대 구성보다 상대적이어야 합니다.

### 워크플로우 모델 {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새로운 워크플로우 모델 또는 수정된 모든 워크플로우 모델은 /conf/global/workflow/models로 마이그레이션해야 합니다.</p>
    <ol>
     <li>수정된 워크플로우 모델을 이전 위치에 있도록 로컬 AEM 6.5 개발 인스턴스에 배포합니다.</li>
     <li>AEM &gt; 도구 &gt; 워크플로우 &gt; 모델에서 AEM 워크플로우 모델 편집기를 사용하여 워크플로우 모델을 편집합니다.</li>
     <li>수정된 AEM 제공 워크플로우 모델을 마이그레이션할 때
      <ol>
       <li>워크플로우 모델 편집기를 열고 브라우저의 주소 URL을 수정하고 경로 세그먼트 /libs/settings/workflow/models 를 /etc/workflow/models 로 바꿉니다.
        <ul>
         <li>예를 들어, 다음과 같이 변경합니다. <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> to <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>워크플로우 모델 편집기에서 편집 모드를 활성화하여 워크플로우 모델 정의를 /conf/global/workflow/models에 복사합니다.</li>
     <li>동기화 단추를 탭하여 /var/workflow/models 아래의 런타임 워크플로우 모델에 대한 변경 사항을 동기화합니다.</li>
     <li>워크플로우 모델 (/conf/global/workflow/models/ 을 모두 내보냅니다.&lt;workflow-model&gt;) 및 런타임 워크플로우 모델 (/var/workflow/models/&lt;workflow-model&gt;)을 사용하여 AEM 프로젝트에 통합할 수 있습니다.
      <ol>
       <li>예를 들어 내보내기:
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code> 및 </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>워크플로우 모델 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>따라서 이전 위치에 지속된 AEM 제공 워크플로우 모델의 사용자 지정은 보존해야 하는 경우 /conf/global/settings/workflow/models로 이동해야 하며, 그렇지 않으면 /libs/settings/workflow/models에서 AEM 제공 워크플로우 모델 정의로 대체됩니다.</p> </td>
  </tr>
 </tbody>
</table>

### 워크플로 인스턴스 {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 위치에 정렬하는 데 필요한 작업은 없습니다.</p> <p>이전 워크플로우 인스턴스는 이전 위치에 안전하게 계속 보관할 수 있으며, 새 워크플로우 인스턴스는 새 위치에 생성됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>에서 명시적 경로 참조
    <code>
     custom
    </code> 이전 위치에 대한 코드도 새 위치를 고려해야 합니다. AEM 워크플로우 API를 사용하도록 이 코드를 리팩터링하는 것이 좋습니다.</td>
  </tr>
 </tbody>
</table>

### 워크플로 런처 {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 워크플로우 런처 또는 수정된 모든 워크플로우 런처를 <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>이전 위치의 새 워크플로우 런처 구성을 새 위치 (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>워크플로우 실행 프로그램 해결은 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>따라서 이전 위치에 지속되는 AEM에서 제공한 워크플로우 런처 의 사용자 지정은 새 위치 (<code>/conf/global/settings/workflow/launcher</code> 보존해야 하는 경우에는 AEM에서 제공하는 Workflow Launcher 정의로 대체됩니다. <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### 워크플로우 스크립트 {#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 위치 또는 수정된 워크플로우 스크립트는 새 위치로 마이그레이션해야 하며 새 위치를 반영하도록 업데이트된 참조 워크플로우 모델 도 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 새 워크플로우 스크립트나 수정된 워크플로우 스크립트를 새 위치에 복사합니다.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 는 SCM에서 유지 관리되어야 합니다.</li>
      </ul> </li>
     <li>워크플로우 모델의 이전 위치에서 워크플로우 스크립트에 대한 모든 참조를 업데이트하여 새 위치를 가리킵니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>AEM 6.4 SP1이 출시되면 6.5까지 이 재구성을 연기하도록 합니다.
     <code>
      upgrade
     </code>.</p> <p>AEM 6.4 SP1이 출시되기 전에 AEM 6.4로 업그레이드하는 경우 업그레이드 프로젝트의 일부로 이 재구성을 수행해야 합니다. 이렇게 하지 않으면 이전 위치에서 스크립트를 참조하는 워크플로우 단계를 편집하고 저장하면 워크플로우 단계에서 워크플로우 스크립트 참조가 완전히 제거되고, 새 위치의 워크플로우 스크립트만 스크립트 선택 드롭다운에서 사용할 수 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

## 향후 업그레이드 전 {#prior-to-upgrade}

### ContextHub 구성 {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 ContextHub 구성 또는 수정된 모든 ContextHub 구성은 새 위치로 마이그레이션해야 하며, 참조하는 AEM Sites 페이지는 새 위치를 반영하도록 업데이트해야 합니다.</p>
    <ol>
     <li>이전 위치에서 새 위치나 수정된 ContextHub 구성을 새 위치로 복사합니다.</li>
     <li>적용 가능한 AEM 구성을 AEM 컨텐츠 계층 구조에 연결합니다.
      <ol>
       <li><strong>AEM Sites &gt; 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 클라우드 구성을 통한 AEM Sites 페이지 계층</strong>.</li>
      </ol> </li>
     <li>앞서 언급한 AEM 컨텐츠 계층에서 마이그레이션된 이전 ContextHub 구성 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 클래식 Cloud Services 디자인 {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치에서 새 위치(<code>/apps</code>).</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> with <code>allowProxy = true</code>.</li>
     <li>에서 이전 위치에 대한 참조를 업데이트합니다. <span class="code">
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span> 속성을 사용합니다.</li>
     <li>이전 위치를 참조하는 페이지를 업데이트하여 새 클라이언트 라이브러리 카테고리를 사용합니다(페이지 구현 코드를 업데이트해야 함).</li>
     <li>/etc.clientlibs/. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 외부로 이동하지 마십시오 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Classic 대시보드 디자인 {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치(/apps)에 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> with <code>allowProxy = true</code>.</li>
     <li>에서 이전 위치에 대한 참조를 업데이트합니다.
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성을 사용합니다.</li>
     <li>이전 위치를 참조하는 페이지를 업데이트하여 새 클라이언트 라이브러리 카테고리를 사용합니다(페이지 구현 코드를 업데이트해야 함).</li>
     <li>/etc.clientlibs/. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 외부로 이동하지 마십시오 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 클래식 Reports 디자인 {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치(/apps)에 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> with <code>allowProxy = true</code>.</li>
     <li>에서 이전 위치에 대한 참조를 업데이트합니다.
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성을 사용합니다.</li>
     <li>이전 위치를 참조하는 페이지를 업데이트하여 새 클라이언트 라이브러리 카테고리를 사용합니다(페이지 구현 코드를 업데이트해야 함).</li>
     <li>/etc.clientlibs/. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 외부로 이동하지 마십시오 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 기본 디자인 {#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치(/apps)에 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> with <code>allowProxy = true</code>.</li>
     <li>에서 이전 위치에 대한 참조를 업데이트합니다.
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성을 사용합니다.</li>
     <li>이전 위치를 참조하는 페이지를 업데이트하여 새 클라이언트 라이브러리 카테고리를 사용합니다(페이지 구현 코드를 업데이트해야 함).</li>
     <li>/etc.clientlibs/. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 외부로 이동하지 마십시오 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Adobe DTM JavaScript 끝점 {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>필요한 작업이 없습니다.</p> <p>공개 이전 위치는 개인 새 위치에 대한 프록시 끝점 역할을 합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Adobe DTM 웹 후크 끝점 {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>필요한 작업이 없습니다.</p> <p>공개 이전 위치는 개인 새 위치에 대한 프록시 끝점 역할을 합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 받은 편지함 작업 {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td>를 사용하십시오 <strong>받은 편지함 제거 유지 관리 작업</strong> 필요에 따라 이전 위치에서 이전 작업을 제거합니다.</td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>작업을 새 위치로 마이그레이션하는 데 필요한 작업은 없습니다.</p>
    <ul>
     <li>이전 위치에 있는 작업은 계속 사용할 수 있고 작동합니다.</li>
     <li>새 작업은 새 위치에 만들어집니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 다중 사이트 관리자 블루프린트 구성 {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>이전 위치</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td>
    <ol>
     <li>다음에서 사용자 지정 구성 복사 <code>/etc/blueprints</code> to <code>/apps/msm</code>.</li>
     <li>제거 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### AEM 프로젝트 대시보드 가젯 구성 {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>신규 또는 수정된 AEM Projects Dashboard Gadget 구성은 새 위치(<code>/apps</code>).</p>
    <ol>
     <li>이전 위치에서 새 위치 또는 수정된 AEM Projects Dashboard Gadget Configurations 를 새 위치(<code>/apps</code>).
      <ol>
       <li>수정되지 않은 AEM Projects Dashboard Gadget 구성 은 이제 새 위치(<code>/libs</code>).</li>
      </ol> </li>
     <li>이전 위치를 참조하는 AEM Projects 템플릿을 업데이트하여 적절한 새 위치를 가리킵니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>AEM 6.4 호환성 패키지가 적용되는 경우 호환성 패키지를 제거할 때 저장소 정렬 활동을 수행해야 합니다.</td>
  </tr>
 </tbody>
</table>

### 복제 알림 전자 메일 템플릿 {#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 또는 수정된 복제 알림 이메일 템플릿은 새 위치(<code>/apps</code>)</p>
    <ol>
     <li>새 위치 또는 수정된 복제 알림 이메일 템플릿을 이전 위치에서 새 위치(<code>/apps</code>).</li>
     <li>이전 위치에서 마이그레이션된 복제 알림 전자 메일 템플릿을 제거합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>새로운 복제 알림 이메일 템플릿 만 지원됩니다.</p> <p>복제 알림 전자 메일 템플릿 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 태그 {#tags}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>모든 태그를 로 마이그레이션해야 합니다. <code>/content/cq:tags</code>.</p>
    <ol>
     <li>이전 위치의 모든 태그를 새 위치에 복사합니다.</li>
     <li>이전 위치에서 모든 태그를 제거합니다.</li>
     <li>AEM Web Console을 통해 다음 위치에서 Day Communication 5 Tagging OSGi 번들을 다시 시작합니다. <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> AEM에서 새 위치 에 컨텐츠가 포함되어 있으며 이 컨텐츠를 사용해야 합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>Day Communication Tagging OSGi 번들을 다시 시작하면 이전 위치가 비어 있는 경우에만 새 위치를 태그 루트로 등록합니다.</p> <p>이전 위치에 대한 참조는 태그 확인을 위해 AEM TagManager API를 활용하는 모든 기능에 대해 새 위치로 마이그레이션한 후 계속 작동합니다.</p> <p>경로를 명시적으로 참조하는 모든 사용자 지정 코드 <code>/etc/tags</code> 를 업데이트해야 합니다. <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, 또는 바람직하게는 이 마이그레이션과 함께 TagManager Java API를 활용하도록 다시 작성하십시오.</p> </td>
  </tr>
 </tbody>
</table>

### 번역 클라우드 서비스 {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 번역 Cloud Services은 모두 새 위치(<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ul>
       <li>에서 AEM 작성 UI를 통해 새 번역 Cloud Services 구성을 수동으로 다시 만듭니다 <strong>도구 &gt; Cloud Services &gt; 번역 Cloud Services</strong>.<br /> 또는 </li>
       <li>이전 위치의 새 번역 Cloud Services 구성을 새 위치 ()에 복사합니다.<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>적용 가능한 AEM 구성을 AEM 컨텐츠 계층 구조에 연결합니다.
      <ol>
       <li>AEM Sites의 <strong>AEM Sites &gt; 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>.</li>
       <li>를 통한 AEM 경험 조각 계층 <strong>AEM 경험 구성요소 &gt; 경험 구성요소 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>.</li>
       <li>를 통한 AEM 경험 조각 폴더 계층 <strong>AEM Experience Fragments &gt; 폴더 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>.<br /> </li>
       <li>AEM Assets 폴더 계층 - <strong>AEM Assets &gt; 폴더 &gt; 폴더 속성 &gt; Cloud Services 탭 &gt; 구성</strong>.</li>
       <li>를 통한 AEM 프로젝트 <strong>AEM 프로젝트 &gt; 프로젝트 &gt; 프로젝트 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>.</li>
      </ol> </li>
     <li>앞서 언급한 AEM 컨텐츠 계층에서 마이그레이션된 이전 번역 Cloud Services의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>번역 Cloud Services 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>마이그레이션된 번역 Cloud Services은 AEM 6.4와 호환되어야 합니다.</p> </td>
  </tr>
 </tbody>
</table>

### 번역 언어 {#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새로 만들거나 수정한 번역 언어 정의를 사용하려면 모든 번역 언어 정의를 새 위치(<code>/apps</code>).</p>
    <ol>
     <li>번역 언어 정의에 추가 또는 수정 사항이 있는 경우 이전 위치의 모든 번역 언어 정의를 새 위치(<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>번역 언어 경로 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>이 해상도는 병합 오버레이를 지원하지 않습니다. 즉, 해결된 경로는 모든 지원 언어를 포함해야 하며 상위 순서 해상도의 지원 언어를 상속하지 않습니다.</p> </td>
  </tr>
 </tbody>
</table>

### 번역 규칙 {#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>수정된 번역 규칙 XML 파일은 새 위치(<code>/apps</code>, 또는 <code>/conf/global</code>).</p> <p>1. 수정된 번역 규칙 XML 파일을 이전 위치에서 새 위치로 복사합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>복제 번역 규칙 XML 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 번역 위젯 클라이언트 라이브러리 {#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치(/apps)에 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> with <code>allowProxy = true</code>.</li>
     <li>에서 이전 위치에 대한 참조를 업데이트합니다.
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성을 사용합니다.</li>
     <li>이전 위치를 참조하는 페이지를 업데이트하여 새 클라이언트 라이브러리 카테고리를 사용합니다(페이지 구현 코드를 업데이트해야 함).</li>
     <li>/etc.clientlibs/. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 외부로 이동하지 마십시오 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 트리 활성화 웹 콘솔 {#tree-activation-web-console}

| **이전 위치** | `/etc/replication/treeactivation` |
|---|---|
| **새 위치** | `/libs/replication/treeactivation` |
| **구조 조정 지침** | 필요한 작업이 없습니다. |
| **메모** | 이제 트리 활성화 웹 콘솔을 를 통해 사용할 수 있습니다. **도구 > 배포 > 복제 > 트리 활성화**. |

{style=&quot;table-layout:auto&quot;}

### 공급업체 번역 커넥터 Cloud Services {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 공급업체 번역 커넥터 Cloud Services은 새 위치(<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ul>
       <li>를 통해 순 새로운 공급업체 번역 커넥터 Cloud Services 구성을 수동으로 만듭니다. <strong>도구 &gt; Cloud Services &gt; 번역 Cloud Services에서 AEM 작성 UI</strong>.<br /> 또는 </li>
       <li>새 공급업체 번역 커넥터 Cloud Services 구성을 이전 위치에서 새 위치(<code>/apps</code>, <code>/conf/global </code>또는 <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>적용 가능한 AEM 구성을 AEM 컨텐츠 계층 구조에 연결합니다.
      <ol>
       <li>AEM Sites의 <strong>AEM Sites &gt; 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>.</li>
       <li>를 통한 AEM 경험 조각 계층 <strong>AEM 경험 구성요소 &gt; 경험 구성요소 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>.</li>
       <li>를 통한 AEM 경험 조각 폴더 계층 <strong>AEM Experience Fragments &gt; 폴더 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>.</li>
       <li>AEM Assets 폴더 계층 - <strong>AEM Assets &gt; 폴더 &gt; 폴더 속성 &gt; Cloud Services 탭 &gt; 구성</strong>.</li>
       <li>를 통한 AEM 프로젝트 <strong>AEM 프로젝트 &gt; 프로젝트 &gt; 프로젝트 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>.</li>
      </ol> </li>
     <li>앞서 언급한 AEM 컨텐츠 계층에서 마이그레이션된 이전 번역 Cloud Services의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>번역 Cloud Services 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 워크플로우 알림 이메일 템플릿 {#workflow-notification-email-templates}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>수정된 모든 워크플로우 알림 이메일 템플릿은 새 위치 (<code>/conf/global</code>).</p>
    <ol>
     <li>수정된 워크플로우 알림 이메일 템플릿을 이전 위치에서 새 위치로 복사합니다.</li>
     <li>이전 위치에서 마이그레이션된 워크플로우 알림 이메일 템플릿을 제거합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>워크플로우 알림 이메일 템플릿 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 워크플로우 패키지 {#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>이전 위치의 기존 워크플로우 패키지를 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>다른 컨텐츠에서 참조하지 않으며 필요하지 않은 이전 위치에서 워크플로우 패키지를 제거합니다.</li>
     <li>다른 콘텐츠에서 참조하지 않지만 새 위치에서 필요한 이전 위치에서 워크플로우 패키지를 이동합니다.</li>
     <li>이전 위치에서 다른 콘텐츠에서 참조하는 모든 워크플로우 패키지를 둡니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>클래식 UI Miscadmin 콘솔을 통해 만든 워크플로우 패키지는 이전 위치에 유지되지만, 다른 모든 패키지는 새 위치로 유지됩니다.</p> <p>이전 위치 또는 이전 위치에 저장된 워크플로우 패키지는 클래식 UI miscadmin 콘솔을 통해 관리할 수 있습니다.</p> </td>
  </tr>
 </tbody>
</table>
