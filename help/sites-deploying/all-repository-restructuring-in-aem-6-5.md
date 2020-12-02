---
title: AEM 6.5의 공용 저장소 재구성
seo-title: AEM 6.5의 공용 저장소 재구성
description: AEM의 모든 영역에 공통으로 적용되는 AEM 6.5의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
seo-description: AEM의 모든 영역에 공통으로 적용되는 AEM 6.5의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: 6396660b642fd78ac7f311fa416efe0e0d52a9e3
workflow-type: tm+mt
source-wordcount: '2721'
ht-degree: 2%

---


# AEM 6.5 {#common-repository-restructuring-in-aem}의 공용 저장소 재구성

상위 [AEM 6.5](/help/sites-deploying/repository-restructuring.md) 페이지의 저장소 재구성 페이지에 설명된 대로 AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 모든 솔루션에 영향을 줄 수 있는 저장소 변경 사항과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업해야 하는 반면 다른 변경 사항은 향후 업그레이드 시까지 연기될 수 있습니다.

**6.5 업그레이드**

* [ContextHub 구성](#contexthub-6.5)
* [워크플로 인스턴스](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [워크플로우 모델](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [워크플로 런처](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [워크플로우 스크립트](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**업그레이드 전**

* [ContextHub 구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [클래식 Cloud Services 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [클래식 대시보드 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [클래식 보고서 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [기본 디자인](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Adobe DTM JavaScript 끝점](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Adobe DTM 웹 후크 끝점](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [받은 편지함 작업](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [다중 사이트 관리자 블루프린트 구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM 프로젝트 대시보드 가젯 구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [복제 알림 이메일 템플릿](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [태그](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [번역 클라우드 서비스](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [번역 언어](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [번역 규칙](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [번역 위젯 클라이언트 라이브러리](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [트리 활성화 웹 콘솔](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [공급업체 번역 커넥터 Cloud Services](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [워크플로우 알림 이메일 템플릿](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 6.5 업그레이드 시 {#with-upgrade}

### ContextHub 구성 {#contexthub-6.5}

AEM 6.4부터는 기본 ContextHub 구성이 없습니다. 따라서 사이트의 루트 수준에서 `cq:contextHubPathproperty`을(를) 설정하여 사용해야 하는 구성을 나타내야 합니다.

1. 사이트의 루트로 이동합니다.
1. 루트 페이지의 페이지 속성을 열고 개인화 탭을 선택합니다.
1. Contexthub 경로 필드에 고유한 ContextHub 구성 경로를 입력합니다.

또한 ContextHub 구성에서, `sling:resourceType`은(는) 반드시 상대적이거나 절대적이지 않도록 업데이트해야 합니다.

1. CRX DE Lite에서 ContextHub 구성 노드의 속성을 엽니다(예:`/apps/settings/cloudsettings/legacy/contexthub`
1. `sling:resourceType`을(를) `/libs/granite/contexthub/cloudsettings/components/baseconfiguration`에서 `granite/contexthub/cloudsettings/components/baseconfiguration`(으)로 변경

즉, ContextHub 구성의 `sling:resourceType`은(는) 절대적이지 않고 상대적이어야 합니다.

### 워크플로우 모델 {#workflow-models}

<table>
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
     <li>수정된 워크플로우 모델을 이전 위치에 존재하는 로컬 AEM 6.4 개발 인스턴스에 배포합니다.</li>
     <li>AEM &gt; 도구 &gt; 워크플로우 &gt; 모델에서 AEM 워크플로우 모델 편집기를 사용하여 워크플로우 모델을 편집합니다.</li>
     <li>수정된 AEM 제공 워크플로우 모델 마이그레이션 시
      <ol>
       <li>워크플로우 모델 편집기가 열리면 브라우저의 주소 URL을 수정하고 경로 세그먼트 /libs/settings/workflow/models를 /etc/workflow/models로 바꿉니다.
        <ul>
         <li>예를 들어 변경:<em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em>http://localhost:4502/editor.html<em>/etc/workflow/models</strong>/dam/update_asset.html</em><strong></strong></li>
        </ul> </li>
      </ol> </li>
     <li>워크플로우 모델 정의를 /conf/global/workflow/models에 복사하는 워크플로우 모델 편집기에서 편집 모드를 활성화합니다.</li>
     <li>동기화 버튼을 눌러 /var/workflow/models 아래의 런타임 워크플로우 모델에 대한 변경 사항을 동기화합니다.</li>
     <li>워크플로우 모델(/conf/global/workflow/models/&lt;workflow-model&gt;)과 런타임 워크플로우 모델(/var/workflow/models/&lt;workflow-model&gt;)을 모두 내보내고 AEM 프로젝트에 통합합니다.
      <ol>
       <li>예를 들어 내보내기:
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> 및 </li>
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
    </ol> <p>따라서 이전 위치에 보관되어 있는 AEM 제공 워크플로우 모델의 사용자 정의 설정을 /conf/global/settings/workflow/models로 이동해야 하며, 그렇지 않으면 /libs/settings/workflow/models에서 AEM 제공 워크플로우 모델 정의로 대체됩니다.</p> </td>
  </tr>
 </tbody>
</table>

### 워크플로 인스턴스 {#workflow-instances}

<table>
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
   <td><p>새 위치에 정렬하는 데 필요한 작업은 없습니다.</p> <p>이전 위치에서 이전 워크플로우 인스턴스는 안전하게 계속 저장할 수 있으며 새 작업 흐름 인스턴스가 새 위치에 생성됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>Any explicit path references in
    이전 위치에 대한 <code>
     custom
    </code> 코드도 새 위치를 고려해야 합니다. AEM Workflow API를 사용하려면 이 코드를 리팩토링하는 것이 좋습니다.</td>
  </tr>
 </tbody>
</table>

### 워크플로 런처 {#workflow-launchers}

<table>
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
   <td><p>새 또는 수정된 모든 워크플로우 발사체는 <code>/conf/global/workflow/launcher/config</code>으로 마이그레이션해야 합니다.</p>
    <ol>
     <li>새 또는 수정된 Workflow Launcher 구성을 이전 위치에서 새 위치(<code>/conf/global</code>)로 복사합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>Workflow Launcher 해결은 다음 순서로 이루어집니다.</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>따라서 이전 위치에 남아 있는 AEM 제공 Workflow Launcher의 모든 사용자 정의는 새 위치(<code>/conf/global/settings/workflow/launcher</code>, 유지하려는 경우, 그렇지 않으면 <code>/libs/settings/workflow/launcher</code>의 AEM 제공 Workflow Launcher 정의로 대체됩니다.</p> </td>
  </tr>
 </tbody>
</table>

### 워크플로 스크립트 {#workflow-scripts}

<table>
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
   <td><p>새로운 워크플로우 스크립트나 수정된 워크플로우 스크립트는 새 위치로 마이그레이션해야 하며 새 위치를 반영하여 업데이트된 참조하는 워크플로우 모델을 참조해야 합니다.</p>
    <ol>
     <li>새 또는 수정된 워크플로 스크립트를 이전 위치에서 새 위치로 복사합니다.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> SCM에서 유지 관리되어야 합니다.</li>
      </ul> </li>
     <li>워크플로우 모델의 이전 위치에서 워크플로우 스크립트에 대한 모든 참조를 업데이트하여 새 위치를 가리킵니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>AEM 6.4 SP1이 출시되면 6.5까지 이러한 재조정을 보류할 수 있게 됩니다.
     <code>
      upgrade
     </code>.</p> <p>AEM 6.4 SP1이 출시되기 전에 AEM 6.4로 업그레이드하는 경우 업그레이드 프로젝트의 일부로 이 재구성을 수행해야 합니다. 이렇게 하지 않으면 이전 위치에서 스크립트를 참조하는 워크플로우 단계를 편집하고 저장하면 워크플로우 단계에서 워크플로우 스크립트 참조가 완전히 제거되고, 스크립트 선택 드롭다운에서 새 위치의 워크플로우 스크립트만 사용할 수 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

## 업그레이드 전 {#prior-to-upgrade}

### ContextHub 구성 {#contexthub-configurations}

<table>
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
   <td><p>새 위치 또는 수정된 모든 ContextHub 구성은 새 위치로 마이그레이션해야 하며 참조하는 AEM Sites 페이지를 업데이트하여 새 위치를 반영해야 합니다.</p>
    <ol>
     <li>새 또는 수정된 ContextHub 구성을 이전 위치에서 새 위치로 복사합니다.</li>
     <li>해당 AEM 구성을 AEM 컨텐츠 계층 구조에 연결합니다.
      <ol>
       <li><strong>AEM Sites &gt; 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 클라우드 구성을 통한 AEM Sites 페이지 계층</strong>.</li>
      </ol> </li>
     <li>앞서 언급한 AEM 컨텐츠 계층 구조에서 마이그레이션된 기존 ContextHub 구성 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 클래식 Cloud Services 디자인 {#classic-cloud-services-designs}

<table>
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
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않은 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치(<code>/apps</code>)로 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>와 함께 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li><span class="code">의 이전 위치에 대한 참조를 업데이트합니다.
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span> 속성.</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(페이지 구현 코드 업데이트 필요).</li>
     <li>/etc.clientlibs/..를 통해 클라이언트 라이브러리의 제공을 허용하도록 AEM Dispatcher 규칙을 업데이트합니다. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리하지 않고 디자인 대화 상자를 통해 수정된 모든 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 <code>/etc</code> 밖으로 이동하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### 클래식 대시보드 디자인 {#classic-dashboards-designs}

<table>
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
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않은 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치에서 새 위치(/apps)로 디자인을 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>와 함께 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li>Update references to the Previous Location in the
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(페이지 구현 코드 업데이트 필요).</li>
     <li>/etc.clientlibs/..를 통해 클라이언트 라이브러리의 제공을 허용하도록 AEM Dispatcher 규칙을 업데이트합니다. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리하지 않고 디자인 대화 상자를 통해 수정된 모든 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 <code>/etc</code> 밖으로 이동하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### 클래식 보고서 디자인 {#classic-reports-designs}

<table>
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
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않은 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치에서 새 위치(/apps)로 디자인을 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>와 함께 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li>Update references to the Previous Location in the
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(페이지 구현 코드 업데이트 필요).</li>
     <li>/etc.clientlibs/..를 통해 클라이언트 라이브러리의 제공을 허용하도록 AEM Dispatcher 규칙을 업데이트합니다. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리하지 않고 디자인 대화 상자를 통해 수정된 모든 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 <code>/etc</code> 밖으로 이동하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### 기본 디자인 {#default-designs}

<table>
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
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않은 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치에서 새 위치(/apps)로 디자인을 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>와 함께 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li>Update references to the Previous Location in the
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(페이지 구현 코드 업데이트 필요).</li>
     <li>/etc.clientlibs/..를 통해 클라이언트 라이브러리의 제공을 허용하도록 AEM Dispatcher 규칙을 업데이트합니다. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리하지 않고 디자인 대화 상자를 통해 수정된 모든 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 <code>/etc</code> 밖으로 이동하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### Adobe DTM JavaScript 끝점 {#adobe-dtm-javascript-endpoint}

<table>
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
   <td><p>필요한 작업이 없습니다.</p> <p>공개 이전 위치는 개인 새 위치의 프록시 끝점 역할을 합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### Adobe DTM 웹 후크 끝점 {#adobe-dtm-web-hook-endpoint}

<table>
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
   <td><p>필요한 작업이 없습니다.</p> <p>공개 이전 위치는 개인 새 위치의 프록시 끝점 역할을 합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### 받은 편지함 작업 {#inbox-tasks}

<table>
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
   <td>필요한 경우 <strong>받은 편지함 유지 관리 작업</strong>을 사용하여 이전 위치에서 이전 작업을 제거합니다.</td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>작업을 새 위치로 마이그레이션하는 작업은 필요하지 않습니다.</p>
    <ul>
     <li>이전 위치에 있는 작업은 계속 사용할 수 있으며 작동합니다.</li>
     <li>새 작업은 새 위치에 생성됩니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 다중 사이트 관리자 블루프린트 구성 {#multi-site-manager-blueprint-configurations}

<table>
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
     <li>사용자 지정 구성을 <code>/etc/blueprints</code>에서 <code>/apps/msm</code>로 복사합니다.</li>
     <li>제거 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### AEM 프로젝트 대시보드 가젯 구성 {#aem-projects-dashboard-gadget-configurations}

<table>
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
   <td><p>신규 또는 수정된 AEM 프로젝트 대시보드 가젯 구성은 새 위치(<code>/apps</code>)로 마이그레이션해야 합니다.</p>
    <ol>
     <li>새 또는 수정된 AEM 프로젝트 대시보드 가젯 구성을 이전 위치에서 새 위치(<code>/apps</code>)로 복사합니다.
      <ol>
       <li>수정되지 않은 AEM 프로젝트 대시보드 가젯 구성은 이제 새 위치(<code>/libs</code>)에 있으므로 복사하지 마십시오.</li>
      </ol> </li>
     <li>이전 위치를 참조하는 모든 AEM Projects 템플릿을 업데이트하여 적절한 새 위치를 지정합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>AEM 6.4 호환성 패키지가 적용되는 경우 호환성 패키지가 제거될 때 저장소 정렬 작업을 수행해야 합니다.</td>
  </tr>
 </tbody>
</table>

### 복제 알림 이메일 템플릿 {#replication-notification-e-mail-template}

<table>
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
   <td><p>새 또는 수정된 복제 알림 이메일 템플릿은 새 위치(<code>/apps</code>)로 마이그레이션해야 합니다.</p>
    <ol>
     <li>새 또는 수정된 복제 알림 이메일 템플릿을 이전 위치에서 새 위치(<code>/apps</code>)로 복사합니다.</li>
     <li>이전 위치에서 마이그레이션된 복제 알림 이메일 템플릿을 제거합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>새로운 복제 알림 이메일 템플릿은 새 로케일을 지원하는 유일한 새로운 기능입니다.</p> <p>복제 알림 이메일 템플릿 해상도는 다음 순서로 발생합니다.</p>
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

<table>
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
   <td><p>모든 태그는 <code>/content/cq:tags</code>으로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 모든 태그를 새 위치로 복사합니다.</li>
     <li>이전 위치에서 모든 태그를 제거합니다.</li>
     <li>AEM Web Console을 통해 AEM용 Day Communication 5 Tagging OSGi 번들을 <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em>에서 다시 시작하여 새 위치에 컨텐츠가 포함되어 있으므로 사용해야 합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>Day Communication Tagging OSGi 번들을 다시 시작하면 이전 위치가 비어 있는 경우에만 새 위치를 태그 루트로 등록합니다.</p> <p>태그 해상도에 AEM TagManager API를 활용하는 모든 기능을 위해 새 위치로 마이그레이션한 후에도 이전 위치에 대한 참조가 계속 작동합니다.</p> <p>경로 <code>/etc/tags</code>을(를) 명시적으로 참조하는 모든 사용자 지정 코드는 <span class="code">/content/(으)로 업데이트해야 합니다.
      <code>
       cq
      </code>
      이 마이그레이션과 함께 <code>
       :tags
      </code></span> 또는 가급적이면 다시 작성하여 TagManager Java API를 활용합니다.</p> </td>
  </tr>
 </tbody>
</table>

### 번역 클라우드 서비스 {#translation-cloud-services}

<table>
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
   <td><p>모든 새 번역 Cloud Services은 새 위치(<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ul>
       <li>AEM 작성 UI를 통해 <strong>도구 &gt; Cloud Services &gt; 번역 Cloud Services</strong>에서 새 번역 Cloud Services 구성을 수동으로 다시 만듭니다.<br /> 또는 </li>
       <li>이전 위치에서 새 번역 Cloud Services 구성을 새 위치(<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)로 복사합니다.</li>
      </ul> </li>
     <li>해당 AEM 구성을 AEM 컨텐츠 계층 구조에 연결합니다.
      <ol>
       <li>AEM Sites 페이지 계층 구조는 <strong>AEM Sites &gt; 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>을 통해 제공됩니다.</li>
       <li>AEM 경험 조각 계층 - <strong>AEM 경험 조각 &gt; 경험 조각 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>을 통해</li>
       <li>AEM 경험 조각 폴더 계층 - <strong>AEM 경험 조각 &gt; 폴더 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>을 통해<br /> </li>
       <li><strong>AEM Assets &gt; 폴더 &gt; 폴더 속성 &gt; Cloud Services 탭 &gt; 구성</strong>을 통해 AEM Assets 폴더 계층 구조를 만듭니다.</li>
       <li>AEM 프로젝트는 <strong>AEM 프로젝트 &gt; 프로젝트 &gt; 프로젝트 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>을 통해 수행할 수 있습니다.</li>
      </ol> </li>
     <li>앞서 언급한 AEM 컨텐츠 계층 구조에서 마이그레이션된 기존 번역 Cloud Services의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>변환 Cloud Services 해상도는 다음 순서로 발생합니다.</p>
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

<table>
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
   <td><p>새로 정의되거나 수정된 번역 언어 정의는 모든 번역 언어 정의를 새 위치(<code>/apps</code>)로 마이그레이션해야 합니다.</p>
    <ol>
     <li>번역 언어 정의에 추가 또는 수정 사항이 있는 경우 이전 위치의 모든 번역 언어 정의를 새 위치(<code>/apps</code>)로 복사합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>번역 언어 경로 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>이 해상도는 병합 오버레이를 지원하지 않습니다. 즉, 해결된 경로에 지원되는 모든 언어가 포함되어야 하며, 고주문 해상도의 지원 언어가 상속되지 않습니다.</p> </td>
  </tr>
 </tbody>
</table>

### 번역 규칙 {#translation-rules}

<table>
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
   <td><p>수정된 번역 규칙 XML 파일은 새 위치(<code>/apps</code> 또는 <code>/conf/global</code>)로 마이그레이션해야 합니다.</p> <p>1. 수정된 번역 규칙 XML 파일을 이전 위치에서 새 위치로 복사합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>복제 변환 규칙 XML 해상도는 다음 순서로 발생합니다.</p>
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

<table>
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
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않은 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치에서 새 위치(/apps)로 디자인을 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>와 함께 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li>Update references to the Previous Location in the
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 속성</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(페이지 구현 코드 업데이트 필요).</li>
     <li>/etc.clientlibs/..를 통해 클라이언트 라이브러리의 제공을 허용하도록 AEM Dispatcher 규칙을 업데이트합니다. 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리하지 않고 디자인 대화 상자를 통해 수정된 모든 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 <code>/etc</code> 밖으로 이동하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### 트리 활성화 웹 콘솔 {#tree-activation-web-console}

| **이전 위치** | `/etc/replication/treeactivation` |
|---|---|
| **새 위치** | `/libs/replication/treeactivation` |
| **구조 조정 지침** | 필요한 작업이 없습니다. |
| **메모** | 트리 활성화 웹 콘솔은 이제 **도구 > 배포 > 복제 > 트리 활성화**&#x200B;를 통해 사용할 수 있습니다. |

### 공급업체 번역 커넥터 Cloud Services {#vendor-translation-connector-cloud-services}

<table>
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
   <td><p>모든 새 공급업체 번역 커넥터 Cloud Services은 새 위치(<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ul>
       <li>도구 &gt; Cloud Services &gt; 번역 Cloud Services</strong>에서 <strong>AEM 작성 UI를 통해 새 공급업체 번역 커넥터 Cloud Services 구성을 수동으로 만듭니다.<br /> 또는 </strong></li>
       <li>새 공급업체 변환 커넥터 Cloud Services 구성을 이전 위치에서 새 위치(<code>/apps</code>, <code>/conf/global </code> 또는 <code>/conf/&lt;tenant&gt;</code>)로 복사합니다.</li>
      </ul> </li>
     <li>해당 AEM 구성을 AEM 컨텐츠 계층 구조에 연결합니다.
      <ol>
       <li>AEM Sites 페이지 계층 구조는 <strong>AEM Sites &gt; 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>을 통해 제공됩니다.</li>
       <li>AEM 경험 조각 계층 - <strong>AEM 경험 조각 &gt; 경험 조각 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>을 통해</li>
       <li>AEM 경험 조각 폴더 계층 - <strong>AEM 경험 조각 &gt; 폴더 &gt; 속성 &gt; Cloud Services 탭 &gt; 클라우드 구성</strong>을 통해</li>
       <li><strong>AEM Assets &gt; 폴더 &gt; 폴더 속성 &gt; Cloud Services 탭 &gt; 구성</strong>을 통해 AEM Assets 폴더 계층 구조를 만듭니다.</li>
       <li>AEM 프로젝트는 <strong>AEM 프로젝트 &gt; 프로젝트 &gt; 프로젝트 속성 &gt; 고급 탭 &gt; 클라우드 구성</strong>을 통해 수행할 수 있습니다.</li>
      </ol> </li>
     <li>앞서 언급한 AEM 컨텐츠 계층 구조에서 마이그레이션된 기존 번역 Cloud Services의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>변환 Cloud Services 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 워크플로 알림 이메일 템플릿 {#workflow-notification-email-templates}

<table>
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
   <td><p>수정된 워크플로 알림 이메일 템플릿은 새 위치(<code>/conf/global</code>)로 마이그레이션해야 합니다.</p>
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

### 워크플로 패키지 {#workflow-packages}

<table>
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
   <td><p>이전 위치의 기존 워크플로우 패키지는 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>다른 컨텐츠에서 참조되지 않고 그렇지 않은 이전 위치에서 워크플로우 패키지를 제거합니다.</li>
     <li>다른 컨텐츠가 참조하지 않고 새 위치에서 필요로 하는 이전 위치에서 워크플로우 패키지를 이동합니다.</li>
     <li>이전 위치의 다른 컨텐츠에서 참조하는 모든 워크플로우 패키지를 그대로 두십시오.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>클래식 UI Miscadmin 콘솔을 통해 생성된 워크플로우 패키지는 이전 위치에 유지되지만 다른 모든 패키지는 새 위치로 유지됩니다.</p> <p>이전 또는 이전 위치에 저장된 워크플로우 패키지는 클래식 UI miscadmin 콘솔을 통해 관리할 수 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

