---
title: 옵션 A - Dynamic Media 구성 - Scene7 모드
description: Dynamic Media - Scene7 모드를 구성하는 방법을 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
hide: true
hidefromtoc: true
feature: Configuration,Scene7 Mode
exl-id: null
source-git-commit: b6000516b88342d6abf8072623cfece43e2ba19d
workflow-type: tm+mt
source-wordcount: '11571'
ht-degree: 2%

---

# 옵션 A - Dynamic Media 구성 - Scene7 모드{#configuring-dynamic-media-scene-mode}

>[!NOTE]
>
>옵션 A - 내가 작성한 두 개의 새 주제가 삭제됩니다. 그러나 주제를 삭제하기 전에 모든 컨텐츠가 이 주제의 영역으로 이동되었습니다. 이전에는 일반 설정 및 게시 설정에 대해 이미 이야기했습니다.

개발, 스테이징 및 프로덕션과 같은 다양한 환경에 대해 Adobe Experience Manager 설정을 사용하는 경우 이러한 각 환경에 대해 Dynamic Media Cloud Services을 구성합니다.

## Dynamic Media 아키텍처 다이어그램 - Scene7 모드 {#architecture-diagram-of-dynamic-media-scene-mode}

**릭: 그대로 유지**

다음 아키텍처 다이어그램은 Dynamic Media - Scene7 모드 작동 방식을 설명합니다.

새로운 아키텍처를 통해 Experience Manager은 기본 소스 자산을 담당하며 자산 처리 및 게시를 위해 Dynamic Media과 동기화됩니다.

1. 기본 소스 자산이 Experience Manager에 업로드되면 Dynamic Media에 복제됩니다. 이때 Dynamic Media은 이미지의 비디오 인코딩 및 동적 변형과 같은 모든 자산 처리 및 표현물 생성을 처리합니다.
(Dynamic Media - Scene7 모드에서 기본 업로드 파일 크기는 2GB 이하입니다. 최대 15GB까지 2GB의 업로드 파일 크기를 활성화하려면 [(선택 사항) 2GB보다 큰 자산을 업로드할 Dynamic Media - Scene7 모드 구성](#optional-config-dms7-assets-larger-than-2gb))
1. 표현물이 생성되면 Experience Manager이 원격 Dynamic Media 표현물에 안전하게 액세스하고 미리 볼 수 있습니다(바이너리가 Experience Manager 인스턴스로 다시 전송되지 않음).
1. 컨텐츠를 게시 및 승인할 준비가 되면, 컨텐츠를 전달 서버에 푸시하고 CDN(Content Delivery Network)에 컨텐츠를 캐시하도록 Dynamic Media 서비스를 트리거합니다.

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>다음 기능 목록을 사용하려면 Adobe Experience Manager - Dynamic Media과 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이러한 기능에서 지원되지 않습니다.
>
>* [스마트 이미징](/help/assets/imaging-faq.md)
>* [캐시 무효화](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [핫링크 보호](/help/assets/hotlink-protection.md)
>* [컨텐츠의 HTTP/2 전달](/help/assets/http2.md)
>* CDN 수준에서 URL 리디렉션
>* Akamai ChinaCDN(중국에서 최적의 전달을 위한)


## Scene7 모드에서 Dynamic Media 활성화 {#enabling-dynamic-media-in-scene-mode}

**릭: 그대로 유지**

[Dynamic Media는 기본적으로 비활성화됩니다. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Dynamic Media 기능을 사용하려면 활성화해야 합니다.

>[!WARNING]
>
>Dynamic Media - Scene7 모드는 용 *Experience Manager 작성자 인스턴스만*. 따라서 다음을 구성해야 합니다 `runmode=dynamicmedia_scene7` Experience Manager 작성자 인스턴스에서 *not* Experience Manager 게시 인스턴스.

Dynamic Media을 활성화하려면 `dynamicmedia_scene7` 터미널 창에 다음을 입력하여 명령줄에서 모드를 실행합니다(사용된 예제 포트는 4502).

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (선택 사항) Dynamic Media 사전 설정 및 구성을 6.3에서 6.5로 마이그레이션 다운타임 없음 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

**릭: 그대로 유지**

이제 Experience Manager Dynamic Media을 6.3에서 6.4 또는 6.5로 업그레이드하면 다운타임 없이 배포할 수 있습니다. 모든 사전 설정 및 구성을 `/etc` to `/conf` CRXDE Lite에서 다음 curl 명령을 실행해야 합니다.

>[!NOTE]
>
>호환성 모드에서 Experience Manager 인스턴스를 실행하는 경우(즉, 호환성 패키지가 설치되어 있으므로) 이러한 명령을 실행할 필요가 없습니다.

호환성 패키지를 사용하거나 사용하지 않는 모든 업그레이드의 경우 다음 Linux® curl 명령을 실행하여 원래 Dynamic Media과 함께 제공된 기본 기본 기본 기본 뷰어 사전 설정을 복사할 수 있습니다.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

만든 사용자 지정 뷰어 사전 설정 및 구성을 마이그레이션하려면 `/etc` to `/conf`다음 Linux® curl 명령을 실행합니다.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 벌크 자산 마이그레이션용 기능 팩 18912 설치 {#installing-feature-pack-for-bulk-asset-migration}

**릭: 그대로 유지**

기능 팩 18912 설치은 다음과 같습니다 *옵션*.

기능 팩 18912을 사용하면 FTP를 통해 자산을 벌크하거나 Dynamic Media - 하이브리드 모드 또는 Dynamic Media Classic에서 Experience Manager의 Dynamic Media - Scene7 모드로 자산을 마이그레이션할 수 있습니다. 다음에서 사용 가능합니다 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

자세한 내용은 [벌크 자산 마이그레이션용 기능 팩 18912 설치](/help/assets/bulk-ingest-migrate.md) 추가 정보.

## Cloud Services에서 Dynamic Media 구성 만들기 {#configuring-dynamic-media-cloud-services}

**릭: 그대로 유지**

**Dynamic Media 구성 전** - Dynamic Media 자격 증명으로 프로비저닝 이메일을 받은 후 [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 계정에 로그인하여 암호를 변경합니다. 프로비저닝 전자 메일에 제공된 암호는 시스템에서 생성되며 임시 암호만 사용할 수 있습니다. Dynamic Media Cloud Service이 올바른 자격 증명으로 설정되도록 암호를 업데이트하는 것이 중요합니다.

![dynamicmediaconfiguration2업데이트됨](assets/dynamicmediaconfiguration2updated.png)

**Cloud Services에서 Dynamic Media 구성을 만들려면:**

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스하고 도구 아이콘을 선택한 다음 로 이동합니다 **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media 구성]**.
1. Dynamic Media 구성 브라우저 페이지의 왼쪽 창에서 **[!UICONTROL 글로벌]** (폴더 아이콘을 의 왼쪽에 선택하지 마십시오.) **[!UICONTROL 글로벌]**)를 선택한 다음 을 선택합니다. **[!UICONTROL 만들기]**.
1. 설정 **[!UICONTROL Dynamic Media 구성 만들기]** 페이지에서 제목과 Dynamic Media 계정 이메일 주소, 암호를 입력한 다음 지역을 선택합니다. 이 정보는 규정 이메일에서 Adobe이 제공합니다. 이메일을 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.

   선택 **[!UICONTROL Dynamic Media에 연결]**.

   >[!NOTE]
   **릭: 그대로 유지??** Dynamic Media 자격 증명으로 프로비저닝 이메일을 받은 후 [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 계정에 로그인하여 암호를 변경합니다. 프로비저닝 전자 메일에 제공된 암호는 시스템에서 생성되며 임시 암호만 사용할 수 있습니다. Dynamic Media Cloud Service이 올바른 자격 증명으로 설정되도록 암호를 업데이트하는 것이 중요합니다.

1. 연결이 성공하면 다음을 설정합니다. 별표(*)가 있는 헤딩은 다음과 같습니다.

   * **[!UICONTROL 회사]** - Dynamic Media 계정의 이름입니다. 여러 Dynamic Media 계정이 있습니다. 예를 들어 서로 다른 하위 브랜드, 사업부, 스테이징 또는 프로덕션 환경이 있을 수 있습니다.

   * **[!UICONTROL 회사 루트 폴더 경로]**

   * **[!UICONTROL 자산 게시]** - 다음 세 가지 옵션 중에서 선택할 수 있습니다.
      * **[!UICONTROL 즉시]** 는 자산이 업로드되면 시스템이 자산을 수집하여 URL/포함을 즉시 제공함을 의미합니다. 자산을 게시하는 데 필요한 사용자 개입이 없습니다.
      * **[!UICONTROL 활성화 시]** 는 URL/포함 링크가 제공되기 전에 먼저 자산을 명시적으로 게시해야 함을 의미합니다.<br><!-- CQDOC-17478, Added March 9, 2021-->Experience Manager 6.5.8 이상에서 Experience Manager 게시 인스턴스는 다음과 같은 정확한 Dynamic Media 메타데이터 값을 반영합니다 `dam:scene7Domain` 및 `dam:scene7FileStatus` in **[!UICONTROL 활성화 시]** 게시 모드만 표시합니다. 이 기능을 사용하려면 서비스 팩 8을 설치한 다음 Experience Manager을 다시 시작하십시오. Sling 구성 관리자로 이동합니다. 구성 찾기 `Scene7ActivationJobConsumer Component` 또는 새 템플릿을 만듭니다.) 확인란을 선택합니다 **[!UICONTROL Dynamic Media 게시 후 메타데이터 복제]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 저장]**.

         ![Dynamic Media 게시 후 메타데이터 복제 확인란](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 선택적 게시]** 이 옵션을 사용하면 Dynamic Media에 게시되는 폴더를 제어할 수 있습니다. 스마트 자르기 또는 동적 표현물과 같은 기능을 사용하거나 미리 보기 위해 Experience Manager에 배타적으로 게시된 폴더를 결정할 수 있습니다. 같은 자산이 *not* 공개 도메인에 전달을 위해 Dynamic Media에 게시되었습니다.<br>여기에서 이 옵션을 **[!UICONTROL Dynamic Media Cloud 구성]** 또는 원하는 경우 폴더 수준, 폴더의 **[!UICONTROL 속성]**.<br>자세한 내용은 [Dynamic Media의 선택적 게시 작업](/help/assets/selective-publishing.md).<br>나중에 이 구성을 변경하거나 나중에 폴더 수준에서 변경하면 해당 변경 사항은 해당 시점부터 업로드하는 새 자산에만 영향을 줍니다. 폴더에 있는 기존 자산의 게시 상태는 다음 중 하나에서 수동으로 변경할 때까지 그대로 유지됩니다 **[!UICONTROL 빠른 게시]** 또는 **[!UICONTROL 게시 관리]** 대화 상자
   * **[!UICONTROL 보안 미리 보기 서버]** - 보안 표현물 미리 보기 서버의 URL 경로를 지정할 수 있습니다. 즉, 표현물이 생성되면 Experience Manager이 원격 Dynamic Media 표현물에 안전하게 액세스하고 미리 볼 수 있습니다(바이너리가 Experience Manager 인스턴스로 다시 전송되지 않음).
회사의 서버나 특수 서버를 사용하기 위해 특별한 계획이 없는 한 Adobe은 이 설정을 지정된 대로 유지하는 것을 권장합니다.

   * **[!UICONTROL 모든 콘텐츠 동기화]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->기본적으로 선택됩니다. Dynamic Media에 대한 동기화에서 자산을 선택적으로 포함하거나 제외하려면 이 선택 사항을 선택 취소합니다. 이 옵션을 선택 해제하면 다음 두 가지 Dynamic Media 동기화 모드 중에서 선택할 수 있습니다.

   * **[!UICONTROL Dynamic Media 동기화 모드]**
      * **[!UICONTROL 기본적으로 활성화됨]** - 제외용으로 특별히 폴더를 표시하지 않으면 기본적으로 모든 폴더에 구성이 적용됩니다. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 기본적으로 비활성화됨]** - Dynamic Media에 동기화할 선택한 폴더를 명시적으로 표시할 때까지 해당 구성은 폴더에 적용되지 않습니다.
Dynamic Media에 동기화할 선택한 폴더를 표시하려면 자산 폴더를 선택한 다음 도구 모음에서 를 선택합니다 **[!UICONTROL 속성]**. 설정 **[!UICONTROL 세부 사항]** 탭, **[!UICONTROL Dynamic Media 동기화 모드]** 드롭다운 목록에서 다음 세 가지 옵션 중에서 선택합니다. 완료되면 을 선택합니다 **[!UICONTROL 저장]**. *기억: 이 세 옵션을 선택한 경우에는 사용할 수 없습니다&#x200B;**[!UICONTROL 모든 콘텐츠 동기화]**더 일찍* 참조 - [Dynamic Media의 폴더 수준에서 선택적 게시 작업](/help/assets/selective-publishing.md).
         * **[!UICONTROL 상속됨]** - 폴더에 명시적 동기화 값이 없습니다. 대신 폴더는 상위 폴더 또는 클라우드 구성의 기본 모드에서 동기화 값을 상속받습니다. 도구 설명을 통해 상속된 표시에 대한 세부 상태입니다.
         * **[!UICONTROL 하위 폴더에 사용]** - Dynamic Media에 동기화할 이 하위 트리에 모든 것을 포함합니다. 폴더별 설정은 클라우드 구성에서 기본 모드를 덮어씁니다.
         * **[!UICONTROL 하위 폴더에 대해 사용 안 함]** - 이 하위 트리의 모든 항목을 Dynamic Media에 동기화하지 않도록 제외합니다.

   >[!NOTE]
   DMS7에서는 버전 관리를 지원하지 않습니다. 또한 지연된 활성화는 **[!UICONTROL 자산 게시]** Dynamic Media 구성 편집 페이지에서 이 **[!UICONTROL 활성화 시]**, 그리고 자산이 처음 활성화될 때까지 에만 해당합니다.
   자산이 활성화되면 모든 업데이트가 즉시 S7 Delivery에 실시간으로 게시됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. Dynamic Media 컨텐츠를 게시하기 전에 안전하게 미리 보려면 Dynamic Media에 연결하려면 Experience Manager 작성자 인스턴스를 &quot;&quot;허용 목록에 추가하다해야 합니다.

   * **릭: 새 게시 설정 주제에 대한 링크** 를 엽니다. [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 계정에 로그인합니다. 자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

   * 페이지 오른쪽 상단 근처에 있는 탐색 막대에서 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 게시 설정]** > **[!UICONTROL 이미지 서버]**.

   * 이미지 서버 게시 페이지의 게시 컨텍스트 드롭다운 목록에서 을 선택합니다 **[!UICONTROL 테스트 이미지 제공]**.
   * 클라이언트 주소 필터에 대해 다음을 선택합니다. **[!UICONTROL 추가]**.
   * 주소를 활성화(설정)하려면 확인란을 선택합니다. Experience Manager 작성자 인스턴스(Dispatcher IP 아님)의 IP 주소를 입력합니다.
   * **[!UICONTROL 저장]**&#x200B;을 선택합니다.

이제 기본 구성을 완료했습니다. Dynamic Media - Scene7 모드를 사용할 준비가 되었습니다.

구성을 추가로 사용자 지정하려면 아래의 작업을 선택적으로 완료할 수 있습니다 [(선택 사항) Dynamic Media - Scene7 모드에서 고급 설정 구성](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (선택 사항) Dynamic Media - Scene7 모드에서 고급 설정 구성 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

**릭: 그대로 유지**

Dynamic Media - Scene7 모드의 구성 및 설정을 추가 사용자 지정하거나 성능을 최적화하려는 경우 다음 중 하나 이상을 완료할 수 있습니다 *옵션* 작업:

* [(선택 사항) 2GB보다 큰 자산을 업로드할 Dynamic Media - Scene7 모드 구성](#optional-config-dms7-assets-larger-than-2gb)
* [(선택 사항) Dynamic Media 게시 설정 구성](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)
   * [(선택 사항) 자산을 공개하기 전에 테스트합니다](#test-assets-before-making-public)
* [(선택 사항) Dynamic Media 일반 설정 구성](#configuring-application-general-settings)
* [(선택 사항) 추가 구성 작업](#additional-configuration-tasks)
* [(선택 사항) Dynamic Media - Scene7 모드의 성능 조정](#optional-tuning-the-performance-of-dynamic-media-scene-mode)
* [(선택 사항) 복제할 자산을 필터링합니다](#optional-filtering-assets-for-replication)

### (선택 사항) 2GB보다 큰 자산을 업로드할 Dynamic Media - Scene7 모드 구성 {#optional-config-dms7-assets-larger-than-2gb}

**릭: 그대로 유지**

Dynamic Media - Scene7 모드에서 기본 자산 업로드 파일 크기는 2GB 이합니다. 그러나 2GB보다 크고 최대 15GB의 자산 업로드를 선택적으로 구성할 수 있습니다.

이 기능을 사용하려면 다음 전제 조건 및 점을 알아 두십시오.

* Dynamic Media - Scene7 모드에서 서비스 팩 6.5.4.0 이상 버전의 Experience Manager 6.5를 실행 중이어야 합니다.
* 이 큰 업로드 기능은 [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) 고객.
* Experience Manager 인스턴스가 Amazon S3 또는 Microsoft® Azure Blob 저장소를 사용하여 구성되었는지 확인하십시오.

   >[!NOTE]
   Blob 저장소 구성에서 이 큰 업로드 기능은 AzureSas에서 지원되지 않으므로 액세스 키 및 비밀 키로 Azure Blob 저장소를 구성합니다.

* Oak&#39;s [직접 이진 액세스 다운로드](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) 활성화됨(Oak) *직접 이진 액세스 업로드* 는 필요하지 않습니다.)

   직접 이진 액세스 다운로드를 활성화하려면 속성을 설정합니다 `presignedHttpDownloadURIExpirySeconds > 0` 데이터 저장소 구성에서 다음을 수행합니다. 더 큰 바이너리를 다운로드하고 다시 시도할 수 있을 만큼 값이 길어야 합니다.

* 15GB보다 큰 자산은 업로드되지 않습니다. (크기 제한은 아래 8단계에서 설정됩니다.)
* 이 **[!UICONTROL Dynamic Media 재처리]** 자산 워크플로우는 폴더에서 트리거되며 Dynamic Media 회사와 이미 동기화된 모든 큰 자산을 재처리합니다. 하지만 큰 자산이 폴더에서 아직 동기화되지 않는 경우 자산을 업로드하지 않습니다. 따라서 Dynamic Media에서 기존 대용량 자산을 동기화하기 위해 다음을 실행할 수 있습니다 **[!UICONTROL Dynamic Media 재처리]** 개별 자산에 대한 자산 워크플로우입니다.

**2GB보다 큰 자산을 업로드하기 위해 Dynamic Media - Scene7 모드를 구성하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.

1. CRXDE Lite 창에서 다음 중 하나를 수행합니다.

   * 왼쪽 레일에서 다음 경로로 이동합니다.

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 위의 경로를 복사하여 도구 모음 아래의 CRXDE Lite 경로 필드에 붙여넣은 다음 키를 누릅니다 `Enter`.

1. 왼쪽 레일에서 마우스 오른쪽 단추를 클릭합니다. `fileupload`를 입력한 다음 팝업 메뉴에서 **[!UICONTROL 오버레이 노드]**.

   ![오버레이 노드 옵션](/help/assets/assets-dm/uploadassets15gb_a.png)

1. 오버레이 노드 대화 상자에서 **[!UICONTROL 일치 노드 유형]** 확인란을 선택하여 옵션을 활성화(켜짐)한 다음 **[!UICONTROL 확인]**.

   ![오버레이 노드 대화 상자](/help/assets/assets-dm/uploadassets15gb_b.png)

1. CRXDE Lite 창에서 다음 중 하나를 수행합니다.

   * 왼쪽 레일에서 다음 오버레이 노드 경로로 이동합니다.

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 위의 경로를 복사하여 도구 모음 아래의 CRXDE Lite 경로 필드에 붙여넣은 다음 키를 누릅니다 `Enter`.

1. 에서 **[!UICONTROL 속성]** 탭, 아래 **[!UICONTROL 이름]** 열, 위치 `sizeLimit`.
1. 오른쪽 `sizeLimit` 이름, 아래에 **[!UICONTROL 값]** 열에서 값 필드를 두 번 클릭합니다.
1. 크기 제한을 원하는 최대 업로드 크기로 늘릴 수 있도록 적절한 값(바이트)을 입력합니다. 예를 들어 업로드 자산 크기 제한을 10GB로 늘리려면 를 입력합니다. `10737418240` 값 필드에 입력할 수 있습니다.
최대 15GB(`2013265920` 바이트). 이 경우 15GB보다 큰 업로드된 자산은 업로드되지 않습니다.


   ![크기 제한 값](/help/assets/assets-dm/uploadassets15gb_c.png)

1. CRXDE Lite 창의 왼쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 모두 저장]**.

   *이제 다음을 수행하여 Granite Workflow 외부 프로세스 작업 핸들러에 대한 시간 제한을 설정합니다.*

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 다음 중 하나를 수행합니다.

   * 다음 URL 경로로 이동합니다.

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 위의 경로를 복사하여 브라우저의 URL 필드에 붙여넣습니다. 반드시 바꾸십시오 `localhost:4502` 를 사용하여 규칙 세트를 단순화하는 것이 좋습니다.

1. 에서 **[!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 처리기]** 대화 상자, **[!UICONTROL 최대 시간 초과]** 필드에서 값을 로 설정합니다. `18000` 분(5시간). 기본값은 10800분(3시간)입니다.

   ![최대 시간 제한 값](/help/assets/assets-dm/uploadassets15gb_d.png)

1. 대화 상자의 오른쪽 아래 모서리에서 **[!UICONTROL 저장]**.

   *이제 다음을 수행하여 Scene7 직접 이진 업로드 프로세스 단계에 대한 시간 제한을 설정합니다.*

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.
1. 워크플로우 모델 페이지에서 을 선택합니다 **[!UICONTROL Dynamic Media 인코딩 비디오]**.
1. 도구 모음에서 를 선택합니다 **[!UICONTROL 편집]**.
1. 워크플로우 페이지에서 **[!UICONTROL Scene7 다이렉트 이진 업로드]** 프로세스 단계.
1. 에서 **[!UICONTROL 단계 속성]** 대화 상자(아래) **[!UICONTROL 공통]** 탭, 아래 **[!UICONTROL 고급 설정]** 제목, **[!UICONTROL 시간 초과]** 필드에 값을 입력합니다. `18000` 분(5시간). 기본값은 입니다. `3600` 분(1시간).
1. 선택 **[!UICONTROL 확인]**.
1. 선택 **[!UICONTROL 동기화]**.
1. 에 대해 14-21단계를 반복합니다 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 모델 및 **[!UICONTROL Dynamic Media 재처리]** 워크플로우 모델.

### (선택 사항) Dynamic Media 게시 설정 구성 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

**릭: 여기에 추가된 새 게시 설정 항목의 전체 컨텐츠**

>[!IMPORTANT]
Dynamic Media 게시 설정은 다음 경우에만 사용할 수 있습니다.
* Scene7 모드에서 Dynamic Media을 실행하고 있습니다.
* 다음 항목이 있습니다. *기존* **[!UICONTROL Dynamic Media 구성]** (in) **[!UICONTROL Cloud Services]**) 내의 아무 곳에나 삽입할 수 있습니다.
* 관리자 권한을 가진 Experience Manager 시스템 관리자입니다.


Dynamic Media 게시 설정 페이지 설정은 Adobe Dynamic Media 서버에서 웹 사이트 또는 응용 프로그램으로 자산이 기본적으로 전달되는 방법을 결정합니다. 지정된 설정이 없으면 Adobe Dynamic Media 서버는 게시 설정 페이지의 기본 설정에 따라 자산을 전달합니다. 예를 들어, 해상도 속성을 포함하지 않는 이미지 전달 요청에 따라 [이미지 서버] 페이지에서 [기본 객체 해상도] 설정이 있는 이미지가 생성됩니다.

관리자는 이미지 서버, 이미지 렌더러 및 비네팅 페이지의 기본 설정을 변경하여 서버에서 자산을 전달하기 위한 기본 설정을 설정할 수 있습니다.

>[!NOTE]
Dynamic Media 게시 설정 은 숙련된 웹 사이트 개발자와 프로그래머가 사용하기 위한 것입니다. Adobe은 이러한 기본 게시 설정을 변경하는 사용자가 Adobe Dynamic Media, HTTP 프로토콜 표준 및 규칙, 기본 이미징 기술에 익숙할 것을 권장합니다.

**Dynamic Media 게시 설정을 구성하려면:**

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 왼쪽 레일에서 도구 아이콘을 선택한 다음 **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 게시 설정]**.
1. 이미지 서버 페이지에서 이미지 서버 - 게시 컨텍스트를 설정한 다음 5개의 탭을 사용하여 기본 게시 설정을 구성합니다.

   * [이미지 서버](#image-server)
   * [보안](#security-tab) 탭
   * [카탈로그 관리](#catalog-management-tab) 탭
   * [요청 속성](#request-attributes-tab) 탭
   * [공통 축소판 속성](#common-thumbnail-attributes-tab) 탭
   * [색상 관리 속성](#color-management-attributes-tab) 탭

   ![Dynamic Media 게시 설정 페이지](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media 게시 설정 페이지,**[!UICONTROL 요청 속성]**탭 선택.*<br><br>

1. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 저장]**.

#### 이미지 서버 {#image-server}

이미지 서버 페이지는 이미지 서버에서 이미지를 전달하는 기본 설정을 설정합니다. 설정은 5개의 카테고리에서 사용할 수 있습니다

| 컨텍스트 게시 | 설명 |
| --- | --- |
| 이미지 제공 | 게시 설정의 컨텍스트를 지정합니다. |
| 이미지 제공 테스트 | 게시 설정을 테스트할 컨텍스트를 지정합니다.<br>자세한 내용은 [자산을 공개하기 전에 테스트](#test-assets-before-making-public). |

#### 보안 탭 {#security-tab}

**[!UICONTROL 클라이언트 주소]** - 하나 이상의 IP 주소 또는 IP 주소 범위를 지정할 수 있습니다. 지정하면 목록에 없는 IP 주소의 클라이언트에서 생성된 이 이미지 카탈로그에 대한 요청이 거부됩니다. 이 규칙은 이미지 전달과 렌더링된 이미지 모두에 적용됩니다.

#### 카탈로그 관리 탭 {#catalog-management-tab}

**[!UICONTROL 규칙 세트 정의 파일 경로]** - 이미지 카탈로그에 대한 규칙 세트 정의를 포함하는 파일을 지정합니다.

참조 - [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오.

#### 요청 속성 탭 {#request-attributes-tab}

이러한 설정은 이미지의 기본 모양과 관련이 있습니다.

| 설정 | 설명 |
| --- | --- |
| **[!UICONTROL 응답 이미지 크기 제한]** | 필수.<br>클라이언트에 반환되는 최대 회신 이미지 너비와 높이를 지정합니다. 요청 시 폭이나 높이 또는 둘 다 이 설정보다 큰 회신 이미지가 발생하면 서버에서 오류를 반환합니다.<br>참조 - [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 난독화 모드 요청]** | base64 인코딩이 유효한 요청에 적용되도록 하려면 활성화합니다.<br>참조 - [RequestObfusation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 잠금 모드 요청]** | 요청에 단순 해시 잠금이 포함되도록 하려면 활성화합니다.<br>참조 - [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 요청 특성]** |  |
| **[!UICONTROL 기본 이미지 파일 접미사]** | 필수.<br>경로에 파일 접미사를 포함하지 않는 경우 카탈로그 경로 및 MaskPath 필드 값에 추가되는 기본 데이터 파일 확장입니다.<br>참조 - [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 글꼴 이름]** | 텍스트 레이어 요청에서 글꼴을 제공하지 않을 경우 사용할 글꼴을 지정합니다. 지정하면 이 이미지 카탈로그의 글꼴 맵이나 기본 카탈로그의 글꼴 맵에 유효한 글꼴 이름 값이어야 합니다.<br>참조 - [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 이미지]** | 요청한 이미지를 찾을 수 없는 요청에 응답하여 반환할 기본 이미지를 제공합니다.<br>참조 - [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 이미지 모드]** | 슬라이더 상자(오른쪽 슬라이더)가 활성화되면 **[!UICONTROL 기본 이미지]** 소스 이미지에서 누락된 각 레이어를 기본 이미지로 바꾸고 컴포지션을 평소대로 반환합니다. 슬라이더 상자가 비활성화되면(왼쪽의 슬라이더) 누락된 이미지가 여러 레이어 중 하나에 불과하더라도 기본 이미지가 전체 합성 이미지를 대체합니다.<br>참조 - [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 보기 크기]** | 필수.<br>요청이 을 사용하여 보기 크기를 명시적으로 지정하지 않는 경우 서버는 이 너비와 높이보다 크지 않은 회신 이미지를 제한합니다 `wid=`, `hei=`, 또는 `scl=`.<br>참조 - [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 썸네일 크기]** | 필수.<br>속성 대신 사용됩니다. **[!UICONTROL 기본 보기 크기]** 축소판 요청(`req=tmb`). 서버는 축소판 요청(`req=tmb`)에서 을 사용하여 크기를 명시적으로 지정하지 않습니다 `wid=`, `hei=`, 또는 `scl=`.<br>참조 - [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 배경색]** | 실제 이미지 데이터를 포함하지 않는 회신 이미지의 영역을 채우는 데 사용되는 RGB 값을 지정합니다.<br>참조 - [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL JPEG 인코딩 특성]** |  |
| **[!UICONTROL 품질]** | JPEG 회신 이미지의 기본 속성을 지정합니다. 다음 **[!UICONTROL 품질]** 필드는 1 - 100 범위에 정의됩니다.<br>참조 - [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 채도 다운샘플링]** | JPEG 인코더에 사용되는 색상 변색 다운샘플링을 활성화하거나 비활성화합니다. |
| **[!UICONTROL 기본 리샘플링 모드]** | 이미지 데이터 크기 조절에 사용할 기본 리샘플링 및 보간 속성을 지정합니다. 다음 경우에 사용 `resMode` 이 요청에 지정되지 않았습니다.<br>참조 - [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |

#### 공통 축소판 속성 탭 {#common-thumbnail-attributes-tab}

이러한 설정은 축소판 이미지의 기본 모양과 정렬에 적용됩니다.

| 설정 | 설명 |
| --- | --- |
| **[!UICONTROL 축소판의 기본 배경색]** | 실제 이미지 데이터가 포함되지 않은 출력 축소판 이미지의 영역을 채우는 데 사용되는 RGB 값을 지정합니다. 축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL Fit]** 또는 **[!UICONTROL 텍스처]**.<br>참조 - [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 가로 정렬]** | 지정된 회신 이미지 사각형에서 축소판 이미지의 가로 정렬을 지정합니다. `wid=` 및 `hei=` 값.<br>축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL Fit]**.<br>다음 세 가지 수평 정렬 중에서 선택할 수 있습니다. **[!UICONTROL 가운데 정렬]**, **[!UICONTROL 왼쪽 정렬]**, 및 **[!UICONTROL 오른쪽 정렬]**.<br>참조 - [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 세로 정렬]** | 지정된 회신 이미지 사각형에서 축소판 이미지의 세로 정렬을 지정합니다. `wid=` 및 `hei=` 값. 축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL Fit]**.<br>다음 세 가지 세로 정렬 중에서 선택할 수 있습니다. **[!UICONTROL 위쪽 정렬]**, **[!UICONTROL 가운데 정렬]**, 및 **[!UICONTROL 아래쪽 정렬]**.<br>참조 - [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 캐시 사용 시간]** | 특정 카탈로그 레코드에 유효한 카탈로그 만료 값이 없는 경우 기본 만료 간격을 시간 단위로 제공합니다. 을 로 설정합니다. `-1` 만료되지 않은 것으로 표시합니다. <br>참조 - [만료](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 축소판 그림 유형]** | 특정 카탈로그 레코드에 올바른 카탈로그 ThumbType 값이 없는 경우 축소판 유형에 대한 기본값을 제공합니다. 축소판 요청에만 사용됩니다(`req=tmb`).<br>다음 세 가지 축소판 유형을 선택할 수 있습니다. **[!UICONTROL 자르기]**, **[!UICONTROL Fit]**, 및 **[!UICONTROL 텍스처]**.<br>참조 - [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 썸네일 해상도]** | 특정 카탈로그 레코드에 유효한 카탈로그 ThumbRes 값이 없는 경우 축소판 개체 해상도의 기본값을 제공합니다. 축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL 텍스처]**.<br>참조 - [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |

#### 색상 관리 속성 탭 {#color-management-attributes-tab}

이러한 설정은 이미지에 사용되는 ICC 색상 프로파일을 결정합니다.

**색상 변환 렌더링 의도**
색상 변환 렌더링 의도를 사용하면 작업 프로필의 기본 렌더링 의도를 재정의하여 소스 색상의 조정 방법을 결정할 수 있습니다. 다음 경우에 사용됩니다.

1. 기본 ICC 프로파일 중 하나는 색상 변환의 대상 색상 공간입니다.
1. 출력 장치(프린터 또는 모니터)는 이 프로파일을 나타냅니다.
1. 지정한 렌더링 의도가 이 프로필에 대해 유효합니다.

다른 렌더링 의도마다 소스 색상의 조정 방식을 결정하는 다양한 규칙이 사용됩니다.

예를 들어 **[!UICONTROL RGB 기본 색상 공간]** to **[!UICONTROL sRGB]**, 및 **[!UICONTROL CMYK 기본 색상 공간]** to **[!UICONTROL WebCoated]**.

이렇게 하면 다음 작업이 수행됩니다.

* RGB 및 CMYK 이미지에 색상 교정을 활성화합니다.
* 색상 프로필이 없는 RGB 이미지는 *sRGB* 색상 공간.
* 색상 프로파일이 없는 CMYK 이미지는 *WebCoated* 색상 공간.
* RGB 출력을 반환하고 *sRGB* 색상 공간.
* CMYK 출력을 반환하는 동적 표현물 *WebCoated* 색상 공간.

참조 - [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오.

>[!NOTE]
일반적으로 업계 표준을 충족하기 위해 Adobe에서 테스트한 선택한 색상 설정에 기본 렌더링 의도를 사용하는 것이 가장 좋습니다. 예를 들어, 북미 또는 유럽에 대한 색상 설정을 선택하는 경우 기본 색상 변환 렌더링 목적은 입니다 **[!UICONTROL 상대 색상 지표]**. 일본에 대한 색상 설정을 선택하는 경우 기본 색상 변환 렌더링 의도는 다음과 같습니다 **[!UICONTROL 지각]**.

| 설정 | 특성 |
| --- | --- |
| **[!UICONTROL CMYK 기본 색상 공간]** | CMYK 데이터의 작업 프로필로 사용할 ICC 색상 프로파일의 이름을 지정합니다. If **[!UICONTROL 지정되지 않음]** 이 선택되면 CMYK 소스 이미지가 포함된 경우 이 이미지 카탈로그에 대해 색상 관리가 비활성화됩니다. 모든 CMYK 작업 영역은 장치에 종속됩니다. 즉, 실제 잉크 및 용지 조합을 기반으로 합니다. CMYK 작업 공간 Adobe 공급 장치는 표준 상용 인쇄 조건을 기반으로 합니다.<br> 참조 - [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 회색 음영 기본 색상 공간]** | 회색 스케일 데이터의 작업 프로필로 사용할 ICC 색상 프로파일의 이름을 지정합니다. If **[!UICONTROL 지정되지 않음]** 이 선택되면 회색 크기 소스 이미지가 포함된 경우 이 이미지 카탈로그에 대해 색상 관리를 사용할 수 없습니다.<br>참조 - [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL RGB 기본 색상 공간]** | RGB 데이터의 작업 프로필로 사용할 ICC 색상 프로파일의 이름을 지정합니다. If **[!UICONTROL 지정되지 않음]** 을 선택하면 RGB 소스 이미지가 포함된 경우 이 이미지 카탈로그에 대해 색상 관리를 사용할 수 없습니다. 일반적으로 선택하는 것이 가장 좋습니다 **[!UICONTROL Adobe RGB]** 또는 **[!UICONTROL sRGB]**&#x200B;특정 장치(예: 모니터 프로필)에 대한 프로필이 아닌, **[!UICONTROL sRGB]** 웹 또는 모바일 장치용 이미지를 준비할 때는 웹 이미지를 보는 데 사용되는 표준 모니터의 색상 공간을 정의하므로 이 옵션을 사용하는 것이 좋습니다. **[!UICONTROL sRGB]** 또한 소비자 수준의 디지털 카메라의 이미지를 사용하여 작업할 때는 대부분의 카메라에서 sRGB를 기본 색상 공간으로 사용하기 때문에 유용합니다.<br>참조 - [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 색상 변환 렌더링 의도]** | **[!UICONTROL 지각]** - 색상 값 자체가 바뀔 수 있어도 인간의 눈으로 자연으로 인식되도록 색상 간의 시각 관계를 유지하는 것을 목표로 합니다. 이 의도는 색상 영역 이외의 색상이 많은 사진 이미지에 적합합니다. 이 설정은 일본 인쇄 업계의 표준 렌더링 의도입니다. |
|  | **[!UICONTROL 상대 색각]** - 소스 색상 공간의 극단적 강조 표시를 대상 색상 공간의 강조 표시와 비교하고 그에 따라 모든 색상을 이동합니다. 색상 영역 밖의 색상은 대상 색상 공간에서 재현성이 가장 가까운 색상으로 바뀝니다. 상대 색상은 이미지의 원래 색상을 [지각]보다 더 많이 유지합니다. 이 설정은 북미 및 유럽에서 인쇄하기 위한 표준 렌더링 의도입니다. |
|  | **[!UICONTROL 채도]** - 색상 정확성을 희생하여 이미지에 선명한 색상을 생성하려고 합니다. 이 렌더링 의도는 그래프 또는 차트와 같은 비즈니스 그래픽에 적합하며, 색상 간의 정확한 관계보다 밝은 포화 색상이 더 중요합니다. |
|  | **[!UICONTROL 절대 색각]** - 대상 색상 영역 내에 있는 색상을 그대로 유지합니다. 색상 영역 외의 색상은 클리핑됩니다. 대상 흰색 점으로 색상 스케일링을 수행하지 않습니다. 이러한 목적은 색상 간의 관계를 보존하지 않고 색상 정확도를 유지하기 위한 것이며 특정 장치의 출력을 시뮬레이션하는 데 적합합니다. 이 의도는 종이 색상이 인쇄된 색상에 미치는 영향을 미리 보는 데 유용합니다. |

### 자산을 공개하기 전에 테스트 {#test-assets-before-making-public}

Secure Testing 을 사용하면 안전한 테스트 환경을 정의하고 구성 가능한 IP 주소 및 범위 세트를 기반으로 강력한 B2B 솔루션을 구축할 수 있습니다. 이 기능을 사용하면 Adobe Dynamic Media 배포를 컨텐츠 관리 및 비즈니스 시스템의 아키텍처와 일치시킬 수 있습니다.

보안 테스트를 통해 게시되지 않은 컨텐츠로 웹 사이트의 스테이징 버전을 미리 볼 수 있습니다.

원할 경우 다음과 같은 이유로 자산을 공개적으로 사용할 수 있도록 하지 않고 스테이징 환경을 만드십시오.

* 공개 실행 전(웹 사이트 스테이징) 웹 사이트를 미리 봅니다.
* B2B 웹 애플리케이션에 가격을 표시하는 eCatalogs와 같이 제한된 액세스가 필요한 자산을 제공합니다.
* 제품 정보 관리 시스템, 고객 서비스 애플리케이션, 교육 사이트 등의 일부로 방화벽 뒤에 자산을 사용합니다.

>[!NOTE]
보안 테스트는 Adobe Dynamic Media Classic 액세스에 영향을 주지 않습니다. Adobe Dynamic Media Classic 보안은 일관되게 유지되며 Adobe Dynamic Media Classic 및 관련 웹 서비스에 액세스하기 위한 일반적인 자격 증명이 필요합니다.

#### 보안 테스트 작동 방식 {#how-test-assets-works}

대부분의 기업들은 방화벽 뒤에 인터넷을 사용한다. 특정 경로를 통해 또는 일반적으로 제한된 범위의 공용 IP 주소를 통해 인터넷에 액세스할 수 있습니다.

기업 네트워크에서 다음과 같은 웹 사이트를 사용하여 공개 IP 주소를 파악할 수 있습니다 [https://www.whatismyip.com](https://www.whatismyip.com/) 또는 기업 IT 조직에서 이 정보를 요청합니다.

보안 테스트를 통해 Dynamic Media Adobe은 스테이징 환경 또는 내부 애플리케이션을 위한 전용 이미지 서버를 설정합니다. 이 서버에 대한 모든 요청은 원본 IP 주소를 확인합니다. 수신 요청이 승인된 IP 주소 목록에 없으면 오류 응답이 반환됩니다. Dynamic Media 회사 Adobe 관리자는 회사의 보안 테스트 환경에 대해 승인된 IP 주소 목록을 구성합니다.

원래 요청의 위치를 확인해야 하므로 Secure Testing 서비스의 트래픽이 공용 Dynamic Media Image Server 트래픽과 같은 컨텐츠 배포 네트워크를 통해 라우팅되지 않습니다. Secure Testing Service에 대한 요청은 공용 Dynamic Media 이미지 서버와 비교하여 약간 더 높은 지연을 갖습니다.

게시되지 않은 자산은 게시하지 않고도 Secure Testing Services에서 즉시 사용할 수 있습니다. 이러한 방식으로 자산이 공개 이미지 서버에 게시되기 전에 미리 보기를 실행할 수 있습니다.

>[!NOTE]
Secure Testing Services는 내부 게시 컨텍스트에서 구성된 카탈로그 서버를 사용합니다. 따라서 회사가 Secure Testing에 게시하도록 구성되어 있는 경우, Adobe Dynamic Media의 업로드된 모든 자산을 Secure Testing 서비스에서 즉시 사용할 수 있게 됩니다. 이 기능은 자산이 업로드 시 게시하도록 표시되는지 여부에 관계없이 적용됩니다.

Secure Testing Services는 현재 다음과 같은 자산 유형 및 기능을 지원합니다.

* 이미지.
* 비네팅(서버 요청 렌더링).
* Render Server 요청(지원되지만 고객이 명시적으로 요청해야 함).
* 이미지 세트, eCatalog, render set 및 미디어 세트를 포함한 집합입니다.
* 표준 Adobe Dynamic Media 리치 미디어 뷰어입니다.
* Adobe Dynamic Media OnDemand JSP 페이지.
* PDF 파일 및 점진적으로 제공되는 비디오와 같은 정적 콘텐츠.
* HTTP 비디오 스트리밍.
* 점진적 비디오 스트리밍.

다음 자산 유형 및 기능은 현재 지원되지 않습니다.

* Adobe Dynamic Media Classic 정보 또는 eCatalog 검색
* RTMP 비디오 스트리밍
* Web-to-print
* UGC(사용자 생성 컨텐츠) 서비스

>[!IMPORTANT]
Adobe Dynamic Media의 신규 또는 기존 UGC 벡터 이미지 자산에 대한 지원은 2021년 9월 30일에 종료되었습니다.

#### Secure Testing 서비스 테스트 {#test-secure-testing-service}

Secure Testing 서비스가 예상대로 작동하는지 확인하려면 다음을 수행하십시오.

##### 계정 준비

1. Adobe 고객 지원 센터에 문의하여 계정에서 보안 테스트를 사용하도록 요청하십시오.
1. Adobe Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 게시 설정]**.
1. 이미지 서버 페이지의 **[!UICONTROL 게시 컨텍스트]** 드롭다운 목록에서 **[!UICONTROL 테스트 이미지 제공]**.
1. 을(를) 선택합니다 **[!UICONTROL 보안]** 탭.
1. 대상 **[!UICONTROL 클라이언트 주소]** 필터, 선택 **[!UICONTROL 추가]**.
1. 에서 **[!UICONTROL IP 주소]** 필드에 IP 주소를 입력합니다.
1. 에서 **[!UICONTROL 마스크]** 필드에 네트 마스크를 입력합니다.

   >[!NOTE]
   두 개 이상의 IP 주소와 네트 마스크를 추가하면 *모두* 자산 호출을 위한 IP 주소 및 모든 가 표시됩니다.

1. 다음 중 하나를 수행하십시오.

   * IP 주소를 더 추가하려면 이전 3단계를 반복합니다.
   * 다음 단계로 진행합니다.

1. 이미지 서버 페이지의 오른쪽 위 모서리에서 을(를) 선택합니다 **[!UICONTROL 저장]**.
1. 원하는 이미지를 Adobe Dynamic Media 계정에 업로드합니다.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 일부 이미지가 게시용으로 표시되어 있고 다른 이미지가 표시되지 않았는지 확인한 다음 게시 작업을 제출하십시오.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 다음 위치로 이동하여 Secure Testing 서비스의 이름을 확인합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 일반 설정]**.
1. 설정 **[!UICONTROL 서버]** 페이지의 오른쪽에 있는 서버 이름을 찾습니다. **[!UICONTROL 게시된 서버 이름]**.

서버 이름이 없거나 서버 URL이 작동하지 않는 경우 Adobe 지원 센터에 문의하십시오.

##### 웹 사이트 변형 준비

게시된 자산과 게시 취소된 자산을 연결하는 웹 사이트의 두 가지 변형이 필요합니다.

* 공개 버전 - 기존 Adobe Dynamic Media URL 구문을 사용하여 자산을 연결합니다.
* 스테이징 버전 - 동일한 구문을 사용하지만 보안 테스트 사이트 이름과 함께 자산을 연결합니다.

##### 테스트 실행

다음 테스트를 수행합니다.

1. 회사 네트워크 내에서 자산이 표시되는지 확인합니다.

   이전에 정의한 IP 주소 범위로 식별된 회사 네트워크 내에서 웹 사이트의 스테이징 버전은 게시용으로 표시되었는지 여부에 관계없이 모든 이미지를 표시합니다. 따라서 미리 보기 승인 또는 제품 출시 전에 이미지를 실수로 사용할 수 있도록 만들지 않고 테스트할 수 있습니다.

   사이트의 공개 버전에 Adobe Dynamic Media에서 이전에 경험했듯이 게시된 자산이 표시되는지 확인합니다.

1. 회사 네트워크 외부에서 게시되지 않은 자산(즉, 게시용으로 표시되지 않은 자산)이 타사 액세스로부터 보호되는지 확인합니다.

   외부(예: 홈 컴퓨터 또는 4G/5G 연결)에서 네트워크에 액세스한 다음 사이트의 공개 버전에 게시된 모든 자산이 표시되지만 게시되지 않은 컨텐츠는 표시되지 않는지 확인합니다.

   승인되지 않은 IP 주소에서 Secure Testing 서비스에 액세스하고 있으므로 스테이징 버전에서 자산이 표시되지 않는지 확인합니다.

### Dynamic Media 일반 설정 구성 {#configuring-application-general-settings}

>[!IMPORTANT]
Dynamic Media 일반 설정은 다음 경우에만 사용할 수 있습니다.
* Scene7 모드에서 Dynamic Media을 실행하고 있습니다.
* 다음 항목이 있습니다. *기존* **[!UICONTROL Dynamic Media 구성]** (in) **[!UICONTROL Cloud Services]**) 내의 아무 곳에나 삽입할 수 있습니다.
* 관리자 권한을 가진 Experience Manager 시스템 관리자입니다.


계정을 만들 때 Dynamic Media Adobe에서 자동으로 회사에 할당된 서버를 제공합니다. 이러한 서버는 웹 사이트 및 애플리케이션에 대한 URL 문자열을 구성하는 데 사용됩니다. 이러한 URL 호출은 계정에만 적용됩니다.

참조 - [Secure Testing Service 테스트](/help/assets/dm-publish-settings.md#test-assets-before-making-public).

**Dynamic Media 일반 설정을 구성하려면 다음을 수행하십시오.**

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 왼쪽 레일에서 도구 아이콘을 선택한 다음 **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 일반 설정]**.
1. 서버 페이지에서 **[!UICONTROL 게시된 서버 이름]** 및 **[!UICONTROL 원본 서버 이름]**, 그런 다음 다섯 개의 탭을 사용하여 기본 게시 설정을 구성합니다.

   * [서버](#server-general-setting)
   * [애플리케이션에 업로드](#upload-to-application)
   * [이미지 편집](#image-editing-tab) 탭
   * [PostScript](#postscript-tab) 탭
   * [Photoshop](#photoshop-tab) 탭
   * [PDF](#pdf-tab) 탭
   * [Illustrator](#illustrator-tab) 탭

   ![Dynamic Media 일반 설정 페이지](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media 일반 설정 페이지,**[!UICONTROL 이미지 편집]**탭 선택.*<br><br>

1. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 저장]**.

#### 서버 {#server-general-setting}

계정을 만들 때 Dynamic Media Adobe에서 자동으로 회사에 할당된 서버를 제공합니다. 이러한 서버는 웹 사이트 및 애플리케이션에 대한 URL 문자열을 구성하는 데 사용됩니다. 이러한 URL 호출은 계정에만 적용됩니다.

| 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 게시된 서버 이름]** | 필수.<br>이 서버는 계정과 관련된 시스템에서 생성한 모든 URL 호출에 사용되는 라이브 CDN(Content Delivery Network) 서버입니다. Adobe 기술 지원에서 이 서버 이름을 변경하지 않도록 지시하는 경우가 아니면 변경하지 마십시오. 이름은 를 사용해야 합니다 `https://` 을 가리키도록 업데이트하는 것이 좋습니다. |
| **[!UICONTROL 원본 서버 이름]** | 필수.<br>이 서버는 품질 보증 테스트에만 사용됩니다. Adobe 기술 지원 센터에서 이 서버 이름을 변경하지 마십시오. |

#### 애플리케이션에 업로드 {#upload-to-application}

* **[!UICONTROL 이미지 덮어쓰기]**

   Adobe Dynamic Media에서는 두 파일의 이름이 같을 수 없습니다. 각 항목의 Adobe Dynamic Media ID(이미지 이름에서 파일 확장명을 뺀 숫자)는 고유해야 합니다. 이 규칙 때문에 **[!UICONTROL 애플리케이션에 업로드]** 에는 덮어쓰기 가 있습니다. 이 옵션의 정확한 효과는 선택한 지정된 이미지 덮어쓰기 옵션에 따라 다릅니다. 다음 옵션은 교체 이미지를 업로드하는 방법을 지정합니다. 원본 이미지를 바꾸거나 중복 이미지가 되는지 여부. 중복 이미지 이름은 `-1`. 예, `chair.tif` 가 이름이 변경되었습니다. `chair-1.tif`. 이러한 옵션은 원본 폴더와 다른 폴더에 업로드된 이미지나 원래 파일 확장명(예: JPG, TIF 또는 PNG)이 다른 이미지에 영향을 줍니다.

   | 이미지 덮어쓰기 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL 동일한 기본 에셋 이름/확장명으로 현재 폴더에 덮어쓰기]** | 기본값.<br>이 옵션은 교체에 대한 가장 엄격한 규칙입니다. 교체 이미지를 원본과 동일한 폴더에 업로드하고 교체 이미지의 파일 확장명이 원본과 동일해야 합니다. 이러한 요구 사항을 충족하지 않으면 복제본이 만들어집니다. |
   | **[!UICONTROL 확장명에 상관없이 동일한 기본 이름으로 현재 폴더에 덮어쓰기]** | 교체 이미지를 원본과 동일한 폴더로 업로드해야 하지만 파일 이름 확장명은 원본과 다를 수 있습니다. 예를 들어 chair.tif는 chair.jpg를 대체합니다. |
   | **[!UICONTROL 동일한 기본 에셋 이름/확장명으로 모든 폴더에 덮어쓰기]** | 교체 이미지의 파일 확장명이 원본 이미지와 동일해야 합니다(예: chair.jpg는 chair.tif가 아니라 chair.jpg로 대체해야 함). 그러나 대체 이미지를 원본과 다른 폴더에 업로드할 수 있습니다. 업데이트된 이미지는 새 폴더에 있습니다. 파일을 원래 위치에서 더 이상 찾을 수 없습니다. |
   | **[!UICONTROL 확장명에 상관없이 동일한 기본 에셋 이름으로 모든 폴더에 덮어쓰기]** | 이 옵션은 가장 포괄적인 대체 규칙입니다. 대체 이미지를 원본과 다른 폴더에 업로드하고, 다른 파일 확장자를 가진 파일을 업로드하고, 원래 파일을 바꿀 수 있습니다. 원본 파일이 다른 폴더에 있는 경우 대체 이미지는 업로드된 새 폴더에 있습니다. |

* **[!UICONTROL 자르기 유지]**

   기존 수동 자르기 정의의 보존을 제어합니다.

   참조 - `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 및 [AssetsJob 재처리](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)둘 다 Dynamic Media 뷰어 참조 가이드에 있습니다.

#### 기본 업로드 옵션 {#default-upload-options}

##### 이미지 편집 탭 {#image-editing-tab}

이 필터를 사용하면 최종 다운샘플링된 이미지에 대해 선명하게 하기 필터 효과를 세밀하게 조정할 수 있습니다. 이 옵션을 사용하면 효과의 강도, 효과의 반경(픽셀 단위 측정) 및 무시되는 대비 임계값을 제어할 수 있습니다.

[언샵 마스크] 효과는 Photoshop의 [언샵 마스크] 필터와 동일한 옵션을 사용합니다. 이름에서 알 수 있듯이 언샵 마스크는 선명하게 하는 필터입니다.

| 언샵 마스크 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 양]** | 필수.<br>가장자리 픽셀에 적용되는 대비 양을 제어합니다.<br>그것을 효과의 강도로 생각해 보세요. Adobe Dynamic Media의 언샵 마스크 값과 Adobe Photoshop의 금액 값의 주요 차이점은 Photoshop의 크기가 1%~500%라는 것입니다. Adobe Dynamic Media에서 값 범위는 `0.0` to `5.0`. Adobe Dynamic Media의 값 5.0은 Photoshop의 500%와 거의 같습니다. 0.9값은 90%와 같은 값입니다. |
| **[!UICONTROL 반경]** | 필수.<br>효과의 반경을 제어합니다.<br>값 범위는 다음과 같습니다 `0` to `250`. 효과는 이미지의 모든 픽셀에서 실행되며 모든 방향으로 모든 픽셀에서 발산됩니다. 반지름은 픽셀 단위로 측정됩니다. 예를 들어 2000 x 2000 픽셀 이미지와 500 x 500 픽셀 이미지에 대해 비슷한 선명하게 하기 효과를 가져오려면 200 x 2000 픽셀 이미지에 두 픽셀의 반경을 설정합니다. 그런 다음 500 x 500 픽셀 이미지에 한 픽셀의 반경 값을 설정합니다. 픽셀이 많은 이미지에 더 큰 값이 사용됩니다. |
| **[!UICONTROL 임계값]** | 필수.<br>임계값은 언샵 마스크 필터를 적용할 때 무시되는 대비 범위입니다. 이 필터를 사용할 때 이미지에 &quot;노이즈&quot;가 도입되지 않도록 이 효과가 중요합니다. 값 범위는 다음과 같습니다 `0` - `255`: 회색 음영 이미지에 있는 명도 단계 수입니다. `0`= 검정, `128`= 50% 회색 및 `255`= 흰색.<br>임계값 `12` 약간의 변화를 무시하면 피부 색조 밝기가 나타나지만, 속눈썹이 피부에 닿는 것과 같은 대비가 있는 부위에 가장자리 대비를 추가할 수 있습니다.<br>누군가의 얼굴 사진이 있는 경우, [언샵 마스크]는 이미지의 수축 부위에 영향을 줍니다. 예를 들어, 속눈썹과 피부의 접촉은 뚜렷한 대조 영역과 부드러운 피부 자체를 만들어 냅니다. 아무리 매끄러운 피부라도 휘도 값의 미묘한 변화를 나타낸다. 임계값을 사용하지 않는 경우 필터는 스킨 픽셀에서 이러한 미묘한 변경 사항을 적용합니다. 이에 따라, 속눈썹의 대비가 증가하면서 잡음과 바람직하지 않은 효과를 만들어 냄으로써 선명도가 향상된다.<br>이 문제를 방지하기 위해 부드러운 피부와 같이 대비가 크게 변경되지 않는 픽셀을 무시하도록 필터에 알리는 임계값 이 도입되었습니다.<br>앞서 표시된 지퍼 그래픽에서 지퍼 옆에 있는 텍스처를 확인합니다. 임계값이 너무 낮아 노이즈를 억제할 수 없으므로 이미지 소음이 표시됩니다. |
| **[!UICONTROL 모노크롬]** | 선명하게 마스크 이미지 밝기(강도)를 해제하려면 선택합니다.<br>각 색상 구성 요소를 개별적으로 언샵 마스크하려면 선택 취소합니다. |

참조 - [Adobe Dynamic Media 및 이미지 서버에서 이미지 선명하게 하기](/help/assets/assets/sharpening_images.pdf).

##### PostScript 탭 {#postscript-tab}

Adobe PostScript® 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다.

Adobe Dynamic Media에서 Adobe PostScript®(EPS) 파일을 사용할 수 있습니다. Adobe Dynamic Media은 이러한 파일을 업로드할 때 이러한 파일을 구성하는 명령을 제공합니다.

PostScript(EPS) 이미지 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다.

| PostScript 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | 파일의 벡터 그래픽을 비트맵 형식으로 변환하려면 [래스터화]를 선택합니다. |
| **[!UICONTROL 렌더링된 이미지의 투명 배경 유지]** | 파일의 배경 투명도를 유지합니다. |
| **[!UICONTROL 해상도 (픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 파일에 인치당 표시되는 픽셀 수를 결정합니다. |
| **[!UICONTROL 색상 공간]** | ・ **[!UICONTROL 자동 감지]** - 파일의 색상 공간을 유지합니다.<br>・ **[!UICONTROL 강제 RGB]** - RGB 색상 공간으로 변환<br>・ **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환<br>・ **[!UICONTROL 회색 음영으로 강제 적용]** - 회색 음영 색상 공간으로 변환 |

##### Photoshop 탭 {#photoshop-tab}

Adobe® Photoshop® 파일에서 템플릿을 만들고, 레이어를 유지 관리하며, 레이어의 이름을 지정하는 방법을 지정하고, 텍스트를 추출하고, 이미지가 템플릿에 고정된 방식을 지정할 수 있습니다.

| Photoshop 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 레이어 유지]** | PSD의 레이어(있는 경우)를 개별 자산으로 이동합니다. 자산 레이어는 PSD과 계속 연결됩니다. [세부 사항 보기]에서 PSD 파일을 열고 레이어 패널을 선택하여 볼 수 있습니다. PSD 파일에서 레이어 보기 및 편집을 참조하십시오. |
| **[!UICONTROL 템플릿 만들기]** | PSD 파일의 레이어에서 템플릿을 만듭니다. |
| **[!UICONTROL 텍스트 추출]** | 사용자가 뷰어에서 텍스트를 검색할 수 있도록 텍스트를 추출합니다. |
| **[!UICONTROL 레이어를 배경 크기로 확장]** | 분리된 이미지 레이어의 크기를 배경 레이어의 크기로 확장합니다. |
| **[!UICONTROL 레이어 이름 지정]** | 분리된 이미지 레이어의 크기를 배경 레이어의 크기로 확장합니다.<br>・ **[!UICONTROL 레이어 이름]** - PSD 파일에서 레이어 이름 뒤에 이미지의 이름을 지정합니다. 예를 들어 원래 PSD 파일에서 가격 태그라는 레이어가 가격 태그라는 이미지가 됩니다. 그러나 PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름(배경, 레이어 1, 레이어 2 등)인 경우 해당 이미지의 이름은 PSD 파일의 레이어 번호 뒤에 지정됩니다. <br>・ **[!UICONTROL Photoshop 및 레이어 번호]** - 원본 레이어 이름을 무시하고 PSD 파일에서 레이어 번호 뒤에 이미지의 이름을 지정합니다. 이미지의 이름은 Photoshop 파일 이름과 추가된 레이어 번호로 지정됩니다. 예를 들어, `Spring Ad.psd` 이름이 지정됨 `Spring Ad_2` Photoshop에 기본값이 아닌 이름이 포함되어 있더라도<br>・ **[!UICONTROL Photoshop 및 레이어 이름]** - PSD 파일 뒤에 레이어 이름 또는 레이어 번호를 사용하여 이미지 이름을 지정합니다. PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름인 경우 레이어 번호가 사용됩니다. 예를 들어 이름이 인 레이어가 있습니다 `Price Tag` PSD 파일에서 `SpringAd` 이름이 지정됨 `Spring Ad_Price Tag`. 기본 이름이 레이어 2인 레이어를 라고 합니다 `Spring Ad_2`. |
| **[!UICONTROL 앵커]** | PSD 파일에서 생성된 계층화된 컴포지션에서 생성된 템플릿에 이미지가 고정되는 방식을 지정합니다. 기본적으로 앵커는 중심입니다. 가운데 앵커는 교체 이미지의 종횡비에 상관없이 교체 이미지가 동일한 공간을 가장 잘 채울 수 있도록 합니다. 템플릿을 참조하고 매개 변수 대체를 사용할 때 이 이미지를 대체하는 다른 측면을 가진 이미지가 동일한 공간을 효과적으로 차지합니다. 템플릿의 할당된 공간을 채우기 위해 응용 프로그램에 교체 이미지가 필요한 경우 다른 설정으로 변경합니다. |

##### PDF 탭 {#pdf-tab}

파일을 래스터화하고, 검색어와 링크를 추출하고, 해상도를 설정하고, 색상 공간을 선택하도록 선택할 수 있습니다.

| PDF 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | ・ **[!UICONTROL 없음]** - PDF 처리가 완료되지 않았습니다.<br>・ **[!UICONTROL 축소판]** - PDF 파일의 각 페이지를 잘라내어 축소판 이미지로 변환합니다.<br> ・ **[!UICONTROL 래스터화]** - PDF 파일의 페이지를 이동하고 벡터 그래픽을 비트맵 이미지로 변환합니다. eCatalog를 만들려면 이 옵션을 선택합니다. |
| **[!UICONTROL 추출]** | ・ **[!UICONTROL 없음]** - PDF에서 검색어 또는 링크가 추출되지 않습니다.<br>・ **[!UICONTROL 검색어]** - eCatalog 뷰어에서 키워드로 파일을 검색할 수 있도록 PDF 파일에서 검색어를 추출합니다.<br>・ **[!UICONTROL 링크]** - PDF 파일에서 링크를 추출하여 eCatalog 뷰어에서 사용되는 이미지 맵으로 변환합니다.<br>・ **[!UICONTROL 검색 단어 및 링크]** - eCatalog 뷰어에서 사용할 검색어와 링크를 모두 추출합니다. |
| **[!UICONTROL 해상도 (픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 PDF 파일에 인치당 표시되는 픽셀 수를 결정합니다. 기본값은 150입니다. |
| **[!UICONTROL 색상 공간]** | ・ **[!UICONTROL 자동 감지]** - PDF 파일의 색상 공간을 유지합니다.<br>・ **[!UICONTROL 강제 RGB]** - RGB 색상 공간으로 변환<br>・ **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환<br>・ **[!UICONTROL 회색 음영으로 강제 적용]** - 회색 음영 색상 공간으로 변환 |

##### Illustrator 탭 {#illustrator-tab}

Adobe Illustrator® 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다.

Adobe Dynamic Media에서 Adobe® Illustrator®(AI) 파일을 사용할 수 있습니다. Adobe Dynamic Media은 이러한 파일을 업로드할 때 이러한 파일을 구성하는 명령을 제공합니다.

AI(Illustrator) 이미지 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다. PostScript 및 Illustrator 파일 형식 옵션은 업로드 작업 옵션 상자의 포스트스크립트 옵션 및 Illustrator 옵션 아래의 업로드 화면에서 사용할 수 있습니다.


| Illustrator 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | 파일의 벡터 그래픽을 비트맵 형식으로 변환하려면 [래스터화]를 선택합니다. |
| **[!UICONTROL 렌더링된 이미지의 투명 배경 유지]** | 파일의 배경 투명도를 유지합니다. |
| **[!UICONTROL 해상도 (픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 파일에 인치당 표시되는 픽셀 수를 결정합니다. |
| **[!UICONTROL 색상 공간]** | ・ **[!UICONTROL 자동 감지]** - 파일의 색상 공간을 유지합니다.<br>・ **[!UICONTROL 강제 RGB]** - RGB 색상 공간으로 변환<br>・ **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환<br>・ **[!UICONTROL 회색 음영으로 강제 적용]** - 회색 음영 색상 공간으로 변환 |


**[!UICONTROL 기본 색상 프로필]** - 다음을 참조하십시오. [색상 관리 구성](#configuring-color-management) 추가 정보.

>[!NOTE]
기본적으로, 선택하면 15개의 표현물이 표시됩니다 **[!UICONTROL 표현물]** 및 15개의 뷰어 사전 설정을 선택할 때 **[!UICONTROL 뷰어]** 를 클릭합니다. 이 제한을 늘릴 수 있습니다. 자세한 내용은 [표시되는 이미지 사전 설정 수를 늘립니다](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 또는 [표시되는 뷰어 사전 설정 수를 늘립니다](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

### (선택 사항) 추가 구성 작업 {#additional-configuration-tasks}

옵션 설정 및 구성 작업은 다음과 같습니다.

* [지원되는 형식에 대한 MIME 유형 편집](#editing-mime-types-for-supported-formats) **릭: 계속?**
* [지원되지 않는 형식에 대한 MIME 유형 추가](#adding-mime-types-for-unsupported-formats) **릭: 계속?**
* [일괄처리 집합 사전 설정을 만들어 이미지 세트 및 스핀 세트 자동 생성](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) **릭: 계속?**

* **[!UICONTROL 호환성 속성]** - **릭: 아직도 필요한가? 클래식** 이 설정을 사용하면 텍스트 레이어의 선행 및 후행 단락을 이전 버전과의 호환성을 위해 버전 3.6의 단락으로 처리할 수 있습니다.
* **[!UICONTROL 지역화 지원]** - **릭: 아직도 필요한가? 클래식** 이러한 설정을 사용하면 여러 로케일 속성을 관리할 수 있습니다. 또한 로케일 맵 문자열을 지정하여 뷰어의 다양한 도구 설명에 대해 지원할 언어를 정의할 수 있습니다. 설정에 대한 자세한 정보 **[지역화 지원]**&#x200B;를 참조하십시오. [자산 현지화를 설정할 때의 고려 사항](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### 지원되는 형식에 대한 MIME 유형 편집 {#editing-mime-types-for-supported-formats}

**릭: 그대로 유지??**

Dynamic Media에서 처리할 자산 유형을 정의하고 고급 자산 처리 매개 변수를 사용자 지정할 수 있습니다. 예를 들어 자산 처리 매개 변수를 지정하여 다음을 수행할 수 있습니다.

* Adobe PDF을 eCatalog 자산으로 변환합니다.
* 개인화를 위해 Adobe Photoshop 문서(.PSD)을 배너 템플릿 자산으로 변환합니다.
* Adobe Illustrator 파일(.AI) 또는 Adobe Photoshop Encapsulated PostScript® 파일(.EPS)을 래스터화합니다.
* [비디오 프로필](/help/assets/video-profiles.md) 및 [이미징 프로필](/help/assets/image-profiles.md) 는 각각 비디오와 이미지 처리를 정의하는 데 사용할 수 있습니다.

[자산 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.

**지원되는 형식에 대한 MIME 유형을 편집하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.
1. 왼쪽 레일에서 다음 위치로 이동합니다.

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME 유형](assets/mimetypes.png)

1. mimeTypes 폴더 아래에서 mime 유형을 선택합니다.
1. CRXDE Lite 페이지의 오른쪽의 아래 부분:

   * 를 두 번 클릭합니다. **[!UICONTROL 활성화됨]** 필드. 기본적으로 모든 자산 MIME 유형이 활성화되어 있습니다(다음으로 설정). **[!UICONTROL true]**)으로 그룹화됩니다. 즉, 자산이 Dynamic Media에 동기화되어 처리됩니다. 이 자산 MIME 유형을 처리하지 않도록 하려면 이 설정을 다음으로 변경하십시오 **[!UICONTROL false]**.

   * 두 번 탭 **[!UICONTROL jobParam]** 연결된 텍스트 필드를 엽니다. 자세한 내용은 [지원되는 Mime 유형](/help/assets/assets-formats.md#supported-mime-types) 허용되는 처리 매개 변수 값 목록의 경우 주어진 mime 유형에 사용할 수 있습니다.

1. 다음 중 하나를 수행하십시오.

   * 추가 MIME 유형을 편집하려면 3-4단계를 반복합니다.
   * CRXDE Lite 페이지의 메뉴 모음에서 **[!UICONTROL 모두 저장]**.

1. 페이지의 왼쪽 위 모서리에서 을(를) 선택합니다 **[!UICONTROL CRXDE Lite]** Experience Manager으로 돌아갑니다.

#### 지원되지 않는 형식에 대한 MIME 유형 추가 {#adding-mime-types-for-unsupported-formats}

**릭: 그대로 유지??**

Experience Manager Assets에서 지원되지 않는 형식에 대한 사용자 지정 MIME 유형을 추가할 수 있습니다. 이전에 MIME 유형을 이동하여 CRXDE Lite에 추가하는 새 노드가 Experience Manager에서 삭제되지 않도록 하십시오 `image_`. 또한 이 활성화된 값이 **[!UICONTROL false]**.

**지원되지 않는 형식에 대한 MIME 유형을 추가하려면 다음을 수행합니다.**

1. Experience Manager에서 로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 새 브라우저 탭이 **[!UICONTROL Adobe Experience Manager 웹 콘솔 구성]** 페이지.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 페이지에서 아래로 스크롤하여 이름으로 이동합니다. *Adobe CQ Scene7 Asset MIME 유형 서비스* 다음 스크린샷과 같습니다. 이름 오른쪽에서 을(를) 선택합니다. **[!UICONTROL 구성 값 편집]** (연필 아이콘).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 설정 **Adobe CQ Scene7 Asset MIME 유형 서비스** 페이지에서 더하기 기호 아이콘 &lt;+>을 선택합니다. 새 MIME 유형을 추가할 더하기 기호를 선택하는 테이블의 위치는 매우 작습니다.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 유형 `DWG=image/vnd.dwg` 방금 추가한 빈 텍스트 필드에서 을 클릭합니다.

   예 `DWG=image/vnd.dwg` 는 데모용으로만 사용됩니다. 여기에 추가하는 MIME 유형은 다른 지원되지 않는 형식일 수 있습니다.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 페이지의 오른쪽 아래 모서리에서 을(를) 선택합니다. **[!UICONTROL 저장]**.

   이때 열려 있는 Adobe Experience Manager 웹 콘솔 구성 페이지가 있는 브라우저 탭을 닫을 수 있습니다.

1. 열려 있는 Experience Manager 콘솔이 있는 브라우저 탭으로 돌아갑니다.
1. Experience Manager에서 로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 왼쪽 레일에서 다음 위치로 이동합니다.

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. MIME 유형을 드래그합니다 `image_vnd.dwg` 바로 위에 떨어뜨려주세요 `image_` 다음 스크린샷에 표시된 것처럼 트리에서 입니다.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. MIME 유형 `image_vnd.dwg` 여전히 선택됨, **[!UICONTROL 속성]** 탭, **[!UICONTROL 활성화됨]** 행, 아래 **[!UICONTROL 값]** 열 헤더에서 값을 두 번 눌러 엽니다 **[!UICONTROL 값]** 드롭다운 목록.
1. 유형 `false` 필드에서 (또는 를) 선택합니다. **[!UICONTROL false]** 드롭다운 목록에서).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. CRXDE Lite 페이지의 왼쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 모두 저장]**.

#### 일괄처리 집합 사전 설정을 만들어 이미지 세트 및 스핀 세트 자동 생성 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

**릭: 그대로 유지??**

자산을 Dynamic Media에 업로드하는 동안 일괄처리 집합 사전 설정을 사용하여 이미지 세트 또는 스핀 세트 만들기를 자동화합니다.

먼저 자산을 집합으로 그룹화하는 방법에 대한 이름 지정 규칙을 정의합니다. 그런 다음 고유한 이름이 지정되고 자체 포함된 지침 세트인 배치 세트 사전 설정을 만듭니다. 사전 설정된 레서피에서 정의된 이름 지정 규칙과 일치하는 이미지를 사용하여 세트를 구성하는 방법을 정의해야 합니다.

파일을 업로드하면 Dynamic Media에서 활성 사전 설정에서 정의된 명명 규칙과 일치하는 모든 파일이 있는 세트를 자동으로 만듭니다.

##### 기본 이름 지정 구성

배치 집합 사전 설정 배합식에서 사용되는 기본 이름 지정 규칙을 만듭니다. 배치 집합 사전 설정 정의에서 선택한 기본 이름 지정 규칙은 일괄 생성 세트에 필요한 모든 것입니다. 사용자가 정의하는 기본 이름 지정 규칙을 사용하도록 배치 세트 사전 설정이 생성됩니다. 회사에서 정의한 기본 이름에 예외가 있는 경우 특정 컨텐츠 세트에 필요한 대체 사용자 지정 이름 지정 규칙을 사용하여 일괄처리 집합 사전 설정을 최대 많이 만들 수 있습니다.

일괄처리 집합 사전 설정 기능을 사용하기 위해 기본 이름 지정 규칙을 설정할 필요는 없지만, 기본 이름 지정 규칙을 사용하는 것이 좋습니다. 일괄 세트 생성을 간소화할 수 있도록 한 세트에 그룹화할 이름 지정 규칙의 요소를 수만큼 정의할 수 있습니다.

또는 **[!UICONTROL 코드 보기]** 사용 가능한 양식 필드가 없는 경우 이 보기에서는 완전히 정규 표현식을 사용하여 이름 지정 규칙 정의를 만듭니다.

정의에 두 요소 일치 및 기본 이름을 사용할 수 있습니다. 이러한 필드를 사용하면 이름 지정 규칙의 모든 요소를 정의하고 해당 요소가 포함된 집합의 이름을 지정하는 데 사용되는 규칙의 부분을 식별할 수 있습니다. 회사의 개별 이름 지정 규칙은 이러한 각 요소에 대해 하나 이상의 정의 라인을 사용하는 경우가 많습니다. 고유 정의에 많은 선을 사용하고 기본 이미지, 색상 요소, 대체 보기 요소 및 견본 요소와 같은 개별 요소로 그룹화할 수 있습니다.

**기본 이름을 구성하려면**

**릭: 그대로 유지??**

1. 를 엽니다. [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 계정에 로그인합니다.

   자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 페이지 상단 근처에 있는 탐색 막대에서 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 기본 이름 지정]**.
1. 선택 **[!UICONTROL 양식 보기]** 또는 **[!UICONTROL 코드 보기]** 를 입력하여 각 요소에 대한 정보를 보고 입력할 수 있습니다.

   을(를) 선택할 수 있습니다 **[!UICONTROL 코드 보기]** 양식 선택과 함께 정규 표현식 값 작성을 보려면 확인란을 선택합니다. 양식 보기에서 어떤 이유로든 사용자를 제한하는 경우 이름 지정 규칙의 요소를 정의하는 데 도움이 되도록 이러한 값을 입력하거나 변경할 수 있습니다. 값을 양식 보기에서 구문 분석할 수 없는 경우 양식 필드는 비활성 상태가 됩니다.

   >[!NOTE]
   비활성화된 양식 필드는 정규 표현식이 올바른지 확인하지 않습니다. 결과 라인 뒤에 각 요소에 대해 작성하는 정규 표현식의 결과가 표시됩니다. 전체 정규 표현식은 페이지 하단에 표시됩니다.

1. 필요에 따라 각 요소를 확장하고 사용할 이름 지정 규칙을 입력합니다.
1. 필요에 따라 다음 중 하나를 수행합니다.

   * 선택 **[!UICONTROL 추가]** 요소에 대해 다른 이름 지정 규칙을 추가하려면 다음을 수행하십시오.
   * 선택 **[!UICONTROL 제거]** 요소에 대한 이름 지정 규칙을 삭제하려면

1. 다음 중 하나를 수행하십시오.

   * 선택 **[!UICONTROL 다른 이름으로 저장]** 사전 설정의 이름을 입력합니다.
   * 선택 **[!UICONTROL 저장]** 기존 사전 설정을 편집하는 경우

##### 배치 집합 사전 설정 만들기

Dynamic Media은 일괄처리 집합 사전 설정을 사용하여 뷰어에 표시할 이미지 세트(대체 이미지, 색상 옵션, 360spin)로 자산을 구성합니다. 일괄처리 집합 사전 설정은 Dynamic Media의 자산 업로드 프로세스와 함께 자동으로 실행됩니다.

일괄처리 집합 사전 설정을 생성, 편집 및 관리할 수 있습니다. 배치 세트 사전 설정 정의에는 두 가지 유형이 있습니다. 설정할 수 있는 기본 이름 지정 규칙에 대해 하나씩, 그리고 사용자 지정 이름 지정 규칙에 대해 하나씩 설정합니다.

양식 필드 메서드를 사용하여 묶음 세트 사전 설정을 정의하거나 정규 표현식을 사용할 수 있는 코드 메서드를 정의할 수 있습니다. 기본 이름 지정에서와 마찬가지로, 양식 보기에서 정의하는 동시에 코드 보기를 선택하고 정규 표현식을 사용하여 정의를 작성할 수 있습니다. 또는 한 보기를 선택 취소하여 단독 또는 다른 보기를 사용할 수 있습니다.

**배치 세트 사전 설정을 생성하려면**

**릭: 그대로 유지??**

1. 를 엽니다. [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 계정에 로그인합니다.

   자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 페이지 상단 근처에 있는 탐색 막대에서 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 배치 집합 사전 설정]**.

   **[!UICONTROL 양식 보기]**&#x200B;세부 사항 페이지의 오른쪽 위 모서리에 설정된 대로 이 기본 보기입니다.

1. 사전 설정 목록 패널에서 **[!UICONTROL 추가]** 화면 오른쪽의 [세부 정보] 패널에서 정의 필드를 활성화하려면
1. 세부 정보 패널의 사전 설정 이름 필드에 사전 설정 이름을 입력합니다.
1. 배치 세트 유형 드롭다운 메뉴에서 사전 설정 유형을 선택합니다.
1. 다음 중 하나를 수행하십시오.

   * 이전에 **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 기본 이름 지정]**, 확장 **[!UICONTROL 자산 이름 지정 규칙]**&#x200B;를 입력한 다음 파일 이름 지정 드롭다운 목록에서 **[!UICONTROL 기본값]**.

   * 사전 설정을 설정할 때 새 이름 지정 규칙을 정의하려면 **[!UICONTROL 자산 이름 지정 규칙]**&#x200B;를 입력한 다음 파일 이름 지정 드롭다운 목록에서 **[!UICONTROL 사용자 지정]**.

1. 시퀀스 순서에 대해 Dynamic Media에서 세트를 그룹화한 후 이미지가 표시되는 순서를 정의합니다.

   기본적으로 자산은 영숫자 순서로 지정됩니다. 그러나 쉼표로 구분된 정규 표현식 목록을 사용하여 순서를 정의할 수 있습니다.

1. 이름 지정 및 생성 규칙 설정의 경우 자산 이름 지정 규칙에서 정의한 기본 이름에 접미사 또는 접두사를 지정합니다. 또한 Dynamic Media 폴더 구조 내에서 세트가 만들어지는 위치를 정의합니다.

   여러 세트를 정의하는 경우 자산 자체가 포함된 폴더와 세트를 구분하십시오. 예를 들어, 이미지 세트 폴더를 만들고 생성된 세트를 여기에 지정합니다.

1. 세부 정보 패널에서 **[!UICONTROL 저장]**.
1. 선택 **[!UICONTROL 활성]** 새 사전 설정 이름 옆에 표시됩니다.

   사전 설정을 활성화하면 Dynamic Media에 자산을 업로드할 때 세트 사전 설정이 적용되어 세트가 생성됩니다.

##### 2D 스핀 세트의 자동 생성을 위한 배치 세트 사전 설정 생성

배치 세트 유형을 사용할 수 있습니다 **[!UICONTROL 다축 스핀 세트]** 2D 스핀 세트 생성을 자동화하는 레서피를 생성합니다. 이미지 그룹화에서는 이미지 자산이 다차원 배열의 해당 위치에서 제대로 정렬되도록 행 및 열 정규 표현식을 사용합니다. 다축 스핀 세트에 있어야 하는 최소 또는 최대 행 또는 열 수는 없습니다.

예를 들어 이름이 인 다중 축 스핀 세트를 만든다고 가정합니다. `spin-2dspin`. 3개의 행을 포함하는 스핀 세트 이미지 세트와 행당 12개의 이미지가 있습니다. 이미지의 이름은 다음과 같습니다.

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

이 정보를 사용하여 배치 세트 유형 배합식을 다음과 같이 생성할 수 있습니다.

![chlimage_1-560](assets/chlimage_1-560.png)

스핀 세트의 공유 자산 이름 부분에 대한 그룹이 **[!UICONTROL 일치]** 필드(강조 표시됨) 행 및 열이 포함된 자산 이름의 변수 부분이 **[!UICONTROL 행]** 및 **[!UICONTROL 열]** 필드(각각)를 반환합니다.

스핀 세트를 업로드하고 게시하면 아래에 나열된 2D 스핀 세트 레서피의 이름을 활성화합니다 **[!UICONTROL 일괄처리 집합 사전 설정]** 에서 **[!UICONTROL 업로드 작업 옵션]** 대화 상자

**2D 스핀 세트의 자동 생성을 위한 배치 세트 사전 설정을 생성하려면:**

**릭: 그대로 유지??**

1. 를 엽니다. [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 계정에 로그인합니다.

   자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 페이지 상단 근처에 있는 탐색 막대에서 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 배치 집합 사전 설정]**.

   **[!UICONTROL 양식 보기]**&#x200B;세부 사항 페이지의 오른쪽 위 모서리에 설정된 대로 이 기본 보기입니다.

1. 사전 설정 목록 패널에서 **[!UICONTROL 추가]** 화면 오른쪽의 [세부 정보] 패널에서 정의 필드를 활성화하려면
1. 세부 정보 패널의 사전 설정 이름 필드에 사전 설정 이름을 입력합니다.
1. 배치 세트 유형 드롭다운 메뉴에서 **[!UICONTROL 자산 세트]**.
1. 하위 유형 드롭다운 목록에서 을 선택합니다 **[!UICONTROL 다축 스핀 세트]**.
1. 확장 **[!UICONTROL 자산 이름 지정 규칙]**&#x200B;를 입력한 다음 파일 이름 지정 드롭다운 목록에서 **[!UICONTROL 사용자 지정]**.
1. 를 사용하십시오 **[!UICONTROL 일치]** 그리고 선택적으로 **[!UICONTROL 기본 이름]** 속성을 사용하여 그룹을 구성하는 이미지 자산 이름에 대한 정규 표현식을 정의합니다.

   예를 들어 리터럴 Match 정규 표현식은 다음과 같을 수 있습니다.

   `(w+)-w+-w+`

1. 확장 **[!UICONTROL 행 열 위치]**&#x200B;그런 다음 2D 스핀 세트 배열 내에서 이미지 자산의 위치에 대한 이름 형식을 정의합니다.

   파일 이름에서 행 또는 열 위치를 포함하려면 괄호를 사용합니다.

   예를 들어 행 정규 표현식의 경우 다음과 같을 수 있습니다.

   `\w+-R([0-9]+)-\w+`

   또는

   `\w+-(\d+)-\w+`

   열 정규 표현식의 경우 다음과 같을 수 있습니다.

   `\w+-\w+-C([0-9]+)`

   또는

   `\w+-\w+-C(\d+)`

   위의 샘플은 데모용으로만 사용됩니다. 원하는 대로 정규 표현식을 만들 수 있습니다.

   >[!NOTE]
   행과 열 정규 표현식의 조합이 다차원 스핀 세트 배열 내에서 자산의 위치를 확인할 수 없는 경우, 자산이 세트에 추가되지 않습니다. 오류가 기록됩니다.

1. 이름 지정 및 생성 규칙 설정의 경우 자산 이름 지정 규칙에서 정의한 기본 이름에 접미사 또는 접두사를 지정합니다.

   또한 Dynamic Media Classic 폴더 구조 내에서 스핀 세트가 만들어지는 위치를 정의합니다.

   여러 세트를 정의하는 경우 자산 자체가 포함된 폴더와 세트를 구분하십시오. 예를 들어, 생성된 세트를 여기에 배치할 스핀 세트 폴더를 만듭니다.

1. 세부 정보 패널에서 **[!UICONTROL 저장]**.
1. 선택 **[!UICONTROL 활성]** 새 사전 설정 이름 옆에 표시됩니다.

   사전 설정을 활성화하면 Dynamic Media에 자산을 업로드할 때 세트 사전 설정이 적용되어 세트가 생성됩니다.

### (선택 사항) Dynamic Media - Scene7 모드의 성능 조정 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

**릭: 그대로 유지??**

Dynamic Media - Scene7 모드가 원활하게 실행되도록 하려면 다음 동기화 성능/확장성 미세 조정 팁을 권장합니다.

* 다양한 파일 형식을 처리하기 위해 사전 정의된 작업 매개 변수 업데이트.
* 사전 정의된 Granite 워크플로우(비디오 자산) 큐 작업자 스레드를 업데이트합니다.
* 사전 정의된 Granite 임시 워크플로우(이미지 및 비비디오 자산) 큐 작업자 스레드를 업데이트합니다.
* Dynamic Media Classic 서버에 대한 최대 업로드 연결 업데이트.

#### 다양한 파일 형식을 처리하기 위해 사전 정의된 작업 매개 변수를 업데이트합니다

**릭: 그대로 유지??**

파일을 업로드할 때 처리 속도를 높이기 위해 작업 매개 변수를 조정할 수 있습니다. 예를 들어 PSD 파일을 업로드하지만 템플릿으로 처리하려는 경우가 아니라면 레이어 추출을 false(off)로 설정할 수 있습니다. 이 경우 튜닝된 작업 매개 변수는 다음과 같이 나타납니다. `process=None&createTemplate=false`.

템플릿 만들기를 설정하려면 다음 매개 변수를 사용하십시오. `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe은 PDF, PostScript® 및 PSD 파일에 다음과 같은 &quot;튜닝된&quot; 작업 매개 변수를 사용하는 것을 권장합니다.

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 파일 유형 | 권장 작업 매개 변수 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

이러한 매개 변수를 업데이트하려면 [MIME 유형 기반 Assets/Dynamic Media Classic 업로드 작업 매개 변수 지원 활성화](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Granite 임시 워크플로우 큐 업데이트 {#updating-the-granite-transient-workflow-queue}

**릭: 그대로 유지??**

Granite Transit 워크플로우 큐는 **[!UICONTROL DAM 자산 업데이트]** 워크플로우. Dynamic Media에서 이미지 수집 및 처리에 사용됩니다.

**Granite Transient 워크플로우 큐를 업데이트하려면:**

1. 다음으로 이동 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 및 검색 **큐: Granite Transient 워크플로 큐**.

   >[!NOTE]
   OSGi PID가 동적으로 생성되므로 직접 URL 대신 텍스트 검색이 필요합니다.

1. 에서 **[!UICONTROL 최대 병렬 작업 수]** 필드에서 숫자를 원하는 값으로 변경합니다.

   추가 **[!UICONTROL 최대 병렬 작업 수]** Dynamic Media에 대한 대규모 파일 업로드를 적절하게 지원하기 위해. 정확한 값은 하드웨어 용량에 따라 다릅니다. 특정 시나리오에서 초기 마이그레이션 또는 1회 벌크 업로드 등 큰 값을 사용할 수 있습니다. 그러나 큰 값(예: 코어 수의 2배)을 사용하면 다른 동시 활동에 부정적인 영향을 줄 수 있습니다. 따라서 특정 사용 사례를 기반으로 값을 테스트 및 조정합니다.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

#### Granite 워크플로우 큐 업데이트 {#updating-the-granite-workflow-queue}

**릭: 그대로 유지??**

Granite 워크플로우 큐는 비임시 워크플로우에 사용됩니다. Dynamic Media에서는 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우.

**Granite 워크플로우 큐를 업데이트하려면:**

1. 다음으로 이동 `https://<server>/system/console/configMgr` 및 검색 **큐: Granite Workflow 큐**.

   >[!NOTE]
   OSGi PID가 동적으로 생성되므로 직접 URL 대신 텍스트 검색이 필요합니다.

1. 에서 **[!UICONTROL 최대 병렬 작업 수]** 필드에서 숫자를 원하는 값으로 변경합니다.

   최대 병렬 작업 을 확장하여 Dynamic Media에 대한 많은 파일 업로드를 적절하게 지원할 수 있습니다. 정확한 값은 하드웨어 용량에 따라 다릅니다. 특정 시나리오에서 초기 마이그레이션 또는 1회 벌크 업로드 등 큰 값을 사용할 수 있습니다. 그러나 큰 값(예: 코어 수의 2배)을 사용하면 다른 동시 활동에 부정적인 영향을 줄 수 있습니다. 따라서 특정 사용 사례를 기반으로 값을 테스트 및 조정합니다.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

#### Dynamic Media Classic 업로드 연결 업데이트 {#updating-the-scene-upload-connection}

**릭: 그대로 유지??**

Scene7 업로드 연결 설정은 Experience Manager 자산을 Dynamic Media Classic 서버에 동기화합니다.

**Dynamic Media Classic 업로드 연결을 업데이트하려면:**

1. 다음으로 이동 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 에서 **[!UICONTROL 연결 수]** 필드 및/또는 **[!UICONTROL 활성 작업 시간 초과]** 필드에서 원하는 대로 번호를 변경합니다.

   다음 **[!UICONTROL 연결 수]** 설정은 Dynamic Media 업로드에 Experience Manager이 허용되는 최대 HTTP 연결 수를 제어합니다. 일반적으로 10개의 연결의 사전 정의된 값으로 충분합니다.

   다음 **[!UICONTROL 활성 작업 시간 초과]** 설정 은 업로드된 Dynamic Media 자산이 게재 서버에 게시될 대기 시간을 결정합니다. 이 값은 기본적으로 2100초 또는 35분입니다.

   대부분의 사용 사례에서 2100으로 설정하면 충분합니다.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### (선택 사항) 복제할 자산을 필터링합니다 {#optional-filtering-assets-for-replication}

**릭: 그대로 유지**

Dynamic Media이 아닌 배포에서는 *모두* Experience Manager 작성 환경의 Experience Manager 게시 노드에 대한 자산(이미지 및 비디오 모두)입니다. Experience Manager 게시 서버에서도 자산을 전달하므로 이 워크플로우가 필요합니다.

그러나 Dynamic Media 배포에서는 자산이 Cloud Service 방식으로 전달되므로 동일한 자산을 Experience Manager 게시 노드에 복제할 필요가 없습니다. 이러한 &quot;하이브리드 게시&quot; 워크플로우를 통해 추가 스토리지 비용과 자산 복제 처리 시간이 늘어납니다. 사이트 페이지와 같은 다른 컨텐츠는 Experience Manager 게시 노드에서 계속 제공됩니다.

필터는 다음과 같은 방법을 제공합니다 *제외* 자산이 복제되지 않고 Experience Manager 게시 노드에 있습니다.

#### 복제에 기본 자산 필터 사용 {#using-default-asset-filters-for-replication}

**릭: 그대로 유지**

이미징, 비디오 또는 둘 다에 Dynamic Media을 사용하는 경우, Adobe이 제공하는 기본 필터를 그대로 사용할 수 있습니다. 다음 필터는 기본적으로 활성화되어 있습니다.

|  | 필터 | MIME 유형 | 표현물 |
| --- | --- | --- | --- |
| Dynamic Media 이미지 제공 | 필터 이미지<br>필터 세트 | 다음으로 시작 **image/**<br>&#x200B;다음 포함 **애플리케이션/** 다음으로 끝남 **설정**. | 곧바로 사용할 수 있는 &quot;필터 이미지&quot;(대화형 이미지를 포함하여 단일 이미지 자산에 적용) 및 &quot;필터 세트&quot;(스핀 세트, 이미지 세트, 혼합 미디어 세트 및 회전 메뉴 세트에 적용)는 다음과 같습니다.<br>・ 원본 이미지 및 정적 이미지 표현물 복제에서 제외합니다. |
| Dynamic Media 비디오 제공 | 필터 비디오 | 다음으로 시작 **video/** | 즉시 사용 가능한 &quot;필터 비디오&quot;는 다음과 같습니다.<br>・ 원본 비디오 및 정적 축소판 그림 표현물 복제에서 제외합니다. |

>[!NOTE]
필터는 MIME 유형에 적용되며 경로별로 지정할 수 없습니다.

#### 복제에 대한 자산 필터 사용자 지정 {#customizing-asset-filters-for-replication}

**릭: 그대로 유지**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스하고 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` 를 클릭하여 필터를 검토합니다.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 필터에 대한 MIME 유형을 정의하려면 다음과 같이 MIME 유형을 찾을 수 있습니다.

   왼쪽 레일에서 를 확장합니다. `content > dam > <locate_your_asset> > jcr:content > metadata`, 그런 다음 테이블에서 `dc:format`.

   다음 그래픽은 자산 경로의 예입니다 `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   다음 사항에 주의하십시오. `dc:format` 자산 `Fiji Red.jpg` is `image/jpeg`.

   형식에 관계없이 모든 이미지에 이 필터를 적용하려면 값을 로 설정하십시오 `image/*` 여기서 `*` 는 모든 형식의 모든 이미지에 적용되는 정규 표현식입니다.

   JPEG 유형의 이미지에만 필터를 적용하려면 값을 입력합니다. `image/jpeg`.

1. 복제에서 포함하거나 제외할 변환을 정의합니다.

   복제에 대해 필터링할 수 있는 문자는 다음과 같습니다.

   | 사용할 문자 | 복제용으로 자산을 필터링하는 방법 |
   | --- | --- |
   | * | 와일드카드 문자 |
   | + | 복제할 자산 포함 |
   | - | 복제에서 자산 제외 |

   다음으로 이동 `content/dam/<locate your asset>/jcr:content/renditions`.

   다음 그래픽은 자산 표현물의 예입니다.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   원본만 복제하려는 경우 `+original`.
