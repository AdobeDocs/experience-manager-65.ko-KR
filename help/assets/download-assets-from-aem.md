---
title: 자산 다운로드
description: 에서 에셋을 다운로드하는 방법 알아보기 [!DNL Adobe Experience Manager] 다운로드 기능을 활성화하거나 비활성화합니다.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
hide: true
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 4%

---

# 에서 에셋 다운로드 [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | 이 문서 |

정적 및 동적 변환을 포함한 에셋을 다운로드할 수 있습니다. 또는 에셋에 대한 링크가 포함된 이메일을 바로 보낼 수 있습니다. [!DNL Adobe Experience Manager Assets]. 다운로드한 에셋은 ZIP 파일에 번들로 제공됩니다. 압축 ZIP 파일의 내보내기 작업에 대한 최대 파일 크기는 1GB입니다. 내보내기 작업당 최대 500개의 총 자산이 허용됩니다.

>[!NOTE]
>
>다음 위치에 읽기 권한이 있는 모든 사용자: `/var/dam/share` 위치에서는 이메일 메시지에 공유되는 다운로드 링크에 액세스할 수 있습니다.
>
>에 대한 읽기 권한이 있는 모든 사용자 `/var/dam/jobs/download` 위치에서 자산을 다운로드할 수 있습니다.
>
>자산 유형(이미지 세트, 스핀 세트, 혼합 미디어 세트 및 회전판 세트)은 다운로드할 수 없습니다.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**에셋을 다운로드하려면 다음 단계를 따르십시오.**

1. 왼쪽 상단 모서리에서 로고를 클릭합니다. 왼쪽 레일에서 **[!UICONTROL 탐색]**.
1. 다음에서 [!UICONTROL 탐색] 페이지, 클릭 **[!UICONTROL 에셋]** > **[!UICONTROL 파일]**.
1. 다운로드할 자산이 포함된 폴더로 이동합니다.
1. 폴더를 선택하거나 폴더 내의 에셋을 하나 이상 선택합니다.
1. 도구 모음에서 를 클릭합니다 **[!UICONTROL 다운로드]**.
1. 다운로드 대화 상자에서 원하는 다운로드 옵션을 선택합니다.

   | 내보내기 또는 다운로드 옵션 | 설명 |
   |---|---|
   | **[!UICONTROL 각 자산에 대해 별도의 폴더 만들기]** | 다운로드하는 각 에셋(에셋의 상위 폴더 아래에 중첩된 하위 폴더의 에셋 포함)을 로컬 컴퓨터의 한 폴더에 포함하려면 이 옵션을 선택합니다. 이 옵션을 선택하지 않으면 기본적으로 폴더 계층 구조가 무시되고 모든 자산이 로컬 컴퓨터의 한 폴더로 다운로드됩니다. |
   | **[!UICONTROL 이메일]** | 사용자에게 이메일 알림이 전송됩니다. 표준 이메일 템플릿은 다음 위치에서 사용할 수 있습니다.<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> 배포 중 사용자 정의하는 템플릿은 다음 위치에서 사용할 수 있습니다. <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>다음 위치에 테넌트별 사용자 지정 템플릿을 저장할 수 있습니다.<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> |
   | **[!UICONTROL 자산]** | 렌디션 없이 에셋을 원본 양식으로 다운로드하려면 이 옵션을 선택합니다.<br>원본 에셋에 하위 에셋이 있는 경우 하위 에셋 옵션을 사용할 수 있습니다. |
   | **[!UICONTROL 렌디션]** | 렌디션은 에셋의 바이너리 표현입니다. 에셋에는 업로드된 파일의 기본 표현이 있습니다. 그들은 얼마든지 표현을 할 수 있다. <br> 이 옵션을 사용하여 다운로드할 변환을 선택할 수 있습니다. 사용할 수 있는 렌디션은 선택한 에셋에 따라 다릅니다. 에셋에 렌디션이 있는 경우 옵션을 사용할 수 있습니다. |
   | **[!UICONTROL 스마트 자르기]** | AEM 내에서 선택한 에셋의 모든 스마트 자르기 렌디션을 다운로드하려면 이 옵션을 선택합니다. 스마트 자르기 렌디션이 포함된 zip 파일이 생성되고 로컬 컴퓨터에 다운로드됩니다. |
   | **[!UICONTROL 동적 렌디션]** | 일련의 대체 변환을 실시간으로 생성하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 다음 중에서 선택하여 동적으로 만들 변환도 선택합니다. [이미지 사전 설정](image-presets.md) 목록을 표시합니다. <br>또한 측정 단위, 형식, 색상 공간, 해상도 및 이미지 반전과 같은 선택적 이미지 수정자를 선택할 수 있습니다. 이 옵션은 다음과 같은 경우에만 사용할 수 있습니다. [!DNL Dynamic Media] 활성화되었습니다. |

1. 대화 상자에서 **[!UICONTROL 다운로드]**.

다운로드할 폴더를 선택하면 폴더 아래의 전체 에셋 계층 구조가 다운로드됩니다. 다운로드하는 각 에셋(상위 폴더 아래에 중첩된 하위 폴더의 에셋 포함)을 개별 폴더에 포함하려면 을 선택합니다 **[!UICONTROL 각 자산에 대해 별도의 폴더 만들기]**.

## 에셋 다운로드 서블릿 활성화 {#enable-asset-download-servlet}

의 기본 서블릿 [!DNL Experience Manager] 인증된 사용자는 서버 및 네트워크를 오버로드할 수 있는 표시되는 자산의 ZIP 파일을 만들기 위해 임의로 큰 동시 다운로드 요청을 실행할 수 있습니다. 이 기능으로 인한 잠재적 DoS 위험을 완화하려면, `AssetDownloadServlet` 게시 인스턴스에 대해 OSGi 구성 요소는 기본적으로 비활성화되어 있습니다.

DAM에서 에셋을 다운로드할 수 있도록 하려면 Asset Share Commons 또는 기타 포털과 같은 구현을 사용할 때 OSGi 구성을 통해 서블릿을 수동으로 활성화하십시오. Adobe은 일상적인 다운로드 요구 사항에 영향을 주지 않고 허용되는 다운로드 크기를 가능한 한 낮게 설정할 것을 권장합니다. 값이 높으면 성능에 영향을 줄 수 있습니다.

1. 게시 실행 모드를 대상으로 하는 명명 규칙을 사용하여 폴더를 만듭니다(`config.publish`): `/apps/<your-app-name>/config.publish`. 실행 모드에 대한 구성 속성을 정의하려면 [실행 모드](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. 구성 폴더에서 다음 형식의 파일을 만듭니다. `nt:file` 명명된 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. 채우기 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 다음을 포함하십시오. 다운로드 최대 크기(바이트)를 값으로 설정합니다. `asset.download.prezip.maxcontentsize`. 아래 샘플은 ZIP 다운로드의 최대 크기를 100kb를 초과하지 않도록 구성합니다.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

기본적으로, `GET` 파일 다운로드 요청, [!DNL Experience Manager] zip 아카이브의 다운로드 크기에 50MB 제한을 적용합니다. 다음을 통해 시작된 다운로드 `POST` 요청 또는 사용자 인터페이스는 이 제한의 영향을 받지 않습니다.

## 에셋 다운로드 서블릿 비활성화 {#disable-asset-download-servlet}

다음 `Asset Download Servlet` 에서 비활성화할 수 있음 [!DNL Experience Manager] 에셋 다운로드 요청을 차단하도록 Dispatcher 구성을 업데이트하여 인스턴스를 게시합니다. OSGi 콘솔을 통해 서블릿을 수동으로 비활성화할 수도 있습니다.

1. Dispatcher 구성을 통해 에셋 다운로드 요청을 차단하려면 `dispatcher.any` 구성 및 규칙에 추가 [필터 섹션](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 게시 인스턴스에서 OSGi 구성 요소를 비활성화하려면 의 OSGi 콘솔에 액세스합니다 `http://[aem_server]:[port]/system/console/components`. 찾기 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` 및 클릭 **[!UICONTROL 사용 안 함]**.

>[!MORELIKETHIS]
>
>* [Brand Portal을 사용하여 에셋 다운로드](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [DRM 보호 에셋 다운로드](drm.md).
>* [Win 또는 Mac 데스크탑에서 Experience Manager 데스크탑 앱을 사용하여 에셋 다운로드](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [지원되는 Adobe Creative Cloud 앱 내에서 에셋 Adobe 링크를 사용하여 에셋을 다운로드합니다](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html).
