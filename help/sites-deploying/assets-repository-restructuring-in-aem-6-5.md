---
title: AEM 6.5의 자산 저장소 재구성
seo-title: AEM 6.5의 자산 저장소 재구성
description: AEM 6.5 for Assets의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
seo-description: AEM 6.5 for Assets의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5의 자산 저장소 재구성 {#assets-repository-restructuring-in-aem}

AEM 6.5 [의 상위 리포지토리 재조정](/help/sites-deploying/repository-restructuring.md) 페이지에 설명된 대로, AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Assets 솔루션에 영향을 주는 리포지토리 변경과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 동안 작업해야 하는 반면, 다른 변경 사항은 향후 업그레이드될 때까지 연기될 수 있습니다.

**6.5 업그레이드 포함**

* [기타](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**업그레이드 전**

* [자산/컬렉션 이벤트 이메일 알림 템플릿](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [클래식 에셋 공유 디자인](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [자산 전자 메일 알림 템플릿 다운로드](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [DRM 라이선스 예](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [링크 공유 전자 메일 알림 템플릿](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign 워크플로우 스크립트](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [비디오 트랜스코딩 구성](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
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
   <td><p>사용자 지정 코드가 이 위치(예: 코드가 이 경로에 명시적으로 의존함), 업그레이드하기 전에 새 위치를 사용하도록 코드를 업데이트해야 합니다.Java API는 JCR의 특정 경로에 대한 종속성을 줄이기 위해 사용할 수 있는 경우에 사용하는 것이 좋습니다.</p> <p>클라이언트가 다운로드할 zip 파일을 저장할 임시 위치입니다. 클라이언트가 에셋 다운로드를 요청할 때부터 업데이트할 필요가 없습니다. 새 위치에 파일이 생성됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## 업그레이드 전 {#prior-to-upgrade}

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
   <td><p>고객이 이메일 템플릿을 수정한 경우 새 저장소 구조에 맞게 다음 작업을 수행합니다.</p>
    <ol>
     <li>이메일 <code>/libs/settings/dam/notification</code> <strong><code>/etc/notification/email/default</code></strong> 템플릿을 <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>대상이<strong> 이 변경 내용에 있으므로 <code>/apps</code></strong> SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더 제거:이메일 템플릿이 이동한 <strong><code>/etc/dam/notification/email/default</code></strong> 후<br />
      <ol>
       <li>아래의<strong> 전자 메일 템플릿에 대한 업데이트가 없는 <code>/etc/notification/email/default</code></strong>경우 AEM 4 설치의 일부로 원래 전자 메일 템플릿이 존재하므로 폴더를 제거할 수 <strong><code>/libs/settings/notification/email/default</code></strong> 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 클래식 에셋 공유 디자인 {#classic-asset-share-designs}

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
   <td><p>디자인 대화 상자를 통해 런타임에 작성되지 않고 SCM에서 관리되는 모든 디자인의 경우 다음 작업을 수행하여 최신 모델에 정렬합니다.</p>
    <ol>
     <li>이전 위치에서 새 위치로 디자인을 <code>/apps</code>복사합니다.</li>
     <li>디자인의 모든 CSS, JavaScript 및 정적 리소스를 클라이언트 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">라이브러리로</a> 변환할 수 <code>allowProxy = true</code>있습니다.</li>
     <li>AEM &gt; DAM 관리 &gt; 자산 공유 <code>cq:designPath</code> 페이지 &gt; 페이지 속성 &gt; 고급 탭 &gt; 디자인 필드를 통해 <strong>속성의 이전 위치에 대한 참조를 업데이트합니다</strong>.</li>
     <li>이전 위치를 참조하는 페이지를 업데이트하여 새 클라이언트 라이브러리 카테고리를 사용합니다. 이를 위해서는 페이지 구현 코드를 업데이트해야 합니다.</li>
     <li>Dispatcher 규칙을 업데이트하여 <code>/etc.clientlibs/</code> 프록시 서블릿을 통해 클라이언트 라이브러리 제공을 허용합니다.</li>
    </ol> <p>SCM에서 관리되지 않고 디자인 대화 상자를 통해 수정된 런타임 시 디자인의 경우 작성 가능한 디자인을 외부로 이동하지 마십시오 <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
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
   <td><p>이메일 템플릿(<strong>다운로드 자산</strong> 또는 <strong>전환 워크플로우 완료</strong>)이 수정된 경우 아래 절차에 따라 새 구조에 맞게 정렬합니다.</p>
    <ol>
     <li>업데이트된 전자 메일 템플릿을 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong><strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>대상이<strong> 이 변경 내용에 있으므로 <code>/apps</code></strong> SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더 제거:이메일 템플릿이 <code>/etc/dam/workflow/notification/email/downloadasset </code>이동한 후<br />
      <ol>
       <li>아래의<strong> 전자 메일 템플릿에 대한 업데이트가 없는 <code>/etc</code></strong>경우 AEM 6.4 설치의 일부로 원래 전자 메일 템플릿이 존재하므로 폴더를 제거할 수 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>기술적으로 조회 기능이 지원되지만(일반적인 Sling CAConfig 조회를 통해 /apps 전에 우선 순위가 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 적용되지만 이후 <code>/etc</code>) 템플릿은 에 배치할 수 있습니다 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. 그러나 이메일 템플릿 편집을 용이하게 하는 런타임 UI가 없으므로 이는 권장되지 않습니다.</td>
  </tr>
 </tbody>
</table>

### DRM 라이선스 예 {#example-drm-licenses}

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
   <td><p>고객이 이메일 템플릿을 수정한 경우 새 저장소 구조에 맞게 정렬합니다.</p>
    <ol>
     <li>업데이트된 전자 메일 템플릿을 <strong><code>/etc/dam/adhocassetshare</code></strong><strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>대상이<strong> 이 변경 내용에 있으므로 <code>/apps</code></strong> SCM에서 지속되어야 합니다.</li>
      </ol> </li>
     <li>폴더 제거:이메일 템플릿이 이동한 <strong><code>/etc/dam/adhocassetshare</code></strong> 후<br />
      <ol>
       <li>아래의<strong> 전자 메일 템플릿에 대한 업데이트가 없는 <code>/etc</code></strong>경우, AEM 6.4 설치의 일부로 원래 전자 메일 템플릿이 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 존재하므로 폴더를 제거할 수 있습니다.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>기술적으로 조회 지원이 <code>/conf/global/settings/dam/adhocassetshare</code> 지원되지만(일반적인 Sling CAConfig 조회를 <code>/apps</code> 통한 우선 순위가 높지만 이후), 템플릿을 에 배치할 수 <code>/etc</code><code>/conf/global/settings/dam/adhocassetshare</code>있습니다. 그러나 이메일 템플릿 편집을 용이하게 하는 런타임 UI가 없으므로 이는 권장되지 않습니다</td>
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
   <td><p>새 저장소 구조에 정렬하려면</p>
    <ol>
     <li>에서 사용자 정의 스크립트 또는 수정된 스크립트 모두 <strong><code>/etc/dam/indesign/scripts</code></strong> 복사 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>AEM에서 제공한 수정되지 않은 스크립트로 새 스크립트 또는 수정된 스크립트만 AEM 6.5 <strong><code>/libs/settings</code></strong> 에서 사용할 수 있습니다.</li>
      </ol> </li>
     <li>미디어 추출 프로세스 WF 단계를 사용하는 모든 워크플로우 모델을 찾아
      <ol>
       <li>워크플로우 단계의 각 인스턴스에 대해, 구성에서 경로를 업데이트하여 적절한 아래의<strong> 또는 <code>/apps/settings/dam/indesign/scripts</code></strong> 적절한 스크립트를 명시적으로 지정합니다 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> .</li>
      </ol> </li>
     <li>완전히<strong> 제거할 <code>/etc/dam/indesign/scripts</code></strong> 수 있습니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>사용자 정의 스크립트는 코드를 저장해야 하는 위치이므로 <code>/apps</code>아래에서 저장하는 것이 좋습니다.</td>
  </tr>
 </tbody>
</table>

### 비디오 트랜스코딩 구성 {#video-transcoding-configurations}

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
   <td><p>프로젝트 수준 사용자 지정을 잘라내어 해당되는 <code>/apps</code> 경로 또는 <code>/conf</code> 경로에 붙여넣어야 합니다.</p> <p>AEM 6.4 리포지토리 구조에 정렬하려면 다음을 수행하십시오.</p>
    <ol>
     <li>수정된 비디오 구성을 에서 <code>/etc/dam/video</code> 로 복사 <code>/apps/settings/dam/video</code></li>
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
   <td><p>기본 뷰어 사전 설정의 경우 새 위치에서만 사용할 수 있습니다.</p> <p>사용자 정의 뷰어 사전 설정의 경우:</p>
    <ul>
     <li>노드를 (으)로 이동하려면 마이그레이션 스크립트를 실행해야 <code>/etc</code> 합니다 <code>/conf</code>. 스크립트는 https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json에 <em>있습니다</em></li>
     <li>또는 구성을 편집할 수 있으며 새 위치에 자동으로 저장됩니다.</li>
    </ul> <p>copyURL/embed 코드를 조정할 필요가 <code>/conf</code>없습니다. 기존 요청은 에서 올바른 컨텐츠로 다시 <code>/etc</code> 라우팅됩니다 <code>/conf</code>.</p> </td>
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
   <td><p>프록시 허용 접두사를 사용하여 새 리소스를 가리키도록 참조를 조정합니다 <code>/libs</code> <code>/etc.clientlibs/</code> .</p> <p>마지막으로 마이그레이션된 클라이언트의 폴더를 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

