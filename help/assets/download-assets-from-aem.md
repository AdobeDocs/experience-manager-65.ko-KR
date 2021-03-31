---
title: 자산 다운로드
description: ' [!DNL Adobe Experience Manager] 에서 에셋을 다운로드하고 다운로드 기능을 활성화하거나 비활성화하는 방법에 대해 학습합니다.'
contentOwner: AG
role: 비즈니스 전문가
feature: 자산 관리,자산 배포
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] {#download-assets-from-aem}에서 에셋 다운로드

정적 및 동적 표현물을 비롯한 자산을 다운로드할 수 있습니다. 또는 [!DNL Adobe Experience Manager Assets]에서 바로 자산에 대한 링크가 있는 이메일을 보낼 수 있습니다. 다운로드한 자산은 ZIP 파일에 번들로 포함됩니다. 압축 ZIP 파일의 최대 파일 크기는 내보내기 작업에 대해 1GB입니다. 내보내기 작업당 최대 500개의 에셋이 허용됩니다.

>[!NOTE]
>
>이메일 수신자는 이메일 메시지의 ZIP 다운로드 링크에 액세스하려면 `dam-users` 그룹의 구성원이어야 합니다. 자산을 다운로드할 수 있으려면 자산 다운로드를 트리거하는 워크플로우를 시작할 수 있는 권한이 구성원에게 있어야 합니다.

이미지 세트, 스핀 세트, 혼합 미디어 집합 및 캐러셀 집합을 다운로드할 수 없습니다.

자산을 다운로드하려면 다음 단계를 수행하십시오.

1. 왼쪽 위 모서리에서 로고를 클릭합니다. 왼쪽 레일에서 **[!UICONTROL 탐색]**&#x200B;을 클릭합니다.
1. [!UICONTROL 탐색] 페이지에서 **[!UICONTROL 자산]** > **[!UICONTROL 파일.]**
1. 다운로드할 자산이 포함된 폴더로 이동합니다.
1. 폴더를 선택하거나 폴더 내의 자산을 하나 이상 선택합니다.
1. 도구 모음에서 **[!UICONTROL 다운로드를 클릭합니다.]**

   ![Experience Manager 자산에서 자산을 다운로드할 때 사용할 수 있는 옵션](/help/assets/assets/asset-download1.png)

   *그림:다운로드 대화 상자에서 사용할 수 있는 옵션입니다.*

1. [다운로드] 대화 상자에서 원하는 다운로드 옵션을 선택합니다.

   | 내보내기 또는 다운로드 옵션 | 설명 |
   |---|---|
   | **[!UICONTROL 각 자산에 대해 별도의 폴더 만들기]** | 다운로드한 각 자산을 로컬 컴퓨터의 한 폴더에 자산의 상위 폴더 아래에 중첩된 하위 폴더에 포함시키려면 이 옵션을 선택합니다. 이 옵션을 선택하지 않으면 기본적으로 폴더 계층 구조가 무시되고 모든 에셋이 로컬 컴퓨터의 한 폴더에 다운로드됩니다. |
   | **[!UICONTROL 이메일]** | 사용자에게 이메일 알림이 전송됩니다. 표준 이메일 템플릿은 다음 위치에서 사용할 수 있습니다.<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> 배포 시 사용자 지정하는 템플릿은 다음 위치에서 사용할 수 있습니다. <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>다음 위치에 임차인별 사용자 지정 템플릿을 저장할 수 있습니다.<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL 자산]** | 표현물 없이 자산을 원래 형식으로 다운로드하려면 이 옵션을 선택합니다.<br>원본 자산에 하위 자산이 있는 경우 하위 자산 옵션을 사용할 수 있습니다. |
   | **[!UICONTROL 표현물]** | 표현물은 자산의 이진 표현입니다. 자산은 업로드된 파일의 기본 표현인 그들은 어떤 수의 진술도 가질 수 있다. <br> 이 옵션을 사용하여 다운로드할 변환을 선택할 수 있습니다. 사용할 수 있는 변환은 선택한 자산에 따라 다릅니다. 자산에 변환이 있는 경우 이 옵션을 사용할 수 있습니다. |
   | **[!UICONTROL 스마트 자르기]** | AEM 내에서 선택한 자산의 모든 스마트 자르기 변환을 다운로드하려면 이 옵션을 선택합니다. 스마트 자르기 변환이 있는 zip 파일이 만들어지고 로컬 컴퓨터에 다운로드됩니다. |
   | **[!UICONTROL 동적 표현물]** | 일련의 대체 변환을 실시간으로 생성하려면 이 옵션을 선택합니다. 이 옵션을 선택할 때 [이미지 사전 설정](image-presets.md) 목록에서 선택하여 동적으로 만들 표현물도 선택할 수 있습니다. <br>또한 측정 크기 및 단위, 형식, 색상 공간, 해상도 및 이미지 반전 등의 선택적 이미지 수정자를 선택할 수 있습니다. 이 옵션은 [!DNL Dynamic Media]이(가) 활성화된 경우에만 사용할 수 있습니다. |

1. 대화 상자에서 **[!UICONTROL 다운로드.]**&#x200B;를 클릭합니다.

다운로드할 폴더를 선택하면 폴더 아래의 전체 자산 계층 구조가 다운로드됩니다. 다운로드한 각 자산(상위 폴더 아래에 중첩된 하위 폴더의 자산 포함)을 개별 폴더에 포함하려면 **[!UICONTROL 각 에셋에 대해 별도의 폴더 만들기]**&#x200B;를 선택합니다.

## 자산 다운로드 서블릿 사용 {#enable-asset-download-servlet}

[!DNL Experience Manager]의 기본 서블릿을 사용하면 인증된 사용자가 서버와 네트워크를 과부시킬 수 있는 표시된 자산의 ZIP 파일을 만들기 위해 임의로 대규모 동시 다운로드 요청을 발행할 수 있습니다. 이 기능으로 인해 발생할 수 있는 DoS 위험을 완화하려면 게시 인스턴스에 대해 기본적으로 `AssetDownloadServlet` OSGi 구성 요소가 비활성화됩니다.

DAM에서 에셋을 다운로드할 수 있도록 하려면 Asset Share Commons나 다른 포털과 유사한 구현을 사용할 경우 OSGi 구성을 통해 수동으로 서블릿을 활성화합니다. Adobe은 일상적인 다운로드 요구 사항에 영향을 주지 않고 허용되는 다운로드 크기를 최대한 낮게 설정할 것을 권장합니다. 높은 가치는 성능에 영향을 줄 수 있습니다.

1. 게시 실행 모드(`config.publish`)를 대상으로 하는 이름 지정 규칙을 사용하여 폴더를 만듭니다.`/apps/<your-app-name>/config.publish`. 실행 모드에 대한 구성 속성을 정의하려면 [실행 모드](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode)를 참조하십시오.
1. 구성 폴더에서 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 이름의 `nt:file` 유형의 파일을 만듭니다.
1. `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`을(를) 다음 항목으로 채웁니다. 다운로드에 대한 최대 크기(바이트)를 `asset.download.prezip.maxcontentsize` 값으로 설정합니다. 아래 샘플은 ZIP 다운로드의 최대 크기를 100kB를 초과하지 않도록 구성합니다.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 자산 다운로드 서블릿 {#disable-asset-download-servlet} 비활성화

`Asset Download Servlet`은(는) 발송자 구성을 업데이트하여 자산 다운로드 요청을 차단함으로써 [!DNL Experience Manager] 게시 인스턴스에서 비활성화할 수 있습니다. 서브렛은 OSGi 콘솔을 통해 직접 비활성화할 수도 있습니다.

1. 디스패처 구성을 통해 자산 다운로드 요청을 차단하려면 `dispatcher.any` 구성을 편집하고 [필터 섹션](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)에 규칙을 추가합니다. `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 게시 인스턴스에서 OSGi 구성 요소를 비활성화하려면 `http://[aem_server]:[port]/system/console/components`의 OSGi 콘솔에 액세스합니다. `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet`을 찾아 **[!UICONTROL 비활성화]**&#x200B;를 클릭합니다.

>[!MORELIKETHIS]
>
>* [브랜드 포털을 사용하여 에셋 다운로드](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [DRM 보호 에셋을 다운로드합니다](drm.md).
>* [Win 또는 Mac 데스크탑에서 Experience Manager 데스크탑 앱을 사용하여 에셋을 다운로드할 수 있습니다](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [지원되는 Adobe Creative Cloud 앱](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html) 내에서 Adobe 에셋 링크를 사용하여 에셋을 다운로드합니다.

