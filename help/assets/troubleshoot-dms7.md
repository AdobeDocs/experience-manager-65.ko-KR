---
title: Dynamic Media 문제 해결 - Scene7 모드
description: Scene7 모드에서 실행 중일 때 Dynamic Media에서 설정, 구성 및 일반 문제를 해결하고 해결하는 방법에 대해 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Troubleshooting
mini-toc-levels: 3
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 0%

---

# Dynamic Media 문제 해결 - Scene7 모드{#troubleshooting-dynamic-media-scene-mode}

다음 문서에서는 **dynamicmedia_scene7** 실행 모드를 실행하는 Dynamic Media의 문제 해결에 대해 설명합니다.

## 설정 및 구성 {#setup-and-configuration}

다음을 수행하여 Dynamic Media이 제대로 설정되었는지 확인합니다.

* 시작 명령에 `-r dynamicmedia_scene7` 실행 모드 인수가 포함되어 있습니다.
* 모든 Adobe Experience Manager 6.4 CFP(누적 수정 팩)가 사용 가능한 모든 Dynamic Media 기능 팩의 *이전*&#x200B;에 처음 설치되었습니다.
* 선택적 기능 팩 18912이 설치되어 있습니다.

  이 선택적 기능 팩은 FTP 지원용 또는 Dynamic Media Classic에서 Dynamic Media으로 자산을 마이그레이션하는 경우에 사용됩니다.

* Cloud Service 사용자 인터페이스로 이동하여 프로비전된 계정이 **[!UICONTROL 사용 가능한 구성]**&#x200B;에 표시되는지 확인합니다.
* `Dynamic Media Asset Activation (scene7)` 복제 에이전트가 활성화되어 있는지 확인하십시오.

  이 복제 에이전트는 작성자의 에이전트에서 찾을 수 있습니다.

## 일반(모든 Assets) {#general-all-assets}

다음은 모든 에셋에 대한 몇 가지 일반적인 팁과 요령입니다.

### 에셋 동기화 상태 속성 {#asset-synchronization-status-properties}

CRXDE Lite에서 다음 에셋 속성을 검토하여 Experience Manager에서 Dynamic Media으로 에셋이 성공적으로 동기화되었는지 확인할 수 있습니다.

| **속성** | **예** | **설명** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | 노드가 Dynamic Media에 연결되어 있다는 일반 표시기. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** 또는 오류 텍스트 | Dynamic Media에 대한 에셋 업로드 상태입니다. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Dynamic Media의 원격 자산에 대한 URL을 생성하려면 채워야 합니다. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **성공** 또는 **실패:`<error text>`** | 에셋에 대한 세트(스핀 세트, 이미지 세트 등), 이미지 사전 설정, 뷰어 사전 설정, 이미지 맵 업데이트 또는 편집된 이미지의 동기화 상태입니다. |

### 동기화 로깅 {#synchronization-logging}

동기화 오류 및 문제가 `error.log`에 기록됩니다(Experience Manager 서버 디렉터리 `/crx-quickstart/logs/`). 충분한 로깅을 사용하여 대부분의 문제의 근본 원인을 확인할 수 있지만 Sling 콘솔([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))을 통해 `com.adobe.cq.dam.ips` 패키지의 DEBUG에 대한 로깅을 늘려 자세한 정보를 수집할 수 있습니다.

### 이동, 복사, 삭제 {#move-copy-delete}

이동, 복사 또는 삭제 작업을 수행하기 전에 다음을 수행합니다.

* 이미지 및 비디오의 경우 이동, 복사 또는 삭제 작업을 수행하기 전에 `<object_node>/jcr:content/metadata/dam:scene7ID` 값이 있는지 확인하십시오.
* 이미지 및 뷰어 사전 설정의 경우 이동, 복사 또는 삭제 작업을 수행하기 전에 `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` 값이 있는지 확인하십시오.
* 위의 메타데이터 값이 누락된 경우 이동, 복사 또는 삭제 작업 전에 에셋을 다시 업로드해야 합니다.

### 버전 제어 {#version-control}

기존 Dynamic Media 에셋(동일한 이름 및 위치)을 바꿀 때 두 에셋을 모두 유지하거나 버전을 대체/만들 수 있습니다.

* 둘 다 유지하면 게시된 에셋 URL에 대해 고유한 이름의 에셋이 만들어집니다. 예를 들어 `image.jpg`은(는) 원본 자산이고 `image1.jpg`은(는) 새로 업로드한 자산입니다.

* Dynamic Media - Scene7 모드 전달에서는 버전 만들기가 지원되지 않습니다. 새 버전은 게재의 기존 에셋을 대체합니다.

## 이미지 및 집합 {#images-and-sets}

이미지 및 세트에 문제가 있는 경우 다음 문제 해결 지침을 참조하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>문제</strong></td>
   <td><strong>디버깅하는 방법</strong></td>
   <td><strong>솔루션</strong></td>
  </tr>
  <tr>
   <td>자산 세부 사항 보기의 URL/포함 복사 단추에 액세스할 수 없음</td>
   <td>
    <ol>
     <li><p>CRX/DE로 이동:</p>
      <ul>
       <li>JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>의 사전 설정이 정의되어 있는지 확인합니다. 이 위치는 Experience Manager 6.x에서 6.4로 업그레이드하고 마이그레이션을 옵트아웃한 경우에 적용됩니다. 그렇지 않으면 위치는 <code>/conf/global/settings/dam/dm/presets/viewer</code>입니다.</li>
       <li>JCR의 에셋에 <code>dam:scene7FileStatus</code><strong> </strong>이(가) 있는지 확인하십시오.<code>PublishComplete</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>페이지 새로 고침/다른 페이지로 이동한 다음 돌아가기(사이드 레일 JSP를 다시 컴파일해야 함)</p> <p>작동하지 않는 경우:</p>
    <ul>
     <li>Publish 에셋.</li>
     <li>에셋을 다시 업로드하고 게시합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>세트 편집기의 자산 선택기가 영구적으로 로드되지 않음</td>
   <td><p>6.4에서 해결할 알려진 문제</p> </td>
   <td><p>선택기를 닫고 다시 엽니다.</p> </td>
  </tr>
  <tr>
   <td>집합 편집의 일부로 자산을 선택한 후 <strong>Select</strong> 단추가 활성화되지 않음</td>
   <td><p> </p> <p>6.4에서 해결할 알려진 문제</p> <p> </p> </td>
   <td><p>먼저 에셋 선택기의 다른 폴더에서 을(를) 선택하고 뒤로 돌아가 에셋을 선택합니다.</p> </td>
  </tr>
  <tr>
   <td>슬라이드 간을 전환한 후 슬라이드 핫스팟이 이동합니다.</td>
   <td><p>모든 슬라이드의 크기가 같은지 확인합니다.</p> </td>
   <td><p>회전판에 대해 크기가 같은 이미지만 사용하십시오.</p> </td>
  </tr>
  <tr>
   <td>이미지가 Dynamic Media 뷰어로 미리 표시되지 않음</td>
   <td><p>메타데이터 속성(CRXDE Lite)에서 에셋에 <code>dam:scene7File</code>이(가) 포함되어 있는지 확인</p> </td>
   <td><p>모든 에셋이 처리를 완료했는지 확인합니다.</p> </td>
  </tr>
  <tr>
   <td>업로드된 에셋이 에셋 선택기에 표시되지 않음</td>
   <td><p>자산에 속성 <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code>(CRXDE Lite)이 있는지 확인</p> </td>
   <td><p>모든 에셋이 처리를 완료했는지 확인합니다.</p> </td>
  </tr>
  <tr>
   <td>자산 처리를 시작하지 않은 경우 카드 보기의 배너에 <strong>새로 만들기</strong>가 표시됩니다.</td>
   <td>에셋 <code>jcr:content</code> &gt; <code>dam:assetState</code> = <code>unprocessed</code>이(가) 워크플로에서 선택되지 않은 경우 확인.</td>
   <td>워크플로우에서 에셋을 가져올 때까지 기다립니다.</td>
  </tr>
  <tr>
   <td>이미지 또는 집합은 뷰어 URL 또는 포함 코드를 표시하지 않습니다</td>
   <td>뷰어 사전 설정이 게시되었는지 확인합니다.</td>
   <td><p><strong>도구</strong> &gt; <strong>Assets</strong> &gt; <strong>뷰어 사전 설정</strong>(으)로 이동하여 뷰어 사전 설정을 게시합니다.</p> </td>
  </tr>
 </tbody>
</table>

## 비디오 {#video}

비디오에 문제가 있는 경우 다음 문제 해결 지침을 참조하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>문제</strong></td>
   <td><strong>디버깅하는 방법</strong></td>
   <td><strong>솔루션</strong></td>
  </tr>
  <tr>
   <td>비디오를 미리 볼 수 없음</td>
   <td>
    <ul>
     <li>폴더에 비디오 프로필이 할당되었는지 확인합니다(지원되지 않는 파일 형식인 경우). 지원되지 않는 경우 이미지만 표시됩니다.</li>
     <li>비디오 프로필에는 AVS 세트를 생성하기 위해 인코딩 사전 설정이 두 개 이상 포함되어야 합니다(단일 인코딩은 MP4 파일에 대한 비디오 콘텐츠로 처리됨. 지원되지 않는 파일의 경우 처리되지 않은 것과 동일하게 처리됨).</li>
     <li>메타데이터에서 <code>dam:scene7FileAvs</code>/<code>dam:scene7File</code>을(를) 확인하여 비디오가 처리를 완료했는지 확인하십시오.</li>
    </ul> </td>
   <td>
    <ol>
     <li>폴더에 비디오 프로필을 할당합니다.</li>
     <li>인코딩 사전 설정을 두 개 이상 포함하도록 비디오 프로필을 편집합니다.</li>
     <li>비디오가 처리를 완료할 때까지 기다립니다.</li>
     <li>비디오를 다시 로드하려면 Dynamic Media 인코딩 비디오 워크플로우가 실행되고 있지 않은지 확인하십시오.<br /> </li>
     <li>비디오를 다시 업로드합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>비디오가 인코딩되지 않음</td>
   <td>
    <ul>
     <li>실행 모드가 <code>dynamicmedia_scene7</code>인지 확인하십시오.</li>
     <li>Dynamic Media 클라우드 서비스가 구성되어 있는지 확인합니다.</li>
     <li>비디오 프로필이 업로드 폴더와 연결되어 있는지 확인합니다.</li>
    </ul> </td>
   <td>
    <ol>
     <li>다음으로 Experience Manager 인스턴스 확인 <code>-r dynamicmedia_scene7</code></li>
     <li>Cloud Service 아래의 Dynamic Media 구성이 올바르게 설정되었는지 확인합니다.</li>
     <li>폴더에 비디오 프로필이 있는지 확인합니다. 또한 비디오 프로필을 확인합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>비디오 처리 시간이 너무 오래 걸림</td>
   <td><p>비디오 인코딩이 계속 진행 중인지 또는 실패 상태에 들어왔는지 확인하려면 다음을 수행하십시오.</p>
    <ul>
     <li>비디오 상태 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> 확인 &gt; <code>dam:assetState</code></li>
     <li>워크플로 콘솔 <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; 인스턴스, 보관, 실패 탭에서 비디오를 모니터링합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>비디오 렌디션 누락</td>
   <td><p>비디오가 업로드되지만 인코딩된 변환은 없습니다.</p>
    <ul>
     <li>폴더에 할당된 비디오 프로필이 있는지 확인합니다.</li>
     <li>메타데이터에서 <code>dam:scene7FileAvs</code>을(를) 확인하여 비디오가 처리를 완료했는지 확인하십시오.</li>
    </ul> </td>
   <td>
    <ol>
     <li>폴더에 비디오 프로필을 할당합니다.</li>
     <li>비디오가 처리를 완료할 때까지 기다립니다.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 뷰어 {#viewers}

뷰어에 문제가 있는 경우 다음 문제 해결 지침을 참조하십시오.

### 문제: 뷰어 사전 설정이 게시되지 않음 {#viewers-not-published}

**디버깅하는 방법**

1. 샘플 관리자 진단 페이지 `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`(으)로 진행합니다.
1. 계산된 값을 관찰합니다. 올바르게 작동하면 다음 항목이 표시됩니다. `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >뷰어 에셋이 동기화되려면 Dynamic Media 클라우드 설정 구성 후 약 10분 정도 걸릴 수 있습니다.

1. 활성화되지 않은 자산이 남아 있는 경우 **활성화되지 않은 모든 Assets 나열** 단추 중 하나를 선택하여 세부 정보를 확인하십시오.

**솔루션**

1. 관리 도구의 뷰어 사전 설정 목록으로 이동: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. 모든 뷰어 사전 설정을 선택한 다음 **Publish**&#x200B;을(를) 선택합니다.
1. 다시 샘플 관리자로 이동하여 활성화되지 않은 자산 수가 이제 0인지 확인합니다.

### 문제: 뷰어 사전 설정 아트워크가 자산 세부 사항의 미리보기 또는 URL/포함 코드 복사에서 404를 반환함 {#viewer-preset-404}

**디버깅하는 방법**

CRXDE Lite에서 다음을 수행합니다.

1. Dynamic Media 동기화 폴더(예: `/content/dam/_CSS/_OOTB`) 내의 `<sync-folder>/_CSS/_OOTB` 폴더로 이동합니다.
1. 문제가 있는 자산의 메타데이터 노드를 찾습니다(예: `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. `dam:scene7*` 속성이 있는지 확인하십시오. 자산이 성공적으로 동기화되고 게시되면 `dam:scene7FileStatus` 세트가 **PublishComplete**(으)로 설정됩니다.
1. 다음 속성 및 문자열 리터럴의 값을 연결하여 다이내믹 미디어에서 직접 아트워크를 요청합니다.

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
예: `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**솔루션**

샘플 에셋 또는 뷰어 사전 설정 아트웍이 동기화되거나 게시되지 않은 경우 전체 복사/동기화 프로세스를 다시 시작합니다.

1. CRXDE Lite 로 이동합니다.
1. `<sync-folder>/_CSS/_OOTB` 삭제.
1. CRX 패키지 관리자 `https://localhost:4502/crx/packmgr/`(으)로 이동합니다.
1. 목록에서 뷰어 패키지를 검색합니다. `cq-dam-scene7-viewers-content`(으)로 시작합니다.
1. **다시 설치**&#x200B;를 선택합니다.
1. Cloud Service에서 Dynamic Media 구성 페이지로 이동한 다음, Dynamic Media - S7 구성에 대한 구성 대화 상자를 엽니다.
1. 변경하지 말고 **저장**&#x200B;을 선택하세요.
이 저장 작업은 샘플 에셋, 뷰어 사전 설정 CSS 및 아트워크를 만들고 동기화하기 위한 논리를 다시 트리거합니다.

### 문제: 뷰어 사전 설정 작성에서 이미지 미리 보기를 로드할 수 없음 {#image-preview-not-loading}

**솔루션**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.
1. 왼쪽 레일에서 다음 위치의 샘플 콘텐츠 폴더로 이동합니다.

   `/content/dam/_DMSAMPLE`

1. `_DMSAMPLE` 폴더를 삭제합니다.
1. 왼쪽 레일에서 다음 위치의 presets 폴더로 이동합니다.

   `/conf/global/settings/dam/dm/presets/viewer`

1. `viewer` 폴더를 삭제합니다.
1. CRXDE Lite 페이지의 왼쪽 상단 모서리 근처에서 **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.
1. CRXDE Lite 페이지의 왼쪽 상단 모서리에서 **홈으로 돌아가기** 아이콘을 선택합니다.
1. Cloud Service[&#128279;](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)에서 Dynamic Media 구성을 다시 만드십시오.
