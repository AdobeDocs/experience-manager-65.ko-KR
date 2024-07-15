---
title: AEM 6.5에서 Assets 저장소 재구성
description: Assets용 Adobe Experience Manager(AEM) 6.5에서 새 저장소 구조로 마이그레이션하는 데 필요한 변경 작업을 수행하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# AEM 6.5에서 Assets 저장소 재구성 {#assets-repository-restructuring-in-aem}

AEM 6.5](/help/sites-deploying/repository-restructuring.md)의 상위 [저장소 재구성 페이지에 설명된 대로 Adobe Experience Manager(AEM) 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Assets 솔루션에 영향을 주는 저장소 변경 사항과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업이 필요하지만, 다른 변경 사항은 향후 업그레이드 전까지 연기될 수 있습니다.

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
   <td>해당 사항 없음</td>
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
     <li><code>/libs/settings/dam/notification</code> 전자 메일 템플릿을 <strong><code>/etc/notification/email/default</code></strong>에서 <strong><code>/apps/settings/notification/email/default</code></strong>(으)로 복사해야 합니다.
      <ol>
       <li>대상이 <strong> <code>/apps</code></strong>에 있으므로 이 변경 내용은 SCM에서 유지되어야 합니다.</li>
      </ol> </li>
     <li>폴더 내의 전자 메일 템플릿을 이동한 후 <strong><code>/etc/dam/notification/email/default</code></strong> 폴더를 제거합니다.<br />
      <ol>
       <li><strong> <code>/etc/notification/email/default</code></strong>의 전자 메일 템플릿이 업데이트되지 않은 경우 원본 전자 메일 템플릿이 AEM 4 설치의 일부로 <strong><code>/libs/settings/notification/email/default</code></strong>에 있으므로 폴더를 제거할 수 있습니다.</li>
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
     <li>이전 위치의 디자인을 <code>/apps</code> 아래의 새 위치로 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>이(가) 있는 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>(으)로 변환합니다.</li>
     <li><strong>AEM &gt; DAM 관리 &gt; 자산 공유 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 디자인 필드</strong>를 통해 <code>cq:designPath</code> 속성의 이전 위치에 대한 참조를 업데이트합니다.</li>
     <li>새 클라이언트 라이브러리 범주를 사용하려면 이전 위치를 참조하는 모든 페이지를 업데이트합니다. 이를 위해서는 페이지 구현 코드를 업데이트해야 합니다.</li>
     <li><code>/etc.clientlibs/</code> 프록시 서블릿을 통해 클라이언트 라이브러리를 제공할 수 있도록 Dispatcher 규칙을 업데이트합니다.</li>
    </ol> <p>SCM에서 관리되지 않는 디자인 및 디자인 대화 상자를 통해 런타임으로 수정된 디자인의 경우 작성 가능한 디자인을 <code>/etc</code> 외부로 이동하지 마십시오.</p> </td>
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
   <td><p>전자 메일 템플릿(<strong>downloadasset</strong> 또는 <strong>transitientworkflowcompleted</strong>)이 수정된 경우 아래 절차를 따라 새 구조에 맞춥니다.</p>
    <ol>
     <li>업데이트된 전자 메일 템플릿을 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong>에서 <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>(으)로 복사해야 합니다.
      <ol>
       <li>대상이 <strong> <code>/apps</code></strong>에 있으므로 이 변경 내용은 SCM에서 유지되어야 합니다.</li>
      </ol> </li>
     <li><code>/etc/dam/workflow/notification/email/downloadasset </code> 폴더 내의 전자 메일 서식 파일을 이동한 후 폴더를 제거합니다.<br />
      <ol>
       <li><strong> <code>/etc</code></strong>의 전자 메일 템플릿이 업데이트되지 않은 경우 원본 전자 메일 템플릿이 AEM 6.4 설치의 일부로 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong>에 있으므로 폴더를 제거할 수 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>은(는) 기술적으로 조회 기능이 지원되지만, 일반적인 Sling CAConfig 조회를 통해 /apps보다 우선하지만 <code>/etc</code> 이후에는 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>에 템플릿을 배치할 수 있습니다. 그러나 이메일 템플릿을 쉽게 편집할 수 있는 런타임 UI가 없으므로 권장되지 않습니다.</td>
  </tr>
 </tbody>
</table>

### DRM 라이센스 예 {#example-drm-licenses}

| **이전 위치** | `/etc/dam/drm/licenses/` |
|---|---|
| **새 위치** | `/libs/settings/dam/drm` |
| **구조 조정 지침** | 해당 사항 없음 |
| **메모** | 해당 사항 없음 |

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
     <li>업데이트된 전자 메일 템플릿을 <strong><code>/etc/dam/adhocassetshare</code></strong>에서 <strong><code>/apps/settings/dam/adhocassetshare</code></strong>(으)로 복사해야 합니다.
      <ol>
       <li>대상이 <strong><code>/apps</code></strong>에 있으므로 이 변경 내용은 SCM에서 유지되어야 합니다.</li>
      </ol> </li>
     <li>폴더 내의 전자 메일 템플릿을 이동한 후 <strong><code>/etc/dam/adhocassetshare</code></strong> 폴더를 제거합니다.<br />
      <ol>
       <li><strong> <code>/etc</code></strong>의 전자 메일 템플릿이 업데이트되지 않은 경우 원본 전자 메일 템플릿이 AEM 6.4 설치의 일부로 <strong><code>/libs/settings/dam/adhocassetshare</code></strong>에 있으므로 폴더를 제거할 수 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><code>/conf/global/settings/dam/adhocassetshare</code>은(는) 기술적으로 조회 기능이 지원되지만, 일반적인 Sling CAConfig 조회를 통해 <code>/apps</code>보다 우선하지만 <code>/etc</code> 이후에는 템플릿을 <code>/conf/global/settings/dam/adhocassetshare</code>에 배치할 수 있습니다. 그러나 이메일 템플릿을 쉽게 편집할 수 있는 런타임 UI가 없으므로 권장되지 않습니다</td>
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
     <li><strong><code>/etc/dam/indesign/scripts</code></strong>에서 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />(으)로 모든 사용자 지정 또는 수정된 스크립트 복사
      <ol>
       <li>AEM 6.5의 <strong><code>/libs/settings</code></strong>에서는 AEM에서 제공하는 수정되지 않은 스크립트로 새 스크립트나 수정된 스크립트만 복사할 수 있습니다.</li>
      </ol> </li>
     <li>미디어 추출 프로세스 WF 단계 및 를 사용하는 모든 워크플로우 모델을 찾습니다.
      <ol>
       <li>워크플로 단계의 각 인스턴스에 대해 <strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 또는 <strong><code>/libs/settings/dam/indesign/scripts</code></strong>에서 적절한 스크립트를 명시적으로 가리키도록 구성의 경로를 업데이트합니다.</li>
      </ol> </li>
     <li><strong> <code>/etc/dam/indesign/scripts</code></strong>을(를) 완전히 제거하십시오.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>사용자 지정 스크립트는 <code>/apps</code>에 저장하는 것이 좋습니다. 코드가 저장될 위치이기 때문입니다.</td>
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
   <td><p>프로젝트 수준 사용자 지정은 해당하는 <code>/apps</code> 또는 <code>/conf</code> 경로에서 잘라내고 붙여 넣어야 합니다.</p> <p>AEM 6.4 저장소 구조를 맞추려면 다음을 수행합니다.</p>
    <ol>
     <li><code>/etc/dam/video</code>에서 수정된 비디오 구성 복사 <code>/apps/settings/dam/video</code></li>
     <li>제거 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 사항 없음</td>
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
     <li><code>/etc</code>에서 <code>/conf</code>(으)로 노드를 이동할 수 있도록 마이그레이션 스크립트를 실행합니다. 스크립트는 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em>에 있습니다.</li>
     <li>또는 구성을 편집할 수 있으며 새 위치에 자동 저장됩니다.</li>
    </ul> <p><code>/conf</code>을(를) 가리키도록 copyURL/embed 코드를 조정할 필요가 없습니다. <code>/etc</code>에 대한 기존 요청이 <code>/conf</code>의 올바른 콘텐츠로 다시 라우팅됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 사항 없음</td>
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
   <td><p><code>/etc.clientlibs/</code> 허용 프록시 접두사를 사용하여 <code>/libs</code>의 새 리소스를 가리키도록 참조를 조정하십시오.</p> <p>마지막으로 마이그레이션된 clientlib에 대한 폴더를에서 제거하여 정리합니다. <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>
