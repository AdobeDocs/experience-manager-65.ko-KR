---
title: Dynamic Media 문제 해결 - Scene7 모드
description: Scene7 모드에서 실행 중인 Dynamic Media 문제 해결
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: Business Practitioner, Administrator
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: 문제 해결
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 2%

---

# Dynamic Media 문제 해결 - Scene7 모드{#troubleshooting-dynamic-media-scene-mode}

다음 문서에서는 **dynamicmedia_scene7** 실행 모드를 실행하는 Dynamic Media의 문제 해결에 대해 설명합니다.

## 설정 및 구성 {#setup-and-configuration}

다음을 수행하여 Dynamic Media이 제대로 설정되어 있는지 확인합니다.

* 시작 명령에 `-r dynamicmedia_scene7` 실행 모드 인수가 포함되어 있습니다.
* 모든 AEM 6.4 CFP(Cumulative Fix Pack)가 사용 가능한 Dynamic Media 기능 팩 전에 *부터 설치되었습니다.*
* 옵션 기능 팩 18912가 설치되어 있습니다.

   이 선택적 기능 팩은 FTP 지원을 위한 것이거나 Dynamic Media Classic에서 Dynamic Media으로 자산을 마이그레이션하는 경우입니다.

* Cloud Services 사용자 인터페이스로 이동하고 제공된 계정이 **[!UICONTROL 사용 가능한 구성 아래에 표시되는지 확인합니다.]**
* `Dynamic Media Asset Activation (scene7)` 복제 에이전트가 활성화되어 있는지 확인합니다.

   이 복제 에이전트는 작성자의 에이전트 아래에 있습니다.

## 일반(모든 자산) {#general-all-assets}

다음은 모든 에셋에 대한 일반적인 팁과 트릭입니다.

### 자산 동기화 상태 속성 {#asset-synchronization-status-properties}

다음 에셋 속성을 CRXDE Lite에서 검토하여 AEM에서 Dynamic Media으로 에셋을 성공적으로 동기화할 수 있습니다.

| **속성** | **예** | **설명** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 노드가 Dynamic Media에 연결되어 있음을 나타내는 일반 표시기. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** PublishComplete 또는 오류 텍스트 | Dynamic Media에 자산 업로드 상태 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Dynamic Media의 원격 자산에 대한 URL을 생성하려면 채워야 합니다. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **다음**   **에 실패했습니다.`<error text>`** | 세트(스핀 세트, 이미지 세트 등), 이미지 사전 설정, 뷰어 사전 설정, 에셋에 대한 이미지 맵 업데이트 또는 편집된 이미지의 동기화 상태입니다. |

### 동기화 로깅 {#synchronization-logging}

동기화 오류 및 문제가 `error.log`(AEM 서버 디렉토리 `/crx-quickstart/logs/`)에 기록됩니다. 대부분의 문제의 근본 원인을 결정하기에 충분한 로깅을 사용할 수 있지만 추가 정보를 수집하기 위해 Sling 콘솔([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))을 통해 `com.adobe.cq.dam.ips` 패키지의 DEBUG에 대한 로깅을 늘릴 수 있습니다.

### 이동, 복사, {#move-copy-delete} 삭제

이동, 복사 또는 삭제 작업을 수행하기 전에 다음을 수행합니다.

* 이미지 및 비디오의 경우 이동, 복사 또는 삭제 작업을 수행하기 전에 `<object_node>/jcr:content/metadata/dam:scene7ID` 값이 있는지 확인합니다.
* 이미지 및 뷰어 사전 설정의 경우 이동, 복사 또는 삭제 작업을 수행하기 전에 `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` 값이 있는지 확인합니다.
* 위의 메타데이터 값이 없는 경우 작업을 이동, 복사 또는 삭제하기 전에 자산을 다시 업로드해야 합니다.

### 버전 제어 {#version-control}

기존 Dynamic Media 자산(이름과 위치)을 바꿀 때 자산을 유지하거나 버전을 교체/만들 수 있습니다.

* 두 가지 모두를 유지하면 게시된 자산 URL에 대한 고유한 이름을 가진 새 자산이 만들어집니다. 예를 들어 `image.jpg`은 원래 자산이고 `image1.jpg`은 새로 업로드된 자산입니다.

* Dynamic Media - Scene7 모드 전달에서는 버전 만들기가 지원되지 않습니다. 새 버전은 전달에 있는 기존 자산을 대체합니다.

## 이미지 및 세트 {#images-and-sets}

이미지 및 세트에 문제가 있는 경우 다음 문제 해결 지침을 참조하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>문제</strong></td>
   <td><strong>디버깅 방법</strong></td>
   <td><strong>솔루션</strong></td>
  </tr>
  <tr>
   <td>자산 세부 사항 보기에서 복사 URL/포함 단추에 액세스할 수 없습니다.</td>
   <td>
    <ol>
     <li><p>CRX/DE로 이동:</p>
      <ul>
       <li>JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>의 사전 설정이 정의되었는지 확인합니다. 이 위치는 AEM 6.x에서 6.4로 업그레이드하고 마이그레이션 해제를 선택한 경우에 적용됩니다. 또는 위치는 <code>/conf/global/settings/dam/dm/presets/viewer</code>입니다.</li>
       <li>JCR의 자산이 메타데이터 아래에 <code>PublishComplete</code>로 표시된 <code>dam:scene7FileStatus</code><strong> </strong>에 있는지 확인합니다.</li>
      </ul> </li>
    </ol> </td>
   <td><p>페이지 새로 고침/다른 페이지로 이동한 후 돌아오십시오(사이드 레일 JSP를 다시 컴파일해야 함).</p> <p>효과가 없는 경우:</p>
    <ul>
     <li>자산을 게시합니다.</li>
     <li>자산을 다시 업로드하고 게시합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>세트 편집기의 자산 선택기가 영구 로딩에 고정됨</td>
   <td><p>6.4에서 해결된 알려진 문제</p> </td>
   <td><p>선택기를 닫고 다시 엽니다.</p> </td>
  </tr>
  <tr>
   <td><strong>세트 </strong> 편집의 일부로 자산을 선택한 후 선택 단추가 활성화되지 않습니다.</td>
   <td><p> </p> <p>6.4에서 해결된 알려진 문제</p> <p> </p> </td>
   <td><p>자산 선택기에서 다른 폴더를 먼저 클릭하고 되돌아가서 자산을 선택합니다.</p> </td>
  </tr>
  <tr>
   <td>회전판 핫스팟은 슬라이드 간 전환 후 이동</td>
   <td><p>모든 슬라이드의 크기가 동일한지 확인합니다.</p> </td>
   <td><p>회전판에 동일한 크기의 이미지만 사용합니다.</p> </td>
  </tr>
  <tr>
   <td>Dynamic Media 뷰어에서 이미지를 미리 볼 수 없음</td>
   <td><p>자산에 메타데이터 속성(CRXDE Lite)에 <code>dam:scene7File</code>이 포함되어 있는지 확인</p> </td>
   <td><p>모든 자산이 처리를 완료했는지 확인합니다.</p> </td>
  </tr>
  <tr>
   <td>업로드된 자산은 자산 선택기에 표시되지 않습니다.</td>
   <td><p>자산 확인 시 속성 <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code>(CRXDE Lite)</p> </td>
   <td><p>모든 자산이 처리를 완료했는지 확인합니다.</p> </td>
  </tr>
  <tr>
   <td>자산이 처리를 시작하지 않은 경우 카드 보기의 배너에 <strong>새로 만들기</strong>가 표시됩니다.</td>
   <td>자산 <code>jcr:content</code> &gt; <code>dam:assetState</code> = <code>unprocessed</code>이 워크플로우에 의해 선택되지 않은 경우 선택합니다.</td>
   <td>워크플로우에서 자산을 선택할 때까지 기다립니다.</td>
  </tr>
  <tr>
   <td>이미지 또는 세트는 뷰어 URL 또는 포함 코드를 표시하지 않습니다.</td>
   <td>뷰어 사전 설정이 게시되었는지 확인합니다.</td>
   <td><p><strong>도구</strong> &gt; <strong>자산</strong> &gt; <strong>뷰어 사전 설정</strong>으로 이동하여 뷰어 사전 설정을 게시합니다.</p> </td>
  </tr>
 </tbody>
</table>

## 비디오 {#video}

비디오 관련 문제가 있는 경우 다음 문제 해결 지침을 참조하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>문제</strong></td>
   <td><strong>디버깅 방법</strong></td>
   <td><strong>솔루션</strong></td>
  </tr>
  <tr>
   <td>비디오를 미리 볼 수 없습니다.</td>
   <td>
    <ul>
     <li>폴더에 비디오 프로필이 할당되었는지 확인합니다(지원되지 않는 파일 형식인 경우). 지원되지 않는 경우 이미지만 표시됩니다.</li>
     <li>비디오 프로필에는 AVS 세트를 생성하려면 인코딩 사전 설정이 두 개 이상 있어야 합니다(단일 인코딩은 MP4 파일의 비디오 컨텐츠로 처리됨).지원되지 않는 파일의 경우 처리되지 않은 파일과 동일하게 처리됩니다.</li>
     <li>메타데이터에서 <code>dam:scene7File</code>의 <code>dam:scene7FileAvs</code>을(를) 확인하여 비디오가 처리를 완료했는지 확인합니다.</li>
    </ul> </td>
   <td>
    <ol>
     <li>폴더에 비디오 프로필을 할당합니다.</li>
     <li>둘 이상의 인코딩 사전 설정을 포함하도록 비디오 프로필을 편집합니다.</li>
     <li>비디오가 처리를 완료할 때까지 기다립니다.</li>
     <li>비디오를 다시 로드하려면 Dynamic Media 비디오 인코딩 작업 과정이 실행되고 있지 않은지 확인하십시오.<br /> </li>
     <li>비디오를 다시 업로드합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>비디오가 인코딩되지 않음</td>
   <td>
    <ul>
     <li>실행 모드가 <code>dynamicmedia_scene7</code>인지 확인합니다.</li>
     <li>Dynamic Media 클라우드 서비스가 구성되어 있는지 확인합니다.</li>
     <li>비디오 프로필이 업로드 폴더와 연관되어 있는지 확인합니다.</li>
    </ul> </td>
   <td>
    <ol>
     <li>AEM 인스턴스를 <code>-r dynamicmedia_scene7</code></li>
     <li>Cloud Services 아래의 Dynamic Media 구성이 올바르게 설정되었는지 확인하십시오.</li>
     <li>폴더에 비디오 프로필이 있는지 확인합니다. 또한 비디오 프로필을 확인하십시오.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>비디오 처리 시간이 너무 오래 걸립니다.</td>
   <td><p>비디오 인코딩이 아직 진행 중인지 또는 오류 상태에 들어갔는지 확인하려면:</p>
    <ul>
     <li>비디오 상태 확인 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>워크플로우 콘솔 <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; 인스턴스, 아카이브, 실패 탭에서 비디오를 모니터링합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>비디오 변환 누락</td>
   <td><p>비디오가 업로드되지만 인코딩된 변환이 없는 경우:</p>
    <ul>
     <li>폴더에 비디오 프로필이 할당되었는지 확인합니다.</li>
     <li>메타데이터에서 <code>dam:scene7FileAvs</code>을(를) 확인함으로써 비디오 처리가 완료되었는지 확인합니다.</li>
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

<table>
 <tbody>
  <tr>
   <td><strong>문제</strong></td>
   <td><strong>디버깅 방법</strong></td>
   <td><strong>솔루션</strong></td>
  </tr>
  <tr>
   <td>뷰어 사전 설정이 게시되지 않았습니다.</td>
   <td><p>샘플 관리자 진단 페이지로 이동합니다. <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>계산된 값을 관찰합니다. 올바르게 작동하면 다음을 볼 수 있습니다.</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>참고</strong>:뷰어 에셋을 동기화할 Dynamic Media 클라우드 설정을 구성한 후 약 10분이 걸릴 수 있습니다.</p> <p>활성화되지 않은 자산이 남아 있는 경우 <strong>활성화되지 않은 모든 자산 목록</strong> 단추 중 하나를 클릭하여 세부 사항을 확인합니다.</p> </td>
   <td>
    <ol>
     <li>관리 도구에서 뷰어 사전 설정 목록으로 이동합니다. <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>모든 뷰어 사전 설정을 선택한 다음 <strong>게시</strong>를 클릭합니다.</li>
     <li>다시 샘플 관리자로 이동하여 활성화되지 않은 자산 수가 0인 것을 확인합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>뷰어 사전 설정 아트웍은 에셋 세부 사항의 미리 보기에서 404를 반환하거나 URL/포함 코드를 복사합니다</td>
   <td><p>CRXDE Lite에서 다음을 수행합니다.</p>
    <ol>
     <li>Dynamic Media 동기화 폴더 내의 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> 폴더(예: <code>/content/dam/_CSS/_OOTB</code>)로 이동합니다.</li>
     <li>문제가 있는 자산의 메타데이터 노드를 찾습니다(예: <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li><code>dam:scene7*</code> 속성이 있는지 확인합니다. 자산이 성공적으로 동기화되고 게시되면 <code>dam:scene7FileStatus</code> 세트가 <strong>PublishComplete</strong>로 표시됩니다.</li>
     <li>다음 속성 및 문자열 리터럴의 값을 연결하여 Dynamic Media에서 직접 아트웍을 요청하려고 합니다
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>예: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>샘플 에셋 또는 뷰어 사전 설정 아트웍이 동기화되거나 게시되지 않은 경우 전체 복사/동기화 프로세스를 다시 시작합니다.</p>
    <ol>
     <li>CRXDE Lite으로 이동합니다.
      <ul>
       <li>삭제 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>CRX 패키지 관리자로 이동합니다.<code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>목록에서 뷰어 패키지 검색(<code>cq-dam-scene7-viewers-content</code>으로 시작)</li>
       <li><strong>다시 설치</strong>를 클릭합니다.</li>
      </ol> </li>
     <li>Cloud Services 아래에서 Dynamic Media 구성 페이지로 이동한 다음 Dynamic Media - S7 구성에 대한 구성 대화 상자를 엽니다.
      <ul>
       <li>변경하지 말고 <strong>저장</strong>을 클릭합니다. 이렇게 하면 샘플 에셋, 뷰어 사전 설정 CSS 및 아트웍을 만들고 동기화하는 로직을 다시 트리거합니다.<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
