---
title: Dynamic Media 구성 - Scene7 모드
description: Dynamic Media - Scene7 모드를 구성하는 방법에 대해 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '6508'
ht-degree: 3%

---

# Dynamic Media 구성 - Scene7 모드{#configuring-dynamic-media-scene-mode}

개발, 스테이징 및 프로덕션과 같은 다양한 환경에 대해 설정된 Adobe Experience Manager을 사용하는 경우 이러한 환경 각각에 대해 Dynamic Media Cloud Service을 구성합니다.

## Dynamic Media - Scene7 모드의 아키텍처 다이어그램 {#architecture-diagram-of-dynamic-media-scene-mode}

다음 아키텍처 다이어그램은 Dynamic Media - Scene7 모드가 작동하는 방식을 설명합니다.

새 아키텍처를 통해 Experience Manager은 기본 소스 자산을 담당하고 자산 처리 및 게시를 위한 Dynamic Media과의 동기화를 담당합니다.

1. 기본 소스 자산이 Experience Manager에 업로드되면 Dynamic Media에 복제됩니다. 이때 Dynamic Media은 비디오 인코딩 및 이미지의 동적 변형과 같은 모든 에셋 처리 및 렌디션 생성을 처리합니다.
(Dynamic Media - Scene7 모드에서 기본 업로드 파일 크기는 2GB 이하입니다. 2GB에서 최대 15GB의 파일 업로드 크기를 사용하려면 [(선택 사항) 2GB보다 큰 에셋의 업로드를 위해 Dynamic Media - Scene7 모드 구성](#optional-config-dms7-assets-larger-than-2gb)을 참조하십시오.
1. 렌디션이 생성되면 Experience Manager은 원격 Dynamic Media 렌디션에 안전하게 액세스하고 미리 볼 수 있습니다(바이너리가 Experience Manager 인스턴스로 다시 전송되지 않음).
1. 콘텐츠를 게시하고 승인할 준비가 되면 Dynamic Media 서비스를 트리거하여 콘텐츠를 게재 서버로 푸시하고 CDN(Content Delivery Network)에서 콘텐츠를 캐시합니다.

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>다음 기능 목록을 사용하려면 Adobe Experience Manager - Dynamic Media과 함께 번들로 제공되는 기본 CDN을 사용해야 합니다. 이러한 기능에서는 다른 모든 사용자 지정 CDN이 지원되지 않습니다.
>
>* [스마트 이미징](/help/assets/imaging-faq.md)
>* [캐시 무효화](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [핫링크 보호](/help/assets/hotlink-protection.md)
>* [컨텐츠의 HTTP/2 전달](/help/assets/http2.md)
>* CDN 수준에서 URL 리디렉션
>* Akamai ChinaCDN(중국에서 최적의 전송을 위해)

## Scene7 모드에서 Dynamic Media 활성화 {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)은(는) 기본적으로 비활성화되어 있습니다. Dynamic Media 기능을 활용하려면 활성화해야 합니다.

>[!WARNING]
>
>Dynamic Media - Scene7 모드는 *Experience Manager 작성자 인스턴스에만 사용됩니다*. 따라서 Experience Manager 작성자 인스턴스에서 `runmode=dynamicmedia_scene7`을(를) 구성해야 하고, Experience Manager Publish 인스턴스에서는 *구성하지*&#x200B;해야 합니다.

Dynamic Media을 사용하려면 터미널 창에 다음을 입력하여 명령줄에서 `dynamicmedia_scene7` 실행 모드를 사용하여 Experience Manager을 시작하십시오(예: 사용된 포트는 4502임).

```shell {.line-numbers}
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (선택 사항) Dynamic Media 사전 설정 및 구성을 6.3에서 6.5 Zero Downtime으로 마이그레이션 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

이제 Experience Manager Dynamic Media을 6.3에서 6.4 또는 6.5로 업그레이드하면 중단 없이 배포할 수 있습니다. 모든 사전 설정 및 구성을 CRXDE Lite에서 `/etc`에서 `/conf`(으)로 마이그레이션하려면 다음 curl 명령을 실행하십시오.

>[!NOTE]
>
>호환성 모드에서 Experience Manager 인스턴스를 실행하는 경우(즉, 호환성 패키지가 설치되어 있는 경우) 이러한 명령을 실행할 필요가 없습니다.

호환성 패키지가 있거나 없는 모든 업그레이드의 경우 다음 Linux® curl 명령을 실행하여 원래 Dynamic Media과 함께 제공된 기본 즉시 사용 가능한 뷰어 사전 설정을 복사할 수 있습니다.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

`/etc`에서 만든 사용자 지정 뷰어 사전 설정 및 구성을 `/conf`(으)로 마이그레이션하려면 다음 Linux® curl 명령을 실행하십시오.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 벌크 자산 마이그레이션용 기능 팩 18912 설치 {#installing-feature-pack-for-bulk-asset-migration}

기능 팩 18912 설치는 *선택 사항*&#x200B;입니다.

기능 팩 18912을 사용하면 FTP를 통해 자산을 대량 수집하거나 Experience Manager 시 Dynamic Media - 하이브리드 모드 또는 Dynamic Media Classic에서 Dynamic Media - Scene7 모드로 자산을 마이그레이션할 수 있습니다. [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)에서 사용할 수 있습니다.

자세한 내용은 [일괄 에셋 18912을 위한 기능 팩 설치](/help/assets/bulk-ingest-migrate.md)를 참조하십시오.

## Cloud Service에서 Dynamic Media 구성 만들기 {#configuring-dynamic-media-cloud-services}

<!-- **Before you configure Dynamic Media** - After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials.

   ![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**To create a Dynamic Media Configuration in Cloud Services:** -->

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스하고 도구 아이콘을 선택한 다음 **[!UICONTROL Cloud Service]** > **[!UICONTROL Dynamic Media 구성]**(으)로 이동합니다.
1. Dynamic Media 구성 브라우저 페이지의 왼쪽 창에서 **[!UICONTROL 전역]**(**[!UICONTROL 전역]** 왼쪽에 있는 폴더 아이콘을 선택하지 않음)을 선택한 다음 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL Dynamic Media 구성 만들기]** 페이지에서 제목, Dynamic Media 계정 전자 메일 주소, 암호를 입력한 다음 지역을 선택합니다. 이 정보는 프로비저닝 이메일에서 Adobe으로 제공됩니다. 이메일을 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.

   **[!UICONTROL Dynamic Media에 연결]**&#x200B;을 선택합니다.

1. **[!UICONTROL 암호 변경]** 대화 상자의 **[!UICONTROL 새 암호]** 필드에 8~25자로 구성된 새 암호를 입력합니다. 암호에는 다음 각 항목 중 하나 이상이 포함되어야 합니다.

   * 대문자
   * 소문자
   * 숫자
   * 특수 문자: `# $ & . - _ : { }`

   **[!UICONTROL 현재 암호]** 필드는 의도적으로 미리 채워져 있으며 상호 작용에서 숨겨집니다.

   필요한 경우 비밀번호 눈 아이콘을 선택하여 비밀번호를 표시하고 입력한 비밀번호의 철자를 확인할 수 있습니다. 암호를 숨기려면 아이콘을 다시 선택합니다.

1. **[!UICONTROL 암호 반복]** 필드에서 새 암호를 다시 입력한 다음 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

   **[!UICONTROL Dynamic Media 구성 만들기]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 저장]**&#x200B;을 선택하면 새 암호가 저장됩니다.

   **[!UICONTROL 암호 변경]** 대화 상자에서 **[!UICONTROL 취소]**&#x200B;를 선택한 경우 새로 만든 Dynamic Media 구성을 저장할 때 새 암호를 입력해야 합니다.

   [Dynamic Media 암호 변경](#change-dm-password)도 참조하세요.

1. 연결에 성공하면 다음을 설정하십시오. 별표(*)가 있는 제목은 필수입니다.

   * **[!UICONTROL 회사]** - Dynamic Media 계정의 이름입니다.

     >[!IMPORTANT]
     >
     >Cloud Service의 Dynamic Media 구성은 Experience Manager 인스턴스에서 하나만 지원됩니다. 구성을 두 개 이상 추가하지 마십시오. Experience Manager 인스턴스의 여러 Dynamic Media 구성이 Adobe에서 지원되거나 권장되지 _않습니다_.

     <!-- CQDOC-19579 and CQDOC-19612 -->

     [Dynamic Media 회사 별칭 계정 구성](/help/assets/dm-alias-account.md)도 참조하세요.

   * **[!UICONTROL 회사 루트 폴더 경로]**

   * **[!UICONTROL Assets 게시]** - 다음 세 가지 옵션 중에서 선택할 수 있습니다.
      * **[!UICONTROL 즉시]**&#x200B;은(는) 에셋이 업로드되면 시스템이 에셋을 수집하여 URL/임베드를 즉시 제공함을 의미합니다. 에셋을 게시하는 데 필요한 사용자 개입이 없습니다.
      * **[!UICONTROL 활성화 시]**&#x200B;는 URL/포함 링크가 제공되기 전에 먼저 자산을 명시적으로 게시해야 함을 의미합니다.<br><!-- CQDOC-17478, Added March 9, 2021-->Experience Manager 6.5.8부터 Publish 인스턴스 Experience Manager은 **[!UICONTROL 활성화 시]** 게시 모드에서만 `dam:scene7Domain` 및 `dam:scene7FileStatus`과(와) 같은 정확한 Dynamic Media 메타데이터 값을 반영합니다. 이 기능을 사용하려면 서비스 팩 8을 설치한 다음 Experience Manager을 다시 시작하십시오. Sling 구성 관리자로 이동합니다. `Scene7ActivationJobConsumer Component`에 대한 구성을 찾거나 새 구성을 만드십시오. **[!UICONTROL Dynamic Media 게시 후 메타데이터 복제]** 확인란을 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

        ![Dynamic Media 게시 후 메타데이터 복제 확인란](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 선택적 Publish]** 이 옵션을 사용하면 Dynamic Media에 게시할 폴더를 제어할 수 있습니다. 스마트 자르기 또는 동적 변환과 같은 기능을 사용하거나 미리 보기 위해 Experience Manager에 독점적으로 게시할 폴더를 결정할 수 있습니다. 동일한 자산은 공개 도메인에 전달하기 위해 Dynamic Media에 게시된 *not*&#x200B;입니다.<br>여기 **[!UICONTROL Dynamic Media 클라우드 구성]**&#x200B;에서 이 옵션을 설정할 수 있습니다. 원하는 경우 폴더의 **[!UICONTROL 속성]**&#x200B;에서 폴더 수준에서 이 옵션을 설정하도록 선택할 수 있습니다.<br>Dynamic Media에서 [선택적 Publish 작업](/help/assets/selective-publishing.md)을 참조하세요.<br>나중에 이 구성을 변경하거나 나중에 폴더 수준에서 변경하면 해당 변경 사항은 이후에 업로드하는 새 자산에만 영향을 줍니다. 폴더에 있는 기존 자산의 게시 상태는 **[!UICONTROL 빠른 Publish]** 또는 **[!UICONTROL 게시 관리]** 대화 상자에서 수동으로 변경할 때까지 그대로 유지됩니다.

   * **[!UICONTROL 보안 미리 보기 서버]** - 보안 변환 미리 보기 서버의 URL 경로를 지정할 수 있습니다. 즉, 렌디션이 생성되면 Experience Manager은 원격 Dynamic Media 렌디션에 안전하게 액세스하고 미리 볼 수 있습니다(바이너리가 Experience Manager 인스턴스로 다시 전송되지 않음).
Adobe 고유한 회사의 서버나 특수 서버를 사용할 특별한 배열이 없는 경우에는 이 설정을 지정된 대로 두는 것이 좋습니다.

   * **[!UICONTROL 모든 콘텐츠 동기화]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->기본적으로 선택됨. Dynamic Media 동기화에서 자산을 선택적으로 포함하거나 제외하려면 이 옵션을 선택 취소합니다. 이 옵션을 선택 해제하면 다음 두 가지 Dynamic Media 동기화 모드 중에서 선택할 수 있습니다.

   * **[!UICONTROL Dynamic Media 동기화 모드]**
      * **[!UICONTROL 기본적으로 사용됨]** - 폴더만 제외하도록 표시하지 않으면 기본적으로 모든 폴더에 구성이 적용됩니다. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 기본적으로 비활성화됨]** - 선택한 폴더를 Dynamic Media에 동기화하도록 명시적으로 표시할 때까지 구성이 폴더에 적용되지 않습니다.
선택한 폴더를 Dynamic Media에 동기화하도록 표시하려면 자산 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 선택합니다. **[!UICONTROL 세부 정보]** 탭의 **[!UICONTROL Dynamic Media 동기화 모드]** 드롭다운 목록에서 다음 세 가지 옵션 중 하나를 선택하십시오. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다. *다음 세 가지 옵션은 이전에&#x200B;**[!UICONTROL 모든 콘텐츠 동기화]**&#x200B;를 선택한 경우 사용할 수 없습니다.* 또한 [Dynamic Media의 폴더 수준에서 선택적 Publish 작업](/help/assets/selective-publishing.md)을 참조하십시오.
         * **[!UICONTROL 상속됨]** - 폴더에 명시적 동기화 값이 없습니다. 대신 폴더는 상위 폴더 중 하나 또는 클라우드 구성의 기본 모드에서 동기화 값을 상속합니다. 상속된 의 자세한 상태는 도구 설명을 통해 표시됩니다.
         * **[!UICONTROL 하위 폴더에 대해 사용]** - Dynamic Media에 동기화하려면 이 하위 트리의 모든 항목을 포함하십시오. 폴더별 설정은 클라우드 구성의 기본 모드를 재정의합니다.
         * **[!UICONTROL 하위 폴더에 대해 사용 안 함]** - 이 하위 트리의 모든 항목을 Dynamic Media으로 동기화하지 못하도록 제외합니다.

   >[!NOTE]
   >
   >Dynamic Media - Scene7 모드에서는 버전 관리를 지원하지 않습니다. Also, delayed activation applies only if **[!UICONTROL Publish Assets]** in the Edit Dynamic Media Configuration page is set to **[!UICONTROL Upon Activation]**, and then only until the first time the asset is activated.
   >
   >자산이 활성화되면 모든 업데이트가 즉시 S7 Delivery에 라이브로 게시됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. Dynamic Media 콘텐츠가 게시되기 전에 안전하게 미리 보기 위해 Experience Manager 작성자는 토큰 기반 유효성 검사를 사용하므로 Experience Manager 작성자는 기본적으로 Dynamic Media 콘텐츠를 미리 봅니다. 그러나 더 많은 IP를 &quot;허용 목록&quot;하여 사용자가 콘텐츠를 안전하게 미리 볼 수 있도록 액세스할 수 있습니다. Experience Manager에서 이 작업을 설정하려면 [이미지 서버에 대한 Dynamic Media Publish 설정 구성 - 보안 탭](/help/assets/dm-publish-settings.md#security-tab)을 참조하십시오.

ACL(액세스 제어 목록) 권한 사용과 같이 구성을 추가로 사용자 지정하려면 선택적으로 [(선택 사항) Dynamic Media - Scene7 모드에서 고급 설정 구성](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)에 있는 작업을 완료할 수 있습니다.

<!-- 1. To securely preview Dynamic Media content before it gets published, Experience Manager uses token-based validation and hence Experience Manager Author previews Dynamic Media content by default. However, you can *allowlist* more IPs to provide users access to securely preview content. To set up this action in Experience Manager, see [Configure Dynamic Media Publish Setup for Image Server - Security tab](/help/assets/dm-publish-settings.md#security-tab).     * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**. -->

이제 기본 구성이 완료되었습니다. Dynamic Media - Scene7 모드를 사용할 준비가 되었습니다.

### Dynamic Media 암호 변경 {#change-dm-password}

Dynamic Media의 암호 만료는 현재 시스템 날짜로부터 100년으로 설정되어 있습니다.

암호에는 다음 각 항목 중 하나 이상이 포함되어야 합니다.

* 대문자
* 소문자
* 숫자
* 특수 문자: `# $ & . - _ : { }`

필요한 경우 비밀번호 눈 아이콘을 선택하여 비밀번호를 표시하고 입력한 비밀번호의 철자를 확인할 수 있습니다. 암호를 숨기려면 아이콘을 다시 선택합니다.

**[!UICONTROL Dynamic Media 구성 편집]** 페이지의 오른쪽 상단에서 **[!UICONTROL 저장]**&#x200B;을 선택하면 변경된 암호가 저장됩니다.

**Dynamic Media에 대한 암호를 변경하려면:**

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 콘솔 왼쪽에서 도구 아이콘을 선택한 다음 **[!UICONTROL Cloud Service] > [!UICONTROL Dynamic Media 구성]**(으)로 이동합니다.
1. Dynamic Media 구성 브라우저 페이지의 왼쪽 창에서 **[!UICONTROL 전역]**&#x200B;을(를) 선택합니다. **[!UICONTROL global]** 왼쪽에 있는 폴더 아이콘을 선택하지 마십시오. 그런 다음 **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL Dynamic Media 구성 편집]** 페이지의 **[!UICONTROL 암호]** 필드 바로 아래에서 **[!UICONTROL 암호 변경]**&#x200B;을 선택합니다.
1. **[!UICONTROL 암호 변경]** 대화 상자에서 다음 작업을 수행합니다.

   * **[!UICONTROL 새 암호]** 필드에 새 암호를 입력합니다.

     **[!UICONTROL 현재 암호]** 필드는 의도적으로 미리 채워져 있으며 상호 작용에서 숨겨집니다.

   * **[!UICONTROL 암호 반복]** 필드에서 새 암호를 다시 입력한 다음 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

1. **[!UICONTROL Dynamic Media 구성 편집]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 저장]**&#x200B;을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 선택합니다.

## (선택 사항) Dynamic Media - Scene7 모드에서 고급 설정 구성 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Dynamic Media - Scene7 모드의 구성 및 설정을 추가로 사용자 지정하거나 성능을 최적화하려면 다음 *옵션* 작업 중 하나 이상을 완료할 수 있습니다.

* [(선택 사항) Dynamic Media - Scene7 모드에서 ACL 권한을 활성화합니다](#optional-enable-acl)

* [(선택 사항) 2GB보다 큰 에셋의 업로드를 위해 Dynamic Media - Scene7 모드 구성](#optional-config-dms7-assets-larger-than-2gb)

* [(선택 사항) Dynamic Media 설정 및 구성 - Scene7 모드 설정](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(선택 사항) Dynamic Media 성능 조정 - Scene7 모드](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(선택 사항) 복제할 자산을 필터링합니다](#optional-filtering-assets-for-replication)

### (선택 사항) Dynamic Media - Scene7 모드에서 액세스 제어 목록 권한 활성화 {#optional-enable-acl}

AEM에서 Dynamic Media - Scene7 모드를 실행하면 PlatformServerServlet에서 ACL(액세스 제어 목록) 권한을 확인하지 않고 현재 `/is/image`개의 요청을 보안 미리 보기 이미지 제공에 전달합니다. 그러나 ACL 권한을 *활성화*&#x200B;할 수 있습니다. 승인된 `/is/image` 요청을 전달합니다. 사용자에게 에셋에 액세스할 권한이 없는 경우 &quot;403 - 금지됨&quot; 오류가 표시됩니다.

**Dynamic Media - Scene7 모드에서 ACL 권한을 활성화하려면 다음 작업을 수행하십시오.**

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. **[!UICONTROL Adobe Experience Manager 웹 콘솔 구성]** 페이지에 새 브라우저 탭이 열립니다.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 페이지에서 *Adobe CQ Scene7 PlatformServer*(으)로 스크롤합니다.

1. 이름 오른쪽에서 연필 아이콘(**[!UICONTROL 구성 값 편집]**)을 선택합니다.

1. **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** 페이지에서 다음 두 가지 설정에 대한 확인란을 선택합니다.

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` - 활성화되면 이 설정은 저장할 120초(2분)(기본값) 동안 권한 결과를 캐시합니다.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` - 활성화되면 이 설정은 Dynamic Media 이미지 서버를 통해 에셋을 미리 보는 동안 사용자의 액세스를 확인합니다.

   ![Dynamic Media - Scene7 모드에서 액세스 제어 목록 설정 사용](/help/assets/assets-dm/acl.png)

1. 페이지의 오른쪽 아래 모서리에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### (선택 사항) 2GB보다 큰 에셋의 업로드를 위해 Dynamic Media - Scene7 모드 구성 {#optional-config-dms7-assets-larger-than-2gb}

Dynamic Media - Scene7 모드에서 기본 에셋 업로드 파일 크기는 2GB 이하입니다. 그러나 2GB보다 크고 최대 15GB의 자산 업로드를 선택적으로 구성할 수 있습니다.

이 기능을 사용하려면 다음 사전 요구 사항과 점에 유의하십시오.

* Dynamic Media - Scene7 모드에서 서비스 팩 6.5.4.0 이상으로 Experience Manager 6.5를 실행해야 합니다.
* 이 대용량 업로드 기능은 [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) 고객에게만 지원됩니다.
* Experience Manager 인스턴스가 Amazon S3 또는 Microsoft® Azure Blob 저장소로 구성되어 있는지 확인하십시오.

  >[!NOTE]
  >
  >Blob 스토리지 구성에서 이 대용량 업로드 기능은 AzureSas에서 지원되지 않으므로 액세스 키 및 비밀 키로 Azure Blob 스토리지를 구성합니다.

* Oak의 [직접 이진 액세스 다운로드](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)를 사용할 수 있습니다(Oak의 *직접 이진 액세스 업로드*&#x200B;는 필요하지 않음).

  다이렉트 이진 액세스 다운로드를 사용하려면 데이터 저장소 구성에서 `presignedHttpDownloadURIExpirySeconds > 0` 속성을 설정합니다. 값은 더 큰 바이너리를 다운로드할 수 있을 만큼 충분히 길어야 하며 다시 시도할 수 있습니다.

* 15GB보다 큰 Assets은 업로드되지 않습니다. (크기 제한은 아래 8단계에서 설정됩니다.)
* 폴더에서 **[!UICONTROL Dynamic Media 재처리]** 자산 워크플로우가 트리거되면 Dynamic Media 회사와 이미 동기화 중인 모든 큰 자산을 재처리합니다. 그러나 큰 에셋이 폴더에서 아직 동기화되지 않은 경우 에셋이 업로드되지 않습니다. 따라서 Dynamic Media의 기존 대용량 에셋을 동기화하려면 개별 에셋에서 **[!UICONTROL Dynamic Media 재처리]** 에셋 워크플로우를 실행할 수 있습니다.

**2GB보다 큰 에셋의 업로드를 위해 Dynamic Media - Scene7 모드를 구성하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.

1. CRXDE Lite 창에서 다음 중 하나를 수행합니다.

   * 왼쪽 레일에서 다음 경로로 이동합니다.

     `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 도구 모음 아래의 CRXDE Lite 경로 필드에 위 경로를 복사하여 붙여 넣은 다음 `Enter`을(를) 누릅니다.

1. 왼쪽 레일에서 `fileupload`을(를) 마우스 오른쪽 단추로 클릭한 다음 팝업 메뉴에서 **[!UICONTROL 오버레이 노드]**&#x200B;를 선택합니다.

   ![오버레이 노드 옵션](/help/assets/assets-dm/uploadassets15gb_a.png)

1. 오버레이 노드 대화 상자에서 **[!UICONTROL 노드 유형 일치]** 확인란을 선택하여 옵션을 활성화(켜기)한 다음 **[!UICONTROL 확인]**&#x200B;을 선택합니다.

   ![오버레이 노드 대화 상자](/help/assets/assets-dm/uploadassets15gb_b.png)

1. CRXDE Lite 창에서 다음 중 하나를 수행합니다.

   * 왼쪽 레일에서 다음 오버레이 노드 경로로 이동합니다.

     `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 도구 모음 아래의 CRXDE Lite 경로 필드에 위 경로를 복사하여 붙여 넣은 다음 `Enter`을(를) 누릅니다.

1. **[!UICONTROL 속성]** 탭의 **[!UICONTROL 이름]** 열에서 `sizeLimit`을(를) 찾습니다.
1. `sizeLimit` 이름 오른쪽의 **[!UICONTROL 값]** 열 아래에서 값 필드를 두 번 클릭합니다.
1. 크기 제한을 원하는 최대 업로드 크기로 늘릴 수 있도록 적절한 값을 바이트 단위로 입력합니다. 예를 들어 업로드 자산 크기 제한을 10GB로 늘리려면 값 필드에 `10737418240`을(를) 입력합니다.
최대 15GB(`2013265920`바이트)의 값을 입력할 수 있습니다. 이 경우 15GB보다 큰 업로드된 에셋은 업로드되지 않습니다.

   ![크기 제한 값](/help/assets/assets-dm/uploadassets15gb_c.png)

1. CRXDE Lite 창의 왼쪽 상단 모서리 근처에서 **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

   *이제 다음을 수행하여 Adobe Granite 워크플로 외부 프로세스 작업 처리기에 대한 시간 제한을 설정합니다.*

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 다음 중 하나를 수행합니다.

   * 다음 URL 경로로 이동합니다.

     `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 위의 경로를 복사하여 브라우저의 URL 필드에 붙여넣습니다. `localhost:4502`을(를) 자신의 Experience Manager 인스턴스로 바꾸십시오.

1. **[!UICONTROL Adobe Granite 워크플로 외부 프로세스 작업 처리기]** 대화 상자의 **[!UICONTROL 최대 시간 초과]** 필드에서 값을 `18000`초(5시간)로 설정합니다. 기본값은 10800초(3시간)입니다.

   ![최대 시간 초과 값](/help/assets/assets-dm/uploadassets15gb_d.png)

1. 대화 상자의 오른쪽 아래 모서리에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   *이제 다음을 수행하여 Scene7 다이렉트 이진 업로드 프로세스 단계에 대한 시간 제한을 설정합니다.*

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**(으)로 이동합니다.
1. 워크플로 모델 페이지에서 **[!UICONTROL Dynamic Media 인코딩 비디오]**&#x200B;를 선택합니다.
1. 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. 워크플로우 페이지에서 **[!UICONTROL Scene7 다이렉트 이진 업로드]** 프로세스 단계를 두 번 클릭합니다.
1. **[!UICONTROL 단계 속성]** 대화 상자의 **[!UICONTROL 공통]** 탭, **[!UICONTROL 고급 설정]** 제목, **[!UICONTROL 시간 초과]** 필드에 `18000`초(5시간)의 값을 입력합니다. 기본값은 `3600`초(1시간)입니다.
1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.
1. **[!UICONTROL 동기화]**&#x200B;를 선택하십시오.
1. **[!UICONTROL DAM 자산 업데이트]** 워크플로 모델 및 **[!UICONTROL Dynamic Media 재처리]** 워크플로 모델에 대해 14~21단계를 반복합니다.

### (선택 사항) Dynamic Media 설정 및 구성 - Scene7 모드 설정 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [이미지 서버에 대한 Dynamic Media Publish 설정 구성](/help/assets/dm-publish-settings.md)
* [Dynamic Media 일반 설정 구성](/help/assets/dm-general-settings.md)
* [색상 관리 구성](#configuring-color-management)
* [지원되는 형식의 MIME 유형 편집](#editing-mime-types-for-supported-formats)
* [지원되지 않는 형식에 대한 MIME 유형 추가](#adding-mime-types-for-unsupported-formats)
* [이미지 집합 및 회전 집합을 자동으로 생성하는 일괄처리 집합 사전 설정을 만듭니다](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)(Dynamic Media Classic 사용자 인터페이스에서 완료)

#### 이미지 서버에 대한 Dynamic Media Publish 설정 구성 {#publishing-setup-for-image-server}

Dynamic Media Publish 설정 페이지는 Adobe Dynamic Media 서버에서 웹 사이트 또는 애플리케이션으로 에셋을 전달하는 방법을 결정하는 기본 설정을 구성합니다.

[이미지 서버에 대한 Dynamic Media Publish 설치 구성](/help/assets/dm-publish-settings.md)을 참조하십시오.

#### Dynamic Media 일반 설정 구성 {#configuring-application-general-settings}

Dynamic Media **[!UICONTROL Publish 서버 이름]** URL과 **[!UICONTROL 원본 서버 이름]** URL을 구성합니다. 특정 사용 사례에 따라 **[!UICONTROL 응용 프로그램에 업로드]** 설정 및 **[!UICONTROL 기본 업로드 옵션]**&#x200B;을 지정할 수도 있습니다.

[Dynamic Media 일반 설정 구성](/help/assets/dm-general-settings.md)을 참조하십시오.

#### 색상 관리 구성 {#configuring-color-management}

Dynamic Media 색상 관리를 사용하면 올바른 에셋에 색상을 지정할 수 있습니다. 색상 수정을 사용하면 수집된 에셋의 색상 공간(RGB, CMYK, 회색) 및 임베드된 색상 프로파일이 유지됩니다. 동적 렌디션을 요청하면 CMYK, RGB 또는 회색 출력을 사용하여 이미지 색상이 대상 색상 공간으로 수정됩니다.

[이미지 사전 설정 구성](/help/assets/managing-image-presets.md)을 참조하십시오.

>[!NOTE]
>
>에셋의 세부 사항 보기에서 **[!UICONTROL 렌디션]**&#x200B;을 선택하면 기본적으로 15개의 렌디션이 표시되고 **[!UICONTROL 뷰어]**&#x200B;를 선택하면 15개의 뷰어 사전 설정이 표시됩니다. You can increase this limit. [표시되는 이미지 사전 설정 수 늘리기](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 또는 [표시되는 뷰어 사전 설정 수 늘리기](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)를 참조하십시오.

#### 지원되는 형식의 MIME 유형 편집 {#editing-mime-types-for-supported-formats}

Dynamic Media에서 처리하는 자산 유형을 정의하고 고급 자산 처리 매개 변수를 사용자 지정할 수 있습니다. 예를 들어, 다음을 수행할 자산 처리 매개 변수를 지정할 수 있습니다.

* Adobe PDF을 eCatalog 자산으로 변환합니다.
* 개인화를 위해 Adobe Photoshop PSD 문서(.personalization)를 배너 템플릿 자산으로 변환합니다.
* Adobe Illustrator 파일(.AI) 또는 Adobe Photoshop Encapsulated PostScript® 파일(.EPS)을 래스터화합니다.
* [비디오 프로필](/help/assets/video-profiles.md) 및 [이미징 프로필](/help/assets/image-profiles.md)을 사용하여 비디오와 이미지 처리를 각각 정의할 수 있습니다.

[Assets 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.

**지원되는 형식의 MIME 형식을 편집하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.
1. 왼쪽 레일에서 다음과 같이 이동합니다.

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME 유형](assets/mimetypes.png)

1. mimeTypes 폴더에서 mime 유형을 선택합니다.
1. CRXDE Lite 페이지 오른쪽의 아래쪽에서 다음을 수행합니다.

   * **[!UICONTROL enabled]** 필드를 두 번 클릭합니다. 기본적으로 모든 에셋 MIME 유형이 활성화됩니다(**[!UICONTROL true]**(으)로 설정). 즉, 에셋이 처리를 위해 Dynamic Media에 동기화됩니다. 이 자산 MIME 형식을 처리 대상에서 제외하려면 이 설정을 **[!UICONTROL false]**(으)로 변경하십시오.

   * 연결된 텍스트 필드를 열려면 **[!UICONTROL jobParam]**&#x200B;을(를) 두 번 선택하십시오. 특정 MIME 유형에 사용할 수 있는 허용되는 처리 매개 변수 값의 목록은 [지원되는 MIME 유형](/help/assets/assets-formats.md#supported-mime-types)을 참조하십시오.

1. 다음 중 하나를 수행하십시오.

   * 더 많은 MIME 유형을 편집하려면 3-4단계를 반복합니다.
   * CRXDE Lite 페이지의 메뉴 표시줄에서 **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

1. Experience Manager의 왼쪽 상단 모서리에서 **[!UICONTROL CRXDE Lite]**&#x200B;을(를) 선택하여 페이지로 돌아갑니다.

#### 지원되지 않는 형식에 대한 MIME 유형 추가 {#adding-mime-types-for-unsupported-formats}

Experience Manager Assets에서 지원되지 않는 형식에 대한 사용자 지정 MIME 유형을 추가할 수 있습니다. `image_` 전에 MIME 형식을 이동하여 CRXDE Lite에 추가한 새 노드가 Experience Manager에 의해 삭제되지 않았는지 확인하십시오. 또한 활성화된 값이 **[!UICONTROL false]**(으)로 설정되어 있는지 확인하십시오.

**지원되지 않는 형식의 MIME 형식을 추가하려면:**

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. **[!UICONTROL Adobe Experience Manager 웹 콘솔 구성]** 페이지에 새 브라우저 탭이 열립니다.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. On the page, scroll down to the name *Adobe CQ Scene7 Asset MIME type Service* as seen the following screenshot. 이름 오른쪽에서 **[!UICONTROL 구성 값 편집]**&#x200B;을 선택합니다(연필 아이콘).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. **Adobe CQ Scene7 자산 MIME 유형 서비스** 페이지에서 더하기 기호 아이콘 &lt;+>을 선택합니다. 테이블에서 새 MIME 유형을 추가할 더하기 기호를 선택하는 위치는 사소합니다.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 방금 추가한 빈 텍스트 필드에 `DWG=image/vnd.dwg`을(를) 입력하십시오.

   예제 `DWG=image/vnd.dwg`은(는) 데모용으로만 사용됩니다. 여기에 추가하는 MIME 유형은 지원되지 않는 다른 형식일 수 있습니다.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 페이지의 오른쪽 아래 모서리에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   이제 Adobe Experience Manager 웹 콘솔 구성 페이지가 열려 있는 브라우저 탭을 닫을 수 있습니다.

1. 열린 Experience Manager 콘솔이 있는 브라우저 탭으로 돌아갑니다.
1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 왼쪽 레일에서 다음과 같이 이동합니다.

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. MIME 형식 `image_vnd.dwg`을(를) 다음 스크린샷과 같이 트리의 `image_` 바로 위에 끌어다 놓습니다.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. MIME 형식 `image_vnd.dwg`이(가) 여전히 선택된 상태에서 **[!UICONTROL 속성]** 탭의 **[!UICONTROL enabled]** 행의 **[!UICONTROL 값]** 열 헤더 아래에서 값을 두 번 선택하여 **[!UICONTROL 값]** 드롭다운 목록을 엽니다.
1. 필드에 `false`을(를) 입력하거나 드롭다운 목록에서 **[!UICONTROL false]**&#x200B;을(를) 선택하십시오.

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. CRXDE Lite 페이지의 왼쪽 상단 모서리 근처에서 **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

#### 이미지 세트 및 스핀 세트를 자동으로 생성하는 일괄처리 집합 사전 설정을 만듭니다. {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

에셋이 Dynamic Media에 업로드되는 동안 일괄처리 집합 사전 설정을 사용하여 이미지 집합 또는 스핀 세트 생성을 자동화합니다.

먼저, 에셋을 세트에서 그룹화하는 방법에 대한 이름 지정 규칙을 정의합니다. 그런 다음 고유하게 이름이 지정되고 자체 포함된 지침 세트인 일괄처리 집합 사전 설정을 만듭니다. 사전 설정된 레시피에서 정의된 명명 규칙과 일치하는 이미지를 사용하여 세트를 구성하는 방법을 정의해야 합니다.

파일을 업로드할 때 Dynamic Media은 활성 사전 설정에서 정의된 명명 규칙과 일치하는 모든 파일을 사용하여 자동으로 세트를 만듭니다.

##### 기본 이름 지정 구성

일괄처리 집합 사전 설정 레시피에 사용되는 기본 명명 규칙을 만듭니다. 일괄처리 집합 사전 설정 정의에서 선택한 기본 명명 규칙은 회사에서 일괄처리 집합을 생성하는 데 필요한 모든 것일 수 있습니다. 사용자가 정의하는 기본 명명 규칙을 사용하도록 일괄처리 집합 사전 설정이 만들어집니다. 회사 정의 기본 이름 지정에 예외가 있는 경우 특정 콘텐츠 세트에 필요한 대체 사용자 지정 이름 지정 규칙을 사용하여 일괄처리 집합 사전 설정을 최대한 많이 만들 수 있습니다.

일괄처리 집합 사전 설정 기능을 사용하기 위해 기본 이름 지정 규칙을 설정할 필요는 없지만 기본 이름 지정 규칙을 사용하는 것이 좋습니다. 일괄처리 집합 생성을 간소화할 수 있도록 집합에서 그룹화할 이름 지정 규칙의 여러 요소를 정의할 수 있습니다.

또는 사용할 수 있는 양식 필드가 없는 **[!UICONTROL 코드 보기]**&#x200B;를 사용할 수 있습니다. 이 뷰에서는 이름 지정 규칙 정의를 완전히 정규 표현식을 사용하여 만듭니다.

[일치]와 [기본 이름]이라는 두 가지 요소를 정의에 사용할 수 있습니다. 이러한 필드를 사용하면 명명 규칙의 모든 요소를 정의할 수 있으며, 규칙이 포함된 세트의 이름을 지정하는 데 사용되는 규칙의 일부를 식별할 수 있습니다. 회사의 개별 명명 규칙에서는 이러한 각 요소에 대해 하나 이상의 정의 라인을 사용하는 경우가 많습니다. 고유한 정의에 대해 여러 줄을 사용하고 주 이미지, 색상 요소, 대체 보기 요소 및 견본 요소와 같은 고유한 요소로 그룹화할 수 있습니다.

**기본 이름 지정을 구성하려면:**

1. [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 연 다음 계정에 로그인하세요.

   자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 페이지 상단 근처에 있는 탐색 표시줄에서 **[!UICONTROL 설정]** > **[!UICONTROL 응용 프로그램 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 기본 이름 지정]**&#x200B;으로 이동합니다.
1. Select **[!UICONTROL View Form]** or **[!UICONTROL View Code]** to specify how you want to view and enter information about each element.

   **[!UICONTROL 코드 보기]** 확인란을 선택하여 양식 선택과 함께 정규식 값 빌드를 볼 수 있습니다. 양식 보기에서 어떤 이유로든 제한하게 되는 경우 이러한 값을 입력하거나 변경하여 명명 규칙의 요소를 정의할 수 있습니다. 값을 양식 보기에서 구문 분석할 수 없으면 양식 필드가 비활성화됩니다.

   >[!NOTE]
   >
   >비활성화한 양식 필드는 정규식이 올바른지 확인하지 않습니다. 결과 라인 뒤에 각 요소에 대해 작성하고 있는 정규 표현식의 결과가 표시됩니다. 전체 정규 표현식은 페이지 하단에 표시됩니다.

1. 필요에 따라 각 요소를 확장하고 사용할 이름 지정 규칙을 입력합니다.
1. 필요에 따라 다음 중 하나를 수행합니다.

   * 요소에 다른 명명 규칙을 추가하려면 **[!UICONTROL 추가]**&#x200B;를 선택하십시오.
   * 요소에 대한 명명 규칙을 삭제하려면 **[!UICONTROL 제거]**&#x200B;를 선택하십시오.

1. 다음 중 하나를 수행하십시오.

   * **[!UICONTROL 다른 이름으로 저장]**&#x200B;을 선택하고 사전 설정 이름을 입력하세요.
   * 기존 사전 설정을 편집하는 경우 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

##### 일괄처리 집합 사전 설정 만들기

Dynamic Media은 일괄처리 집합 사전 설정을 사용하여 뷰어에 표시할 자산을 이미지 세트(대체 이미지, 색상 옵션, 360 회전)로 구성합니다. 일괄처리 집합 사전 설정은 Dynamic Media의 에셋 업로드 프로세스와 함께 자동으로 실행됩니다.

일괄처리 집합 사전 설정을 만들고, 편집하고, 관리할 수 있습니다. 배치 집합 사전 설정 정의에는 두 가지 형태가 있습니다. 하나는 설정할 수 있는 기본 이름 지정 규칙에 대한 것이고 다른 하나는 즉석에서 만드는 사용자 지정 이름 지정 규칙에 대한 것입니다.

양식 필드 메소드를 사용하여 일괄처리 집합 사전 설정을 정의하거나, 정규 표현식을 사용할 수 있는 코드 메소드를 사용할 수 있습니다. 기본 이름 지정에서와 같이 [양식 보기]에서 정의하는 동시에 [코드 보기]를 선택하고 정규 표현식을 사용하여 정의를 작성할 수 있습니다. 또는 보기 중 하나를 선택 해제하여 둘 중 하나를 단독으로 사용할 수 있습니다.

**일괄처리 집합 사전 설정을 만들려면:**

1. [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 연 다음 계정에 로그인하세요.

   자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 페이지 상단 근처에 있는 탐색 표시줄에서 **[!UICONTROL 설정]** > **[!UICONTROL 응용 프로그램 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]**&#x200B;으로 이동합니다.

   세부 정보 페이지의 오른쪽 상단에 설정된 **[!UICONTROL 양식 보기]**&#x200B;가 기본 보기입니다.

1. [사전 설정 목록] 패널에서 **[!UICONTROL 추가]**&#x200B;를 선택하여 화면 오른쪽의 [세부 정보] 패널에 있는 정의 필드를 활성화합니다.
1. [세부 정보] 패널의 [사전 설정 이름] 필드에 사전 설정 이름을 입력합니다.
1. [일괄처리 집합 유형] 드롭다운 메뉴에서 사전 설정 유형을 선택합니다.
1. 다음 중 하나를 수행하십시오.

   * 이전에 **[!UICONTROL 응용 프로그램 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 기본 이름 지정]**&#x200B;에서 설정한 기본 이름 지정 규칙을 사용하는 경우 **[!UICONTROL 자산 이름 지정 규칙]**&#x200B;을 확장한 다음 파일 이름 지정 드롭다운 목록에서 **[!UICONTROL 기본]**&#x200B;을 선택합니다.

   * 사전 설정을 설정할 때 새 이름 지정 규칙을 정의하려면 **[!UICONTROL 자산 이름 지정 규칙]**&#x200B;을 확장한 다음 파일 이름 지정 드롭다운 목록에서 **[!UICONTROL 사용자 지정]**&#x200B;을 선택합니다.

1. 시퀀스 순서의 경우 Dynamic Media에서 세트가 그룹화된 후 이미지가 표시되는 순서를 정의합니다.

   기본적으로 에셋은 영숫자 순으로 정렬됩니다. 그러나 쉼표로 구분된 정규 표현식 목록을 사용하여 순서를 정의할 수 있습니다.

1. 이름 지정 및 생성 규칙 설정의 경우 에셋 이름 지정 규칙에서 정의한 기본 이름에 접미사 또는 접두어를 지정합니다. 또한 Dynamic Media 폴더 구조 내에서 세트가 만들어지는 위치를 정의합니다.

   많은 수의 세트를 정의하는 경우 에셋 자체를 포함하는 폴더와 세트를 구분합니다. 예를 들어 이미지 세트 폴더를 만들고 생성된 세트를 여기에 추가합니다.

1. 세부 정보 패널에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 새 사전 설정 이름 옆에 있는 **[!UICONTROL 활성]**&#x200B;을 선택합니다.

   사전 설정을 활성화하면 Dynamic Media에 에셋을 업로드할 때 일괄처리 집합 사전 설정이 적용되어 세트가 생성됩니다.

##### 2D 회전 집합의 자동 생성을 위한 일괄처리 집합 사전 설정 만들기

일괄처리 집합 유형 **[!UICONTROL 다축 회전 집합]**&#x200B;을(를) 사용하여 2D 회전 집합의 생성을 자동화하는 레시피를 만들 수 있습니다. 이미지 그룹화에서는 이미지 에셋이 다차원 배열의 해당 위치에 올바르게 정렬되도록 행 및 열 정규 표현식을 사용합니다. 다축 회전 집합에 포함해야 하는 행이나 열의 최소 또는 최대 수는 없습니다.

예를 들어 `spin-2dspin`(이)라는 다축 회전 집합을 만들려고 한다고 가정합니다. 세 개의 행을 포함하고 행당 12개의 이미지가 있는 일련의 스핀 세트 이미지가 있습니다. 이미지 이름은 다음과 같이 지정됩니다.

```xml {.line-numbers}
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

이 정보를 사용하여 다음과 같이 배치 세트 유형 배합식을 생성할 수 있습니다.

![chlimage_1-560](assets/chlimage_1-560.png)

회전 집합의 공유 에셋 이름 부분에 대한 그룹화가 **[!UICONTROL 일치]** 필드에 강조 표시된 대로 추가됩니다. The variable part of the asset name containing the row and column is added to the **[!UICONTROL Row]** and **[!UICONTROL Column]** fields, respectively.

When the Spin Set is uploaded and published, you would activate the name of the 2D Spin Set recipe that is listed under **[!UICONTROL Batch Set Presets]** in the **[!UICONTROL Upload Job Options]** dialog box.

**2D 회전 집합의 자동 생성을 위한 일괄처리 집합 사전 설정을 만들려면:**

1. [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 연 다음 계정에 로그인하세요.

   자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 페이지 상단 근처에 있는 탐색 표시줄에서 **[!UICONTROL 설정]** > **[!UICONTROL 응용 프로그램 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]** > **[!UICONTROL 일괄처리 집합 사전 설정]**&#x200B;으로 이동합니다.

   세부 정보 페이지의 오른쪽 상단에 설정된 **[!UICONTROL 양식 보기]**&#x200B;가 기본 보기입니다.

1. [사전 설정 목록] 패널에서 **[!UICONTROL 추가]**&#x200B;를 선택하여 화면 오른쪽의 [세부 정보] 패널에 있는 정의 필드를 활성화합니다.
1. [세부 정보] 패널의 [사전 설정 이름] 필드에 사전 설정 이름을 입력합니다.
1. In the Batch Set Type drop-down menu, select **[!UICONTROL Asset Set]**.
1. [하위 유형] 드롭다운 목록에서 **[!UICONTROL 다축 회전 집합]**&#x200B;을 선택합니다.
1. **[!UICONTROL 자산 이름 지정 규칙]**&#x200B;을 확장한 다음 파일 이름 지정 드롭다운 목록에서 **[!UICONTROL 사용자 지정]**&#x200B;을 선택합니다.
1. Use the **[!UICONTROL Match]** and, optionally, **[!UICONTROL Base Name]** attributes to define a regular expression for the naming of image assets that make up the grouping.

   예를 들어 리터럴 Match 정규 표현식은 다음과 같이 표시될 수 있습니다.

   `(w+)-w+-w+`

1. **[!UICONTROL 행 열 위치]**&#x200B;를 확장한 다음 2D 회전 집합 배열 내에서 이미지 에셋의 위치에 대한 이름 형식을 정의합니다.

   파일 이름에서 행 또는 열 위치를 포함하려면 괄호를 사용합니다.

   예를 들어 행 정규 표현식의 경우 다음과 같이 표시될 수 있습니다.

   `\w+-R([0-9]+)-\w+`

   또는

   `\w+-(\d+)-\w+`

   열 정규 표현식은 다음과 같이 표시될 수 있습니다.

   `\w+-\w+-C([0-9]+)`

   또는

   `\w+-\w+-C(\d+)`

   위의 샘플은 데모용입니다. 필요에 맞게 원하는 대로 정규 표현식을 만들 수 있습니다.

   >[!NOTE]
   >
   >행 및 열 정규 표현식의 조합으로 다차원 회전 집합 배열 내에서 에셋의 위치를 결정할 수 없는 경우 에셋이 집합에 추가되지 않습니다. 오류도 기록됩니다.

1. 이름 지정 및 생성 규칙 설정의 경우 에셋 이름 지정 규칙에서 정의한 기본 이름에 접미사 또는 접두어를 지정합니다.

   또한 Dynamic Media Classic 폴더 구조 내에서 회전 세트를 만들 위치를 정의합니다.

   많은 수의 세트를 정의하는 경우 에셋 자체를 포함하는 폴더와 세트를 구분합니다. 예를 들어 스핀 세트 폴더를 만들어 생성된 집합을 여기에 추가합니다.

1. 세부 정보 패널에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 새 사전 설정 이름 옆에 있는 **[!UICONTROL 활성]**&#x200B;을 선택합니다.

   사전 설정을 활성화하면 Dynamic Media에 에셋을 업로드할 때 일괄처리 집합 사전 설정이 적용되어 세트가 생성됩니다.

### (선택 사항) Dynamic Media 성능 조정 - Scene7 모드 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Dynamic Media - Scene7 Adobe 모드가 원활하게 실행되도록 하려면 다음 동기화 성능/확장성 미세 조정 팁을 권장합니다.

* 다른 파일 형식의 처리를 위해 사전 정의된 작업 매개 변수 업데이트.
* 사전 정의된 Granite 워크플로우(비디오 자산) 큐 작업자 스레드를 업데이트합니다.
* 사전 정의된 Granite 임시 워크플로우(이미지 및 비비디오 자산)를 업데이트하면 작업자 스레드가 대기열에 포함됩니다.
* Dynamic Media Classic 서버에 대한 최대 업로드 연결 업데이트.

#### 다양한 파일 형식 처리를 위해 사전 정의된 작업 매개 변수 업데이트

파일을 업로드할 때 처리 속도를 높이기 위해 작업 매개 변수를 조정할 수 있습니다. 예를 들어 PSD 파일을 업로드하지만 템플릿으로 처리하지 않으려는 경우 레이어 추출을 false(꺼짐)로 설정할 수 있습니다. 이 경우 튜닝된 작업 매개 변수는 다음과 같이 표시됩니다. `process=None&createTemplate=false`.

템플릿 만들기를 켜려면 다음 매개 변수를 사용합니다. `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe은 PDF, PostScript® 및 PSD 파일에 대해 다음 &quot;조정된&quot; 작업 매개 변수를 사용할 것을 권장합니다.

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 파일 유형 | 권장 작업 매개 변수 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

이러한 매개 변수를 업데이트하려면 [MIME 유형 기반 Assets/Dynamic Media Classic 업로드 작업 매개 변수 지원 사용](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)의 단계를 따릅니다.

#### Granite transient 워크플로 큐 업데이트 {#updating-the-granite-transient-workflow-queue}

Granite Transit Workflow 큐는 **[!UICONTROL DAM 자산 업데이트]** 워크플로에 사용됩니다. Dynamic Media에서는 이미지 수집 및 처리에 사용됩니다.

**Granite 임시 워크플로 큐를 업데이트하려면:**

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)(으)로 이동하여 **큐: Granite Transient 워크플로 큐**&#x200B;를 검색합니다.

   >[!NOTE]
   >
   >OSGi PID가 동적으로 생성되므로 직접 URL 대신 텍스트 검색이 필요합니다.

1. **[!UICONTROL 최대 병렬 작업]** 필드에서 숫자를 원하는 값으로 변경합니다.

   **[!UICONTROL 최대 병렬 작업]**&#x200B;을 늘려 Dynamic Media에 대량의 파일을 업로드할 수 있습니다. 정확한 값은 하드웨어 용량에 따라 다릅니다. 초기 마이그레이션 또는 1회 일괄 업로드 등의 특정 시나리오에서는 큰 값을 사용할 수 있습니다. 그러나 큰 값(예: 코어 수의 2배)을 사용하면 다른 동시 활동에 부정적인 영향을 줄 수 있습니다. 따라서 특정 사용 사례를 기반으로 값을 테스트하고 조정합니다.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0&ndash;1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

#### Granite 워크플로우 큐 업데이트 {#updating-the-granite-workflow-queue}

Granite Workflow 큐는 임시 워크플로우에 사용됩니다. Dynamic Media에서는 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우로 비디오를 처리하는 데 사용되었습니다.

**Granite 워크플로 큐를 업데이트하려면:**

1. `https://<server>/system/console/configMgr`(으)로 이동하여 **큐: Granite 워크플로 큐**&#x200B;를 검색합니다.

   >[!NOTE]
   >
   >OSGi PID가 동적으로 생성되므로 직접 URL 대신 텍스트 검색이 필요합니다.

1. **[!UICONTROL 최대 병렬 작업]** 필드에서 숫자를 원하는 값으로 변경합니다.

   최대 병렬 작업 을 늘려 Dynamic Media에 대량의 파일 업로드를 적절히 지원할 수 있습니다. 정확한 값은 하드웨어 용량에 따라 다릅니다. 초기 마이그레이션 또는 1회 일괄 업로드 등의 특정 시나리오에서는 큰 값을 사용할 수 있습니다. 그러나 큰 값(예: 코어 수의 2배)을 사용하면 다른 동시 활동에 부정적인 영향을 줄 수 있습니다. 따라서 특정 사용 사례를 기반으로 값을 테스트하고 조정합니다.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

#### Dynamic Media Classic 업로드 연결 업데이트 {#updating-the-scene-upload-connection}

Scene7 업로드 연결 설정은 Experience Manager 에셋을 Dynamic Media Classic 서버에 동기화합니다.

**Dynamic Media Classic 업로드 연결을 업데이트하려면:**

1. `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`(으)로 이동
1. **[!UICONTROL 연결 수]** 필드 및/또는 **[!UICONTROL 활성 작업 시간 초과]** 필드에서 원하는 대로 수를 변경합니다.

   **[!UICONTROL 연결 수]** 설정은 Dynamic Media 업로드에 대한 Experience Manager에 허용된 최대 HTTP 연결 수를 제어합니다. 일반적으로 사전 정의된 10개 연결이면 됩니다.

   **[!UICONTROL 활성 작업 시간 초과]** 설정은 업로드된 Dynamic Media 자산이 게재 서버에 게시될 대기 시간을 결정합니다. 이 값은 기본적으로 2100초(35분)입니다.

   대부분의 사용 사례에서는 2100으로 설정하면 충분합니다.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### (선택 사항) 복제할 자산을 필터링합니다 {#optional-filtering-assets-for-replication}

Dynamic Media이 아닌 배포에서는 Experience Manager 작성 환경에서 Experience Manager Publish 노드로 *모두*&#x200B;개의 자산(이미지와 비디오 모두)을 복제합니다. Experience Manager Publish 서버도 자산을 제공하기 때문에 이 워크플로가 필요합니다.

그러나 Dynamic Media 배포에서는 자산이 Cloud Service을 통해 전달되므로 동일한 자산을 Experience Manager 게시 노드에 복제할 필요가 없습니다. 이러한 &quot;하이브리드 게시&quot; 워크플로는 자산을 복제하기 위해 추가 스토리지 비용과 더 긴 처리 시간을 피합니다. 사이트 페이지와 같은 다른 콘텐츠는 Experience Manager 게시 노드에서 계속 제공됩니다.

필터에서 Experience Manager 게시 노드에 복제되지 않도록 자산을 *제외*&#x200B;할 수 있습니다.

#### 복제에 기본 자산 필터 사용 {#using-default-asset-filters-for-replication}

이미징에 Dynamic Media을 사용하거나, 비디오에 사용하거나, 두 가지 모두를 사용하는 경우 Adobe이 제공하는 기본 필터를 그대로 사용할 수 있습니다. 다음 필터는 기본적으로 활성화되어 있습니다.

|   | 필터 | MIME 유형 | 렌디션 |
| --- | --- | --- | --- |
| Dynamic Media 이미지 게재 | filter-image<br>filter-sets | **image/**<br> Contains **applications/**(으)로 시작하고 **set**(으)로 끝납니다. | 기본 제공되는 &quot;filter-images&quot;(대화형 이미지를 포함한 단일 이미지 자산에 적용) 및 &quot;filter-sets&quot;(스핀 세트, 이미지 세트, 혼합 미디어 세트 및 회전판 세트에 적용)는 다음과 같습니다.<br>· 원본 이미지 및 정적 이미지 렌디션의 복제에서 제외합니다. |
| Dynamic Media 비디오 게재 | filter-video | **비디오/**(으)로 시작 | 기본 제공되는 &quot;비디오 필터링&quot;은 <br>· 원본 비디오 및 정적 썸네일 표현물을 복제하지 않도록 제외합니다. |

>[!NOTE]
>
>필터는 MIME 유형에 적용되며 경로별로 지정할 수 없습니다.

#### 복제를 위한 자산 필터 사용자 지정 {#customizing-asset-filters-for-replication}

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스하고 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters`(으)로 이동하여 필터를 검토합니다.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 필터에 대한 MIME 유형을 정의하려면 다음과 같이 MIME 유형을 찾을 수 있습니다.

   왼쪽 레일에서 `content > dam > <locate_your_asset> > jcr:content > metadata`을(를) 확장한 다음 테이블에서 `dc:format`을(를) 찾습니다.

   다음 그래픽은 `dc:format`에 대한 자산의 경로의 예입니다.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   자산 `Fiji Red.jpg`의 `dc:format`이(가) `image/jpeg`입니다.

   이 필터가 형식에 관계없이 모든 이미지에 적용되도록 하려면 값을 `image/*`(으)로 설정합니다. 여기서 `*`은(는) 모든 형식의 모든 이미지에 적용되는 정규 표현식입니다.

   유형 JPEG의 이미지에만 필터를 적용하려면 `image/jpeg` 값을 입력하십시오.

1. 복제에서 포함 또는 제외할 변환을 정의합니다.

   복제를 위해 필터링하는 데 사용할 수 있는 문자는 다음과 같습니다.

   | 사용할 문자 | 복제를 위해 자산을 필터링하는 방법 |
   | --- | --- |
   | * | 와일드카드 문자 |
   | + | 복제용 자산 포함 |
   | - | 복제에서 자산 제외 |

   다음으로 이동 `content/dam/<locate your asset>/jcr:content/renditions`.

   다음 그래픽은 에셋 표현물의 예입니다.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   원본만 복제하려면 `+original`을(를) 입력해야 합니다.
