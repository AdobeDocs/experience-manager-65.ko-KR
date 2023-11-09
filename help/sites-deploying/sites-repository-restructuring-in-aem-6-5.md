---
title: AEM 6.5의 Sites 저장소 재구성
description: Sites용 AEM 6.5에서 새 저장소 구조로 마이그레이션하는 데 필요한 변경 작업을 수행하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 1%

---

# AEM 6.5의 Sites 저장소 재구성 {#sites-repository-restructuring-in-aem}

상위에 설명된 대로 [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md) 페이지 AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Sites 솔루션에 영향을 주는 저장소 변경 사항과 관련된 작업을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업이 필요하지만, 다른 변경 사항은 향후 업그레이드 전까지 연기될 수 있습니다.

**6.5 업그레이드 포함**

* [ContextHub 선분](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**향후 업그레이드 전**

* [Adobe Analytics 클라이언트 라이브러리](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [클래식 Microsoft Word에서 웹 페이지 디자인으로 전환](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [모바일 장치 에뮬레이터 구성](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [다중 사이트 관리자 블루프린트 구성](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [다중 사이트 관리자 롤아웃 구성](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [페이지 이벤트 알림 전자 메일 템플릿](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [페이지 스캐폴딩](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [응답형 격자 줄이기](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [정적 템플릿 디자인](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Adobe Target 통합 클라이언트 라이브러리](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation 클라이언트 라이브러리](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 6.5 업그레이드 포함 {#with-upgrade}

### ContextHub 선분 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code><br /> </p> <p><code>/conf/settings/settings/wcm/segments</code><br /> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 ContextHub 세그먼트 또는 수정된 ContextHub 세그먼트가 AEM에서 편집되지 않고 소스 제어에서 편집되는 경우 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치에서 새 ContextHub 세그먼트 또는 수정된 ContextHub 세그먼트를 적절한 새 위치(/<code>apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>이전 위치의 ContextHub 세그먼트에 대한 참조를 새 위치의 마이그레이션된 ContextHub 세그먼트로 업데이트합니다(<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>다음 QueryBuilder 쿼리는 ContextHub 세그먼트에 대한 모든 참조를 이전 위치에 찾습니다.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> 다음을 통해 실행할 수 있습니다. <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM QueryBuilder Debugger UI</a>. 이것은 트래버스 쿼리이므로 프로덕션에 대해 실행하지 말고, 필요에 따라 트래버스 제한이 조정되었는지 확인하십시오.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>이전 위치에 지속된 ContextHub 세그먼트는에서 읽기 전용으로 표시됩니다. <strong>AEM &gt; 개인화 &gt; 대상</strong>.</p> <p>AEM에서 ContextHub 세그먼트를 편집할 수 있게 하려면 새 위치로 마이그레이션해야 합니다(<code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>). AEM에서 만든 모든 새 ContentHub 세그먼트 는 새 위치로 유지됩니다(<code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>).</p> <p>AEM Sites 페이지 속성은 이전 위치(<code>/etc</code>) 또는 단일 새 위치(<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)을 선택해야 하므로 ContextHub 세그먼트를 그에 따라 마이그레이션해야 합니다.</p> <p>AEM 참조 사이트에서 사용하지 않는 모든 ContextHub 세그먼트를 제거하고 새 위치로 마이그레이션할 수 없습니다.</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>참고: ClientContext이 사용 중이라면 ContextHub로 변환하는 것이 좋습니다.</p> </td>
  </tr>
 </tbody>
</table>

## 향후 업그레이드 전 {#prior-to-upgrade}

### Adobe Analytics 클라이언트 라이브러리 {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>이러한 클라이언트 라이브러리를 사용자 지정하는 경우 경로가 아닌 범주별로 클라이언트 라이브러리를 참조해야 합니다.</p>
    <ol>
     <li>이전 위치에서 경로별 클라이언트 라이브러리에 대한 참조를 업데이트하여 사용해야 합니다 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">프레임워크를 참조하는 AEM 클라이언트 라이브러리</a>.</li>
     <li>AEM 클라이언트 라이브러리 참조 프레임워크를 사용할 수 없는 경우 AEM 클라이언트 라이브러리 프록시 서블릿을 통해 클라이언트 라이브러리의 절대 경로를 참조할 수 있습니다.
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>이러한 클라이언트 라이브러리는 편집할 수 없습니다.</p> <p>클라이언트 라이브러리 범주를 얻으려면 다음을 방문하십시오. <code>cq:ClientLIbraryFolder</code> crxdelIte를 통해 노드를 실행하고 categories 속성을 검사합니다.</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 클래식 Microsoft Word에서 웹 페이지 디자인으로 전환 {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 모든 디자인의 경우.</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치로 복사합니다. (<code>/apps</code>).</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> 포함 <code>allowProxy = true</code>.</li>
     <li>cq:designPath 속성에서 이전 위치에 대한 참조를 업데이트합니다.</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(이렇게 하려면 페이지 구현 코드를 업데이트해야 함).</li>
     <li>AEM Dispatcher 규칙을 업데이트하여 를 통해 클라이언트 라이브러리 제공 허용 <code>/etc.clientlibs/</code> 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않는 디자인 및 디자인 대화 상자를 통해 런타임 수정을 위한 경우:</p>
    <ul>
     <li>작성자 가능 디자인을 외부로 이동하지 않음 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 모바일 장치 에뮬레이터 구성 {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td>새 모바일 장치 에뮬레이터 구성을 새 위치로 마이그레이션해야 합니다.
    <ol>
     <li>이전 위치에서 새 위치로 새 모바일 장치 에뮬레이터 구성 복사(<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>이러한 모바일 장치 에뮬레이터 구성에 의존하는 AEM Sites 페이지의 경우 페이지의 <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> 노드: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>이러한 모바일 장치 에뮬레이터 구성에 의존하는 편집 가능한 템플릿의 경우 다음을 가리키며 편집 가능한 템플릿을 업데이트합니다. <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> 새 위치로 이동합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>모바일 장치 에뮬레이터 구성 확인은 다음 순서로 수행됩니다.</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 다중 사이트 관리자 블루프린트 구성 {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/apps/msm</code> (고객 블루프린트 구성)</p> <p><code>/libs/msm</code> (Screens, Commerce에 대한 기본 블루프린트 구성)</p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 다중 사이트 관리자 블루프린트 구성이나 수정된 구성을 새 위치( )로 마이그레이션해야 합니다.<code>/apps</code>).</p>
    <ol>
     <li>이전 위치에서 새 위치로 새 다중 사이트 관리자 블루프린트 구성 또는 수정된 블루프린트 구성을 복사합니다(<code>/apps</code>).</li>
     <li>이전 위치에서 마이그레이션된 다중 사이트 관리자 블루프린트 구성을 제거합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>AEM에서 제공하는 다중 사이트 관리자 블루프린트 구성이 의 새 위치에 있습니다. <code>/libs</code>.</p> <p>콘텐츠가 다중 사이트 관리자 파란색 구성을 참조하지 않으므로 조정할 콘텐츠 참조가 없습니다.</p> </td>
  </tr>
 </tbody>
</table>

### 다중 사이트 관리자 롤아웃 구성 {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 다중 사이트 관리자 롤아웃 구성 또는 수정된 구성을 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치에서 새 위치로 신규 또는 수정된 다중 사이트 관리자 롤아웃 구성 복사(<code>/apps</code>).</li>
     <li>AEM Pages의 참조를 이전 위치의 다중 사이트 관리자 롤아웃 구성으로 업데이트하여 새 위치의 해당 위치(<code>/libs</code> 또는 <code>/apps</code>).</li>
    </ol> <p>이전 위치에서 마이그레이션된 다중 사이트 관리자 롤아웃 구성을 제거합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>이전 위치에서 마이그레이션된 다중 사이트 관리자 롤아웃 구성을 제거하지 못하면 중복 롤아웃 옵션이 AEM 작성자에게 표시됩니다.</td>
  </tr>
 </tbody>
</table>

### 페이지 이벤트 알림 전자 메일 템플릿 {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 페이지 이벤트 알림 전자 메일 템플릿만 지원됩니다.</p> <p>페이지 이벤트 전자 메일 템플릿 해결은 다음 순서로 수행됩니다.</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>새로 만들거나 수정한 모든 페이지 이벤트 알림 전자 메일 템플릿은 <code>/apps</code>:</p>
    <ol>
     <li>이전 위치에서 새 위치로 신규 또는 수정된 페이지 이벤트 알림 이메일 템플릿 복사(<code>/apps</code>).</li>
     <li>이전 위치에서 마이그레이션된 페이지 이벤트 알림 전자 메일 템플릿을 제거합니다.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 페이지 스캐폴딩 {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td>이전 위치에서 만든 스캐폴딩은 기존 스캐폴딩 프레임워크를 사용하므로 새 위치로 마이그레이션할 수 없습니다. 새 위치에 맞게 기존 스캐폴딩은 지원되는 스캐폴딩 프레임워크를 사용하여 다시 개발해야 합니다.</td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 응답형 격자 줄이기 {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>사용자 지정 LESS 파일의 이전 위치에 대한 참조를 업데이트해야 새 위치에서 가져올 수 있습니다.</p>
    <ul>
     <li>이전 위치에서 grid_base.less를 참조하는 참조 사용자 정의 LESS 파일을 업데이트하여 새 위치를 참조합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>존재하지 않는 항목 참조 <code>grid_base.less</code> 이 파일을 사용하면 페이지 및 템플릿 편집기의 레이아웃 모드가 작동하지 않고 페이지 레이아웃이 중단됩니다.</td>
  </tr>
 </tbody>
</table>

### 정적 템플릿 디자인 {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 모든 디자인의 경우.</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치로 복사합니다. (<code>/apps</code>).</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> 포함 <code>allowProxy = true</code>.</li>
     <li>의 이전 위치에 대한 참조 업데이트 <code>cq:designPath</code> 를 통한 속성 <strong>AEM &gt; 사이트 &gt; 사용자 지정 사이트 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 디자인 필드</strong>.</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(이렇게 하려면 페이지 구현 코드를 업데이트해야 함).</li>
     <li>AEM Dispatcher 규칙을 업데이트하여 를 통해 클라이언트 라이브러리 제공 허용 <code>/etc.clientlibs/</code> 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않는 디자인 및 디자인 대화 상자를 통해 런타임 수정을 위한 경우:</p>
    <ul>
     <li>작성자 가능 디자인을 외부로 이동하지 않음 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>권장 접근 방법은 디자인 대신 구조 콘텐츠 및 정책을 사용하는 편집 가능한 템플릿을 사용하여 AEM Sites 및 페이지를 작성하는 것입니다.</td>
  </tr>
 </tbody>
</table>

<!-- Search&Promote is end of life as of September 1, 2022 ### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Previous location</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>New location(s)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Restructuring guidance</strong></td>
   <td><p>Any custom use of these Client Libraries should reference the Client Library by category, and not by path.</p>
    <ol>
     <li>Any references to the Client Library by path at the Previous Location should be updated to use <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM's Client Library referencing framework</a>.</li>
     <li>If AEM's Client Library referencing framework cannot be used, the absolute path of the Client Libraries can be referenced via AEM's Client Library Proxy servlet:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td><p>Editing of these Client Libraries was never supported.</p> <p>To obtain the Client Library categories, visit each cq:ClientLIbraryFolder node via CRXDELite and inspect the categories property:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table> -->

### Adobe Target 통합 클라이언트 라이브러리 {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>이러한 클라이언트 라이브러리를 사용자 지정할 때 경로가 아닌 범주별로 클라이언트 라이브러리를 참조해야 합니다.</p>
    <ol>
     <li>이전 위치에서 경로별 클라이언트 라이브러리에 대한 참조를 업데이트하여 사용해야 합니다 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">프레임워크를 참조하는 AEM 클라이언트 라이브러리</a>.</li>
     <li>AEM 클라이언트 라이브러리 참조 프레임워크를 사용할 수 없는 경우 AEM 클라이언트 라이브러리 프록시 서블릿을 통해 클라이언트 라이브러리의 절대 경로를 참조할 수 있습니다.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>이러한 클라이언트 라이브러리는 편집할 수 없습니다.</p> <p>클라이언트 라이브러리 범주를 얻으려면 CRXDELite를 통해 각 cq:ClientLIbraryFolder 노드를 방문하여 범주 속성을 검사하십시오.</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### WCM Foundation 클라이언트 라이브러리 {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>이러한 클라이언트 라이브러리를 사용자 지정할 때 경로가 아닌 범주별로 클라이언트 라이브러리를 참조해야 합니다.</p>
    <ol>
     <li>이전 위치에서 경로별 클라이언트 라이브러리에 대한 참조를 업데이트하여 사용해야 합니다 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">프레임워크를 참조하는 AEM 클라이언트 라이브러리</a>.</li>
     <li>AEM 클라이언트 라이브러리 참조 프레임워크를 사용할 수 없는 경우 AEM 클라이언트 라이브러리 프록시 서블릿을 통해 클라이언트 라이브러리의 절대 경로를 참조할 수 있습니다.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>이러한 클라이언트 라이브러리는 편집할 수 없습니다.</p> <p>클라이언트 라이브러리 범주를 얻으려면 다음을 방문하십시오. <code>cq:ClientLIbraryFolder</code> crxdelIte를 통해 노드를 실행하고 categories 속성을 검사합니다.</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
