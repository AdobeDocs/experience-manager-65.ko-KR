---
title: '[!DNL Adobe Experience Manager]에서 디지털 자산을 다운로드합니다.'
description: '[!DNL Adobe Experience Manager]에서 자산을 다운로드하고 다운로드 기능을 활성화하거나 비활성화하는 방법을 알아봅니다.'
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 에셋 다운로드 [!DNL Adobe Experience Manager]{#download-assets-from-aem}

정적 및 동적 표현물을 포함한 자산을 다운로드할 수 있습니다. 또는 링크를 포함한 이메일을 자산에서 직접 보낼 수 [!DNL Adobe Experience Manager Assets]있습니다. 다운로드한 자산은 ZIP 파일에 번들로 포함되어 있습니다. 압축 ZIP 파일의 최대 파일 크기는 내보내기 작업의 경우 1GB입니다. 내보내기 작업당 최대 500개의 에셋이 허용됩니다.

>[!NOTE]
>
>이메일 수신자는 이메일 메시지의 ZIP 다운로드 링크에 액세스하려면 `dam-users` 그룹의 구성원이어야 합니다. 자산을 다운로드할 수 있으려면 멤버는 자산 다운로드를 트리거하는 워크플로우를 시작할 권한이 있어야 합니다.

자산을 다운로드하려면 자산으로 이동하고 자산을 선택한 다음 **[!UICONTROL 도구 모음에서 다운로드를]** 누릅니다. 결과 대화 상자에서 다운로드 옵션을 지정합니다.

자산 유형 이미지 세트, 스핀 세트, 혼합 미디어 세트 및 캐러셀 세트는 다운로드할 수 없습니다.

![Experience Manager 자산에서 자산을 다운로드할 때 사용할 수 있는 옵션](assets/asset_download_dialog.png)

*그림:자산을 다운로드할 때 사용할 수 있는[!DNL Experience Manager Assets]옵션.*

내보내기/다운로드 옵션은 다음과 같습니다. 다이내믹 표현물은 다이내믹 미디어에 고유하며 선택한 자산 외에 즉각적으로 표현물을 생성할 수 있습니다. 이 옵션은 다이내믹 미디어가 활성화된 경우에만 사용할 수 있습니다.

| 내보내기 또는 다운로드 옵션 | 설명 |
|---|---|
| [!UICONTROL 자산] | 변환 없이 자산을 원래 형식으로 다운로드하려면 이 옵션을 선택합니다. |
| [!UICONTROL 표현물] | 표현물은 자산의 이진 표현입니다. 자산은 업로드된 파일의 기본 표현입니다. 그것들은 어떤 수의 진술도 가질 수 있습니다. <br> 이 옵션을 사용하여 다운로드할 변환을 선택할 수 있습니다. 사용할 수 있는 변환은 선택한 자산에 따라 다릅니다. |
| [!UICONTROL 동적 표현물] | 동적 표현물은 다른 표현물을 즉석에서 생성합니다. 이 옵션을 선택할 때 이미지 사전 설정 목록에서 선택하여 동적으로 만들 표현물도 [선택합니다](image-presets.md) . <br>또한 측정 크기 및 단위, 형식, 색상 공간, 해상도 및 이미지 수정자(예: 이미지 반전) 선택 |
| [!UICONTROL 이메일] | 사용자에게 이메일 알림이 전송됩니다. 표준 이메일 템플릿은 다음 위치에서 사용할 수 있습니다.<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> 배포 중에 사용자 정의하는 템플릿은 다음 위치에 있어야 합니다. <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>다음 위치에 임차인별 사용자 지정 템플릿을 저장할 수 있습니다.<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> |
| [!UICONTROL 각 자산에 대해 별도의 폴더 만들기] | 자산을 다운로드하는 동안 폴더 계층을 유지하려면 이 옵션을 선택합니다. 기본적으로 폴더 계층은 무시되고 모든 자산은 로컬 시스템의 한 폴더에 다운로드됩니다. |

자산에 변환이 있는 경우 옵션 변환 옵션을 사용할 수 있습니다. 자산에 하위 자산이 포함된 경우 하위 자산 옵션을 사용할 수 있습니다.

다운로드할 폴더를 선택하면 폴더 아래의 전체 자산 계층이 다운로드됩니다. 다운로드한 각 자산(상위 폴더 아래에 중첩된 하위 폴더의 자산 포함)을 개별 폴더에 포함하려면 각 자산에 **[!UICONTROL 대해]**&#x200B;별도의 폴더 만들기를 선택합니다.

## 자산 다운로드 서블릿 활성화 {#enable-asset-download-servlet}

의 기본 서블릿을 [!DNL Experience Manager] 사용하면 인증된 사용자가 보이는 자산의 ZIP 파일을 만들기 위해 서버와 네트워크를 오버로드할 수 있는 임의 대용량의 동시 다운로드 요청을 발행할 수 있습니다. 이 기능으로 인해 발생할 수 있는 DoS 위험을 줄이기 위해 `AssetDownloadServlet` 게시 인스턴스에 대해 기본적으로 OSGi 구성 요소가 비활성화됩니다.

DAM에서 에셋을 다운로드할 수 있도록 하려면 Asset Share Commons나 기타 포털과 같은 구현을 사용할 때 OSGi 구성을 통해 서블릿을 수동으로 활성화합니다. Adobe에서는 일상적인 다운로드 요구 사항에 영향을 주지 않고 가능한 한 낮은 다운로드 크기를 설정할 것을 권장합니다. 높은 가치는 성능에 영향을 줄 수 있습니다.

1. 게시 실행 모드를 타깃팅하는 이름 지정 규칙이 있는 폴더( `config.publish`즉,

   `/apps/<your-app-name>/config.publish`

   실행 모드에 대한 구성 속성을 정의하려면 [실행 모드를](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode) 참조하십시오.

1. 구성 폴더에서 `nt:file` 이름이 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`지정된 유형의 새 파일을 만듭니다.
1. 다음으로 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 채웁니다. 다운로드의 최대 크기(바이트)를 값으로 `asset.download.prezip.maxcontentsize`설정합니다. 아래 샘플은 ZIP 다운로드의 최대 크기를 100kB를 초과하지 않도록 구성합니다.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 자산 다운로드 서블릿 비활성화 {#disable-asset-download-servlet}

Publish `Asset Download Servlet` 인스턴스에서는 [!DNL Experience Manager] 디스패처 구성을 업데이트하여 모든 자산 다운로드 요청을 차단함으로써 이 기능을 비활성화할 수 있습니다. OSGi 콘솔을 통해 직접 서블릿을 수동으로 비활성화할 수도 있습니다.

1. 발송자 구성을 통해 자산 다운로드 요청을 차단하려면 `dispatcher.any` 구성을 편집하고 [필터 섹션에](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)새 규칙을 추가합니다.

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 게시 인스턴스에서 OSGi 구성 요소를 수동으로 비활성화할 수 있습니다. 이 경우 에서 OSGi 콘솔로 이동합니다 `<aem-host>/system/console/components`. [비활성화]를 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` 찾아 **[!UICONTROL 클릭합니다]**.

>[!MORELIKETHIS]
>
>* [DRM 보호 에셋 다운로드](drm.md)
>* [Win 또는 Mac 데스크탑에서 Experience Manager 데스크탑 앱을 사용하여 에셋 다운로드](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [지원되는 Adobe Creative Cloud 앱에서 Adobe Assets Link를 사용하여 에셋 다운로드](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)

