---
title: AEM 6.5의 Assets 저장소 재구성
description: Assets용 Adobe Experience Manager(AEM) 6.5에서 새 저장소 구조로 마이그레이션하는 데 필요한 변경 작업을 수행하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 2%

---

# AEM 6.5의 Assets 저장소 재구성 {#assets-repository-restructuring-in-aem}

상위에 설명된 대로 [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md) 페이지 AEM(Adobe Experience Manager) 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Assets 솔루션에 영향을 주는 저장소 변경 사항과 관련된 작업을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업이 필요하지만, 다른 변경 사항은 향후 업그레이드 전까지 연기될 수 있습니다.

**6.5 업그레이드 포함**

* [기타](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**향후 업그레이드 전**

* [에셋/컬렉션 이벤트 E-메일 알림 템플릿](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [클래식 자산 공유 디자인](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [자산 전자 메일 알림 템플릿 다운로드](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [DRM 라이센스 예](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [링크 공유 전자 메일 알림 템플릿](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign 워크플로 스크립트](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [비디오 코드 변환 구성](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [기타](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 6.5 업그레이드 포함 {#with-upgrade}

### 기타 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>사용자 지정 코드가 이 위치에 의존하는 경우(즉, 코드가 이 경로를 명시적으로 의존하는 경우), 업그레이드하기 전에 새 위치를 사용하도록 코드를 업데이트해야 합니다. 이상적으로 Java™ API는 JCR의 특정 경로에 대한 종속성을 줄이는 데 사용할 수 있을 때 사용됩니다.</p> <p>클라이언트가 다운로드할 zip 파일을 보관할 임시 위치입니다. 클라이언트에서 에셋 다운로드를 요청하므로 업데이트할 필요가 없습니다. 새 위치에 파일이 생성됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## 향후 업그레이드 전 {#prior-to-upgrade}

### 에셋/컬렉션 이벤트 E-메일 알림 템플릿 {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>고객이 이메일 템플릿을 수정한 경우 다음 작업을 수행하여 새 저장소 구조에 맞게 조정합니다.</p>
    <ol>
     <li>다음 <code>/libs/settings/dam/notification</code> 전자 메일 템플릿은에서 복사해야 합니다. <strong><code>/etc/notification/email/default</code></strong> 끝 <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>대상이 다음 위치에 있으므로<strong> <code>/apps</code></strong>, 이 변경 사항은 SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더 제거: <strong><code>/etc/dam/notification/email/default</code></strong> 그 안에 있는 전자 메일 템플릿이 이동되었습니다.<br />
      <ol>
       <li>다음 기간 동안 전자 메일 템플릿이 업데이트되지 않은 경우<strong> <code>/etc/notification/email/default</code></strong>원래 전자 메일 템플릿이 아래에 있으므로 폴더를 제거할 수 있습니다 <strong><code>/libs/settings/notification/email/default</code></strong> AEM 4 설치의 일부.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 클래식 자산 공유 디자인 {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>SCM에서 관리되고 디자인 대화 상자를 통해 런타임에 작성되지 않는 디자인의 경우 다음 작업을 수행하여 최신 모델에 맞춥니다.</p>
    <ol>
     <li>이전 위치의 디자인을 아래의 새 위치로 복사합니다. <code>/apps</code>.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a> 포함 <code>allowProxy = true</code>.</li>
     <li>의 이전 위치에 대한 참조 업데이트 <code>cq:designPath</code> 의 방식으로 된 속성 <strong>AEM &gt; DAM 관리 &gt; 자산 공유 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 디자인 필드</strong>.</li>
     <li>새 클라이언트 라이브러리 범주를 사용하려면 이전 위치를 참조하는 모든 페이지를 업데이트합니다. 이를 위해서는 페이지 구현 코드를 업데이트해야 합니다.</li>
     <li>를 통해 클라이언트 라이브러리 제공을 허용할 수 있도록 Dispatcher 규칙을 업데이트합니다. <code>/etc.clientlibs/</code> 프록시 서블릿.</li>
    </ol> <p>SCM에서 관리되지 않는 디자인 및 디자인 대화 상자를 통해 런타임 수정을 수행하는 디자인의 경우 작성 가능한 디자인을 외부로 이동하지 마십시오 <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 자산 전자 메일 알림 템플릿 다운로드 {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>전자 메일 템플릿(<strong>downloadasset</strong> 또는 <strong>transitientworkflow 완료됨</strong>)을 수정한 후 아래 절차를 따라 새 구조에 맞춥니다.</p>
    <ol>
     <li>업데이트된 전자 메일 템플릿은에서 복사해야 합니다. <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> 끝 <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>대상이 다음 위치에 있으므로<strong> <code>/apps</code></strong>, 이 변경 사항은 SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더 제거: <code>/etc/dam/workflow/notification/email/downloadasset </code>그 안에 있는 전자 메일 템플릿이 이동되었습니다.<br />
      <ol>
       <li>다음 기간 동안 전자 메일 템플릿이 업데이트되지 않은 경우<strong> <code>/etc</code></strong>원래 전자 메일 템플릿이 아래에 있으므로 폴더를 제거할 수 있습니다 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> AEM 6.4 설치의 일부로 사용됩니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>While <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 는 조회 시 기술적으로 지원됩니다(일반적인 Sling CAConfig 조회를 통해 /apps보다 우선하지만 다음 이후 <code>/etc</code>) 템플릿을 배치할 수 있습니다 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. 그러나 이메일 템플릿을 쉽게 편집할 수 있는 런타임 UI가 없으므로 권장되지 않습니다.</td>
  </tr>
 </tbody>
</table>

### DRM 라이센스 예 {#example-drm-licenses}

| **이전 위치** | `/etc/dam/drm/licenses/` |
|---|---|
| **새 위치** | `/libs/settings/dam/drm` |
| **구조 조정 지침** | N/A |
| **메모** | N/A |

### 링크 공유 전자 메일 알림 템플릿 {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>고객이 이메일 템플릿을 수정한 경우 새 저장소 구조에 맞춰 다음과 같이 하십시오.</p>
    <ol>
     <li>업데이트된 전자 메일 템플릿은에서 복사해야 합니다. <strong><code>/etc/dam/adhocassetshare</code></strong> 끝 <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>대상이 다음 위치에 있으므로<strong><code>/apps</code></strong>, 이 변경 사항은 SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더 제거: <strong><code>/etc/dam/adhocassetshare</code></strong> 그 안에 있는 전자 메일 템플릿이 이동되었습니다.<br />
      <ol>
       <li>다음 기간 동안 전자 메일 템플릿이 업데이트되지 않은 경우<strong> <code>/etc</code></strong>원래 전자 메일 템플릿이 아래에 있으므로 폴더를 제거할 수 있습니다 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> AEM 6.4 설치의 일부로 사용됩니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>While <code>/conf/global/settings/dam/adhocassetshare</code> 은(는) 조회 시 기술적으로 지원됩니다(이전에는 이 기능이 우선함). <code>/apps</code> 일반적인 Sling CAConfig 조회의 방식으로, 하지만 <code>/etc</code>), 템플릿을에 배치할 수 있습니다 <code>/conf/global/settings/dam/adhocassetshare</code>. 그러나 이메일 템플릿을 쉽게 편집할 수 있는 런타임 UI가 없으므로 권장되지 않습니다</td>
  </tr>
 </tbody>
</table>

### InDesign 워크플로 스크립트 {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 저장소 구조에 맞추려면 다음을 수행합니다.</p>
    <ol>
     <li>에서 모든 사용자 지정 또는 수정된 스크립트 복사 <strong><code>/etc/dam/indesign/scripts</code></strong> 끝 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>AEM에서 제공하는 수정되지 않은 스크립트로 새 스크립트나 수정된 스크립트만 복사할 수 있습니다. <strong><code>/libs/settings</code></strong> AEM 6.5에서</li>
      </ol> </li>
     <li>미디어 추출 프로세스 WF 단계 및 를 사용하는 모든 워크플로우 모델을 찾습니다.
      <ol>
       <li>워크플로 단계의 각 인스턴스에 대해 아래의 적절한 스크립트를 명시적으로 가리키도록 구성에서 경로를 업데이트합니다<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 또는 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 적절합니다.</li>
      </ol> </li>
     <li>제거<strong> <code>/etc/dam/indesign/scripts</code></strong> 전적으로.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>사용자 지정된 스크립트는에 저장하는 것이 좋습니다. <code>/apps</code>가 코드가 저장되는 위치이므로 이 위치에 코드를 저장해야 합니다.</td>
  </tr>
 </tbody>
</table>

### 비디오 코드 변환 구성 {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>프로젝트 수준 사용자 지정은 잘라내어 동등한 수준 아래에 붙여넣어야 합니다. <code>/apps</code> 또는 <code>/conf</code> 해당되는 경우 경로.</p> <p>AEM 6.4 저장소 구조를 맞추려면 다음을 수행합니다.</p>
    <ol>
     <li>에서 수정된 비디오 구성 복사 <code>/etc/dam/video</code> 끝 <code>/apps/settings/dam/video</code></li>
     <li>제거 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 뷰어 사전 설정 구성 {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>기본 뷰어 사전 설정의 경우 새 위치에서만 사용할 수 있습니다.</p> <p>사용자 지정 뷰어 사전 설정의 경우:</p>
    <ul>
     <li>다음에서 노드를 이동할 수 있도록 마이그레이션 스크립트 실행 <code>/etc</code> 끝 <code>/conf</code>. 스크립트는에 있습니다. <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>또는 구성을 편집할 수 있으며 새 위치에 자동 저장됩니다.</li>
    </ul> <p>을 가리키도록 copyURL/embed 코드를 조정하지 않아도 됩니다. <code>/conf</code>. 에 대한 기존 요청 <code>/etc</code> 의 올바른 콘텐츠로 리디렉션됩니다. <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 기타 {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>아래의 새 리소스를 가리키도록 모든 참조 조정 <code>/libs</code> 사용 <code>/etc.clientlibs/</code> 프록시 접두사를 허용합니다.</p> <p>마지막으로 마이그레이션된 clientlib에 대한 폴더를에서 제거하여 정리합니다. <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>
