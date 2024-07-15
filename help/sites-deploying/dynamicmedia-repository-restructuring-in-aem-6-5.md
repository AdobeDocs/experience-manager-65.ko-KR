---
title: Adobe Experience Manager 6.5에서 Dynamic Media 저장소 재구성
description: Dynamic Media용 Experience Manager 6.5에서 새 저장소 구조로 마이그레이션하는 데 필요한 변경 작업을 수행하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Adobe Experience Manager 6.5에서 Dynamic Media 저장소 재구성 {#dynamic-media-repository-restructuring-in-aem}

Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md)의 상위 [저장소 재구성 페이지에 설명된 대로 Experience Manager 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 Dynamic Media에 영향을 주는 저장소 변경 사항과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 Experience Manager 6.5 업그레이드 프로세스 중에 작업이 필요하지만, 다른 변경 사항은 향후 업그레이드 전까지 연기될 수 있습니다.

**향후 업그레이드 전**

* [사용자 지정 응용 비디오 인코딩 구성](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media(DMS7) 클라우드 구성](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media(DM 하이브리드) Cloud Service 구성](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTube Cloud Service 구성](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [기타](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 향후 업그레이드 전 {#prior-to-upgrade}

### 사용자 지정 응용 비디오 인코딩 구성  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>다음 마이그레이션 스크립트를 실행하여 새 위치로 마이그레이션할 수 있습니다.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>또는 Experience Manager UI에서 구성을 편집할 수 있으며 변경 사항이 새 위치에 저장됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media(DMS7) 클라우드 구성 {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>고객은 <br /> 위치에서 마이그레이션 스크립트를 실행할 수 있습니다. </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Dynamic Media OSGi 번들을 다시 시작합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 사항 없음</td>
  </tr>
 </tbody>
</table>

### Dynamic Media(DM 하이브리드) Cloud Service 구성 {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>아래 마이그레이션 스크립트를 실행하여 최신 모델에 맞출 수 있습니다.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTube Cloud Service 구성  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>1. YouTube의 모든 비디오 게시 취소<br /> 2. 이전 위치에서 모든 채널을 복사하는 것을 포함하여 새 TouchUI(<code>/conf</code>부터)를 사용하여 YouTube 구성을 만듭니다<br /> 3. Publish 모든 비디오가 YouTube으로 돌아갑니다.</p> <p>이 워크플로우로 인해 새 YouTube URL이 생성됩니다. TouchUI YouTube 구성을 만들기 전에 게시를 취소하지 않는 경우 기회가 주어지면 다시 만든 채널이 다시 게시되므로 속성 아래에 여러 YouTube URL이 나열됩니다. 이 기능은 속성에 나열된 URL이 쓸모없다는 것을 의미합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 기타 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>고객은 아래 마이그레이션 스크립트를 실행할 수 있습니다.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>또는 Experience Manager UI에서 구성을 편집할 수 있으며 변경 사항이 새 위치에 저장됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 사항 없음</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>고객은 아래 마이그레이션 스크립트를 실행할 수 있습니다.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 사항 없음</td>
  </tr>
 </tbody>
</table>
