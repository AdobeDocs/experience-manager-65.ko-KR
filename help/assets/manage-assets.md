---
title: 디지털 자산 관리
description: 디지털 에셋의 업로드, 다운로드, 편집, 검색, 삭제, 주석 달기 및 버전 지정과 같은 에셋 관리 작업에 대해 알아봅니다.
contentOwner: AG
role: User
feature: Asset Management,Search
mini-toc-levels: 4
exl-id: 158607e6-b4e9-4a3f-b023-4023d60c97d2
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '10038'
ht-degree: 3%

---

# 디지털 자산 관리 {#manage-digital-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-digital-assets.html?lang=en) |
| AEM 6.5 | 이 문서 |

위치 [!DNL Adobe Experience Manager Assets], 에셋을 저장하고 제어하는 것 이상의 작업을 수행할 수 있습니다. [!DNL Experience Manager] 는 엔터프라이즈급 자산 관리 기능을 제공합니다. 에셋을 편집 및 공유하고, 고급 검색을 실행하고, 수십 개의 지원되는 파일 형식의 여러 렌디션을 만들 수 있습니다. 또한 버전 및 디지털 권한을 관리하고, 에셋 처리를 자동화하고, 메타데이터를 관리 및 관리하며, 주석을 사용하여 공동 작업을 수행할 수도 있습니다.

이 문서에서는 에셋 생성 또는 업로드, 메타데이터 업데이트, 복사, 이동 및 삭제, 게시, 게시 취소 및 검색과 같은 기본 에셋 관리 작업에 대해 설명합니다. 사용자 인터페이스를 이해하려면 다음을 참조하십시오. [assets 사용자 인터페이스 시작](/help/sites-authoring/basic-handling.md). 콘텐츠 조각을 관리하려면 다음을 참조하십시오. [콘텐츠 조각 관리](/help/assets/content-fragments/content-fragments-managing.md) 에셋.

## 폴더 만들기 {#creating-folders}

에셋 컬렉션(예: 모두)을 구성할 때 `Nature` 이미지를 만들 때 폴더를 만들어 함께 보관할 수 있습니다. 폴더를 사용하여 에셋을 분류하고 구성할 수 있습니다. [!DNL Experience Manager Assets] 는 작업을 향상시키기 위해 폴더에 에셋을 구성할 필요가 없습니다.

>[!NOTE]
>
>* 공유 [!DNL Assets] 유형의 폴더 `sling:OrderedFolder` 은(는) Experience Cloud에 공유할 때 지원되지 않습니다. 폴더를 공유하려면 선택하지 마십시오. [!UICONTROL 주문됨] 폴더를 만들 때.
>* [!DNL Experience Manager] 을(를) 사용할 수 없음 `subassets` word를 폴더 이름으로 사용합니다. 조합 자산에 대한 하위 자산을 포함하는 노드용으로 예약된 키워드입니다.

1. 디지털 자산 폴더에서 폴더를 만들 위치로 이동합니다. 메뉴에서 다음을 클릭합니다. **[!UICONTROL 만들기]**. 선택 **[!UICONTROL 새 폴더]**.
1. 다음에서 **[!UICONTROL 제목]** 필드에 폴더 이름을 입력합니다. 기본적으로 DAM은 사용자가 제공한 제목을 폴더 이름으로 사용합니다. 폴더가 만들어지면 기본값을 재정의하고 다른 폴더 이름을 지정할 수 있습니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 디지털 에셋 폴더에 폴더가 표시됩니다.

공백으로 구분된 다음 문자는 지원되지 않습니다.

* 에셋 파일 이름에는 다음 문자를 사용할 수 없습니다. `* / : [ \\ ] | # % { } ? &`
* 에셋 폴더 이름에는 다음 문자를 사용할 수 없습니다. `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

자산 파일 이름의 확장에 특수 문자를 포함하지 마십시오.

## 자산 업로드 {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

로컬 폴더 또는 네트워크 드라이브에서 다양한 유형의 에셋(이미지, PDF 파일, RAW 파일 등)을 업로드하여 [!DNL Experience Manager Assets].

>[!NOTE]
>
>Dynamic Media - Scene7 모드에서 기본 에셋 업로드 파일 크기는 2GB 이하입니다. 2GB보다 크고 최대 15GB의 자산 업로드를 구성하려면 다음을 참조하십시오. [(선택 사항) 2GB보다 큰 에셋의 업로드를 위해 Dynamic Media - Scene7 모드 구성](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb).

>[!IMPORTANT]
>
>파일 이름이 100자를 초과하는 Experience Manager에 업로드하는 에셋은 Dynamic Media에서 사용할 때 약식 이름을 갖습니다.
>
>파일 이름의 처음 100자는 그대로 사용되고, 나머지 문자는 영숫자 문자열로 대체됩니다. 이 이름 변경 방법은 Dynamic Media에서 자산을 사용할 때 고유한 이름을 보장합니다. 또한 Dynamic Media에서 허용되는 최대 에셋 파일 이름 길이를 수용하기 위한 것입니다.

자산에 지정된 처리 프로필이 있거나 없는 폴더에 자산을 업로드하도록 선택할 수 있습니다.

처리 프로필이 할당된 폴더의 경우 프로필 이름이 카드 보기의 썸네일에 표시됩니다. 목록 보기에서 프로파일 이름이에 나타납니다. **처리 프로필** 열. 다음을 참조하십시오 [처리 프로필](/help/assets/processing-profiles.md).

에셋을 업로드하기 전에 에셋이 [형식](/help/assets/assets-formats.md) that [!DNL Experience Manager Assets] 를 지원합니다.

1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 디지털 에셋을 추가할 위치로 이동합니다.
1. 에셋을 업로드하려면 다음 중 하나를 수행하십시오.

   * 도구 모음에서 를 클릭합니다 **[!UICONTROL 만들기]**. 그런 다음 메뉴에서 **[!UICONTROL 파일]**. 필요한 경우 제공된 대화 상자에서 파일 이름을 변경할 수 있습니다.
   * HTML5를 지원하는 브라우저에서 [!DNL Assets] 사용자 인터페이스. 파일 이름을 바꾸는 대화 상자가 표시되지 않습니다.

   ![자산을 업로드하는 옵션 만들기](assets/create-options.png)

   여러 파일을 선택하려면 `Ctrl` 또는 `Command` 키를 누르고 파일 선택기 대화 상자에서 에셋을 선택합니다. iPad을 사용하는 경우 한 번에 하나의 파일만 선택할 수 있습니다.

   큰 에셋(500MB 초과)의 업로드를 일시 중지하고 나중에 동일한 페이지에서 다시 시작할 수 있습니다. 클릭 **[!UICONTROL 일시 중지]** 업로드가 시작될 때 나타나는 진행률 표시줄 옆에 있습니다.

   ![자산 업로드 진행률 표시줄](assets/upload-progress-bar.png)

큰 자산으로 간주되는 위의 크기를 구성할 수 있습니다. 예를 들어 1000MB(500MB가 아님) 이상의 자산을 큰 자산으로 간주하도록 시스템을 구성할 수 있습니다. 이 경우, **[!UICONTROL 일시 중지]** 크기가 1000MB보다 큰 에셋을 업로드하면 진행률 표시줄에 표시됩니다.

다음 [!UICONTROL 일시 중지] 1000MB보다 큰 파일을 1000MB 보다 작은 파일과 함께 업로드하면 옵션이 표시되지 않습니다. 그러나 1000MB 미만의 파일 업로드를 취소하면 **[!UICONTROL 일시 중지]** 옵션이 나타납니다.

크기 제한을 수정하려면 다음을 구성합니다. `chunkUploadMinFileSize` 의 속성 `fileupload` 사용 가능한 CRX 저장소의 노드 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`.

다음을 클릭: **[!UICONTROL 일시 중지]**, 로 전환됩니다. **[!UICONTROL 재생]** 옵션을 선택합니다. 업로드를 다시 시작하려면 다음을 클릭하십시오. **[!UICONTROL 재생]**.

진행 중인 업로드를 취소하려면 닫기( )를 클릭합니다.`X`)을 클릭하여 제품에서 사용할 수 있습니다. 업로드 작업을 취소하면 [!DNL Assets] 부분적으로 업로드한 에셋 부분을 삭제합니다.

업로드를 재개하는 기능은 특히 큰 에셋을 업로드하는 데 오랜 시간이 걸리는 낮은 대역폭 시나리오 및 네트워크 문제에서 유용합니다. 업로드 작업을 일시 중지하고 나중에 상황이 개선되면 계속할 수 있습니다. 다시 시작하면 일시 중지한 시점부터 업로드가 시작됩니다.

업로드 작업 중, [!DNL Experience Manager] 업로드되는 에셋의 일부를 CRX 저장소의 데이터 청크로 저장합니다. 업로드가 완료되면, [!DNL Experience Manager] 이러한 청크를 저장소의 단일 데이터 블록으로 통합합니다.

완료되지 않은 청크 업로드 작업에 대한 정리 작업을 구성하려면 `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.

>[!CAUTION]
>
>기본값이 500MB이고 청크 크기가 50MB인 경우 청크 업로드가 트리거됩니다. 를 편집하는 경우 [Apache Jackrabbit Oak TokenConfiguration](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16464.html) 및 설정 `timeout configuration` 에셋을 업로드하는 데 걸리는 시간보다 적으면 에셋 업로드가 진행되는 동안 세션 시간 초과 상황이 발생합니다. 따라서 `chunkUploadMinFileSize` 및 `chunksize` 각 청크 요청이 세션을 새로 고치도록 하는 것입니다.
>
>자격 증명 만료 시간 제한, 대기 시간, 대역폭 및 예상 동시 업로드가 주어지면 다음을 선택할 수 있는 가장 높은 값입니다.
>
>* 업로드가 진행되는 동안 자격 증명 만료가 발생할 가능성이 높은 크기의 파일에 대해 청크 업로드가 활성화되도록 합니다.
>
>* 자격 증명이 만료되기 전에 각 청크가 완료되는지 확인합니다.

에셋을 업로드하는 위치에서 이미 사용할 수 있는 에셋과 동일한 이름의 에셋을 업로드하는 경우 경고 대화 상자가 표시됩니다.

업로드된 새 에셋의 이름을 바꾸어 기존 에셋을 바꾸거나, 다른 버전을 생성하거나, 둘 다 유지하도록 선택할 수 있습니다. 기존 에셋을 교체하는 경우 에셋에 대한 메타데이터 및 기존 에셋에 대한 이전 수정 사항(예: 주석 또는 자르기)이 삭제됩니다. 두 에셋을 모두 유지하도록 선택하면 새 에셋의 이름이 number로 변경됩니다 `1` 이름에 추가됩니다.

![자산 이름 충돌을 해결하는 이름 충돌 대화 상자](assets/resolve-naming-conflict.png)

>[!NOTE]
>
>다음을 선택할 때 **[!UICONTROL 바꾸기]** 다음에서 [!UICONTROL 이름 충돌] 대화 상자에서 새 에셋에 대한 에셋 ID가 다시 생성됩니다. 이 ID는 이전 에셋의 ID와 다릅니다.
>
>Assets Insights가 로 노출 횟수 또는 클릭 수를 추적할 수 있는 경우 [!DNL Adobe Analytics]로 설정하면 재생성된 에셋 ID가에서 에셋에 대해 캡처된 데이터가 무효화됩니다. [!DNL Analytics].

업로드한 에셋이에 있는 경우 [!DNL Assets], **[!UICONTROL 복제가 감지됨]** 대화 상자에 중복 에셋을 업로드하려고 한다는 경고가 표시됩니다. 대화 상자는 다음 경우에만 나타납니다. `SHA 1` 기존 에셋의 바이너리에 대한 체크섬 값이 업로드한 에셋의 체크섬 값과 일치합니다. 이 경우 에셋의 이름은 중요하지 않습니다.

>[!NOTE]
>
>다음 [!UICONTROL 복제가 감지됨] 대화 상자는 중복 감지 기능이 활성화된 경우에만 표시됩니다. 중복 감지 기능을 활성화하려면 다음을 참조하십시오. [중복 감지 활성화](/help/assets/duplicate-detection.md).

![중복 에셋 감지 대화 상자](assets/duplicate-asset-detected.png)

에서 중복 에셋을 유지하려면 [!DNL Assets], 클릭 **[!UICONTROL 유지]**. 업로드한 중복 에셋을 삭제하려면 **[!UICONTROL 삭제]**.

[!DNL Experience Manager Assets] 는 파일 이름에 금지된 문자가 있는 에셋을 업로드할 수 없습니다. 허용되지 않는 문자 이상이 포함된 파일 이름으로 에셋을 업로드하려는 경우, [!DNL Assets] 경고 메시지를 표시하고 이러한 문자를 제거하거나 허용되는 이름으로 업로드할 때까지 업로드를 중지합니다.

조직의 특정 파일 이름 지정 규칙에 맞추기 위해 [!UICONTROL 자산 업로드] 대화 상자를 통해 업로드하는 파일의 긴 이름을 지정할 수 있습니다.

그러나 공백으로 구분된 다음 문자는 지원되지 않습니다.

* 자산 파일 이름에는 다음이 포함되지 않아야 합니다. `* / : [ \\ ] | # % { } ? &`
* 자산 폴더 이름에는 다음이 포함될 수 없습니다. `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

자산 파일 이름의 확장에 특수 문자를 포함하지 마십시오.

![업로드 진행 상황 대화 상자에 업로드한 파일과 업로드에 실패한 파일의 상태가 표시됩니다](assets/bulk-upload-progress.png)

또한 [!DNL Assets] 사용자 인터페이스는 업로드한 가장 최근 에셋 또는 처음 만든 폴더를 표시합니다.

파일을 업로드하기 전에 업로드 작업을 취소하는 경우 [!DNL Assets] 현재 파일 업로드를 중단하고 콘텐츠를 새로 고칩니다. 그러나 이미 업로드된 파일은 삭제되지 않습니다.

의 업로드 진행 상황 대화 상자 [!DNL Assets] 성공적으로 업로드된 파일 및 업로드하지 못한 파일 수를 표시합니다.

### 직렬 업로드 {#serialuploads}

많은 자산을 대량으로 업로드하면 상당한 입출력 리소스가 소모되어 성능이 저하될 수 있습니다 [!DNL Assets] 배포. 특히 인터넷 연결 속도가 느린 경우 디스크 I/O가 급증하면서 업로드 시간이 급격히 늘어난다. 또한 웹 브라우저에는 POST 요청 수에 대한 추가 제한이 있을 수 있습니다 [!DNL Assets] 은 동시 자산 업로드를 처리할 수 있습니다. 따라서 업로드 작업이 실패하거나 너무 빨리 종료됩니다. 다른 말로 하자면 [!DNL Experience Manager Assets] 여러 파일을 수집하는 동안 일부 파일을 놓치거나 모든 파일을 수집하지 못할 수 있습니다.

이 상황을 극복하기 위해 [!DNL Assets] 모든 에셋을 동시에 수집하는 대신 일괄 업로드 작업 동안 한 번에 하나의 에셋을 수집합니다(직렬 업로드).

자산의 직렬 업로드는 기본적으로 활성화됩니다. 기능을 비활성화하고 동시 업로드를 허용하려면 다음을 오버레이하십시오. `fileupload` crx-de의 노드 및 `parallelUploads` 다음으로 속성: `true`.

### FTP를 사용하여 에셋 업로드 {#uploading-assets-using-ftp}

Dynamic Media을 사용하면 FTP 서버를 통해 에셋을 일괄 업로드할 수 있습니다. 큰 자산(>1GB)을 업로드하거나 전체 폴더 및 하위 폴더를 업로드하려면 FTP를 사용해야 합니다. FTP 업로드가 반복적으로 실행되도록 설정할 수도 있습니다.

>[!NOTE]
>
>Dynamic Media - Scene7 모드에서 기본 에셋 업로드 파일 크기는 2GB 이하입니다. 2GB보다 크고 최대 15GB의 자산 업로드를 구성하려면 다음을 참조하십시오. [(선택 사항) 2GB보다 큰 에셋의 업로드를 위해 Dynamic Media - Scene7 모드 구성](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb).

>[!NOTE]
>
>18912 Dynamic Media - Scene7 모드에서 FTP를 통해 에셋을 업로드하려면 [!DNL Experience Manager] 작성자 인스턴스. 연락처 [Adobe 고객 지원](https://experienceleague.adobe.com/?support-solution=General#support) fp-18912에 액세스하여 FTP 계정 설정을 완료합니다. 자세한 내용은 [벌크 자산 마이그레이션용 기능 팩 18912 설치](/help/assets/bulk-ingest-migrate.md).
>
>FTP를 사용하여 에셋을 업로드하는 경우에서 지정된 업로드 설정입니다. [!DNL Experience Manager] 무시합니다. 대신 Dynamic Media Classic에서 정의한 파일 처리 규칙이 사용됩니다.

**FTP를 사용하여 에셋을 업로드하려면**

1. 선택한 FTP 클라이언트를 사용하여 프로비저닝 이메일에서 받은 FTP 사용자 이름 및 암호를 사용하여 FTP 서버에 로그인합니다. FTP 클라이언트에서 FTP 서버에 파일이나 폴더를 업로드합니다.

1. 를 엽니다. [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)을 클릭한 다음 계정에 로그인합니다.

   자격 증명 및 로그인은 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 전역 탐색 모음에서 를 클릭합니다. **[!UICONTROL 업로드]**.
1. 업로드 페이지의 왼쪽 상단 모서리에서 을(를) 클릭합니다. **[!UICONTROL FTP를 통해]** 탭.
1. 페이지 왼쪽에서 파일을 업로드할 FTP 폴더를 선택하고, 페이지 오른쪽에서 대상 폴더를 선택합니다.
1. 페이지의 오른쪽 아래 모서리 근처에서 을 클릭합니다. **[!UICONTROL 작업 옵션]** 선택한 폴더의 에셋을 기준으로 원하는 옵션을 설정합니다.

   다음을 참조하십시오 [업로드 작업 옵션](#upload-job-options).

   >[!NOTE]
   >
   >FTP를 통해 에셋을 업로드할 때 Dynamic Media Classic(S7)에서 설정한 업로드 작업 옵션이에 설정된 에셋 처리 매개 변수보다 우선합니다 [!DNL Experience Manager].

1. 업로드 작업 옵션 대화 상자의 오른쪽 아래 모서리에서 을(를) 클릭합니다 **[!UICONTROL 저장]**.
1. 업로드 페이지의 오른쪽 아래 모서리에서 **[!UICONTROL 업로드 제출]**.

   업로드 진행 상황을 보려면 전역 탐색 모음에서 를 클릭합니다. **[!UICONTROL 작업]**. 작업 페이지에 업로드 진행 상황이 표시됩니다. 에서 작업을 계속할 수 있습니다. [!DNL Experience Manager] 언제든지 Dynamic Media Classic의 [작업] 페이지로 돌아가서 진행 중인 작업을 검토합니다.
진행 중인 업로드 작업을 취소하려면 다음을 클릭하십시오. **[!UICONTROL 취소]** 을 클릭합니다.

#### 업로드 작업 옵션 {#upload-job-options}

| 업로드 옵션 | 하위 선택 | 설명 |
|---|---|---|
| 작업 이름 | | 텍스트 필드에 미리 채워진 기본 이름에는 사용자가 입력한 이름 부분과 날짜 및 시간 스탬프가 포함됩니다. 이 업로드 작업에 기본 이름을 사용하거나 직접 만든 작업의 이름을 입력할 수 있습니다. <br>작업 및 기타 업로드 및 게시 작업은 작업 페이지에 기록되며, 이 페이지에서 작업 상태를 확인할 수 있습니다. |
| 업로드 후 게시 | | 업로드한 에셋을 자동으로 게시합니다. |
| 확장명에 상관없이 동일한 기본 에셋 이름으로 모든 폴더에 덮어쓰기 | | 업로드하는 파일이 기존 파일을 같은 이름으로 바꾸려면 이 옵션을 선택합니다. 이 옵션의 이름은 의 설정에 따라 다를 수 있습니다. **[!UICONTROL 응용 프로그램 설정]** > **[!UICONTROL 일반 설정]** > **[!UICONTROL 애플리케이션에 업로드]** > **[!UICONTROL 이미지 덮어쓰기]**. |
| 업로드 시 Zip 또는 Tar 파일 압축 풀기 | | |
| 작업 옵션 | | 클릭 **[!UICONTROL 작업 옵션]** 따라서 다음을 열 수 있습니다 [!UICONTROL 업로드 작업 옵션] 대화 상자를 열고 전체 업로드 작업에 영향을 주는 옵션을 선택합니다. 이러한 옵션은 모든 파일 유형에 대해 동일합니다.<br>응용 프로그램 일반 설정 페이지에서 시작하여 파일을 업로드하기 위한 기본 옵션을 선택할 수 있습니다. 이 페이지를 열려면 다음을 선택하십시오. **[!UICONTROL 설정]** > **[!UICONTROL 응용 프로그램 설정]**. 다음 항목 선택 **[!UICONTROL 기본 업로드 옵션]** 옵션 열기 [!UICONTROL 업로드 작업 옵션] 대화 상자. |
| | http 화이트보드 | 일회성 또는 반복을 선택합니다. 반복 작업을 설정하려면 반복 옵션(일별, 주별, 월별 또는 사용자 지정)을 선택하여 FTP 업로드 작업이 반복될 시기를 지정합니다. 그런 다음 필요에 따라 예약 옵션을 지정합니다. |
| | 하위 폴더 포함 | 업로드할 폴더 내의 모든 하위 폴더를 업로드합니다. 업로드한 폴더 및 하위 폴더의 이름이에 자동으로 입력됩니다 [!DNL Experience Manager Assets]. |
| | 자르기 옵션 | 이미지의 측면에서 수동으로 자르려면 [자르기] 메뉴를 선택하고 [수동]을 선택합니다. 그런 다음 이미지의 모든 면 또는 각 면에서 자를 픽셀 수를 입력합니다. 이미지가 잘리는 정도는 이미지 파일의 ppi(인치당 픽셀) 설정에 따라 달라집니다. 예를 들어, 이미지에 150ppi가 표시되고 [위쪽], [오른쪽], [아래쪽] 및 [왼쪽] 텍스트 상자에 75를 입력하면 각 면에서 1/2인치가 잘립니다.<br> 이미지에서 공백 픽셀을 자동으로 자르려면 [자르기] 메뉴를 열고 [수동]을 선택한 다음 [위쪽], [오른쪽], [아래쪽] 및 [왼쪽] 필드에 픽셀 측정값을 입력하여 측면에서 자릅니다. 자르기 메뉴에서 트림을 선택하고 다음 옵션을 선택할 수도 있습니다.<br> **다음을 기준으로 트림** <ul><li>**색상** - 색상 옵션을 선택합니다. 그런 다음 [모퉁이] 메뉴를 선택하고 자르려는 공백 색상을 가장 잘 나타내는 색상으로 이미지의 모퉁이를 선택합니다.</li><li>**투명도** - 투명도 옵션을 선택합니다.<br> **허용 오차** - 슬라이더를 드래그하여 0 - 1 사이의 공차를 지정합니다. 색상에 따라 트리밍하려면 0을 지정하여 이미지의 모퉁이에서 선택한 색상과 정확히 일치하는 경우에만 픽셀을 자릅니다. 1에 가까운 숫자를 사용하면 더 많은 색상 차이를 사용할 수 있습니다.<br>투명도를 기준으로 트리밍하려면 0을 지정하여 픽셀이 투명한 경우에만 자를 수 있습니다. 숫자가 1에 가까울수록 투명도가 높아집니다.</li></ul><br>이러한 자르기 옵션은 비파괴적입니다. |
| | 색상 프로파일 옵션 | 게재에 사용되는 최적화된 파일을 만들 때 색상 변환을 선택합니다.<ul><li>기본 색상 보존: 이미지에 색상 공간 정보가 포함될 때마다 소스 이미지 색상이 유지되며 색상 변환은 없습니다. 오늘날 거의 모든 이미지에는 해당 색상 프로파일이 이미 포함되어 있습니다. 그러나 CMYK 소스 이미지에 포함된 색상 프로파일이 없는 경우에는 색상이 sRGB(표준 빨강 녹색 파랑) 색상 공간으로 변환됩니다. sRGB는 웹 페이지에 이미지를 표시하는 데 권장되는 색상 공간입니다.</li><li>원본 색상 공간 유지: 지점에서 색상 변환 없이 원본 색상을 유지합니다. 포함된 색상 프로파일이 없는 이미지의 경우 [제작] 설정에서 구성한 기본 색상 프로파일을 사용하여 모든 색상 변환이 수행됩니다. 이 옵션을 사용하여 만든 파일의 색상과 색상 프로파일이 일치하지 않을 수 있습니다. 따라서 [기본 색상 보존] 옵션을 사용하는 것이 좋습니다.</li><li>사용자 지정 시작 > 종료<br> [변환]과 [색상 공간으로 변환]을 선택할 수 있는 메뉴를 엽니다. 이 고급 옵션은 소스 파일에 포함된 모든 색상 정보를 무시합니다. 제출하는 모든 이미지에 잘못되거나 누락된 색상 프로파일 데이터가 포함된 경우 이 옵션을 선택합니다.</li></ul> |
| | 이미지 편집 옵션 | 이미지에서 클리핑 마스크를 유지하고 색상 프로파일을 선택할 수 있습니다.<br> 다음을 참조하십시오 [업로드 시 이미지 편집 옵션 설정](#setting-image-editing-options-at-upload). |
| | Postscript 옵션 | PostScript® 파일을 래스터화하고, 파일을 자르고, 투명한 배경을 유지하고, 해상도를 선택하고, 색상 공간을 선택할 수 있습니다.<br> 다음을 참조하십시오 [포스트스크립트 및 Illustrator 업로드 옵션 설정](#setting-postscript-and-illustrator-upload-options). |
| | Photoshop 옵션 | Adobe® Photoshop® 파일에서 템플릿을 만들고, 레이어를 유지하고, 레이어 이름 지정 방법을 지정하고, 텍스트를 추출하고, 이미지가 템플릿에 고정되는 방법을 지정할 수 있습니다.<br> 템플릿은에서 지원되지 않습니다. [!DNL Experience Manager].<br> 다음을 참조하십시오 [Photoshop 업로드 옵션 설정](#setting-photoshop-upload-options). |
| | PDF 옵션 | 파일을 래스터화하고, 검색어와 링크를 추출하고, eCatalog를 자동 생성하고, 해상도를 설정하고, 색상 공간을 선택할 수 있습니다.<br>전자 카탈로그는 다음에서 지원되지 않습니다. [!DNL Experience Manager]. <br> 다음을 참조하십시오 [PDF 업로드 옵션 설정 중](#setting-pdf-upload-options).<br>**참고**: 추출할 PDF의 최대 페이지 수는 새 업로드의 경우 5000페이지입니다. 이 제한은 2022년 12월 31일에 100페이지(모든 PDF에 대해)로 변경됩니다. 참조: [Dynamic Media 제한 사항](/help/assets/limitations.md). |
| | Illustrator 옵션 | Adobe Illustrator® 파일을 래스터화하고 투명한 배경을 유지하며 해상도를 선택하고 색상 공간을 선택할 수 있습니다.<br> 다음을 참조하십시오 [포스트스크립트 및 Illustrator 업로드 옵션 설정](#setting-postscript-and-illustrator-upload-options). |
| | EVideo 옵션 | [비디오 사전 설정]을 선택하여 비디오 파일을 트랜스코딩할 수 있습니다.<br> 다음을 참조하십시오 [eVideo 업로드 옵션 설정 중](#setting-evideo-upload-options). |
| | 일괄 처리 집합 사전 설정 | 업로드한 파일에서 이미지 세트 또는 회전 세트를 만들려면 사용할 사전 설정에 대한 활성 열을 클릭합니다. 두 개 이상의 사전 설정을 선택할 수 있습니다. Dynamic Media Classic의 [애플리케이션 설정/일괄처리 집합 사전 설정] 페이지에서 사전 설정을 만듭니다.<br> 다음을 참조하십시오 [이미지 세트 및 스핀 세트를 자동으로 생성하도록 일괄처리 집합 사전 설정 구성](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 일괄 처리 집합 사전 설정 만들기에 대해 자세히 알아보십시오.<br> 다음을 참조하십시오 [업로드 시 일괄처리 집합 사전 설정 설정](#setting-batch-set-presets-at-upload). |

#### 업로드 시 이미지 편집 옵션 설정 {#setting-image-editing-options-at-upload}

AI, EPS 및 PSD 파일을 포함한 이미지 파일을 업로드할 때에서 다음 편집 작업을 수행할 수 있습니다. [!UICONTROL 업로드 작업 옵션] 대화 상자:

* 이미지 가장자리에서 공백을 자릅니다(위 표의 설명 참조).
* 이미지의 측면에서 수동으로 자릅니다(위 표의 설명 참조).
* 색상 프로파일을 선택합니다(위 표의 옵션 설명 참조).
* 클리핑 패스에서 마스크를 만듭니다.
* 언샵 마스킹 옵션을 사용하여 이미지 선명하게 하기
* 녹아웃 배경

<!--
| Option | Sub-option | Description |
|---|---|---|
| Create Mask From Clipping Path | | Create a mask for the image based on its clipping path information. This option applies to images created with image-editing applications in which a clipping path was created. |
| Unsharp Masking | | Lets you fine-tune a sharpening filter effect on the final downsampled image, controlling the intensity of the effect, the radius of the effect (as measured in pixels), and a threshold of contrast that is ignored.<br> This effect uses the same options as Photoshop's Unsharp Mask filter. Contrary to what the name suggests, Unsharp Mask is a sharpening filter. Under Unsharp Masking, set the options you want. Setting options are described in the following: |
| | Amount | Controls the amount of contrast that is applied to edge pixels.<br> Think of it as the intensity of the effect. The main difference between the amount values of Unsharp Mask in Dynamic Media and the amount values in Adobe Photoshop, is that Photoshop has an amount range of 1% to 500%. Whereas, in Dynamic Media, the value range is 0.0 to 5.0. A value of 5.0 is the rough equivalent of 500% in Photoshop; a value of 0.9 is the equivalent of 90%, and so on. |
| | Radius | Controls the radius of the effect. The value range is 0-250.<br> The effect is run on all pixels in an image and radiates out from all pixels in all directions. The radius is measured in pixels. For example, to get a similar sharpening effect for a 2000 x 2000 pixel image and 500 x 500 pixel image, you would set a radius of two pixels on the 2000 x 2000 pixel image and a radius value of one pixel on the 500 x 500 pixel image. A larger value is used for an image that has more pixels. |
| | Threshold | Threshold is a range of contrast that is ignored when the Unsharp Mask filter is applied. It is important so that no "noise" is introduced to an image when this filter is used. The value range is 0-255, which is the number of brightness steps in a grayscale image. 0=black, 128=50% gray and 255=white.<br> For example, a threshold value of 12 ignores slight variations is skin tone brightness to avoid adding noise, but still add edge contrast to areas such as where eyelashes meet skin.<br> For example, if you have a photo of someone's face, the Unsharp Mask affects the parts of the image, such as where eyelashes and skin meet to create an obvious area of contrast, and the smooth skin itself. Even the smoothest skin exhibits subtle changes in brightness values. If you do not use a threshold value, the filter accentuates these subtle changes in skin pixels. In turn, a noisy and undesirable effect is created while contrast on the eyelashes is increased, enhancing sharpness.<br> To avoid this issue, a threshold value is introduced that tells the filter to ignore pixels that do not change contrast dramatically, like smooth skin.<br> In the zipper graphic shown earlier, notice the texture next to the zippers. Image noise is exhibited because the threshold values were too low to suppress the noise. |
| | Monochrome | Select to unsharp-mask image brightness (intensity).<br> Deselect to unsharp-mask each color component separately. |
| Knockout Background | | Automatically removes the background of an image when you upload it. This technique is useful to draw attention to a particular object and make it stand out from a busy background. Select to enable or "turn on" the Knockout Background feature and the following sub-options: |
| | Corner | Required.<br> The corner of the image that is used to define the background color to knockout.<br> You can choose from **Upper Left**, **Bottom Left**, **Upper Right**, or **Bottom Right**. |
| | Fill Method | Required.<br> Controls pixel transparency from the Corner location that you set.<br> You can choose from the following fill methods: <ul><li>**Flood Fill** - turns all pixels transparent that match the Corner that you have specified and are connected to it.</li><li>**Match Pixel** - turns all matching pixels transparent, regardless of their location on the image.</li></ul> |
| | Tolerance | Optional.<br> Controls the allowable amount of variation in pixel color matching based on the Corner location that you set.<br> Use a value of 0.0 to match pixel colors exactly or, use a value of 1.0 to allow for the greatest variation. |
-->

#### PostScript 및 Illustrator 업로드 옵션 설정 {#setting-postscript-and-illustrator-upload-options}

포스트스크립트(EPS) 또는 Illustrator(AI) 이미지 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 파일을 래스터화하고 투명 배경을 유지하며 해상도를 선택하고 색상 공간을 선택할 수 있습니다. PostScript 및 Illustrator 파일 형식 지정 옵션은 [!UICONTROL 업로드 작업 옵션] 아래의 대화 상자 [!UICONTROL PostScript 옵션] 및 [!UICONTROL Illustrator 옵션].

| 옵션 | 하위 선택 | 설명 |
|---|---|---|
| 처리 중 | | 선택 **[!UICONTROL 래스터화]** 를 클릭하여 파일의 벡터 그래픽을 비트맵 형식으로 변환합니다. |
| 렌더링된 이미지에서 투명 배경 유지 | | 파일의 배경 투명도를 유지합니다. |
| 해결 방법 | | 해상도 설정을 결정합니다. 이 설정은 파일의 인치당 표시되는 픽셀 수를 결정합니다. |
| 색상 공간 | | [색상 공간] 메뉴를 선택하고 다음 색상 공간 옵션 중에서 선택합니다. |
| | 자동 감지 | 파일의 색상 공간을 유지합니다. |
| | 강제 RGB | RGB 색상 공간으로 변환합니다. |
| | CMYK로 강제 설정 | CMYK 색상 공간으로 변환합니다. |
| | 회색 음영으로 강제 설정 | 회색 음영 색상 공간으로 변환합니다. |

#### Photoshop 업로드 옵션 설정 {#setting-photoshop-upload-options}

Photoshop 문서(PSD) 파일은 이미지 템플릿을 만드는 데 가장 많이 사용됩니다. PSD 파일을 업로드할 때 파일에서 이미지 템플릿을 자동으로 만들 수 있습니다( [!UICONTROL 템플릿 만들기] 옵션을 선택할 수 있습니다.

Dynamic Media은 파일을 사용하여 템플릿을 만드는 경우 레이어가 있는 PSD 파일에서 여러 이미지를 만듭니다. 각 레이어에 대해 하나의 이미지가 만들어집니다.

사용 [!UICONTROL 자르기 옵션] 및 [!UICONTROL 색상 프로파일 옵션], Photoshop 업로드 옵션 사용.

>[!NOTE]
>
>템플릿은에서 지원되지 않습니다. [!DNL Experience Manager].

| 옵션 | 하위 선택 | 설명 |
|---|---|---|
| 레이어 유지 | | PSD의 레이어(있는 경우)를 개별 에셋으로 분할합니다. 에셋 레이어는 PSD과 연결된 상태로 유지됩니다. 세부 사항 보기의 PSD 파일을 열고 레이어 패널을 선택하여 해당 파일을 볼 수 있습니다. |
| 템플릿 만들기 | | PSD 파일의 레이어로 템플릿을 만듭니다. |
| 텍스트 추출 | | 사용자가 뷰어에서 텍스트를 검색할 수 있도록 텍스트를 추출합니다. |
| 레이어를 배경 크기로 확장 | | 리핑된 이미지 레이어의 크기를 배경 레이어의 크기로 확장합니다. |
| 레이어 이름 지정 | | PSD 파일의 레이어는 별도의 이미지로 업로드됩니다. |
| | 레이어 이름 | PSD 파일에서 해당 레이어 이름 뒤에 이미지 이름을 지정합니다. 예를 들어 원본 PSD 파일에서 Price Tag 라는 이름의 레이어는 Price Tag 라는 이미지가 됩니다. 그러나 PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름(배경, 레이어 1, 레이어 2 등)이면 PSD 파일에서 해당 레이어 번호의 이름을 따서 이미지 이름이 지정됩니다. 기본 레이어 이름 뒤에 이름이 지정되지 않습니다. |
| | Photoshop 및 레이어 번호 | 원래 레이어 이름을 무시하고 PSD 파일에서 레이어 번호 뒤에 이미지 이름을 지정합니다. 이미지 이름은 Photoshop 파일 이름과 추가된 레이어 번호로 지정됩니다. 예를 들어 Spring Ad.psd라는 파일의 두 번째 레이어는 Photoshop에 기본값이 아닌 이름이 있더라도 Spring Ad_2 라는 이름이 지정됩니다. |
| | Photoshop 및 레이어 이름 | PSD 파일 뒤에 레이어 이름 또는 레이어 번호를 붙여서 이미지 이름을 지정합니다. PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름인 경우 레이어 번호가 사용됩니다. 예를 들어 SpringAd라는 PSD 파일에서 Price Tag라는 레이어는 Spring Ad_Price Tag라는 이름으로 지정됩니다. 기본 이름이 Layer 2인 레이어는 Spring Ad_2라고 합니다. |
| 앵커 | | PSD 파일에서 생성된 레이어 컴포지션에서 생성된 템플릿에서 이미지가 고정되는 방식을 지정합니다. 기본적으로 앵커는 가운데입니다. 가운데 앵커를 사용하면 대체 이미지의 종횡비에 관계없이 대체 이미지가 동일한 공간을 가장 잘 채울 수 있습니다. 템플릿을 참조하고 매개 변수 대체를 사용할 때 이 이미지를 대체하는 다른 양상의 이미지가 동일한 공간을 효과적으로 차지합니다. 템플릿에서 할당된 공간을 채우기 위해 응용 프로그램에 교체 이미지가 필요한 경우 다른 설정으로 변경합니다. |

#### PDF 업로드 옵션 설정 {#setting-pdf-upload-options}

PDF 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 페이지를 자르고, 검색어를 추출하고, 인치당 픽셀 수 해상도를 입력하고, 색상 공간을 선택합니다. PDF 파일에는 종종 트림 여백, 자르기 표시, 등록 표시 및 기타 프린터 표시가 들어 있습니다. PDF 파일을 업로드할 때 페이지 양쪽에서 이러한 표시를 자를 수 있습니다.

추출을 위해 고려되는 PDF의 최대 페이지 수는 새 업로드의 경우 5000페이지입니다. 이 제한은 2022년 12월 31일에 100페이지(모든 PDF에 대해)로 변경됩니다. 참조: [Dynamic Media 제한 사항](/help/assets/limitations.md).

>[!NOTE]
>
>전자 카탈로그는 다음에서 지원되지 않습니다. [!DNL Experience Manager].

다음 옵션 중에서 선택합니다.

| 옵션 | 하위 선택 | 설명 |
|---|---|---|
| 처리 중 | 래스터화 | (기본값) PDF 파일의 페이지를 리핑하고 벡터 그래픽을 비트맵 이미지로 변환합니다. eCatalog를 만들려면 이 옵션을 선택합니다. |
| 추출 | 단어 검색 | eCatalog 뷰어에서 키워드로 파일을 검색할 수 있도록 PDF 파일에서 단어를 추출합니다. |
| | 링크 | PDF 파일에서 링크를 추출하여 eCatalog 뷰어에서 사용되는 이미지 맵으로 변환합니다. |
| 여러 페이지 PDF에서 eCatalog 자동 생성 | | PDF 파일에서 eCatalog를 자동으로 만듭니다. eCatalog의 이름은 업로드한 PDF 파일의 이름을 따릅니다. 이 옵션은 PDF 파일을 업로드할 때 래스터화하는 경우에만 사용할 수 있습니다. |
| 해결 방법 | | 해상도 설정을 결정합니다. 이 설정은 PDF 파일에서 인치당 표시되는 픽셀 수를 결정합니다. 기본값은 150입니다. |
| 색상 공간 | | [색상 공간] 메뉴를 선택하고 PDF 파일에 사용할 색상 공간을 선택합니다. 대부분의 PDF 파일에는 RGB 이미지와 CMYK 색상 이미지가 모두 있습니다. RGB 색상 공간은 온라인 보기에 바람직하다. |
| | 자동 감지 | PDF 파일의 색상 공간을 유지합니다. |
| | RGB로 강제 실행 | RGB 색상 공간으로 변환합니다. |
| | CMYK로 강제 실행 | CMYK 색상 공간으로 변환합니다. |
| | 회색 음영으로 강제 실행 | 회색 음영 색상 공간으로 변환합니다. |

#### eVideo 업로드 옵션 설정 {#setting-evideo-upload-options}

다양한 비디오 사전 설정에서 선택하여 비디오 파일을 변환하려면 다음과 같이 하십시오.

| 옵션 | 하위 선택 | 설명 |
|---|---|---|
| 응용 비디오 | | 모바일, 태블릿 및 데스크톱에 전송할 비디오를 만드는 데 모든 종횡비에 작동하는 단일 인코딩 사전 설정입니다. 이 사전 설정으로 인코딩된 업로드된 소스 비디오는 고정된 높이로 설정됩니다. 그러나 비디오의 종횡비를 유지하기 위해 너비가 자동으로 조절됩니다. <br>가장 좋은 방법은 응용 비디오 인코딩을 사용하는 것입니다. |
| 단일 인코딩 사전 설정 | 인코딩 사전 설정 정렬 | 선택 **[!UICONTROL 이름]** 또는 **[!UICONTROL 크기]** 데스크탑, 모바일 및 태블릿 아래에 나열된 인코딩 사전 설정을 이름 또는 해상도 크기별로 정렬하려는 경우 |
| | 데스크탑 | 데스크탑 컴퓨터에 스트리밍 또는 점진적 비디오 경험을 제공하기 위한 MP4 파일을 만듭니다. 원하는 해상도 크기 및 타겟 데이터 속도를 사용하여 하나 이상의 종횡비를 선택합니다. |
| | 모바일 | iPhone 또는 Android™ 모바일 장치에서 전송할 MP4 파일을 만듭니다. 원하는 해상도 크기 및 타겟 데이터 속도를 사용하여 하나 이상의 종횡비를 선택합니다. |
| | 태블릿 | iPad 또는 Android™ 태블릿 디바이스에서 전송할 MP4 파일을 만듭니다. 원하는 해상도 크기 및 타겟 데이터 속도를 사용하여 하나 이상의 종횡비를 선택합니다. |

#### 업로드 시 일괄처리 집합 사전 설정 설정 설정 {#setting-batch-set-presets-at-upload}

업로드된 이미지에서 이미지 세트 또는 회전 세트를 자동으로 만들려면 사용할 사전 설정의 활성 열을 클릭합니다. 두 개 이상의 사전 설정을 선택할 수 있습니다.

다음을 참조하십시오 [이미지 세트 및 스핀 세트를 자동으로 생성하도록 일괄처리 집합 사전 설정 구성](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 일괄 처리 집합 사전 설정 만들기에 대해 자세히 알아보십시오.

### 스트리밍된 업로드 {#streamed-uploads}

Adobe Experience Manager에 많은 에셋을 업로드하는 경우 서버에 대한 I/O 요청이 크게 증가하므로 업로드 효율성이 떨어지고 일부 업로드 작업이 시간 초과될 수도 있습니다. [!DNL Experience Manager Assets] 는 에셋 스트리밍을 지원합니다. 스트리밍된 업로드는 저장소에 복사하기 전에 서버의 임시 폴더에 있는 자산 저장소를 방지하여 업로드 작업 중 디스크 I/O를 줄입니다. 대신 데이터가 저장소로 직접 전송됩니다. 이렇게 하면 큰 에셋을 업로드하는 시간과 시간 초과가 줄어들 수 있습니다. 스트리밍된 업로드는에서 기본적으로 활성화됩니다. [!DNL Assets].

>[!NOTE]
>
>3.1 미만의 서블릿 API 버전을 사용하는 JEE 서버에서 실행 중인 Adobe Experience Manager에 대해 스트리밍 업로드가 비활성화되었습니다.

### 자산이 포함된 ZIP 아카이브 추출 {#extractzip}

지원되는 다른 에셋과 마찬가지로 ZIP 아카이브를 업로드할 수 있습니다. 동일한 파일 이름 규칙이 ZIP 파일에 적용됩니다. [!DNL Experience Manager] DAM 위치에 ZIP 아카이브를 추출할 수 있습니다. 아카이브 파일의 확장명에 ZIP이 포함되어 있지 않은 경우 컨텐츠를 사용하여 파일 유형 검색을 활성화합니다.

한 번에 하나의 ZIP 아카이브를 선택하고 **[!UICONTROL 아카이브 추출]**&#x200B;을 클릭하고 대상 폴더를 선택합니다. 충돌(있는 경우)을 처리할 옵션을 선택합니다. ZIP 파일의 에셋이 대상 폴더에 있는 경우 다음 옵션 중 하나를 선택할 수 있습니다. 추출 건너뛰기, 기존 파일 바꾸기, 두 에셋 모두 이름 바꾸기로 유지 또는 버전 만들기.

추출이 완료되면, [!DNL Experience Manager] 알림이 알림 영역에서 표시됩니다. While [!DNL Experience Manager] zip을 추출하므로 추출을 중단하지 않고 작업으로 돌아갈 수 있습니다.

![ZIP 파일 추출 알림](assets/Zip-extraction-notification.png)

이 기능의 몇 가지 제한 사항은 다음과 같습니다.

* 대상에 동일한 이름의 폴더가 있는 경우 ZIP 파일의 에셋이 기존 폴더에서 추출됩니다.
* 추출을 취소하면 이미 추출한 에셋이 삭제되지 않습니다.
* 두 개의 ZIP 파일을 동시에 선택하고 추출할 수 없습니다. ZIP 아카이브를 한 번에 하나만 추출할 수 있습니다.
* ZIP 아카이브를 업로드할 때 업로드 대화 상자에 500 서버 오류가 표시되면 설치 후 다시 시도하십시오 [최신 서비스 팩](/help/release-notes/release-notes.md).

## 자산 미리보기 {#previewing-assets}

에셋을 미리 보려면 다음 단계를 수행합니다.

1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 미리 보려는 에셋의 위치로 이동합니다.
1. 원하는 자산을 클릭하여 열 수 있습니다.

1. 미리보기 모드에서 다음에 대한 확대/축소 옵션을 사용할 수 있습니다. [지원되는 이미지 유형](/help/assets/assets-formats.md#supported-raster-image-formats) (대화형 편집 사용).

   자산을 확대하려면 `+` (또는 에셋의 돋보기를 클릭합니다). 축소하려면 `-`. 확대하면 패닝으로 이미지의 모든 영역을 자세히 볼 수 있습니다. 확대/축소 재설정 화살표를 사용하면 원래 보기로 돌아갑니다. 뷰를 원래 크기로 재설정하려면 를 클릭합니다 **[!UICONTROL 재설정]** ![보기 재설정](assets/do-not-localize/revert.png).

**키보드 키만 사용하여 에셋 미리보기**

키보드를 사용하여 에셋을 미리 보려면 다음 단계를 수행합니다.

1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 를 사용하여 원하는 에셋으로 이동합니다. `Tab` 화살표 키를 사용합니다.

1. 누르기 `Enter` 를 클릭하여 자산을 열 수 있습니다. 미리보기 모드에서 에셋을 확대할 수 있습니다.

1. 자산을 확대하려면 다음 작업을 수행하십시오.
   1. 사용 `Tab` 확대 옵션으로 포커스를 이동하는 키입니다.
   1. 사용 `Enter` 이미지를 확대하는 키입니다.

   축소하려면 `Tab` 키를 눌러 축소 옵션에 포커스를 두고 키를 누릅니다. `Enter`.

1. 사용 `Shift` + `Tab` 이미지에서 포커스를 다시 이동하는 키입니다.

1. 확대/축소된 이미지 주위로 이동하려면 화살표 키를 사용합니다.

>[!MORELIKETHIS]
>
>* [Dynamic Media 에셋 미리보기](/help/assets/previewing-assets.md).
>* [하위 자산 보기](managing-linked-subassets.md#viewing-subassets).

## 속성 및 메타데이터 편집 {#editing-properties}

1. 편집할 메타데이터가 있는 에셋의 위치로 이동합니다.

1. 에셋을 선택한 다음 도구 모음에서 를 선택합니다. **[!UICONTROL 속성]** 에셋의 속성을 볼 수 있습니다. 또는 **[!UICONTROL 속성]** 에셋 카드에 대한 빠른 작업

   ![자산 카드 보기의 속성 빠른 작업](assets/properties_quickaction.png)

1. 다음에서 [!UICONTROL 속성] 페이지를 만들고 다양한 탭에서 메타데이터 속성을 편집합니다. 예를 들어 **[!UICONTROL 기본]** 탭에서 제목과 설명을 편집합니다.

   >[!NOTE]
   >
   >의 레이아웃 [!UICONTROL 속성] 페이지 및 사용 가능한 메타데이터 속성은 기본 메타데이터 스키마에 따라 다릅니다. 의 레이아웃을 수정하는 방법을 알아보려면 [!UICONTROL 속성] 페이지, 참조 [메타데이터 스키마](/help/assets/metadata-schemas.md).

1. To schedule a particular date/time for the activation of the asset, use the date picker beside the **[!UICONTROL On Time]** field.

   ![날짜 시간 선택기 또는 설정 시간 필드의 키보드 키를 사용하여 자산 활성화 날짜 및 시간을 추가합니다.](assets/datepicker.png)

   *그림: 날짜 선택기를 사용하여 자산 활성화를 예약합니다.*

1. 확인 **[!UICONTROL 설정/해제 시간 도달]** 메타데이터 속성에서 복제 에이전트 트리거를 업데이트하려는 경우 옵션입니다.
   ![에이전트 설정](assets-dm/Agent-settings.png)

1. 특정 기간 후에 에셋을 비활성화하려면 옆에 있는 날짜 선택기에서 비활성화 날짜/시간을 선택합니다. **[!UICONTROL 해제 시간]** 필드. 비활성화 날짜는 에셋의 활성화 날짜 이후여야 합니다. 다음 이후 [!UICONTROL 해제 시간], 에셋 및 해당 렌디션은 [!DNL Assets] 웹 인터페이스 또는 HTTP API를 통해.

1. 다음에서 **[!UICONTROL 태그]** 필드에서 태그를 하나 이상 선택합니다. 사용자 지정 태그를 추가하려면 상자에 태그의 이름을 입력하고 를 선택합니다 `Enter`. 새 태그는에 저장됩니다. [!DNL Experience Manager]. [!DNL YouTube] 게시하려면 태그가 필요합니다. 다음을 참조하십시오 [YouTube에 비디오 게시](video.md#publishing-videos-to-youtube).

   >[!NOTE]
   >
   >태그를 만들려면 다음 위치에 쓰기 권한이 있어야 합니다. `/content/cq:tags/default` CRX 저장소에서

1. 자산에 등급을 지정하려면 **[!UICONTROL 고급]** 탭을 클릭한 다음 적절한 위치에서 별 을 클릭하여 원하는 등급을 지정합니다.

   ![등급 할당을 위한 자산 속성의 고급 탭](assets/ratings.png)

   에셋에 지정하는 등급 점수는 아래에 표시됩니다 **[!UICONTROL 등급]**. 에셋을 평가한 사용자로부터 에셋이 받은 평균 등급 점수는 아래에 표시됩니다 **[!UICONTROL 등급]**. 또한 평균 등급 점수에 기여하는 등급 점수의 구분이 아래에 표시됩니다. **[!UICONTROL 등급 분류]**. 평균 등급 점수에 따라 에셋을 검색할 수 있습니다.

1. 에셋에 대한 사용 통계를 보려면 **[!UICONTROL Insights]** 탭.

   사용 통계에는 다음이 포함됩니다.

   * 에셋을 보거나 다운로드한 횟수
   * 에셋이 사용된 채널/디바이스
   * 자산이 최근에 사용된 크리에이티브 솔루션

   자세한 내용은 [Assets Insights](/help/assets/asset-insights.md).

1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.
1. 다음 위치로 이동 [!DNL Assets] 사용자 인터페이스. 제목, 설명, 등급 등을 포함하여 편집된 메타데이터 속성은 카드 보기의 자산 카드와 목록 보기의 관련 열에 표시됩니다.

## 에셋 복사 {#copying-assets}

에셋 또는 폴더를 복사하면 전체 에셋 또는 폴더가 콘텐츠 구조와 함께 복사됩니다. 복사한 에셋 또는 폴더가 대상 위치에 복제됩니다. 소스 위치의 자산은 변경되지 않습니다.

에셋의 특정 사본에 고유한 몇 가지 속성은 이월되지 않습니다. 몇 가지 예는 다음과 같습니다.

* 에셋 ID, 생성 날짜 및 시간, 버전 및 버전 내역. 이러한 속성 중 일부는 속성으로 표시됩니다. `jcr:uuid`, `jcr:created`, 및 `cq:name`.

* 작성 시간 및 참조된 경로는 각 에셋과 각 에셋의 렌디션에 대해 고유합니다.

다른 속성 및 메타데이터 정보는 유지됩니다. 에셋을 복사할 때에는 부분 복사본이 만들어지지 않습니다.

1. 위치 [!DNL Assets] 인터페이스에서 하나 이상의 에셋을 선택하고 **[!UICONTROL 복사]** 을 클릭합니다. 또는 **[!UICONTROL 복사]** ![자산 인터페이스의 도구 모음에서 복사 옵션](assets/do-not-localize/copy_icon.png) 자산 카드의 빠른 작업

   >[!NOTE]
   >
   >를 사용하는 경우 [!UICONTROL 복사] 빠른 작업: 한 번에 하나의 에셋만 복사할 수 있습니다.

1. 에셋을 복사할 위치로 이동합니다.

   >[!NOTE]
   >
   >동일한 위치에서 에셋을 복사하는 경우 [!DNL Experience Manager] 는 이름의 변형을 자동으로 생성합니다. 예를 들어 이라는 에셋을 복사하는 경우 `Square`, [!DNL Experience Manager] 는 사본에 대한 제목을 다음과 같이 자동 생성합니다. `Square1`.

1. 다음을 클릭합니다. **[!UICONTROL 붙여넣기]** ![자산 도구 모음의 붙여넣기 옵션](assets/do-not-localize/paste.png) 도구 모음의 에셋 옵션 그런 다음 자산이 이 위치에 복사됩니다.

   >[!NOTE]
   >
   >다음 **[!UICONTROL 붙여넣기]** 붙여넣기 작업이 완료될 때까지 도구 모음에서 옵션을 사용할 수 있습니다.

## 에셋 이동 및 이름 바꾸기 {#moving-or-renaming-assets}

에셋(또는 폴더)을 다른 위치로 이동하면 에셋을 복사하는 동안과 달리 에셋(또는 폴더)이 복제되지 않습니다. 에셋(또는 폴더)은 대상 위치에 배치되고 소스 위치에서 제거됩니다. 에셋을 새 위치로 이동할 때 에셋의 이름을 변경할 수도 있습니다.
게시된 에셋을 다른 위치로 이동하는 경우 에셋을 선택적으로 다시 게시할 수 있습니다. 기본적으로 게시된 에셋에 대한 이동 작업은 게시 취소됩니다. 작성자가 자산을 선택하면 이동된 자산이 다시 게시됩니다. [!UICONTROL 다시 게시] 자산을 이동할 때 옵션을 선택합니다.

![자산을 이동할 때 이미 게시된 자산을 다시 게시할 수 있습니다](assets/republish-on-move.png)

에셋 또는 폴더를 이동하려면 다음을 수행합니다.

1. 이동할 자산의 위치로 이동합니다.

1. 에셋을 선택하고 **[!UICONTROL 이동]** 도구 모음의 옵션입니다.
   ![자산 도구 모음의 이동 옵션](assets/do-not-localize/move.png)

1. 다음에서 [!UICONTROL 자산 이동] 마법사에서 다음 중 하나를 수행합니다.

   * 에셋을 이동한 후 에셋의 이름을 지정합니다. 그런 다음 **[!UICONTROL 다음]** 계속합니다.

   * 클릭 **[!UICONTROL 취소]** 프로세스를 중지합니다.

   >[!NOTE]
   >
   >* 새 위치에 해당 이름을 가진 에셋이 없는 경우 에셋에 동일한 이름을 지정할 수 있습니다. 그러나 에셋을 같은 이름의 에셋이 있는 위치로 이동하는 경우에는 다른 이름을 사용해야 합니다. 동일한 이름을 사용하는 경우 이름 변형이 자동으로 생성됩니다. 예를 들어 에셋의 이름이 Square인 경우 시스템에서는 해당 복사본에 대한 이름 Square1을 생성합니다.
   >* 이름을 바꿀 때 파일 이름에 공백이 허용되지 않습니다.

1. 다음에서 **[!UICONTROL 대상 선택]** 대화 상자에서 다음 중 하나를 수행합니다.

   * 에셋의 새 위치로 이동한 다음 **[!UICONTROL 다음]** 계속합니다.

   * 클릭 **[!UICONTROL 뒤로]** (으)로 돌아가기 **[!UICONTROL 이름 바꾸기]** 화면.

1. 이동하는 에셋에 참조하는 페이지, 에셋 또는 컬렉션이 있는 경우 **[!UICONTROL 참조 조정]** 탭 옆에 표시 **[!UICONTROL 대상 선택]** 탭.

   다음 중 하나를 수행합니다. **[!UICONTROL 참조 조정]** 화면:

   * 새 세부 정보를 기반으로 조정할 참조를 지정한 다음 을 클릭합니다 **[!UICONTROL 이동]** 계속합니다.

   * 다음에서 **[!UICONTROL 조정]** 열에서 에셋에 대한 참조를 선택/선택 취소합니다.
   * 클릭 **[!UICONTROL 뒤로]** (으)로 돌아가기 **[!UICONTROL 대상 선택]** 화면.

   * 클릭 **[!UICONTROL 취소]** 이동 작업을 중지합니다.

   참조를 업데이트하지 않으면 계속해서 자산의 이전 경로를 가리킵니다. 참조를 조정하면 새 에셋 경로로 업데이트됩니다.

### 드래그 작업을 사용하여 에셋 이동 {#move-using-drag}

를 사용하지 않고 자산(또는 폴더)을 대상 위치로 끌어 동위 폴더로 이동할 수 있습니다. [!UICONTROL 이동] 사용자 인터페이스의 옵션입니다. 그러나 이 작업은 목록 보기에서만 수행할 수 있습니다.

자산을 드래그하여 이동하는 것은 열리지 않습니다 [!UICONTROL 자산 이동] 따라서 이동하는 동안 에셋의 이름을 변경하는 옵션이 제공되지 않습니다. 또한 이미 게시된 에셋은 다시 게시하기 위해 사용자의 승인을 구하지 않고, 드래그하여 이동할 때 다시 게시됩니다.

![자산을 끌어 동위 폴더로 자산 이동](assets/move-by-drag.gif)

## 렌디션 관리 {#managing-renditions}

1. 원본을 제외한 에셋에 대한 렌디션을 추가하거나 제거할 수 있습니다. 렌디션을 추가하거나 제거할 에셋의 위치로 이동합니다.

1. 페이지를 열 자산을 클릭합니다.
1. Experience Manager 인터페이스에서 를 선택합니다. **[!UICONTROL 표현물]** 목록에서 삭제할 수 있습니다.
1. 다음에서 **[!UICONTROL 표현물]** 패널, 에셋에 대해 생성된 렌디션 목록을 봅니다.

   ![자산 세부 사항 페이지의 렌디션 패널](assets/renditions_panel.png)

   >[!NOTE]
   >
   >기본적으로, [!DNL Assets] 미리 보기 모드에서 에셋의 원본 렌디션을 표시하지 않습니다. 관리자는 오버레이를 사용하여 를 구성할 수 있습니다 [!DNL Assets] 미리보기 모드에서 원본 렌디션을 표시하려면

1. 렌디션을 보거나 삭제하려면 렌디션을 선택합니다.

   **렌디션 삭제**

   에서 렌디션 선택 **[!UICONTROL 표현물]** 패널을 클릭한 다음 **[!UICONTROL 렌디션 삭제]** ![렌디션 삭제 옵션](assets/do-not-localize/deleteoutline.png) 도구 모음의 옵션입니다. 에셋 처리가 완료된 후에는 렌디션을 일괄적으로 삭제할 수 없습니다. 개별 에셋의 경우 사용자 인터페이스에서 렌디션을 수동으로 제거할 수 있습니다. 여러 에셋의 경우 Experience Manager을 사용자 정의하여 특정 렌디션을 삭제하거나 에셋을 삭제하고 삭제된 에셋을 다시 업로드할 수 있습니다.

   **새 렌디션 업로드**

   에셋에 대한 에셋 세부 사항 페이지로 이동하고 **[!UICONTROL 렌디션 추가]** ![새 렌디션을 업로드하기 위한 렌디션 추가 옵션](assets/do-not-localize/add.png) 옵션을 사용하여 에셋에 대한 새 렌디션을 업로드할 수 있습니다.

   >[!NOTE]
   >
   >If you select a rendition from the **[!UICONTROL Renditions]** panel, the toolbar changes context and displays only those actions that are relevant to the rendition. 다음과 같은 옵션 [!UICONTROL 렌디션 업로드] 옵션이 표시되지 않습니다. To view these options in the toolbar, navigate to the details page for the asset.

   이미지 또는 비디오 에셋의 세부 사항 페이지에 표시할 렌디션의 차원을 구성할 수 있습니다. 지정한 차원에 따라, [!DNL Assets] 은 정확한 또는 가장 가까운 치수의 렌디션을 표시합니다.

   To configure rendition dimensions of an image at the asset detail level, overlay the `renditionpicker` node (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) and configure the value of the width property. 속성 구성 **[!UICONTROL 크기(길이)(KB)]** 이미지 크기에 따라 에셋 세부 사항 페이지에서 렌디션을 사용자 지정할 수 있도록 폭 대신 사용됩니다. For size-based customization, the property `preferOriginal` assigns preference to the original if the size of the matched rendition is greater than the original.

   마찬가지로 오버레이하여 주석 페이지 이미지를 사용자 정의할 수 있습니다 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![CRXDE의 오버레이 변환선택기 노드를 사용하여 주석 페이지 이미지 사용자 지정](assets/renditionpicker-node.png)

   비디오 에셋에 대한 렌디션 차원을 구성하려면 다음 위치로 이동합니다. `videopicker` 위치에 있는 CRX 저장소의 노드 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`를 클릭하고 노드를 오버레이한 다음 적절한 속성을 편집합니다.

   >[!NOTE]
   >
   >비디오 주석은 HTML 5와 호환되는 비디오 형식이 있는 브라우저에서만 지원됩니다. 또한 브라우저에 따라 서로 다른 비디오 형식이 지원됩니다. 그러나 MXF 비디오 포맷은 비디오 주석에서 아직 지원되지 않습니다.

하위 자산 생성 및 보기에 대한 자세한 내용은 [하위 자산 관리](managing-linked-subassets.md#generate-subassets).

## 에셋 삭제 {#deleting-assets}

에셋을 삭제하려면 다음에 대한 삭제 권한이 필요합니다. `dam/asset`. 수정 권한만 있는 경우 에셋 메타데이터를 편집하고 에셋에 주석을 추가할 수 있습니다. 그러나 에셋 또는 에셋의 메타데이터는 삭제할 수 없습니다.

다른 페이지에서 들어오는 참조를 확인하거나 제거하려면 에셋을 삭제하기 전에 관련 참조를 업데이트하십시오. 사용자가 참조된 에셋을 삭제하고 끊어진 링크를 남기지 못하도록 하려면 오버레이를 사용하여 강제 삭제 옵션을 비활성화하십시오.

에셋 또는 에셋이 포함된 폴더를 삭제하려면

1. 삭제할 에셋 또는 폴더의 위치로 이동합니다.

1. 에셋 또는 폴더를 선택하고 **[!UICONTROL 삭제]** ![옵션 삭제](assets/do-not-localize/deleteoutline.png) 을 클릭합니다.

   삭제를 확인하면:

   * 에셋에 참조가 없으면 에셋이 삭제됩니다.

   * 에셋에 참조가 있을 경우 오류 메시지에 **하나 이상의 에셋이 참조됨**. 다음을 선택할 수 있습니다. **[!UICONTROL 강제 삭제]** 또는 **[!UICONTROL 취소]**.

   >[!NOTE]
   >
   >* 다른 페이지에서 들어오는 참조를 확인하거나 제거하려면 에셋을 삭제하기 전에 관련 참조를 업데이트하십시오. 또한, 오버레이를 사용하여 강제 삭제 옵션을 비활성화하여, 사용자가 참조된 자산을 삭제하고 끊어진 링크를 남기지 못하도록 할 수 있습니다.
   >* 을(를) 삭제할 수 있습니다 *폴더* 체크 아웃된 에셋 파일이 들어 있습니다. 폴더를 삭제하기 전에 사용자가 디지털 자산을 체크아웃하지 않았는지 확인하십시오.

>[!NOTE]
>
>사용자 인터페이스에서 위의 방법을 사용하여 폴더를 삭제하면 연결된 사용자 그룹도 삭제됩니다.
>
>그러나 기존의 중복, 미사용 및 자동 생성된 사용자 그룹은 다음을 사용하여 저장소에서 정리할 수 있습니다. `clean` 작성자 인스턴스의 JMX에 있는 메서드(`https://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).

## 자산 다운로드 {#downloading-assets}

다음을 참조하십시오 [Experience Manager에서 에셋 다운로드](/help/assets/download-assets-from-aem.md).

## 자산 게시 또는 게시 취소 {#publish-assets}

에셋을에 업로드, 처리 또는 편집한 후 [!DNL Experience Manager] 작성자는 자산을 게시 서버에 게시합니다. 게시를 통해 자산을 공개적으로 사용할 수 있습니다. 게시 취소 작업으로 게시 서버에서 자산이 제거되었지만 작성 서버에서는 제거되지 않았습니다.

관련 정보의 경우 [!DNL Dynamic Media], 참조 [게시 [!DNL Dynamic Media] assets](/help/assets/publishing-dynamicmedia-assets.md).

1. 게시하거나 게시 환경에서 제거하려는(게시 취소) 에셋 또는 에셋 폴더의 위치로 이동합니다.

1. 게시를 취소할 에셋 또는 폴더를 선택하고 **[!UICONTROL 게시 관리]** ![게시 관리 옵션](assets/do-not-localize/globe-publication.png) 도구 모음의 옵션입니다. 또는 빠르게 게시하려면 **[!UICONTROL 빠른 게시]** 도구 모음의 옵션입니다. 게시하려는 폴더에 빈 폴더가 포함되어 있으면 빈 폴더는 게시되지 않습니다.

1. 다음 항목 선택 **[!UICONTROL 게시]** 또는 **[!UICONTROL 게시 취소]** 필요에 따라 옵션을 선택합니다.

   ![게시 취소 작업](assets/unpublish_action.png)
   *그림: 게시 및 게시 취소 옵션과 예약 옵션*

1. 선택 **[!UICONTROL 지금]** 자산을 즉시 처리하거나 **[!UICONTROL 나중에]** 을 클릭하여 작업을 예약합니다. 다음을 선택하는 경우 날짜 및 시간 선택 **[!UICONTROL 나중에]** 옵션을 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. 게시할 때 에셋이 다른 에셋을 참조하는 경우 해당 참조가 마법사에 나열됩니다. 마지막 게시 이후 게시가 취소되거나 수정된 참조만 표시됩니다. 게시하려는 참조를 선택합니다.

1. 게시를 취소할 때 에셋이 다른 에셋을 참조하는 경우 게시를 취소할 참조를 선택합니다. **[!UICONTROL 게시 취소]**&#x200B;를 클릭합니다. 확인 대화 상자에서 **[!UICONTROL 취소]** 작업을 중지하려면 **[!UICONTROL 게시 취소]** 지정된 날짜에 에셋의 게시가 취소되는지 확인합니다.

에셋 또는 폴더 게시 또는 게시 취소와 관련된 다음 제한 사항 및 팁을 이해합니다.

* 다음에 대한 옵션: [!UICONTROL 게시 관리] 복제 권한이 있는 사용자 계정만 사용할 수 있습니다.
* 복잡한 에셋의 게시를 취소하는 동안 에셋만 게시 취소합니다. 게시된 다른 에셋에서 참조할 수 있으므로 참조 게시를 취소하지 마십시오.
* 빈 폴더는 게시되지 않습니다.
* 처리 중인 자산을 게시하는 경우 원래 콘텐츠만 게시됩니다. 렌디션이 누락되었습니다. 처리가 완료될 때까지 기다린 다음 처리가 완료되면 자산을 게시하거나 다시 게시합니다.

## 폐쇄된 사용자 그룹 {#closed-user-group}

CUG(폐쇄형 사용자 그룹)는에서 게시된 특정 에셋 폴더에 대한 액세스를 제한하는 데 사용됩니다 [!DNL Experience Manager]. 폴더에 대한 CUG를 생성하는 경우 폴더(폴더 에셋 및 하위 폴더 포함)에 대한 액세스는 할당된 구성원 또는 그룹으로만 제한됩니다. 폴더에 액세스하려면 보안 자격 증명을 사용하여 로그인해야 합니다.

CUG는 자산에 대한 액세스를 제한하는 추가 방법입니다. 폴더의 로그인 페이지를 구성할 수도 있습니다.

1. 에서 폴더 선택 [!DNL Assets] 인터페이스를 클릭하고 [!UICONTROL 속성] 속성 페이지를 표시할 수 있도록 도구 모음에서 옵션을 선택합니다.
1. 다음에서 **[!UICONTROL 권한]** 탭, 아래에 구성원 또는 그룹 추가 **[!UICONTROL 폐쇄된 사용자 그룹]**.

   ![폐쇄된 사용자 그룹에 사용자 추가](assets/add_user.png)

1. 사용자가 폴더에 액세스할 때 로그인 화면을 표시하려면 **[!UICONTROL 사용]** 옵션을 선택합니다. 그런 다음 의 로그인 페이지 경로를 선택합니다 [!DNL Experience Manager]을 클릭하고 변경 내용을 저장합니다.

   ![사용자가 폴더에 액세스할 때 표시할 로그인 페이지를 활성화하고 선택합니다.](assets/login_page.png)

   >[!NOTE]
   >
   >로그인 페이지 경로를 지정하지 않으면 [!DNL Experience Manager] 게시 인스턴스에 기본 로그인 페이지를 표시합니다.

1. 폴더를 게시한 다음 게시 인스턴스에서 액세스해 보십시오. 로그인 화면이 표시됩니다.
1. CUG 멤버인 경우 보안 인증서를 입력합니다. 다음 뒤에 폴더가 표시됩니다. [!DNL Experience Manager] 인증.

## 자산 검색 {#assetsearch}

자산 검색은 디지털 자산 관리 시스템 사용의 중심입니다. 이 기능은 광고, 비즈니스 사용자 및 마케터의 강력한 자산 관리 또는 DAM 관리자의 관리에 중요합니다.

가장 적절한 에셋을 검색하고 사용하기 위한 간단한 고급 사용자 지정 검색에 대해서는 [Experience Manager에서 에셋 검색](search-assets.md).

## 빠른 작업 {#quick-actions}

빠른 작업 아이콘은 한 번에 하나의 에셋에 사용할 수 있습니다. 장치에 따라 다음 작업을 수행하여 빠른 작업 아이콘을 표시합니다.

* 터치 장치: 터치 및 홀드. 예를 들어 iPad에서 빠른 작업이 표시되도록 자산을 선택하고 유지할 수 있습니다.
* 비-터치 장치: 마우스 포인터. 예를 들어 데스크탑 디바이스에서 포인터를 자산 썸네일 위에 두면 빠른 작업 표시줄이 표시됩니다.

### 에셋 탐색 및 선택 {#navigating-and-selecting-assets}

를 사용하여 사용 가능한 보기(카드, 열 및 목록)가 있는 에셋을 보고, 탐색하고, 선택할 수 있습니다. **[!UICONTROL 선택]** 옵션을 선택합니다.

목록 보기 및 열 보기에서 **[!UICONTROL 선택]** 자산 썸네일 위로 포인터를 가져가면 옵션이 표시됩니다.

카드 보기에서 **[!UICONTROL 선택]** 옵션은 빠른 작업으로 표시됩니다.

에서 폴더 또는 컬렉션을 탐색할 때 [!DNL Assets] 사용자 인터페이스 브라우저에서 다음을 사용하여 표시되거나 로드된 모든 에셋을 선택할 수 있습니다. [!UICONTROL 모두 선택] 오른쪽 상단의 옵션입니다. 처음에는 100개의 자산만 카드 보기에 로드되고 200개의 자산만 목록 보기에 로드됩니다. 검색 결과 페이지를 스크롤할 때 더 많은 에셋이 뷰에 로드됩니다. 다음 [!UICONTROL 모두 선택] 옵션은 로드된 에셋만 선택합니다.

자세한 내용은 [리소스 보기 및 선택](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

## 이미지 편집 {#editing-images}

의 편집 도구 [!DNL Assets] 인터페이스를 사용하면 이미지 에셋에서 소규모 편집 작업을 수행할 수 있습니다. 이미지에 대해 자르기, 회전, 뒤집기 및 기타 편집 작업을 수행할 수 있습니다. 이미지 맵을 에셋에 추가할 수도 있습니다.

>[!NOTE]
>
>일부 구성 요소의 경우 전체 화면 모드에 사용 가능한 추가 옵션이 있습니다.

1. 다음 중 하나를 수행하여 자산을 편집 모드로 엽니다.

   * 에셋을 선택한 다음 를 클릭합니다 **[!UICONTROL 편집]** 을 클릭합니다.
   * 클릭 **[!UICONTROL 편집]** 카드 보기의 자산에 표시되는 옵션입니다.
   * 클릭 **[!UICONTROL 편집]** 도구 모음에서 ![도구 모음의 편집 옵션](assets/do-not-localize/edit_icon.png).

1. 이미지를 자르려면 **[!UICONTROL 자르기]** ![이미지 자르기 옵션](assets/do-not-localize/crop.png).

1. Select the desired option from the list. 자르기 영역은 선택한 옵션에 따라 이미지에 나타납니다. The **Free Hand** option lets you crop the image without any aspect ratio restrictions.

1. 자를 영역을 선택하고 이미지에서 크기를 조정하거나 위치를 변경합니다.

1. 사용 **[!UICONTROL 실행 취소]** ![도구 모음 옵션 실행 취소](assets/do-not-localize/undo.png) 및 **[!UICONTROL 다시 실행]** ![다시 실행 도구 모음 옵션](assets/do-not-localize/redo.png) 옵션을 사용하여 자르지 않은 이미지로 되돌리거나 자른 이미지를 각각 유지합니다.
1. 적절한 을(를) 클릭합니다 **[!UICONTROL 회전]** 이미지를 시계 방향으로 또는 반 시계 방향으로 회전하는 옵션입니다.

   ![시계 방향 및 반시계 방향 회전 옵션](assets/do-not-localize/rotate-options.png)

1. 적절한 을(를) 클릭합니다 **[!UICONTROL 뒤집기]** 이미지를 가로로 뒤집으려면 옵션을 선택합니다 ![수평 반사 옵션](assets/do-not-localize/flip-horizontal.png) 또는 세로로 ![수직 반사 옵션](assets/do-not-localize/flip-vertical.png).

1. 이미지 편집을 완료하려면 **[!UICONTROL 완료]** ![마침 옵션](assets/do-not-localize/check-ok-done-icon.png). 클릭 **완료** 또한 렌디션의 재생성도 시작합니다.

>[!NOTE]
>
>이미지 편집은 BMP, GIF, PNG 및 JPEG 파일 형식에 대해 지원됩니다.

이미지 편집기를 사용하여 이미지 맵을 추가할 수도 있습니다. 자세한 내용은 [이미지 맵 추가](/help/assets/image-maps.md).

>[!NOTE]
>
>TXT 파일을 편집하려면 다음을 설정합니다 **일별 CQ 링크 외부화** 구성 관리자에서.

## 타임라인 {#timeline}

타임라인을 사용하면 에셋에 대한 활성 워크플로우, 댓글/주석, 활동 로그 및 버전과 같은 선택한 항목에 대한 다양한 이벤트를 볼 수 있습니다.

![자산에 대한 타임라인 항목 정렬](assets/sort_timeline.gif)

*그림: 에셋의 타임라인 항목을 정렬합니다.*

>[!NOTE]
>
>다음에서 [컬렉션 콘솔](/help/assets/manage-collections.md#navigating-the-collections-console), **[!UICONTROL 모두 표시]** 목록은 댓글 및 워크플로만 볼 수 있는 옵션을 제공합니다. 또한 콘솔에 나열된 최상위 수준 컬렉션에만 타임라인이 표시됩니다. 컬렉션 내부를 탐색하는 경우에는 표시되지 않습니다.

>[!NOTE]
>
>타임라인에 여러 개 포함 [컨텐츠 조각과 관련된 옵션](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

## 에셋에 주석 달기 {#annotating}

주석은 이미지 또는 비디오에 추가된 댓글 또는 설명 주석입니다. 주석은 마케터에게 자산에 대한 공동 작업을 수행하고 피드백을 남길 수 있는 기능을 제공합니다.

비디오 주석은 HTML5와 호환되는 비디오 형식이 있는 브라우저에서만 지원됩니다. 다음 비디오 형식 [!DNL Assets] 는 브라우저에 따라 다릅니다. 그러나 MXF 비디오 포맷은 비디오 주석에서 아직 지원되지 않습니다.

>[!NOTE]
>
>컨텐츠 조각의 경우 [주석은 조각 편집기에서 생성됩니다](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment).

1. 주석을 추가할 자산의 위치로 이동합니다.
1. 다음을 클릭합니다. **[!UICONTROL 주석]** 다음 중 한 가지 옵션을 선택할 수 있습니다.

   * [빠른 작업](/help/assets/manage-assets.md#quick-actions)
   * 에셋을 선택하거나 에셋 페이지로 이동한 후 도구 모음에서

1. Add a comment in the **[!UICONTROL Comment]** box at the bottom of the timeline. Alternatively, mark up an area on the image and add an annotation in the **[!UICONTROL Add Annotation]** dialog.

1. 사용자에게 주석에 대해 알리려면 사용자의 이메일 주소를 지정하고 주석을 추가합니다. 예를 들어 Aaron MacDonald에게 주석에 대해 알리려면 을 @aa. 일치하는 모든 사용자에 대한 힌트가 목록에 표시됩니다. 목록에서 Aaron의 이메일 주소를 선택하면 댓글이 있는 사용자를 태그 지정할 수 있습니다. 마찬가지로 주석 내, 주석 앞 또는 뒤의 어느 곳에서든 더 많은 사용자에 태그를 지정할 수 있습니다.

   ![사용자의 이메일 주소를 지정하고 주석을 추가하여 사용자에게 알립니다.](assets/annotate-gif.gif)

   >[!NOTE]
   >
   >관리자가 아닌 사용자의 경우, 다음 위치에 대한 읽기 권한이 있는 경우에만 제안 사항이 표시됩니다. `/home` crxde의 경로.

1. 주석을 추가한 후 **[!UICONTROL 추가]** 저장하려고. 주석에 대한 알림이 Aaron에게 전송됩니다.

   >[!NOTE]
   >
   >저장하기 전에 여러 주석을 추가할 수 있습니다.

1. 클릭 **[!UICONTROL 닫기]** 주석 모드를 종료합니다.
1. 알림을 보려면 다음에로그인하십시오. [!DNL Assets] Aaron MacDonald의 자격 증명으로 **[!UICONTROL 알림]** 알림을 보는 옵션.

   >[!NOTE]
   >
   >비디오 에셋에 주석을 추가할 수도 있습니다. 비디오에 주석을 달 때 플레이어는 일시 중지하여 프레임에 주석을 달 수 있도록 합니다. 자세한 내용은 [비디오 자산 관리](/help/assets/managing-video-assets.md). MXF 비디오 포맷은 비디오 주석에서 아직 지원되지 않습니다.

1. 사용자를 구분할 수 있도록 다른 색상을 선택하려면 프로필 옵션을 클릭하고 를 클릭하십시오. **[!UICONTROL 내 환경 설정]**.

   ![사용자 프로필 옵션을 선택한 다음 내 환경 설정 을 선택하여 사용자 환경 설정 을 엽니다](assets/User-profile-preferences.png)

   에서 원하는 색상을 지정합니다. **[!UICONTROL 주석 색상]** 상자를 클릭한 다음 **[!UICONTROL Accept]**.

   ![사용자 환경 설정에서 주석 색상을 선택하여 사용자 성향 색상을 설정합니다.](assets/Annotation-color.png)

>[!NOTE]
>
>컬렉션에 주석을 추가할 수도 있습니다. 그러나 컬렉션에 하위 컬렉션이 포함되어 있으면 상위 컬렉션에만 주석/설명을 추가할 수 있습니다. 하위 컬렉션에는 주석 달기 옵션을 사용할 수 없습니다.

### 저장된 주석 보기 {#viewing-saved-annotations}

한 번에 하나의 주석만 볼 수 있습니다.

>[!NOTE]
>
>여러 주석을 선택하는 경우 최신 주석이 사용자 인터페이스에 표시됩니다.
>
>다중 선택은 주석이 있는 에셋을 PDF으로 인쇄하는 경우에만 지원됩니다.

**자산에 대해 저장된 주석을 보려면 다음 작업을 수행하십시오.**

1. 에셋 위치로 이동하여 에셋 페이지를 엽니다.

1. Experience Manager 인터페이스에서 다음을 선택합니다. **[!UICONTROL 타임라인]**.
1. From the **[!UICONTROL Show All]** list in the timeline, select **[!UICONTROL Comments]** to filter the results based on annotations.

   에서 주석 클릭 **[!UICONTROL 타임라인]** 패널에서 해당 주석을 보려면 선택합니다.

   ![이미지에서 주석을 볼 수 있는 타임라인 패널](assets/timeline-view-annotations.png)

   클릭 **[!UICONTROL 삭제]**&#x200B;을 클릭하여 특정 주석을 삭제합니다.

### 주석 인쇄 {#printing-annotations}

자산에 주석이 있거나 검토 워크플로우가 적용된 경우, 오프라인 검토를 위한 PDF 파일로 자산 및 검토 상태를 주석과 함께 인쇄할 수 있습니다.

주석만 인쇄하도록 선택하거나 상태를 검토할 수도 있습니다.

>[!NOTE]
>
>주석이 있는 에셋을 PDF으로 인쇄하는 동안 여러 주석을 선택할 수 있습니다.

주석을 인쇄하고 상태를 검토하려면 **[!UICONTROL 인쇄]** 마법사의 지시를 따릅니다. 다음 **[!UICONTROL 인쇄]** 하나 이상의 주석 또는 검토 상태가 지정된 자산이 있는 경우에만 도구 모음에 옵션이 표시됩니다.

1. 다음에서 [!DNL Assets] 인터페이스에서 에셋의 미리보기 페이지를 엽니다.
1. 다음 중 하나를 수행하십시오.

   * 모든 주석과 검토 상태를 인쇄하려면 3단계를 건너뛰고 바로 4단계로 이동합니다.
   * 특정 주석을 인쇄하고 상태를 검토하려면 [타임라인](/help/assets/manage-assets.md#timeline) 그런 다음 3단계로 이동합니다.

1. 특정 주석을 인쇄하려면 타임라인에서 주석을 선택합니다.

   ![타임라인에서 주석을 선택하여 인쇄합니다.](assets/timeline-select-annotations.png)

   검토 상태만 인쇄하려면 타임라인에서 선택합니다.

1. 클릭 **[!UICONTROL 인쇄]** 을 클릭합니다.

1. 인쇄 대화 상자에서 주석/검토 상태를 PDF에 표시할 위치를 선택합니다. 예를 들어 인쇄된 이미지가 포함된 페이지의 오른쪽 상단에 주석/상태를 인쇄하려면 **왼쪽 위** 설정. 기본적으로 선택되어 있습니다.

   You can choose other settings depending on the position where you want the annotations/status to appear in the printed PDF. If you want the annotations/status to appear in a page that is separate from the printed asset, choose **[!UICONTROL Next Page]**.

1. 클릭 **[!UICONTROL 인쇄]**. Depending upon the option you choose in step 2, the generated PDF displays the annotations/status at the specified position. For example, if you choose to print both annotations and the review status using the **Top-Left** setting, the generated output resembles the PDF file depicted here.

   ![생성된 PDF에 대한 주석 및 검토 상태](assets/annotation-status-pdf.png)

1. 다운로드 ![PDF을 위한 다운로드 옵션](assets/do-not-localize/download.png) 또는 인쇄 ![PDF의 인쇄 옵션](assets/do-not-localize/print.png) 오른쪽 상단의 옵션을 사용하는 PDF.

   >[!NOTE]
   >
   >에셋에 하위 에셋이 있는 경우 모든 하위 에셋을 해당 페이지 단위 주석과 함께 인쇄할 수 있습니다.

   렌더링된 PDF 파일의 모양(예: 글꼴 색상, 크기 및 스타일)을 편집하려면 **[!UICONTROL 주석 PDF 구성]** 을 누르고 원하는 옵션을 수정합니다. 예를 들어 승인됨 상태의 표시 색상을 변경하려면 해당 필드의 색상 코드를 수정합니다. 주석의 글꼴 색상 변경에 대한 자세한 내용은 [주석 달기](/help/assets/manage-assets.md#annotating).

   ![PDF 문서에 에셋 주석을 인쇄하기 위한 구성](assets/annotation-print-pdf-config.png)

   렌더링된 PDF 파일로 돌아가서 새로 고칩니다. 새로 고친 PDF은 변경 사항을 반영합니다.

자산에 외국어(특히 라틴어가 아닌 언어)의 주석이 포함된 경우 먼저 [!DNL Experience Manager] 서버: 이러한 주석을 인쇄할 수 있습니다. CQ-DAM-Handler-Gibson 글꼴 관리자 서비스를 구성할 때 원하는 언어의 글꼴이 있는 경로를 제공합니다.

1. URL에서 CQ-DAM-Handler-Gibson 글꼴 관리자 서비스 구성 페이지를 엽니다. `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl`.
1. CQ-DAM-Handler-Gibson 글꼴 관리자 서비스를 구성하려면 다음 중 하나를 수행합니다.

   * 시스템 글꼴 디렉터리 옵션에서 시스템의 글꼴 디렉터리에 대한 전체 경로를 지정합니다. 예를 들어 Mac 사용자인 경우 다음과 같이 경로를 지정할 수 있습니다. */Library/Fonts* 시스템 글꼴 디렉토리 옵션에서 선택합니다. [!DNL Experience Manager] 이 디렉토리에서 글꼴을 가져옵니다.
   * 다음 이름의 디렉터리 만들기 `fonts` 의 내부 `crx-quickstart` 폴더를 삭제합니다. CQ-DAM-Handler-Gibson 글꼴 관리자 서비스는 해당 위치에서 글꼴을 자동으로 가져옵니다. `crx-quickstart/fonts`. Adobe 서버 글꼴 디렉토리 옵션 내에서 이 기본 경로를 재정의할 수 있습니다.

   * 시스템에 글꼴용 폴더를 만들고 원하는 글꼴을 폴더에 저장합니다. 그런 다음 Customer Fonts 디렉토리 옵션에 해당 폴더에 대한 전체 경로를 지정합니다.

1. URL에서 주석 PDF 구성에 액세스합니다 `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig`.
1. 다음과 같이 올바른 글꼴 패밀리 세트로 주석 PDF을 구성합니다.

   * 문자열 포함 `<font_family_name_of_custom_font, sans-serif>` font-family 옵션 내에서 사용할 수 있습니다. 예를 들어 CJK(중국어, 일본어 및 한국어)로 주석을 인쇄하려면 문자열을 포함합니다 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` font-family 옵션에서 사용할 수도 있습니다. 힌디어로 주석을 인쇄하려면 적절한 글꼴을 다운로드하고 글꼴 모음을 Arial® Unicode MS®, Noto Sans, Noto Sans CJK JP, Noto Sans Devanagari, sans-serif로 구성합니다.

1. 다시 시작 [!DNL Experience Manager] 배포.

다음은 를 구성하는 방법의 예입니다 [!DNL Experience Manager] 한중일(중국어, 일본어, 한국어)로 주석을 인쇄하려면

1. 다음 링크에서 Google Noto CJK 글꼴을 다운로드하여 글꼴 관리자 서비스에 구성된 글꼴 디렉터리에 저장합니다.

   * All In One 슈퍼 CJK 글꼴: [https://fonts.google.com/noto/use](https://fonts.google.com/noto/use)
   * Noto Sans(유럽 언어의 경우): [https://fonts.google.com/noto](https://fonts.google.com/noto)
   * 원하는 언어에 대해서는 참고 글꼴을 사용하십시오. [https://fonts.google.com/noto](https://fonts.google.com/noto)

1. font-family 매개 변수를 로 설정하여 주석 PDF 파일을 구성합니다. `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`. 이 구성은 기본적으로 사용할 수 있으며 모든 유럽 및 CJK 언어에 대해 작동합니다.
1. 선택한 언어가 2단계에서 언급한 언어와 다른 경우 기본 글꼴 패밀리에 적절한(쉼표로 구분된) 항목을 추가합니다.

## 에셋 버전 생성, 관리, 미리보기 및 되돌리기 {#asset-versioning}

버전 관리는 특정 시점에 디지털 에셋의 스냅샷을 만듭니다. 버전 관리는 나중에 자산을 이전 상태로 복원하는 데 도움이 됩니다. 예를 들어 에셋에 대한 변경 내용을 실행 취소하려면 편집되지 않은 버전의 에셋을 복원합니다. 위치 [!DNL Experience Manager], 버전을 만들고, 현재 개정을 보고, 두 이미지 버전 간의 차이점을 나란히 보고, 에셋을 이전 버전으로 복원할 수 있습니다.

에서 버전을 만들 수 있습니다. [!DNL Experience Manager] 다음과 같은 경우:

* 동일한 위치에 존재하는 동일한 파일 이름으로 에셋을 업로드합니다. 새 에셋이거나 동일한 에셋의 수정된 버전일 수 있습니다.
* 에서 이미지 편집 [!DNL Experience Manager] 변경 내용을 저장합니다.
* 에셋의 메타데이터를 편집합니다.
* 사용 [!DNL Experience Manager] 기존 자산을 체크아웃하고 편집하며 [변경 사항 업로드](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#edit-assets-upload-updated-assets).

워크플로우를 통해 자동 버전 관리를 활성화할 수도 있습니다. 에셋에 대한 버전을 만들면 버전과 함께 메타데이터 및 렌디션이 저장됩니다. 변환은 업로드된 JPEG 파일의 PNG 변환과 같이 동일한 이미지의 대체 표현물입니다.

1. 버전을 만들 에셋의 위치로 이동한 다음 에셋을 클릭하여 미리보기를 엽니다. 페이지의 왼쪽 상단 모서리에서 메뉴를 열고 을 선택합니다. **[!UICONTROL 타임라인]**.

   ![왼쪽 탐색 메뉴에서 타임라인 옵션을 선택합니다](assets/timeline.png)

   *그림: 페이지 왼쪽 상단에서 메뉴 열기 및 선택 [!UICONTROL 타임라인] 옵션을 선택합니다.*

1. 에셋의 버전을 생성하려면 다음을 수행합니다.

   * 다음을 클릭합니다. **[!UICONTROL 작업]** 맨 아래에
   * 클릭 **[!UICONTROL 다른 버전으로 저장]** 에셋의 버전을 생성할 수 있습니다. 선택적으로 레이블 및 주석을 추가합니다.
   * 클릭 **[!UICONTROL 만들기]** 을 클릭하여 버전을 만듭니다.

     ![사이드바에서 에셋 버전 만들기](assets/create-new-version-from-timeline.png)

     *그림: 에서 에셋 버전 만들기 [!UICONTROL 타임라인] 왼쪽 사이드바.*

1. 에셋 버전을 보려면 다음과 같이 하십시오.

   * 클릭 **[!UICONTROL 모두 표시]** 위치: [!UICONTROL 타임라인].
   * 클릭 **[!UICONTROL 버전]**. 에셋에 대해 생성된 모든 버전은 왼쪽 사이드바에 나열됩니다.

   * 에셋의 특정 버전을 선택하고 **[!UICONTROL 버전 미리 보기]**.

1. 이전 버전의 자산으로 되돌리려면 다음을 수행합니다. 되돌린 후 이 버전은 [!DNL Assets] 인터페이스와 를 사용할 수 있습니다.

   * 에셋의 버전을 클릭합니다. 선택적으로 레이블 및 주석을 추가합니다.
   * 클릭 **[!UICONTROL 이 버전으로 되돌리기]**.

     ![되돌릴 버전 선택](assets/select_version.png)

     *그림: 버전을 선택하고 되돌립니다. 그러면 DAM 사용자가 사용할 수 있는 현재 버전이 됩니다.*

1. 두 버전의 이미지를 비교하려면 다음 단계를 수행합니다.
   * 현재 버전과 비교할 버전을 클릭합니다.
   * 슬라이더를 왼쪽으로 드래그하여 이 버전을 현재 버전에 중첩하고 비교합니다.

   ![슬라이더를 사용하여 자산의 선택한 버전을 현재 버전과 비교](assets/version-slider.gif)

   *그림: 슬라이더를 사용하여 선택한 에셋 버전을 현재 버전과 쉽게 비교할 수 있습니다.*

### 자산에 대한 워크플로우 시작 {#starting-a-workflow-on-an-asset}

자산을 처리하는 워크플로를 적용하려면 다음을 참조하십시오. [에셋에서 워크플로 시작](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset).

## 컬렉션 {#collections}

컬렉션은 순서가 지정된 에셋 세트입니다. 컬렉션을 사용하여 사용자 간에 관련 에셋을 공유하거나 유사한 에셋을 함께 클러스터링하여 손쉽게 검색할 수 있습니다.

* 이러한 에셋에 대한 참조만 포함하므로 컬렉션에는 서로 다른 위치의 에셋이 포함될 수 있습니다. 각 컬렉션은 자산의 참조 무결성을 유지합니다.
* 편집, 보기 등을 포함하여 다양한 권한 수준을 가진 여러 사용자와 컬렉션을 공유할 수 있습니다.

컬렉션 관리에 대한 자세한 내용은 [디지털 자산 컬렉션 관리](/help/assets/manage-collections.md).

## 데스크탑 앱 또는 Adobe 자산 링크에서 자산을 볼 때 만료된 자산 숨기기 {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] 데스크탑 앱을 사용하면 Windows 또는 Mac 데스크탑에서 DAM 저장소에 액세스할 수 있습니다. Adobe 에셋 링크를 사용하면 지원되는 내에서 에셋에 액세스할 수 있습니다. [!DNL Creative Cloud] 데스크탑 애플리케이션.

내에서 에셋을 검색할 때 [!DNL Experience Manager] 사용자 인터페이스에서는 만료된 에셋이 표시되지 않습니다. 관리자는 데스크탑 앱 및 Asset Link에서 자산을 검색할 때 만료된 자산을 보고 검색하고 가져오지 않도록 다음 구성을 수행할 수 있습니다. 이 구성은 관리자 권한과 관계없이 모든 사용자에 대해 작동합니다.

다음 CURL 명령을 실행합니다. 에 대한 읽기 액세스 권한 확인 `/conf/global/settings/dam/acpapi/` 에셋에 액세스하는 사용자용입니다. 에 속한 사용자 `dam-user` 기본적으로 그룹에 권한이 있습니다.

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

자세한 내용은 방법 을 참조하십시오 [데스크탑 앱을 사용하여 DAM 자산 찾아보기](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 및 [Adobe 에셋 링크를 사용하는 방법](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html).
