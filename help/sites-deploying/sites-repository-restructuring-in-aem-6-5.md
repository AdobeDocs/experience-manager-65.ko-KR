---
title: AEM 6.5의 사이트 저장소 재구성
seo-title: AEM 6.5의 사이트 저장소 재구성
description: AEM 6.5 for Sites의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 사항을 수행하는 방법을 살펴볼 수 있습니다.
seo-description: AEM 6.5 for Sites의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 사항을 수행하는 방법을 살펴볼 수 있습니다.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 1%

---


# AEM 6.5의 사이트 저장소 재구성 {#sites-repository-restructuring-in-aem}

상위 [AEM 6.5](/help/sites-deploying/repository-restructuring.md) 페이지의 저장소 재구성 페이지에 설명된 대로 AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Sites 솔루션에 영향을 주는 저장소 변경과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 동안 작업해야 하는 반면, 다른 변경 사항은 향후 업그레이드될 때까지 연기될 수 있습니다.

**6.5 업그레이드 포함**

* [ContextHub 선분](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**향후 업그레이드 전**

* [Adobe Analytics 클라이언트 라이브러리](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [클래식 Microsoft Word에서 웹 페이지 디자인으로](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [모바일 장치 에뮬레이터 구성](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [다중 사이트 관리자 블루프린트 구성](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [다중 사이트 관리자 롤아웃 구성](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [페이지 이벤트 알림 이메일 템플릿](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [페이지 스캐폴딩](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [반응형 격자 덜](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [정적 템플릿 디자인](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Adobe 검색 및 홍보 통합 클라이언트 라이브러리](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Adobe Target 통합 클라이언트 라이브러리](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 6.5 업그레이드 시 {#with-upgrade}

### ContextHub 선분 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 또는 수정된 ContextHub 세그먼트가 AEM에서 편집되지 않고 소스 제어에서 편집하려는 경우 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 새 또는 수정된 ContextHub 세그먼트를 적절한 새 위치(/<code>apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)로 복사</li>
     <li>이전 위치의 ContextHub 세그먼트에 대한 참조를 새 위치(<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>)의 마이그레이션된 ContextHub 세그먼트에 대한 참조를 업데이트합니다.</li>
    </ol> <p>다음 QueryBuilder 쿼리는 이전 위치에서 ContextHub 세그먼트에 대한 모든 참조를 찾습니다.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> 이 작업은  <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM QueryBuilder 디버거 UI를 통해 실행할 수 있습니다</a>. 이것은 탐색 쿼리이므로 프로덕션에서 실행하지 말고 필요에 따라 트래픽 제한을 조정하십시오.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>ContextHub 세그먼트가 이전 위치에 지속되면 <strong>AEM &gt; Personalization &gt; Audiences</strong>에 읽기 전용으로 표시됩니다.</p> <p>ContextHub 세그먼트를 AEM에서 편집할 수 있으려면 새 위치(<code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)로 마이그레이션해야 합니다. AEM에서 만든 모든 새 ContentHub 세그먼트 세그먼트는 새 위치(<code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)로 유지됩니다.</p> <p>AEM Sites 페이지 속성은 이전 위치(<code>/etc</code>) 또는 단일 새 위치(<code>/apps</code>, <code>/conf/global</code> 또는 <code>/conf/&lt;tenant&gt;</code>)만 선택할 수 있으므로 이에 따라 ContextHub 세그먼트가 마이그레이션되어야 합니다.</p> <p>AEM 참조 사이트에서 사용하지 않은 ContextHub 세그먼트는 모두 제거하고 새 위치로 마이그레이션할 수 없습니다.</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>참고:ClientContext을 사용 중인 경우 ContextHub로 변환하는 것이 좋습니다.</p> </td>
  </tr>
 </tbody>
</table>

## 업그레이드 전 {#prior-to-upgrade}

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
   <td><p>이러한 클라이언트 라이브러리를 사용자 정의할 때 사용하는 모든 사용자 지정 사용은 경로 대신 범주별로 클라이언트 라이브러리를 참조해야 합니다.</p>
    <ol>
     <li>이전 위치의 경로별로 클라이언트 라이브러리에 대한 모든 참조는 프레임워크</a>을 참조하는 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM 클라이언트 라이브러리를 사용하도록 업데이트해야 합니다.</a></li>
     <li>프레임워크 참조 AEM 클라이언트 라이브러리를 사용할 수 없는 경우 클라이언트 라이브러리의 절대 경로를 AEM Client Library Proxy 서블릿을 통해 참조할 수 있습니다.
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
   <td><p>이러한 클라이언트 라이브러리의 편집은 지원되지 않습니다.</p> <p>클라이언트 라이브러리 범주를 가져오려면 CRXDELite를 통해 각 <code>cq:ClientLIbraryFolder</code> 노드를 방문하여 categories 속성을 검사합니다.</p>
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

### 클래식 Microsoft Word에서 웹 페이지 디자인 {#classic-microsoft-word-to-web-page-designs}

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
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임 시 작성되지 않은 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치(<code>/apps</code>)로 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>이(가) 있는 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li>cq:designPath 속성에서 이전 위치에 대한 참조를 업데이트합니다.</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(페이지 구현 코드를 업데이트해야 함).</li>
     <li><code>/etc.clientlibs/</code> 프록시 서블릿을 통해 클라이언트 라이브러리 제공을 허용하도록 AEM Dispatcher 규칙을 업데이트합니다.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 <code>/etc</code> 밖으로 이동하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
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
   <td>새로운 모바일 장치 에뮬레이터 구성은 새 위치로 마이그레이션해야 합니다.
    <ol>
     <li>새 모바일 장치 에뮬레이터 구성을 이전 위치에서 새 위치(<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>)로 복사합니다.</li>
     <li>이러한 모바일 장치 에뮬레이터 구성에 의존하는 모든 AEM Sites 페이지의 경우 페이지의 <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> 노드:<br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>이러한 모바일 장치 에뮬레이터 구성에 의존하는 편집 가능한 템플릿의 경우 <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span>를 새 위치로 보냅니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>모바일 장치 에뮬레이터 구성 해상도는 다음 순서로 발생합니다.</p>
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
   <td><p><code>/apps/msm</code> (고객 블루프린트 구성)</p> <p><code>/libs/msm</code> (화면, 상거래에 대한 기본 블루프린트 구성)</p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새로운 사이트 관리자 블루프린트 구성을 수정하거나 새로 만든 사람은 모두 새 위치(<code>/apps</code>)로 마이그레이션해야 합니다.</p>
    <ol>
     <li>새 사이트 관리자 블루프린트 구성을 이전 위치에서 새 위치(<code>/apps</code>)로 복사합니다.</li>
     <li>이전 위치에서 마이그레이션된 다중 사이트 관리자 블루프린트 구성을 제거합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>AEM에서 제공한 모든 다중 사이트 관리자 블루프린트 구성은 <code>/libs</code>의 새 위치에 있습니다.</p> <p>콘텐트는 다중 사이트 관리자 파란색 구성을 참조하지 않으므로 조정할 내용 참조가 없습니다.</p> </td>
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
   <td><p>새 사이트 관리자 또는 수정된 모든 다중 사이트 관리자 롤아웃 구성은 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>새 사이트 관리자 롤아웃 구성을 이전 위치의 새 위치(<code>/apps</code>)로 복사합니다.</li>
     <li>AEM 페이지의 모든 참조를 이전 위치의 다중 사이트 관리자 롤아웃 구성으로 업데이트하여 새 위치(<code>/libs</code> 또는 <code>/apps</code>)의 상대 위치를 가리킵니다.</li>
    </ol> <p>이전 위치에서 마이그레이션된 다중 사이트 관리자 롤아웃 구성을 제거합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>이전 위치에서 마이그레이션된 다중 사이트 관리자 롤아웃 구성을 제거하지 않으면 AEM 작성자에게 중복된 롤아웃 옵션이 표시됩니다.</td>
  </tr>
 </tbody>
</table>

### 페이지 이벤트 알림 이메일 템플릿 {#page-event-notification-e-mail-template}

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
   <td><p>새 로케일을 지원하는 유일한 새 페이지 이벤트 알림 이메일 템플릿만 지원됩니다.</p> <p>페이지 이벤트 이메일 템플릿 해상도는 다음 순서로 발생합니다.</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>새로 만들거나 수정된 페이지 이벤트 알림 이메일 템플릿은 <code>/apps</code> 아래의 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치에서 새 위치 또는 수정된 페이지 이벤트 알림 이메일 템플릿을 새 위치(<code>/apps</code>)로 복사합니다.</li>
     <li>이전 위치에서 마이그레이션된 페이지 이벤트 알림 이메일 템플릿을 제거합니다.</li>
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
   <td>이전 위치 아래에 만들어진 스캐폴딩은 기존 스캐폴딩 프레임워크를 사용하며 새 위치로 마이그레이션할 수 없습니다. 새 위치에 정렬하려면 지원되는 Scaffolding 프레임워크를 사용하여 기존 Scaffolding을 다시 개발해야 합니다.</td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 반응형 격자 LESS {#responsive-grid-less}

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
   <td><p>사용자 정의 LESS 파일의 이전 위치에 대한 모든 참조는 새 위치에서 가져오기 위해 업데이트해야 합니다.</p>
    <ul>
     <li>이전 위치에서 grid_base.less를 참조하는 모든 참조 사용자 지정 LESS 파일을 업데이트하여 새 위치를 참조합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>기존 파일이 아닌 <code>grid_base.less</code> 파일을 참조하면 페이지 및 템플릿 편집기의 레이아웃 모드가 작동하지 않고 페이지 레이아웃이 중단됩니다.</td>
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
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임 시 작성되지 않은 모든 디자인의 경우</p>
    <ol>
     <li>이전 위치의 디자인을 새 위치(<code>/apps</code>)로 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>이(가) 있는 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li><strong>AEM &gt; 사이트 &gt; 사용자 지정 사이트 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 디자인 필드</strong>를 통해 <code>cq:designPath</code> 속성에서 이전 위치에 대한 참조를 업데이트합니다.</li>
     <li>새 클라이언트 라이브러리 범주를 사용하도록 이전 위치를 참조하는 페이지를 업데이트합니다(페이지 구현 코드를 업데이트해야 함).</li>
     <li><code>/etc.clientlibs/</code> 프록시 서블릿을 통해 클라이언트 라이브러리 제공을 허용하도록 AEM Dispatcher 규칙을 업데이트합니다.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 디자인의 경우</p>
    <ul>
     <li>작성 가능한 디자인을 <code>/etc</code> 밖으로 이동하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>권장 방법은 디자인 대신 구조 컨텐츠 및 정책을 사용하는 편집 가능한 템플릿을 사용하여 AEM Sites 및 페이지를 만드는 것입니다.</td>
  </tr>
 </tbody>
</table>

### Adobe 검색 및 홍보 통합 클라이언트 라이브러리 {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>이러한 클라이언트 라이브러리를 사용자 정의할 때 사용하는 모든 사용자 정의 사용은 경로가 아니라 범주별로 클라이언트 라이브러리를 참조해야 합니다.</p>
    <ol>
     <li>이전 위치의 경로별로 클라이언트 라이브러리에 대한 모든 참조는 프레임워크</a>을 참조하는 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM 클라이언트 라이브러리를 사용하도록 업데이트해야 합니다.</a></li>
     <li>AEM Client Library referencing framework를 사용할 수 없는 경우 클라이언트 라이브러리의 절대 경로를 AEM Client Library Proxy 서블릿을 통해 참조할 수 있습니다.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>이러한 클라이언트 라이브러리의 편집은 지원되지 않습니다.</p> <p>클라이언트 라이브러리 범주를 얻으려면 CRXDELite를 통해 각 cq:ClientLibraryFolder 노드를 방문하여 categories 속성을 검사합니다.</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

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
   <td><p>이러한 클라이언트 라이브러리를 사용자 정의할 때 사용하는 모든 사용자 정의 사용은 경로가 아니라 범주별로 클라이언트 라이브러리를 참조해야 합니다.</p>
    <ol>
     <li>이전 위치의 경로별로 클라이언트 라이브러리에 대한 모든 참조는 프레임워크</a>을 참조하는 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM 클라이언트 라이브러리를 사용하도록 업데이트해야 합니다.</a></li>
     <li>AEM Client Library referencing framework를 사용할 수 없는 경우 클라이언트 라이브러리의 절대 경로를 AEM Client Library Proxy 서블릿을 통해 참조할 수 있습니다.</li>
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
   <td><p>이러한 클라이언트 라이브러리의 편집은 지원되지 않습니다.</p> <p>클라이언트 라이브러리 범주를 얻으려면 CRXDELite를 통해 각 cq:ClientLibraryFolder 노드를 방문하여 categories 속성을 검사합니다.</p>
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
   <td><p>이러한 클라이언트 라이브러리를 사용자 정의할 때 사용하는 모든 사용자 정의 사용은 경로가 아니라 범주별로 클라이언트 라이브러리를 참조해야 합니다.</p>
    <ol>
     <li>이전 위치의 경로별로 클라이언트 라이브러리에 대한 모든 참조는 프레임워크</a>을 참조하는 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM 클라이언트 라이브러리를 사용하도록 업데이트해야 합니다.</a></li>
     <li>프레임워크 참조 AEM 클라이언트 라이브러리를 사용할 수 없는 경우 클라이언트 라이브러리의 절대 경로를 AEM Client Library Proxy 서블릿을 통해 참조할 수 있습니다.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><p>이러한 클라이언트 라이브러리의 편집은 지원되지 않습니다.</p> <p>클라이언트 라이브러리 범주를 가져오려면 CRXDELite를 통해 각 <code>cq:ClientLIbraryFolder</code> 노드를 방문하여 categories 속성을 검사합니다.</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

