---
title: AEM 6.5의 Assets 저장소 구조 변경
seo-title: AEM 6.5의 Assets 저장소 구조 변경
description: Assets용 AEM 6.5의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 작업을 수행하는 방법을 알아봅니다.
seo-description: Assets용 AEM 6.5의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 작업을 수행하는 방법을 알아봅니다.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: 업그레이드
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 2%

---

# AEM 6.5에서 자산 저장소 구조 변경 {#assets-repository-restructuring-in-aem}

AEM 6.5에서 상위 [저장소 구조 변경 페이지에 설명된 대로 AEM 6.5로 업그레이드하는 고객은 이 페이지에서 AEM Assets 솔루션에 영향을 주는 저장소 변경 사항과 관련된 작업 작업을 평가해야 합니다. ](/help/sites-deploying/repository-restructuring.md) 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업 노력이 필요한 반면, 다른 변경 사항은 향후 업그레이드될 때까지 지연될 수 있습니다.

**6.5 업그레이드**

* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**향후 업그레이드 전**

* [자산/수집 이벤트 이메일 알림 템플릿](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [클래식 자산 공유 디자인](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [자산 이메일 알림 템플릿 다운로드](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [DRM 라이선스 예](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [링크 공유 전자 메일 알림 템플릿](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign 워크플로우 스크립트](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [비디오 코드 변환 구성](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 6.5 업그레이드( {#with-upgrade} 포함)

### Misc {#misc}

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
   <td><p>사용자 지정 코드가 이 위치(예: 코드가 이 경로에 명시적으로 사용됨) 업그레이드하기 전에 새 위치를 사용하도록 코드를 업데이트해야 합니다.사용 가능한 경우 JCR의 특정 경로에 대한 종속성을 줄이는 데 이상적으로 Java API를 사용합니다.</p> <p>클라이언트가 다운로드할 zip 파일을 저장할 임시 위치입니다. 클라이언트가 자산을 다운로드하도록 요청할 때 업데이트할 필요가 없습니다. 새 위치에 파일이 생성됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## 향후 업그레이드 전 {#prior-to-upgrade}

### 자산/컬렉션 이벤트 이메일 알림 템플릿 {#asset-collection-event-e-mail-notification-template}

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
   <td><p>고객이 전자 메일 템플릿을 수정한 경우 새 저장소 구조에 맞게 다음 작업을 수행합니다.</p>
    <ol>
     <li><code>/libs/settings/dam/notification</code> 전자 메일 템플릿은 <strong><code>/etc/notification/email/default</code></strong>에서 <strong><code>/apps/settings/notification/email/default</code></strong>(으)로 복사해야 합니다.
      <ol>
       <li>대상이<strong> <code>/apps</code></strong>이므로 이 변경 사항은 SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더를 제거합니다.<strong><code>/etc/dam/notification/email/default</code></strong> 내에 있는 전자 메일 템플릿이 이동된 후.<br />
      <ol>
       <li><strong> <code>/etc/notification/email/default</code></strong> 아래의 전자 메일 템플릿에 대한 업데이트가 없는 경우 AEM 4 설치의 일부로 <strong><code>/libs/settings/notification/email/default</code></strong> 아래에 원래 전자 메일 템플릿이 있으므로 폴더를 제거할 수 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
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
   <td><p>디자인 대화 상자를 통해 런타임에 작성되지 않고 SCM에서 관리되는 모든 디자인에 대해 다음 작업을 수행하여 최신 모델에 맞춥니다.</p>
    <ol>
     <li>이전 위치에서 <code>/apps</code> 아래의 새 위치로 디자인을 복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 <code>allowProxy = true</code>를 사용하는 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">클라이언트 라이브러리</a>로 변환합니다.</li>
     <li><strong>AEM &gt; DAM 관리자 &gt; 자산 공유 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 디자인 필드</strong>를 통해 <code>cq:designPath</code> 속성에서 이전 위치에 대한 참조를 업데이트합니다.</li>
     <li>이전 위치를 참조하는 모든 페이지를 업데이트하여 새 클라이언트 라이브러리 카테고리를 사용합니다. 이렇게 하려면 페이지 구현 코드를 업데이트해야 합니다.</li>
     <li><code>/etc.clientlibs/</code> 프록시 서블릿을 통해 클라이언트 라이브러리 제공을 허용하도록 Dispatcher 규칙을 업데이트합니다.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 시 모든 디자인의 경우 권한 있는 디자인을 <code>/etc</code> 외부로 이동하지 마십시오.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 자산 이메일 알림 템플릿 다운로드 {#download-asset-e-mail-notification-template}

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
   <td><p>전자 메일 템플릿(<strong>다운로드 자산</strong> 또는 <strong>transendworkflowcompleted</strong>)이 수정된 경우 다음 절차에 따라 새 구조에 맞춥니다.</p>
    <ol>
     <li>업데이트된 전자 메일 템플릿은 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong>에서 <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>(으)로 복사해야 합니다.
      <ol>
       <li>대상이<strong> <code>/apps</code></strong>이므로 이 변경 사항은 SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더를 제거합니다.<code>/etc/dam/workflow/notification/email/downloadasset </code>내에 있는 전자 메일 템플릿이 이동된 후.<br />
      <ol>
       <li><strong> <code>/etc</code></strong> 아래의 이메일 템플릿에 대한 업데이트가 없는 경우 AEM 6.4 설치의 일부로 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 아래에 원래 이메일 템플릿이 있으므로 폴더를 제거할 수 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>은(는) 기술적으로 조회 지원을 위해 지원되지만(일반적인 Sling CAConfig 조회를 통해 /apps 전에 우선 적용되지만 <code>/etc</code> 이후에 템플릿을 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>에 배치할 수 있습니다.) 그러나 이메일 템플릿 편집을 용이하게 하기 위해 런타임 UI가 없으므로 이 방법은 권장되지 않습니다.</td>
  </tr>
 </tbody>
</table>

### DRM 라이센스 예 {#example-drm-licenses}

| **이전 위치** | `/etc/dam/drm/licenses/` |
|---|---|
| **새 위치** | `/libs/settings/dam/drm` |
| **구조 조정 지침** | 해당 없음 |
| **메모** | 해당 없음 |

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
   <td><p>고객이 전자 메일 템플릿을 수정한 경우 새 저장소 구조에 맞게 합니다.</p>
    <ol>
     <li>업데이트된 전자 메일 템플릿은 <strong><code>/etc/dam/adhocassetshare</code></strong>에서 <strong><code>/apps/settings/dam/adhocassetshare</code></strong>(으)로 복사해야 합니다.
      <ol>
       <li>대상이<strong> <code>/apps</code></strong>이므로 이 변경 사항은 SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더를 제거합니다.<strong><code>/etc/dam/adhocassetshare</code></strong> 내에 있는 전자 메일 템플릿이 이동된 후.<br />
      <ol>
       <li><strong> <code>/etc</code></strong> 아래의 이메일 템플릿에 대한 업데이트가 없는 경우 AEM 6.4 설치의 일부로 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 아래에 원래 이메일 템플릿이 있으므로 폴더를 제거할 수 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td><code>/conf/global/settings/dam/adhocassetshare</code>은(는) 기술적으로 조회 지원을 위해 지원되지만(일반적인 Sling CAConfig 조회를 통해 <code>/apps</code> 전에 우선하지만 <code>/etc</code> 이후에 템플릿을 <code>/conf/global/settings/dam/adhocassetshare</code>에 배치할 수 있습니다.) 그러나 이메일 템플릿 편집을 용이하게 하기 위해 런타임 UI가 없으므로 이 방법은 권장되지 않습니다</td>
  </tr>
 </tbody>
</table>

### InDesign 워크플로우 스크립트 {#indesign-workflow-scripts}

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
   <td><p>새 저장소 구조에 맞추기</p>
    <ol>
     <li><strong><code>/etc/dam/indesign/scripts</code></strong>에서 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />로 모든 사용자 지정 스크립트나 수정된 스크립트를 복사합니다.
      <ol>
       <li>새 스크립트 또는 수정된 스크립트만 AEM 6.5에서 <strong><code>/libs/settings</code></strong>을 통해 AEM에서 제공하는 수정되지 않은 스크립트로 복사할 수 있습니다</li>
      </ol> </li>
     <li>미디어 추출 프로세스 WF 단계를 사용하는 모든 워크플로우 모델을 찾아
      <ol>
       <li>워크플로우 단계의 각 인스턴스에 대해 <strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 또는 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 아래의 적절한 스크립트를 명시적으로 가리키도록 구성의 경로를 업데이트합니다.</li>
      </ol> </li>
     <li><strong> <code>/etc/dam/indesign/scripts</code></strong>을 완전히 제거합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>사용자 지정된 스크립트는 코드를 저장해야 하는 위치이므로 <code>/apps</code> 아래에 저장하는 것이 좋습니다.</td>
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
   <td><p>프로젝트 수준 사용자 지정은 해당하는 <code>/apps</code> 또는 <code>/conf</code> 경로 아래에서 잘라내어 붙여 넣어야 합니다.</p> <p>AEM 6.4 저장소 구조에 정렬하려면</p>
    <ol>
     <li>수정된 비디오 구성을 <code>/etc/dam/video</code>에서 (으)로 복사합니다. <code>/apps/settings/dam/video</code></li>
     <li>제거 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
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
   <td><p>곧바로 사용할 수 있는 뷰어 사전 설정 의 경우 새 위치에서만 사용할 수 있습니다.</p> <p>사용자 지정 뷰어 사전 설정의 경우:</p>
    <ul>
     <li>노드를 <code>/etc</code>에서 <code>/conf</code>(으)로 이동하려면 마이그레이션 스크립트를 실행해야 합니다. 스크립트는 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em>에 있습니다.</li>
     <li>또는 구성을 편집할 수 있으며 새 위치에 자동으로 저장됩니다.</li>
    </ul> <p><code>/conf</code>을 가리키도록 copyURL/embed 코드를 조정할 필요가 없습니다. <code>/etc</code>에 대한 기존 요청은 <code>/conf</code>의 올바른 컨텐츠로 다시 라우팅됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

### Misc {#misc2}

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
   <td><p><code>/etc.clientlibs/</code> 프록시 허용 접두사를 사용하여 <code>/libs</code> 아래의 새 리소스를 가리키도록 참조를 조정합니다.</p> <p>마지막으로 마이그레이션된 clientlibs의 폴더를 제거하여 정리합니다. <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>
