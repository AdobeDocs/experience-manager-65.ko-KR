---
title: 연결된 Assets을 사용하여  [!DNL Sites]에서 DAM 에셋 공유
description: 다른  [!DNL Adobe Experience Manager Sites] 배포에서 웹 페이지를 만들 때 원격  [!DNL Adobe Experience Manager Assets] 배포에서 사용할 수 있는 자산을 사용합니다.
contentOwner: AK
mini-toc-levels: 2
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3909'
ht-degree: 15%

---

# 연결된 Assets을 사용하여 [!DNL Experience Manager Sites]에서 DAM 에셋 공유 {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=ko) |
| AEM 6.5 | 이 문서 |


대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 배포할 수 있습니다. 이러한 웹 사이트를 만드는 데 사용되는 웹 사이트 제작 기능과 디지털 자산이 서로 다른 배포에 있을 수 있습니다. 함께 작업하는 데 필요한 기존 배포가 지리적으로 분산되는 이유 중 하나가 될 수 있습니다. 또 다른 이유는 모회사가 함께 사용하려는 다른 [!DNL Experience Manager] 버전을 포함하여 형식이 다른 인프라로 이어지는 획득일 수 있습니다.

연결된 Assets 기능은 [!DNL Experience Manager Sites]과(와) [!DNL Experience Manager Assets]을(를) 통합하여 위의 사용 사례를 지원합니다. 사용자는 별도의 [!DNL Assets] 배포의 디지털 자산을 사용하는 웹 페이지를 [!DNL Sites]에서 만들 수 있습니다.

>[!NOTE]
>
>웹 페이지를 작성하기 위해 별도의 사이트 배포에서 원격 DAM 배포에 사용할 수 있는 자산을 사용해야 하는 경우에만 연결된 Assets을 구성하십시오.

## 연결된 Assets 개요 {#overview-of-connected-assets}

[!UICONTROL 페이지 편집기]의 페이지를 대상 대상으로 편집할 때 작성자는 자산의 소스로 사용되는 다른 [!DNL Assets] 배포의 자산을 원활하게 검색, 탐색 및 포함할 수 있습니다. 관리자는 [!DNL Sites] 기능이 있는 [!DNL Experience Manager] 배포와 [!DNL Assets] 기능이 있는 [!DNL Experience Manager] 배포의 일회성 통합을 만듭니다. 사이트 작성자는 연결된 Assets을 통해 사이트의 웹 페이지에서 Dynamic Media 이미지를 사용하고 스마트 자르기 및 이미지 사전 설정과 같은 Dynamic Media 기능을 사용할 수도 있습니다.

[!DNL Sites] 작성자의 경우 원격 자산을 읽기 전용 로컬 자산으로 사용할 수 있습니다. 이 기능은 사이트 편집기에서 원격 자산을 원활하게 검색하고 액세스할 수 있도록 지원합니다. Sites에서 전체 에셋 코퍼스를 사용할 수 있어야 하는 기타 사용 사례의 경우, 연결된 Assets을 사용하지 않고 에셋을 일괄적으로 마이그레이션하는 것이 좋습니다. [Experience Manager Assets 마이그레이션 안내서](/help/assets/assets-migration-guide.md)를 참조하세요.

### 사전 요구 사항 및 지원되는 배포 {#prerequisites}

이 기능을 사용하거나 구성하기 전에 다음을 확인하십시오.

* 사용자는 각 배포에서 적절한 사용자 그룹에 속합니다.
* [!DNL Adobe Experience Manager] 배포 형식의 경우 지원되는 기준 중 하나가 충족됩니다. as a Cloud Service [!DNL Experience Manager] 6.5 [!DNL Assets]은(는) [!DNL Experience Manager]에서 작동합니다. 이 기능이 [!DNL Experience Manager]에서 [!DNL Cloud Service] (으)로 작동하는 방법에 대한 자세한 내용은 [Experience Manageras a Cloud Service 의 연결된 Assets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=ko)을 참조하십시오.

  | | [!DNL Sites] as a [!DNL Cloud Service] | AMS의 [!DNL Experience Manager] 6.5 [!DNL Sites] | [!DNL Experience Manager] 6.5 [!DNL Sites] 온-프레미스 |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 지원됨 | 지원됨 | 지원됨 |
  | AMS **의**&#x200B;[!DNL Experience Manager] 6.5 [!DNL Assets] | 지원됨 | 지원됨 | 지원됨 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 온-프레미스** | 지원되지 않음 | 지원되지 않음 | 지원되지 않음 |

### 지원되는 파일 형식 {#mimetypes}

작성자가 콘텐츠 파인더에서 이미지와 다음 유형의 문서를 검색하고 페이지 편집기에서 검색된 에셋을 드래그합니다. 문서가 `Download` 구성 요소에 추가되고 이미지가 `Image` 구성 요소에 추가됩니다. 작성자가 기본 `Download` 또는 `Image` 구성 요소를 확장하는 모든 사용자 지정 [!DNL Experience Manager] 구성 요소에 원격 자산을 추가할 수도 있습니다. 지원되는 형식은 다음과 같습니다.

* **이미지 형식**: [이미지 구성 요소](assets-formats.md#supported-raster-image-formats)에서 지원하는 형식입니다.
* **문서 형식**: [지원되는 문서 형식](assets-formats.md#supported-document-formats)을 참조하세요.

### 관련 사용자 및 그룹 {#users-and-groups-involved}

기능 및 해당 사용자 그룹을 구성하고 사용하는 데 관련된 여러 가지 역할이 아래에 설명되어 있습니다. 로컬 범위는 작성자가 웹 페이지를 만드는 사용 사례에 사용됩니다. 원격 범위는 필요한 자산을 호스팅하는 DAM 배포에 사용됩니다. [!DNL Sites] 작성자가 이러한 원격 자산을 가져옵니다.

| 역할 | 범위 | 사용자 그룹 | 연습의 사용자 이름 | 설명 |
|---|---|---|---|---|
| [!DNL Sites] 관리자 | 로컬 | [!DNL Experience Manager] `administrators` | `admin` | [!DNL Experience Manager]을(를) 설정하고 원격 [!DNL Assets] 배포와의 통합을 구성하십시오. |
| DAM 사용자 | 로컬 | `Authors` | `ksaner` | `/content/DAM/connectedassets/`에서 가져온 자산을 보고 복제하는 데 사용됩니다. |
| [!DNL Sites] 작성자 | 로컬 | <ul><li>`Authors`(원격 DAM에 대한 읽기 액세스 권한과 로컬 [!DNL Sites]에 대한 작성자 액세스 권한 있음) </li> <li>로컬 [!DNL Sites]의 `dam-users`</li></ul> | `ksaner` | 최종 사용자는 이 통합을 사용하여 콘텐츠 속도를 향상시키는 [!DNL Sites] 작성자입니다. 작성자가 [!UICONTROL 콘텐츠 파인더]를 사용하고 로컬 웹 페이지에서 필요한 이미지를 사용하여 원격 DAM에서 자산을 검색하고 찾아봅니다. `ksaner` DAM 사용자의 자격 증명이 사용됩니다. |
| [!DNL Assets] 관리자 | 원격 | [!DNL Experience Manager] `administrators` | 원격 [!DNL Experience Manager]의 `admin` | CORS(원본 간 리소스 공유)를 구성합니다. |
| DAM 사용자 | 원격 | `Authors` | 원격 [!DNL Experience Manager]의 `ksaner` | 원격 [!DNL Experience Manager] 배포의 작성자 역할입니다. [!UICONTROL 콘텐츠 파인더]를 사용하여 연결된 Assets에서 자산을 검색하고 찾아봅니다. |
| DAM 배포자(기술 사용자) | 원격 | [!DNL Sites] `Authors` | 원격 [!DNL Experience Manager]의 `ksaner` | 원격 배포에 있는 이 사용자는 [!DNL Experience Manager] 로컬 서버([!DNL Sites] 작성자 역할 아님)에서 [!DNL Sites] 작성자를 대신하여 원격 자산을 가져오는 데 사용됩니다. 이 역할은 위의 두 `ksaner` 역할과 동일하지 않으며 다른 사용자 그룹에 속합니다. |

### 연결된 Assets 아키텍처 {#connected-assets-architecture}

Experience Manager을 사용하면 원격 DAM 배포를 소스로 여러 Experience Manager [!DNL Sites] 배포에 연결할 수 있습니다. 그러나 원격 DAM 배포가 하나만 있는 [!DNL Sites] 배포에 연결할 수 있습니다.

원격 DAM 배포에 연결할 최적의 사이트 인스턴스 수를 평가합니다. Adobe은 연결된 각 사이트 인스턴스가 원격 DAM의 데이터 트래픽에 기여하므로 사이트 인스턴스를 배포에 점진적으로 연결하고 원격 DAM에 성능에 영향을 주지 않는지 테스트할 것을 권장합니다.

다음 다이어그램은 지원되는 시나리오를 보여 줍니다.

![연결된 Assets 아키텍처](assets/connected-assets-architecture.png)

다음 다이어그램은 지원되지 않는 시나리오를 보여 줍니다.

![연결된 Assets 아키텍처](assets/connected-assets-architecture-unsupported.png)

## [!DNL Sites] 및 [!DNL Assets] 배포 간 연결 구성 {#configure-a-connection-between-sites-and-assets-deployments}

[!DNL Experience Manager] 관리자가 이 통합을 만들 수 있습니다. 만들고 나면 이를 사용하는 데 필요한 권한이 사용자 그룹을 통해 설정됩니다. 사용자 그룹은 [!DNL Sites] 배포 및 DAM 배포에 정의되어 있습니다.

연결된 Assets 및 로컬 [!DNL Sites] 연결을 구성하려면 다음 단계를 수행하십시오.

1. 기존 [!DNL Sites] 배포에 액세스하거나 다음 명령을 사용하여 배포를 만드십시오.

   1. JAR 파일의 폴더에서 터미널에서 다음 명령을 실행하여 각 [!DNL Experience Manager] 서버를 만듭니다.

      `java -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 몇 분 후에 [!DNL Experience Manager] 서버가 성공적으로 시작됩니다. 이 [!DNL Sites] 배포를 웹 페이지 작성을 위한 로컬 시스템으로 간주합니다(예: `https://[local_sites]:4502`).

1. 적절한 범위의 사용자 및 역할이 [!DNL Sites] 배포 및 AMS의 [!DNL Assets] 배포에 있는지 확인하십시오. [!DNL Assets] 배포에 기술 사용자를 만들고 [관련된 사용자 및 그룹](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)에 언급된 사용자 그룹에 추가합니다.

1. `https://[local_sites]:4502`에서 로컬 [!DNL Sites] 배포에 액세스합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 연결된 자산 구성]**&#x200B;을 클릭하고 다음 값을 제공합니다.

   1. 구성의 **[!UICONTROL 제목]**.
   1. **[!UICONTROL 원격 DAM URL]**&#x200B;은(는) `https://[assets_servername]:[port]` 형식의 [!DNL Assets] 위치의 URL입니다.
   1. DAM 배포자의 자격 증명(기술 사용자)
   1. **[!UICONTROL 탑재 지점]** 필드에 [!DNL Experience Manager]이(가) 자산을 가져오는 로컬 [!DNL Experience Manager] 경로를 입력합니다. 예를 들어 `remoteassets` 폴더입니다. DAM에서 가져온 자산은 [!DNL Sites] 배포의 이 폴더에 저장됩니다.
   1. **[!UICONTROL 로컬 사이트 URL]**&#x200B;은(는) [!DNL Sites] 배포의 위치입니다. [!DNL Assets] 배포에서는 이 값을 사용하여 이 [!DNL Sites] 배포에서 가져온 디지털 자산에 대한 참조를 유지합니다.
   1. [!DNL Sites] 기술 사용자의 자격 증명입니다.
   1. **[!UICONTROL 원본 이진 전송 최적화 임계값]** 필드의 값은 원본 에셋(렌디션 포함)이 동기적으로 전송되는지 여부를 지정합니다. 파일 크기가 비교적 큰 자산이 비동기식으로 가장 잘 동기화되는 반면 파일 크기가 더 작은 Assets을 쉽게 가져올 수 있습니다. 값은 네트워크 기능에 따라 다릅니다.
   1. 데이터 저장소를 사용하여 자산을 저장하고 데이터 저장소가 두 배포 간에 공유되는 경우 **[!UICONTROL 연결된 Assets과 공유되는 데이터 저장소]**&#x200B;를 선택하십시오. 이 경우 실제 자산 바이너리를 데이터 저장소에서 사용할 수 있고 전송되지 않으므로 임계값 제한은 문제가 되지 않습니다.

   ![연결된 Assets 기능에 대한 일반적인 구성](assets/connected-assets-typical-config.png)

   *그림: 연결된 Assets 기능에 대한 일반적인 구성*

1. [!DNL Assets] 배포의 기존 디지털 자산이 이미 처리되었으며 렌디션이 생성됩니다. 이러한 렌디션은 이 기능을 사용하여 가져오므로 렌디션을 다시 생성할 필요가 없습니다. 워크플로 시작 관리자를 비활성화하여 렌디션의 재생성을 방지합니다. ([!DNL Sites]) 배포에서 런처 구성을 조정하여 `connectedassets` 폴더를 제외합니다(자산은 이 폴더에서 가져옴).

   1. [!DNL Sites] 배포에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 런처]**&#x200B;를 클릭합니다.

   1. **[!UICONTROL DAM 자산 업데이트]** 및 **[!UICONTROL DAM 메타데이터 원본에 쓰기]**&#x200B;로 워크플로우를 사용하여 런처를 검색합니다.

   1. 워크플로우 런처를 선택하고 작업 표시줄에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

   1. [!UICONTROL 속성] 마법사에서 **[!UICONTROL 경로]** 필드를 다음 매핑으로 변경하여 마운트 지점 **[!UICONTROL connectedassets]**&#x200B;을(를) 제외하도록 정규식을 업데이트합니다.

   | 이전 | 이후 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >작성자가 자산을 가져올 때 원격 배포에서 사용할 수 있는 모든 렌디션을 가져옵니다. 가져온 자산의 렌디션을 더 만들려면 이 구성 단계를 건너뜁니다. [!UICONTROL DAM 자산 업데이트] 워크플로우가 트리거되어 더 많은 렌디션을 만듭니다. 이러한 변환은 로컬 [!DNL Sites] 배포에서만 사용할 수 있으며 원격 DAM 배포에서는 사용할 수 없습니다.

1. [!DNL Assets] 배포의 CORS 구성에서 [!DNL Sites] 배포를 허용된 원본으로 추가합니다. 자세한 내용은 [CORS 이해](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ko)를 참조하십시오.

1. [동일한 사이트 쿠키 지원 구성](/help/sites-administering/same-site-cookie-support.md).

구성된 [!DNL Sites] 배포와 [!DNL Assets] 배포 간의 연결을 확인할 수 있습니다.

![연결된 Assets의 연결 테스트 구성 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*그림: 연결된 Assets의 연결 테스트 구성 [!DNL Sites].*

## Dynamic Media 에셋 사용 {#dynamic-media-assets}


연결된 Assets을 사용하면 Sites 페이지의 원격 DAM 배포에서 [!DNL Dynamic Media]에 의해 처리된 이미지 자산을 사용할 수 있으며 스마트 자르기 및 이미지 사전 설정과 같은 Dynamic Media 기능을 사용할 수 있습니다.

연결된 Assets에 [!DNL Dynamic Media]을(를) 사용하려면:

1. 동기화 모드가 활성화된 원격 DAM 배포에서 [!DNL Dynamic Media]을(를) 구성합니다.
1. [연결된 Assets](#configure-a-connection-between-sites-and-assets-deployments)을(를) 구성합니다.
1. 원격 DAM에 구성된 것과 동일한 회사 이름으로 Sites 인스턴스에서 [!DNL Dynamic Media]을(를) 구성합니다. 연결된 자산에서 작업하려면 Sites 배포에 Dynamic Media 계정에 대한 읽기 전용 액세스 권한이 있어야 합니다. 따라서 Sites 인스턴스의 Dynamic Media 구성에서 동기화 모드를 비활성화해야 합니다.

>[!CAUTION]
>
>연결된 Assets 및 [!DNL Dynamic Media] 구성에서는 [!DNL Dynamic Media]을(를) 사용하여 [!DNL Sites] 배포에서 사용할 수 있는 로컬 자산을 처리할 수 없습니다.

## 구성 [!DNL Dynamic Media] {#configure-dynamic-media}

[!DNL Assets] 및 [!DNL Sites] 배포에서 [!DNL Dynamic Media]을(를) 구성하려면:

1. 원격 [!DNL Assets] 작성자 배포에서 [!DNL Dynamic Media]을(를) 전역 구성으로 활성화하고 구성합니다. Dynamic Media을 구성하려면 [Dynamic Media 구성](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services)을 참조하십시오.
원격 [!DNL Assets] 배포의 [!UICONTROL Dynamic Media 동기화 모드]에서 **[!UICONTROL 기본적으로 사용]**&#x200B;을 선택합니다.

1. [사이트 및 자산 배포 간 연결 구성](#configure-a-connection-between-sites-and-assets-deployments)에 설명된 대로 연결된 Assets 구성을 만듭니다. 또한 **[!UICONTROL Dynamic Media 연결된 Assets에 대한 원본 렌디션 가져오기]** 옵션을 선택하십시오.

1. 로컬 [!DNL Sites] 및 원격 [!DNL Assets] 배포에서 [!DNL Dynamic Media]을(를) 구성합니다. 지침을 따라 [구성 [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services)합니다.

   * 모든 구성에서 동일한 회사 이름을 사용합니다.
   * 로컬 [!DNL Sites]의 [!UICONTROL Dynamic Media 동기화 모드]에서 **[!UICONTROL 기본적으로 사용 안 함]**&#x200B;을 선택합니다. [!DNL Sites] 배포에는 [!DNL Dynamic Media] 계정에 대한 읽기 전용 액세스 권한이 있어야 합니다.
   * 로컬 [!DNL Sites]의 **[!UICONTROL Publish Assets]** 옵션에서 **[!UICONTROL 선택적 Publish]**&#x200B;을(를) 선택합니다. **[!UICONTROL 모든 콘텐츠 동기화]**&#x200B;를 선택하지 마십시오.

1. 이미지 핵심 구성 요소에서 [[!DNL Dynamic Media] 지원을 사용하도록 설정](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=ko#dynamic-media). 이 기능을 사용하면 로컬 [!DNL Sites] 배포의 웹 페이지에서 작성자가 [!DNL Dynamic Media]개의 이미지를 사용할 때 기본 [이미지 구성 요소](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html)에 [!DNL Dynamic Media]개의 이미지가 표시됩니다.

## 원격 자산 사용 {#use-remote-assets}

웹 사이트 작성자가 콘텐츠 파인더를 사용하여 DAM 배포에 연결합니다. 작성자는 구성 요소에서 원격 자산을 찾아보고 검색하고 드래그할 수 있습니다. 원격 DAM을 인증하려면 관리자가 제공한 자격 증명(있는 경우)을 가까이 보관하십시오.

작성자는 로컬 DAM 및 원격 DAM 배포에서 사용할 수 있는 자산을 단일 웹 페이지에서 사용할 수 있습니다. 콘텐츠 파인더를 사용하여 로컬 DAM을 검색하거나 원격 DAM을 검색합니다.

로컬 [!DNL Sites] 배포에서 사용할 수 있는 동일한 분류 계층 구조와 함께 정확한 해당 태그가 있는 원격 자산의 태그만 가져옵니다. 다른 태그는 모두 무시됩니다. 전체 텍스트 검색을 제공하므로 작성자는 원격 [!DNL Experience Manager] 배포에 있는 모든 태그를 사용하여 원격 자산을 검색할 수 있습니다.

### 사용 연습 {#walk-through-of-usage}

위의 설정을 사용하여 작성 환경에서 기능이 어떻게 작동하는지 파악합니다. 원격 DAM 배포 시 원하는 문서 또는 이미지를 사용합니다.

1. [!DNL Experience Manager] 작업 영역에서 **[!UICONTROL Assets]** > **[!UICONTROL 파일]**&#x200B;에 액세스하여 원격 배포의 [!DNL Assets] 인터페이스로 이동합니다. 또는 브라우저에서 `https://[assets_servername_ams]:[port]/assets.html/content/dam`에 액세스합니다. 선택한 자산을 업로드합니다.
1. [!DNL Sites] 배포의 오른쪽 상단 모서리에 있는 프로필 활성자에서 **[!UICONTROL 가장 대상]**&#x200B;을 클릭합니다. `ksaner`를 사용자 이름으로 지정하고 제공된 옵션을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 사이트]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**&#x200B;에서 We.Retail 웹 사이트 페이지를 엽니다. 페이지를 편집합니다. 또는 브라우저에서 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`에 액세스하여 페이지를 편집합니다.

   페이지의 왼쪽 위 모서리에서 **[!UICONTROL 사이드 패널 전환]**&#x200B;을 클릭합니다.

1. [!UICONTROL Assets] 탭(원격 콘텐츠 파인더)을 열고 **[!UICONTROL 연결된 Assets에 로그인]**&#x200B;을 클릭합니다.
1. 자격 증명을 제공합니다(사용자 이름: `ksaner`, 암호: `password`). 이 사용자는 [!DNL Experience Manager] 배포 모두에 대한 작성 권한이 있습니다.
1. DAM에 추가한 자산을 검색합니다. 원격 자산이 왼쪽 패널에 표시됩니다. 이미지 또는 문서를 필터링하고 지원되는 문서 유형을 추가로 필터링합니다. 이미지를 `Image` 구성 요소로, 문서를 `Download` 구성 요소로 드래그합니다.

   가져온 자산은 로컬 [!DNL Sites] 배포에서 읽기 전용입니다. [!DNL Sites] 구성 요소에서 제공하는 옵션을 사용하여 가져온 자산을 편집할 수 있습니다. 구성 요소별 편집은 원본에 영향을 주지 않습니다.

   ![원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션](assets/filetypes_filter_connected_assets.png)

   *그림: 원격 DAM에서 자산을 검색할 때 문서 형식 및 이미지를 필터링하는 옵션*

1. 에셋의 원본을 비동기식으로 가져오는 경우 및 가져오기 작업이 실패할 경우 사이트 작성자에게 알립니다. 작성자는 작성 중이나 작성 후에도 [비동기 작업](/help/sites-administering/asynchronous-jobs.md) 사용자 인터페이스에서 가져오기 작업 및 오류에 대한 자세한 정보를 볼 수 있습니다.

   ![백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.](assets/assets_async_transfer_fails.png)

   *그림: 백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.*

1. 페이지를 게시할 때 [!DNL Experience Manager]은(는) 페이지에서 사용되는 전체 자산 목록을 표시합니다. 게시할 때 원격 자산을 성공적으로 가져오는지 확인합니다. 가져온 각 자산의 상태를 확인하려면 [비동기 작업](/help/sites-administering/asynchronous-jobs.md) 사용자 인터페이스를 참조하십시오.

   >[!NOTE]
   >
   >하나 이상의 원격 자산을 완전히 가져오지 않더라도 페이지가 게시됩니다. [!DNL Experience Manager] 알림 영역에는 비동기 작업 페이지에 표시되는 오류에 대한 알림이 표시됩니다.

>[!CAUTION]
>
>가져온 원격 자산은 웹 페이지에서 사용한 경우 로컬 폴더에 액세스할 권한이 있는 모든 사람이 검색하고 사용할 수 있습니다. 가져온 자산은 로컬 폴더(위의 연습에서 `connectedassets`)에 저장됩니다. 또한 자산은 [!UICONTROL 콘텐츠 파인더]를 통해 로컬 저장소에서 검색하고 볼 수 있습니다.

가져온 자산은 연결된 메타데이터를 편집할 수 없다는 점을 제외하고 다른 로컬 자산으로 사용할 수 있습니다.

### 웹 페이지 간 에셋 사용 확인 {#asset-usage-references}

[!DNL Experience Manager]을(를) 사용하면 DAM 사용자가 에셋에 대한 모든 참조를 확인할 수 있습니다. 원격 [!DNL Sites] 및 복합 자산의 자산 사용을 이해하고 관리하는 데 도움이 됩니다. [!DNL Experience Manager Sites] 배포에 있는 웹 페이지의 많은 작성자가 다른 웹 페이지의 원격 [!DNL Assets]에 있는 자산을 사용할 수 있습니다. 자산 관리를 단순화하고 참조가 손상되지 않도록 DAM 사용자가 로컬 및 원격 웹 페이지에서 자산 사용을 확인하는 것이 중요합니다. 자산의 [!UICONTROL 속성] 페이지에 있는 [!UICONTROL 참조] 탭에는 자산의 로컬 및 원격 참조가 나열됩니다.

[!DNL Assets] 배포에서 참조를 보고 관리하려면 다음 단계를 따르십시오.

1. [!DNL Assets] 콘솔에서 자산을 선택하고 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 참조]** 탭을 클릭합니다. [!DNL Assets] 배포에서 자산을 사용하려면 **[!UICONTROL 로컬 참조]**&#x200B;를 참조하십시오. 연결된 Assets 기능을 사용하여 자산을 가져온 [!DNL Sites] 배포에서 자산을 사용하려면 **[!UICONTROL 원격 참조]를 참조하십시오.

   ![자산 속성 페이지의 원격 참조](assets/connected-assets-remote-reference.png)

1. [!DNL Sites]페이지에 대한 참조는 각 로컬 [!DNL Sites]에 대한 참조 총 개수를 표시합니다. 모든 참조를 찾고 총 참조 수를 표시하는 데 시간이 걸릴 수 있습니다.
1. 참조 목록은 대화형이며 DAM 사용자는 참조를 클릭하여 참조 페이지를 열 수 있습니다. 어떤 이유로 원격 참조를 가져올 수 없는 경우 사용자에게 실패를 알리는 알림이 표시됩니다.
1. 사용자는 에셋을 이동하거나 삭제할 수 있습니다. 에셋을 이동하거나 삭제할 때 선택한 모든 에셋/폴더의 총 참조 수가 경고 대화 상자에 표시됩니다. 참조가 아직 검색되지 않은 에셋을 삭제하면 경고 대화 상자가 표시됩니다.

   ![삭제 강제 경고](assets/delete-referenced-asset.png)

### 원격 DAM의 자산 업데이트 관리 {#manage-updates-in-remote-dam}

원격 DAM과 [!DNL Sites] 배포 간에 [연결을 구성](#configure-a-connection-between-sites-and-assets-deployments)한 후 원격 DAM의 자산을 [!DNL Sites] 배포에서 사용할 수 있게 됩니다. 그런 다음 원격 DAM 에셋 또는 폴더에서의 작업을 업데이트하고, 삭제하고, 이름을 바꾸고, 이동할 수 있습니다. 업데이트는 [!DNL Sites] 배포에서 자동으로 사용할 수 있으며 약간의 지연이 있습니다. 또한 로컬 [!DNL Experience Manager Sites] 페이지에서 원격 DAM의 자산을 사용하는 경우 원격 DAM의 자산에 대한 업데이트가 [!DNL Sites] 페이지에 표시됩니다.

자산을 한 위치에서 다른 위치로 이동하는 동안 자산이 [!DNL Sites] 페이지에 표시되도록 [참조를 조정](/help/assets/manage-assets.md)하십시오. 로컬 [!DNL Sites] 배포에서 액세스할 수 없는 위치로 자산을 이동하면 해당 자산이 Sites 배포에 표시되지 않습니다.

원격 DAM에서 자산에 대한 메타데이터 속성을 업데이트할 수도 있으며 변경 내용은 로컬 [!DNL Sites] 배포에서 사용할 수 있습니다.

[!DNL Sites] 작성자는 [!DNL Sites] 배포에서 사용 가능한 업데이트를 미리 본 다음 변경 내용을 다시 게시하여 [!DNL Experience Manager] 게시 인스턴스에서 사용할 수 있도록 할 수 있습니다.

[!DNL Experience Manager]은(는) 사이트 작성자가 [!DNL Sites] 페이지에서 자산을 사용하지 못하도록 `Remote Assets Content Finder`의 자산에 만료된 상태 시각적 표시기를 표시합니다. [!DNL Sites] 페이지에서 만료된 상태의 자산을 사용하는 경우 해당 자산이 [!DNL Experience Manager] 게시 인스턴스에 표시되지 않습니다.

## 자주 묻는 질문 {#frequently-asked-questions}

+++**[!DNL Sites] 배포에서 사용 가능한 자산을 사용해야 하는 경우 연결된 Assets을 구성해야 합니까?**

이 경우 연결된 Assets을 구성할 필요가 없습니다. [!DNL Sites] 배포에서 사용 가능한 자산을 사용할 수 있습니다.

+++

+++**연결된 Assets 기능을 언제 구성해야 합니까?**

[!DNL Sites] 배포의 원격 DAM 배포에서 사용할 수 있는 자산을 사용해야 하는 경우에만 연결된 Assets 기능을 구성하십시오.

+++

+++**연결된 Assets을 구성한 후 여러 [!DNL Sites] 배포를 원격 DAM 배포에 연결할 수 있습니까?**

예. 연결된 Assets을 구성한 후 여러 [!DNL Sites] 배포를 원격 DAM 배포에 연결할 수 있습니다. 자세한 내용은 [연결된 Assets 아키텍처](#connected-assets-architecture)를 참조하십시오.

+++

+++**연결된 Assets을 구성한 후 [!DNL Sites] 배포에 연결할 수 있는 원격 DAM 배포의 수는 몇 개입니까?**

연결된 Assets을 구성한 후 원격 DAM 배포 하나를 [!DNL Sites] 배포에 연결할 수 있습니다. 자세한 내용은 [연결된 Assets 아키텍처](#connected-assets-architecture)를 참조하십시오.

+++

+++**연결된 Assets을 구성한 후 [!DNL Sites] 배포에서 Dynamic Media 자산을 사용할 수 있습니까?**

연결된 Assets을 구성한 후 [!DNL Dynamic Media]개의 자산을 [!DNL Sites] 배포에서 읽기 전용 모드로 사용할 수 있습니다. 따라서 [!DNL Dynamic Media]을(를) 사용하여 [!DNL Sites] 배포에서 자산을 처리할 수 없습니다. 자세한 내용은 [사이트 및 Dynamic Media 배포 간 연결 구성](#dynamic-media-assets)을 참조하십시오.

+++

+++**연결된 Assets을 구성한 후 [!DNL Sites] 배포의 원격 DAM 배포에서 이미지 및 문서 형식 유형의 자산을 사용할 수 있습니까?**

예. 연결된 Assets을 구성한 후 [!DNL Sites] 배포의 원격 DAM 배포에서 이미지 및 문서 형식 유형의 자산을 사용할 수 있습니다.

+++

+++**연결된 Assets을 구성한 후 [!DNL Sites] 배포에서 원격 DAM 배포의 콘텐츠 조각 및 비디오 자산을 사용할 수 있습니까?**

아니요. 연결된 Assets을 구성한 후에는 [!DNL Sites] 배포에서 원격 DAM 배포의 콘텐츠 조각 및 비디오 자산을 사용할 수 없습니다.

+++

+++**연결된 Assets을 구성한 후 [!DNL Sites] 배포의 원격 DAM 배포에서 Dynamic Media 자산을 사용할 수 있습니까?**

예. 연결된 Assets을 구성한 후 [!DNL Sites] 배포의 원격 DAM 배포에서 Dynamic Media 이미지 자산을 구성하고 사용할 수 있습니다. 자세한 내용은 [사이트 및 Dynamic Media 배포 간 연결 구성](#dynamic-media-assets)을 참조하십시오.

+++

+++**연결된 Assets을 구성한 후 원격 DAM 에셋 또는 폴더에서의 작업을 업데이트하고, 삭제하고, 이름을 바꾸고, 이동할 수 있습니까?**

예. 연결된 Assets을 구성한 후 원격 DAM 에셋 또는 폴더에서의 작업을 업데이트하고, 삭제하고, 이름을 바꾸고, 이동 할 수 있습니다. 업데이트는 약간의 지연과 함께 Sites 배포에서 자동으로 사용할 수 있습니다. 자세한 내용은 [원격 DAM의 자산 업데이트 관리](#handling-updates-to-remote-assets)를 참조하십시오.

+++

+++**연결된 Assets을 구성한 후 [!DNL Sites] 배포에서 자산을 추가하거나 수정하고 원격 DAM 배포에서 사용할 수 있도록 설정할 수 있습니까?**

[!DNL Sites] 배포에 자산을 추가할 수 있지만 원격 DAM 배포에 해당 자산을 사용할 수 없습니다.

+++

## 제한 사항 및 우수 사례 {#tip-and-limitations}

* 에셋 사용에 대한 통찰력을 얻으려면 [!DNL Sites] 인스턴스에서 [Assets 통찰력](/help/assets/asset-insights.md) 기능을 구성하십시오.

* 원격 자산을 [이미지 구성 요소 구성 대화 상자](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=ko#configure-dialog)(으)로 끌 수 없습니다. 그러나 **[!UICONTROL 구성]**&#x200B;을 클릭하지 않고 사이트 페이지의 이미지 구성 요소로 원격 자산을 직접 드래그할 수 있습니다.

### 권한 및 자산 관리 {#permissions-and-managing-assets}

* 로컬 자산은 읽기 전용 복사본입니다. [!DNL Experience Manager]개의 구성 요소가 자산을 원본에 영향을 주지 않고 편집합니다. 다른 편집 작업은 허용되지 않습니다.
* 로컬로 가져온 자산은 작성용으로만 사용할 수 있습니다. 자산 업데이트 워크플로우를 적용할 수 없고 메타데이터를 편집할 수 없습니다.
* 이미지 및 나열된 문서 형식만 지원됩니다. [!DNL Content Fragments] 및 [!DNL Experience Fragments]은(는) 지원되지 않습니다.
* [!DNL Experience Manager]이(가) 메타데이터 스키마를 가져오지 않습니다. 즉, 가져온 모든 메타데이터가 표시되지 않을 수 있습니다. 스키마가 [!DNL Sites] 배포에서 별도로 업데이트되면 모든 메타데이터 속성이 표시됩니다.
* 작성자가 원격 DAM 배포에 액세스할 수 없는 경우에도 모든 [!DNL Sites] 작성자는 가져온 복사본에 대한 읽기 권한을 갖습니다.
* 통합을 사용자 지정할 수 있는 API 지원이 없습니다.
* 이 기능을 통해 원격 자산을 원활하게 검색하고 사용할 수 있습니다. 로컬 배포에서 많은 원격 자산을 한 번에 사용할 수 있도록 하려면 자산을 마이그레이션하는 것이 좋습니다. [자산 마이그레이션 안내서](assets-migration-guide.md)를 참조하십시오.
* [!UICONTROL 페이지 속성] 사용자 인터페이스에서 원격 자산을 페이지 축소판으로 사용할 수 없습니다. [!UICONTROL 이미지 선택]을 클릭하여 [!UICONTROL 썸네일]에서 [!UICONTROL 페이지 속성] 사용자 인터페이스에 있는 웹 페이지의 썸네일을 설정할 수 있습니다.

### 설정 및 라이선스 {#setup-licensing}

* [!DNL Adobe Managed Services]에서 [!DNL Assets] 배포가 지원됩니다.
* [!DNL Sites]은(는) 한 번에 하나의 [!DNL Assets] 배포에 연결할 수 있습니다.
* 원격 리포지토리로 작동하는 [!DNL Assets]의 라이선스가 필요합니다.
* 로컬 작성 배포로 작동하는 [!DNL Sites]의 라이선스가 하나 이상 필요합니다.

### 사용 {#usage}

* 작성할 때 원격 자산을 검색하고 로컬 페이지에서 드래그할 수 있습니다. 다른 기능은 지원되지 않습니다.
* 5초 후에 가져오기 작업 시간이 종료됩니다. 네트워크 문제가 있는 경우 작성자가 자산을 가져오는 데 문제가 있을 수 있습니다. 작성자가 [!UICONTROL 콘텐츠 파인더]에서 [!UICONTROL 페이지 편집기] (으)로 원격 자산을 끌어 다시 시도할 수 있습니다.
* `Image` 구성 요소를 통해 지원되는 편집과 원본에 영향을 주지 않는 간단한 편집은 가져온 자산에서 수행할 수 있습니다. 자산은 읽기 전용입니다.
* 자산을 다시 가져오는 유일한 방법은 페이지에서 자산을 드래그하는 것입니다. API 지원 또는 업데이트할 에셋을 다시 가져오는 다른 방법은 없습니다.
* 자산이 DAM에서 서비스 해제된 경우 [!DNL Sites]페이지에서 계속 사용됩니다.
* 자산의 원격 참조 항목을 비동기식으로 가져옵니다. 참조와 총 횟수는 실시간이 아니며, DAM 사용자가 참조를 조회하는 동안 사이트 작성자가 에셋을 사용하는 경우에는 차이가 있을 수 있습니다. DAM 사용자는 페이지를 새로 고치고 몇 분 후에 다시 시도하여 총 수를 가져올 수 있습니다.

## 문제 해결 {#troubleshoot}

일반적인 오류를 해결하려면 다음 단계를 수행합니다.

* [!UICONTROL 콘텐츠 파인더]에서 원격 자산을 검색할 수 없는 경우 필요한 역할과 권한이 있는지 확인하십시오.

* 하나 이상의 이유로 원격 DAM에서 가져온 자산은 웹 페이지에 게시되지 않을 수 있습니다. 원격 서버에 존재하지 않거나, 가져오기 위한 적절한 권한이 없거나, 네트워크 오류가 원인일 수 있습니다. 원격 DAM에서 자산이 제거되지 않았는지 확인합니다. 적절한 권한이 있고 사전 요구 사항이 충족되는지 확인하십시오. 에셋을 페이지에 다시 추가하고 다시 게시합니다. [비동기 작업 목록](/help/sites-administering/asynchronous-jobs.md)에서 자산 가져오기 오류를 확인합니다.

* 로컬 [!DNL Sites] 배포에서 원격 DAM 배포에 액세스할 수 없는 경우 사이트 간 쿠키가 허용되고 [동일한 사이트 쿠키 지원](/help/sites-administering/same-site-cookie-support.md)이 구성되었는지 확인하십시오. 사이트 간 쿠키가 차단된 경우 [!DNL Experience Manager]의 배포를 인증할 수 없습니다. 예를 들어, 시크릿 모드의 [!DNL Google Chrome]은(는) 서드파티 쿠키를 차단할 수 있습니다. [!DNL Chrome] 브라우저에서 쿠키를 허용하려면 주소 표시줄에서 &#39;눈&#39; 아이콘을 클릭하고 **사이트가 작동하지 않음** > **차단됨**(으)로 이동한 다음 원격 DAM URL을 선택하고 로그인 토큰 쿠키를 허용하십시오. 또는 [서드파티 쿠키를 활성화하는 방법](https://support.google.com/chrome/answer/95647)을 참조하십시오.

  ![시크릿 모드에서 Chrome 브라우저에 쿠키 오류가 발생했습니다](assets/chrome-cookies-incognito-dialog.png)

* Experience Manager Sites as a Cloud Service 사이트 배포에서 Managed Services 원격 DAM 배포 Adobe에 액세스할 수 없는 경우 원격 DAM이 Dispatcher 구성에 다음 내용을 포함하도록 `"/etc/httpd/conf.d/available_vhosts`에서 사용할 수 있는 `aem_author.vhost` 파일을 업데이트하십시오.

  ```xml
  Header Set Access-Control-Allow-Origin <Local Sites instance host>
  Header Set Access-Control-Allow-Credentials true
  ```

* 원격 참조가 검색되지 않아 오류 메시지가 표시되는 경우 [!DNL Sites] 배포를 사용할 수 있는지 확인하고 네트워크 연결 문제가 있는지 확인하십시오. 확인하려면 나중에 다시 시도하십시오. [!DNL Assets] 배포는 [!DNL Sites] 배포와의 연결을 두 번 설정한 다음 오류를 보고합니다.

  ![자산 원격 참조를 검색하지 못함](assets/reference-report-failure.png)

* 쿠키가 Sites 서버에서 Google Chrome의 Assets 서버로 전송되지 않으면 Assets 연결이 HTTPS를 통해 전송되지 않기 때문입니다. Assets 인스턴스에서 HTTPS를 사용하지 않는 경우 Assets 서버를 인증하면 `SameSite=None` 헤더를 응답에 추가할 수 없습니다.

