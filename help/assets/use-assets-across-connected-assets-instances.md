---
title: 연결된 에셋을 사용하여에서 DAM 에셋 공유 [!DNL Sites]
description: 원격에서 사용 가능한 자산 사용 [!DNL Adobe Experience Manager Assets] 다른 웹 페이지에서 웹 페이지를 만들 때 배포 [!DNL Adobe Experience Manager Sites] 배포.
contentOwner: AK
mini-toc-levels: 2
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3949'
ht-degree: 17%

---

# 연결된 에셋을 사용하여에서 DAM 에셋 공유 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=en) |
| AEM 6.5 | 이 문서 |


대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 배포할 수 있습니다. 이러한 웹 사이트를 만드는 데 사용되는 웹 사이트 제작 기능과 디지털 자산이 서로 다른 배포에 있을 수 있습니다. 함께 작업하는 데 필요한 기존 배포가 지리적으로 분산되는 이유 중 하나가 될 수 있습니다. 다른 이유는 다른 것을 포함하여, 이종 인프라로 이어지는 취득일 수 있다 [!DNL Experience Manager] 상위 회사가 함께 사용하려는 버전입니다.

연결된 자산 기능은 다음을 통합하여 위의 사용 사례를 지원합니다 [!DNL Experience Manager Sites] 및 [!DNL Experience Manager Assets]. 사용자는에서 웹 페이지를 만들 수 있습니다. [!DNL Sites] 별도의 디지털 에셋을 사용하는 경우 [!DNL Assets] 배포.

>[!NOTE]
>
>웹 페이지 작성을 위해 별도의 Sites 배포에서 원격 DAM 배포에 사용할 수 있는 자산을 사용해야 하는 경우에만 연결된 자산을 구성합니다.

## 연결된 자산 개요 {#overview-of-connected-assets}

에서 페이지 편집 시 [!UICONTROL 페이지 편집기] 작성자는 타겟 대상으로 다른 에셋의 에셋을 원활하게 검색, 탐색 및 포함할 수 있습니다 [!DNL Assets] 자산 소스 역할을 하는 배포. 관리자는 의 배포를 한 번만 통합합니다 [!DNL Experience Manager] 포함 [!DNL Sites] 의 다른 배포를 통한 기능 [!DNL Experience Manager] 포함 [!DNL Assets] 기능. 사이트 작성자는 연결된 에셋을 통해 사이트의 웹 페이지에서 Dynamic Media 이미지를 사용할 수도 있고 스마트 자르기 및 이미지 사전 설정과 같은 Dynamic Media 기능을 활용할 수 있습니다.

의 경우 [!DNL Sites] 작성자는 원격 자산을 읽기 전용 로컬 자산으로 사용할 수 있습니다. 이 기능은 사이트 편집기에서 원격 자산을 원활하게 검색하고 액세스할 수 있도록 지원합니다. Sites에서 전체 에셋 코퍼스를 사용할 수 있어야 하는 기타 사용 사례의 경우 연결된 에셋을 사용하는 대신 에셋을 일괄적으로 마이그레이션하는 것이 좋습니다. 다음을 참조하십시오 [Experience Manager Assets 마이그레이션 안내서](/help/assets/assets-migration-guide.md).

### 사전 요구 사항 및 지원되는 배포 {#prerequisites}

이 기능을 사용하거나 구성하기 전에 다음을 확인하십시오.

* 사용자는 각 배포에서 적절한 사용자 그룹에 속합니다.
* 대상 [!DNL Adobe Experience Manager] 배포 유형, 지원되는 기준 중 하나가 충족됩니다. [!DNL Experience Manager] 6.5 [!DNL Assets] 와 함께 작업 [!DNL Experience Manager] as a Cloud Service. 에서 이 기능이 작동하는 방식에 대한 자세한 정보 [!DNL Experience Manager] as a [!DNL Cloud Service], 참조 [Experience Manager의 연결된 자산 as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html).

  | | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] AMS에서 | [!DNL Experience Manager] 6.5 [!DNL Sites] 온-프레미스 |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 지원됨 | 지원됨 | 지원됨 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] AMS에서** | 지원됨 | 지원됨 | 지원됨 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 온-프레미스** | 지원되지 않음 | 지원되지 않음 | 지원되지 않음 |

### 지원되는 파일 형식 {#mimetypes}

작성자가 콘텐츠 파인더에서 이미지와 다음 유형의 문서를 검색하고 페이지 편집기에서 검색된 에셋을 드래그합니다. 문서가 다음에 추가됩니다 `Download` 구성 요소 및 이미지를 `Image` 구성 요소. 작성자가 원하는 경우 원격 자산을 추가할 수도 있습니다 [!DNL Experience Manager] 기본값을 확장하는 구성 요소 `Download` 또는 `Image` 구성 요소. 지원되는 형식은 다음과 같습니다.

* **이미지 형식**: [이미지 구성 요소](assets-formats.md#supported-raster-image-formats) 를 지원합니다.
* **문서 형식**: 다음을 참조하십시오. [지원되는 문서 형식](assets-formats.md#supported-document-formats).

### 관련 사용자 및 그룹 {#users-and-groups-involved}

기능 및 해당 사용자 그룹을 구성하고 사용하는 데 관련된 여러 가지 역할이 아래에 설명되어 있습니다. 로컬 범위는 작성자가 웹 페이지를 만드는 사용 사례에 사용됩니다. 원격 범위는 필요한 자산을 호스팅하는 DAM 배포에 사용됩니다. 다음 [!DNL Sites] 작성자가 이러한 원격 자산을 가져옵니다.

| 역할 | 범위 | 사용자 그룹 | 연습의 사용자 이름 | 설명 |
|---|---|---|---|---|
| [!DNL Sites] administrator | 로컬 | [!DNL Experience Manager] `administrators` | `admin` | 설정 [!DNL Experience Manager] 및 원격 시스템과의 통합 구성 [!DNL Assets] 배포. |
| DAM 사용자 | 로컬 | `Authors` | `ksaner` | `/content/DAM/connectedassets/`에서 가져온 자산을 보고 복제하는 데 사용됩니다. |
| [!DNL Sites] 작성자 | 로컬 | <ul><li>`Authors` (원격 DAM에 대한 읽기 액세스 권한과 로컬에 대한 작성자 액세스 권한 있음) [!DNL Sites]) </li> <li>`dam-users` 로컬 [!DNL Sites]</li></ul> | `ksaner` | 최종 사용자는 [!DNL Sites] 이 통합을 사용하여 콘텐츠 속도를 향상시키는 작성자. 작성자가 를 사용하여 원격 DAM에서 자산을 검색하고 찾아봅니다. [!UICONTROL 콘텐츠 파인더] 로컬 웹 페이지에서 필요한 이미지 사용. `ksaner` DAM 사용자의 자격 증명이 사용됩니다. |
| [!DNL Assets] administrator | 원격 | [!DNL Experience Manager] `administrators` | `admin` 원격 [!DNL Experience Manager] | CORS(원본 간 리소스 공유)를 구성합니다. |
| DAM 사용자 | 원격 | `Authors` | `ksaner` 원격 [!DNL Experience Manager] | 원격에서 작성자 역할 [!DNL Experience Manager] 배포. 를 사용하여 연결된 자산에서 자산 검색 및 찾아보기 [!UICONTROL 콘텐츠 파인더]. |
| DAM 배포자(기술 사용자) | 원격 | [!DNL Sites] `Authors` | `ksaner` 원격 [!DNL Experience Manager] | 원격 배포에 있는 이 사용자는 [!DNL Experience Manager] 로컬 서버(다음이 아님) [!DNL Sites] 작성자 역할) 을(를) 대신해 원격 자산을 가져옵니다. [!DNL Sites] 작성자. 이 역할은 위의 두 `ksaner` 역할과 동일하지 않으며 다른 사용자 그룹에 속합니다. |

### 연결된 자산 아키텍처 {#connected-assets-architecture}

Experience Manager을 사용하면 원격 DAM 배포를 소스로 여러 Experience Manager에 연결할 수 있습니다 [!DNL Sites] 배포. 그러나 다음을 연결할 수 있습니다 [!DNL Sites] 원격 DAM 배포가 하나만 있는 배포.

원격 DAM 배포에 연결할 최적의 사이트 인스턴스 수를 평가합니다. Adobe은 연결된 각 사이트 인스턴스가 원격 DAM의 데이터 트래픽에 기여하므로 사이트 인스턴스를 배포에 점진적으로 연결하고 원격 DAM에 성능에 영향을 주지 않는지 테스트할 것을 권장합니다.

다음 다이어그램은 지원되는 시나리오를 보여 줍니다.

![연결된 자산 아키텍처](assets/connected-assets-architecture.png)

다음 다이어그램은 지원되지 않는 시나리오를 보여 줍니다.

![연결된 자산 아키텍처](assets/connected-assets-architecture-unsupported.png)

## 다음 간 연결 구성 [!DNL Sites] 및 [!DNL Assets] 배포 {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] 관리자가 이 통합을 만들 수 있습니다. 만들고 나면 이를 사용하는 데 필요한 권한이 사용자 그룹을 통해 설정됩니다. 사용자 그룹은 [!DNL Sites] 배포 및 DAM 배포 시.

연결된 자산 및 로컬 구성하기 [!DNL Sites] 연결, 다음 단계를 수행합니다.

1. 기존 액세스 [!DNL Sites] 배포 또는 다음 명령을 사용하여 배포 만들기:

   1. JAR 파일의 폴더에서 터미널에서 다음 명령을 실행하여 각 파일을 생성합니다 [!DNL Experience Manager] 서버입니다.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 몇 분 후에 [!DNL Experience Manager] 서버가 정상적으로 시작됩니다. 고려 사항 [!DNL Sites] 웹 페이지 작성을 위한 로컬 시스템으로 배포(예: `https://[local_sites]:4502`.

1. 에 적절한 범위의 사용자 및 역할이 있는지 확인합니다. [!DNL Sites] 배포 및 [!DNL Assets] ams에서 배포. 에서 기술 사용자 만들기 [!DNL Assets] 배포 및에 언급된 사용자 그룹에 추가 [관련 사용자 및 그룹](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. 로컬 액세스 [!DNL Sites] 배포 위치 `https://[local_sites]:4502`. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 연결된 자산 구성]**&#x200B;을 클릭하고 다음 값을 제공합니다.

   1. A **[!UICONTROL 제목]** 을 참조하십시오.
   1. **[!UICONTROL 원격 DAM URL]** 은 의 URL입니다. [!DNL Assets] 형식에서 위치 `https://[assets_servername]:[port]`.
   1. DAM 배포자의 자격 증명(기술 사용자)
   1. 다음에서 **[!UICONTROL 마운트 지점]** 필드에 로컬을 입력합니다. [!DNL Experience Manager] 경로: [!DNL Experience Manager] 자산을 가져옵니다. 예를 들면 `remoteassets` 폴더를 입력합니다. DAM에서 가져온 자산은 의 이 폴더에 저장됩니다. [!DNL Sites] 배포.
   1. **[!UICONTROL 로컬 사이트 URL]** 는 의 위치입니다. [!DNL Sites] 배포. [!DNL Assets] 배포에서는 이 값을 사용하여 이 로 가져온 디지털 자산에 대한 참조를 유지 관리합니다. [!DNL Sites] 배포.
   1. 의 자격 증명 [!DNL Sites] 기술 사용자.
   1. 값: **[!UICONTROL 원본 이진 전송 최적화 임계값]** 필드는 원본 에셋(렌디션 포함)이 동기적으로 전송되는지 여부를 지정합니다. 상대적으로 파일 크기가 큰 자산이 비동기식으로 가장 잘 동기화되는 반면 파일 크기가 작은 자산을 쉽게 가져올 수 있습니다. 값은 네트워크 기능에 따라 다릅니다.
   1. 선택 **[!UICONTROL 연결된 자산과 공유되는 데이터 저장소]**&#x200B;를 사용하는 경우 데이터 저장소를 사용하여 자산을 저장하고 데이터 저장소가 두 배포 간에 공유됩니다. 이 경우 실제 자산 바이너리를 데이터 저장소에서 사용할 수 있고 전송되지 않으므로 임계값 제한은 문제가 되지 않습니다.

   ![연결된 자산 기능에 대한 일반적인 구성](assets/connected-assets-typical-config.png)

   *그림: 연결된 자산 기능에 대한 일반적인 구성*

1. 의 기존 디지털 에셋 [!DNL Assets] 배포가 이미 처리되고 렌디션이 생성됩니다. 이러한 렌디션은 이 기능을 사용하여 가져오므로 렌디션을 다시 생성할 필요가 없습니다. 워크플로 시작 관리자를 비활성화하여 렌디션의 재생성을 방지합니다. 에서 런처 구성 조정([!DNL Sites]) 제외할 배포 `connectedassets` 폴더(자산을 이 폴더에서 가져옵니다.)

   1. 날짜 [!DNL Sites] 배포, 클릭 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 런처]**.

   1. **[!UICONTROL DAM 자산 업데이트]** 및 **[!UICONTROL DAM 메타데이터 원본에 쓰기]**&#x200B;로 워크플로우를 사용하여 런처를 검색합니다.

   1. 워크플로우 런처를 선택하고 작업 표시줄에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

   1. 다음에서 [!UICONTROL 속성] 마법사, 변경 **[!UICONTROL 경로]** 필드는 다음 매핑으로 사용되어 마운트 지점을 제외하도록 해당 정규식을 업데이트합니다. **[!UICONTROL connecedassets]**.

   | 이전 | 이후 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >작성자가 자산을 가져올 때 원격 배포에서 사용할 수 있는 모든 렌디션을 가져옵니다. 가져온 자산의 렌디션을 더 만들려면 이 구성 단계를 건너뜁니다. 다음 [!UICONTROL DAM 자산 업데이트] 워크플로우가 트리거되어 더 많은 렌디션을 만듭니다. 이러한 렌디션은 로컬에서만 사용할 수 있습니다. [!DNL Sites] 원격 DAM 배포가 아닌 배포.

1. 추가 [!DNL Sites] 의 CORS 구성에서 허용된 원본으로 배포 [!DNL Assets] 배포. 자세한 내용은 [CORS 이해](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. 구성 [동일 사이트 쿠키 지원](/help/sites-administering/same-site-cookie-support.md).

구성된 간 연결을 확인할 수 있습니다. [!DNL Sites] 배포 및 [!DNL Assets] 배포.

![연결된 자산의 연결 테스트가 구성됨 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*그림: 구성된 연결된 자산의 연결 테스트 [!DNL Sites].*

## Dynamic Media 에셋 사용 {#dynamic-media-assets}


연결된 에셋을 사용하여에서 처리한 이미지 에셋을 사용할 수 있습니다 [!DNL Dynamic Media] 사이트 페이지의 원격 DAM 배포에서 스마트 자르기 및 이미지 사전 설정과 같은 Dynamic Media 기능을 활용합니다.

사용 [!DNL Dynamic Media] 연결된 자산:

1. 구성 [!DNL Dynamic Media] 동기화 모드가 활성화된 원격 DAM 배포에서.
1. 구성 [연결된 자산](#configure-a-connection-between-sites-and-assets-deployments).
1. 구성 [!DNL Dynamic Media] 원격 DAM에 구성된 것과 동일한 회사 이름을 가진 Sites 인스턴스에서 를 실행합니다. 연결된 자산에서 작업하려면 Sites 배포에 Dynamic Media 계정에 대한 읽기 전용 액세스 권한이 있어야 합니다. 따라서 Sites 인스턴스의 Dynamic Media 구성에서 동기화 모드를 비활성화해야 합니다.

>[!CAUTION]
>
>연결된 자산 및 [!DNL Dynamic Media] 구성, 사용할 수 없음 [!DNL Dynamic Media] 에서 사용할 수 있는 로컬 에셋을 처리하려면 [!DNL Sites] 배포.

## 구성 [!DNL Dynamic Media] {#configure-dynamic-media}

구성하려면 [!DNL Dynamic Media] 날짜 [!DNL Assets] 및 [!DNL Sites] 배포:

1. 활성화 및 구성 [!DNL Dynamic Media] 원격에서 전역 구성으로 [!DNL Assets] 작성자 배포. Dynamic Media을 구성하려면 다음을 참조하십시오. [Dynamic Media 구성](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).
원격 [!DNL Assets] 배포, 위치 [!UICONTROL Dynamic Media 동기화 모드], 선택 **[!UICONTROL 기본적으로 활성화됨]**.

1. 에 설명된 대로 연결된 자산 구성 만들기 [사이트 및 자산 배포 간 연결 구성](#configure-a-connection-between-sites-and-assets-deployments). 또한 을 선택합니다. **[!UICONTROL Dynamic Media에 연결된 에셋의 원본 렌디션 가져오기]** 옵션을 선택합니다.

1. 구성 [!DNL Dynamic Media] 로컬 [!DNL Sites] 및 원격 [!DNL Assets] 배포. 다음 지침을 따르십시오 [구성 [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).

   * 모든 구성에서 동일한 회사 이름을 사용합니다.
   * 로컬 [!DNL Sites], 위치 [!UICONTROL Dynamic Media 동기화 모드], 선택 **[!UICONTROL 기본적으로 비활성화됨]**. 다음 [!DNL Sites] 배포에는 읽기 전용 액세스 권한이 있어야 함 [!DNL Dynamic Media] 계정입니다.
   * 로컬 [!DNL Sites], **[!UICONTROL 자산 게시]** 옵션, 선택 **[!UICONTROL 선택적 게시]**. 선택 안 함 **[!UICONTROL 모든 콘텐츠 동기화]**.

1. 사용 [[!DNL Dynamic Media] 이미지 핵심 구성 요소에서 지원](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). 이 기능은 기본값을 활성화합니다. [이미지 구성 요소](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) 표시 [!DNL Dynamic Media] 다음과 같은 경우 이미지 [!DNL Dynamic Media] 이미지는 로컬 웹 페이지의 작성자가 사용합니다. [!DNL Sites] 배포.

## 원격 자산 사용 {#use-remote-assets}

웹 사이트 작성자가 콘텐츠 파인더를 사용하여 DAM 배포에 연결합니다. 작성자는 구성 요소에서 원격 자산을 찾아보고 검색하고 드래그할 수 있습니다. 원격 DAM을 인증하려면 관리자가 제공한 자격 증명(있는 경우)을 가까이 보관하십시오.

작성자는 로컬 DAM 및 원격 DAM 배포에서 사용할 수 있는 자산을 단일 웹 페이지에서 사용할 수 있습니다. 콘텐츠 파인더를 사용하여 로컬 DAM을 검색하거나 원격 DAM을 검색합니다.

로컬에서 사용할 수 있는 동일한 분류 계층 구조와 함께 정확한 해당 태그가 있는 원격 자산의 태그만 가져옵니다 [!DNL Sites] 배포. 다른 태그는 모두 무시됩니다. 작성자는 원격에 있는 모든 태그를 사용하여 원격 자산을 검색할 수 있습니다 [!DNL Experience Manager] 전체 텍스트 검색을 제공하므로 배포.

### 사용 연습 {#walk-through-of-usage}

위의 설정을 사용하여 작성 환경에서 기능이 어떻게 작동하는지 파악합니다. 원격 DAM 배포 시 원하는 문서 또는 이미지를 사용합니다.

1. 다음 위치로 이동 [!DNL Assets] 를 통해 원격 배포의 인터페이스 **[!UICONTROL 에셋]** > **[!UICONTROL 파일]** 출처: [!DNL Experience Manager] 작업 영역. 또는 브라우저에서 `https://[assets_servername_ams]:[port]/assets.html/content/dam`에 액세스합니다. 선택한 자산을 업로드합니다.
1. 다음에서 [!DNL Sites] 배포, 오른쪽 상단의 프로필 활성자에서 **[!UICONTROL 다음 사용자로 가장]**. `ksaner`를 사용자 이름으로 지정하고 제공된 옵션을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 사이트]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**&#x200B;에서 We.Retail 웹 사이트 페이지를 엽니다. 페이지를 편집합니다. 또는 브라우저에서 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`에 액세스하여 페이지를 편집합니다.

   페이지의 왼쪽 위 모서리에서 **[!UICONTROL 사이드 패널 전환]**&#x200B;을 클릭합니다.

1. 를 엽니다. [!UICONTROL 에셋] 탭(원격 콘텐츠 파인더) 및 클릭 **[!UICONTROL 연결된 자산에 로그인]**.
1. 자격 증명을 제공합니다(사용자 이름: `ksaner`, 암호: `password`). 이 사용자는 다음 두 항목에 대한 작성 권한이 있습니다. [!DNL Experience Manager] 배포.
1. DAM에 추가한 자산을 검색합니다. 원격 자산이 왼쪽 패널에 표시됩니다. 이미지 또는 문서를 필터링하고 지원되는 문서 유형을 추가로 필터링합니다. 이미지를 `Image` 구성 요소로, 문서를 `Download` 구성 요소로 드래그합니다.

   가져온 자산은 로컬에서 읽기 전용입니다. [!DNL Sites] 배포. 에서 제공하는 옵션을 계속 사용할 수 있습니다. [!DNL Sites] 가져온 자산을 편집할 구성 요소입니다. 구성 요소별 편집은 원본에 영향을 주지 않습니다.

   ![원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션](assets/filetypes_filter_connected_assets.png)

   *그림: 원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션.*

1. 에셋의 원본을 비동기식으로 가져오는 경우 및 가져오기 작업이 실패할 경우 사이트 작성자에게 알립니다. 작성자는 작성 중이나 작성 후에도 의 가져오기 작업 및 오류에 대한 자세한 정보를 볼 수 있습니다. [비동기 작업](/help/sites-administering/asynchronous-jobs.md) 사용자 인터페이스.

   ![백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.](assets/assets_async_transfer_fails.png)

   *그림: 백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.*

1. 페이지를 게시할 때, [!DNL Experience Manager] 페이지에서 사용되는 자산의 전체 목록을 표시합니다. 게시할 때 원격 자산을 성공적으로 가져오는지 확인합니다. 가져온 각 자산의 상태를 확인하려면 다음을 참조하십시오. [비동기 작업](/help/sites-administering/asynchronous-jobs.md) 사용자 인터페이스.

   >[!NOTE]
   >
   >하나 이상의 원격 자산을 완전히 가져오지 않더라도 페이지가 게시됩니다. 다음 [!DNL Experience Manager] 알림 영역에는 비동기 작업 페이지에 표시되는 오류에 대한 알림이 표시됩니다.

>[!CAUTION]
>
>가져온 원격 자산은 웹 페이지에서 사용한 경우 로컬 폴더에 액세스할 권한이 있는 모든 사람이 검색하고 사용할 수 있습니다. 가져온 자산은 로컬 폴더에 저장됩니다(`connectedassets` (위의 연습에서). 또한 자산은 [!UICONTROL 콘텐츠 파인더]를 통해 로컬 저장소에서 검색하고 볼 수 있습니다.

가져온 자산은 연결된 메타데이터를 편집할 수 없다는 점을 제외하고 다른 로컬 자산으로 사용할 수 있습니다.

### 웹 페이지 간 에셋 사용 확인 {#asset-usage-references}

[!DNL Experience Manager] dam 사용자가 에셋에 대한 모든 참조를 확인할 수 있습니다. 원격 자산의 사용을 이해하고 관리하는 데 도움이 됩니다 [!DNL Sites] 및 복합 에셋에 포함될 수 있습니다. 의 많은 웹 페이지 작성자 [!DNL Experience Manager Sites] 배포는 원격으로 자산을 사용할 수 있습니다. [!DNL Assets] 다른 웹 페이지에서. 자산 관리를 단순화하고 참조가 손상되지 않도록 DAM 사용자가 로컬 및 원격 웹 페이지에서 자산 사용을 확인하는 것이 중요합니다. 다음 [!UICONTROL 참조] 에셋의 탭 [!UICONTROL 속성] 페이지에는 자산의 로컬 및 원격 참조가 나열됩니다.

에서 참조를 보고 관리하려면 [!DNL Assets] 배포에서 다음 단계를 수행합니다.

1. 에서 에셋 선택 [!DNL Assets] 콘솔 및 클릭 **[!UICONTROL 속성]** 을 클릭합니다.
1. 클릭 **[!UICONTROL 참조]** 탭. 다음을 참조하십시오 **[!UICONTROL 로컬 참조]** 에서 에셋 사용 [!DNL Assets] 배포. ** 참조[!UICONTROL 원격 참조] 의 에셋 사용 [!DNL Sites] 연결된 자산 기능을 사용하여 자산을 가져온 배포입니다.

   ![자산 속성 페이지의 원격 참조](assets/connected-assets-remote-reference.png)

1. 에 대한 참조 [!DNL Sites] 페이지에는 각 로컬에 대한 총 참조 수가 표시됩니다. [!DNL Sites]. 모든 참조를 찾고 총 참조 수를 표시하는 데 시간이 걸릴 수 있습니다.
1. 참조 목록은 대화형이며 DAM 사용자는 참조를 클릭하여 참조 페이지를 열 수 있습니다. 어떤 이유로 원격 참조를 가져올 수 없는 경우 사용자에게 실패를 알리는 알림이 표시됩니다.
1. 사용자는 에셋을 이동하거나 삭제할 수 있습니다. 에셋을 이동하거나 삭제할 때 선택한 모든 에셋/폴더의 총 참조 수가 경고 대화 상자에 표시됩니다. 참조가 아직 검색되지 않은 에셋을 삭제하면 경고 대화 상자가 표시됩니다.

   ![강제 삭제 경고](assets/delete-referenced-asset.png)

### 원격 DAM의 자산 업데이트 관리 {#manage-updates-in-remote-dam}

다음 이후 [연결 구성](#configure-a-connection-between-sites-and-assets-deployments) 원격 DAM과 [!DNL Sites] 배포를에서 사용할 수 있도록 원격 DAM의 자산이 [!DNL Sites] 배포. 그런 다음 원격 DAM 에셋 또는 폴더에서의 작업을 업데이트하고, 삭제하고, 이름을 바꾸고, 이동할 수 있습니다. 업데이트는 약간의 지연과 함께 다음에서 자동으로 사용할 수 있습니다. [!DNL Sites] 배포. 또한 원격 DAM의 자산이 로컬에서 사용되는 경우 [!DNL Experience Manager Sites] 원격 DAM의 자산에 대한 업데이트가 [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다.

자산을 한 위치에서 다른 위치로 이동하는 동안 [참조 조정](/help/assets/manage-assets.md) 에셋이에 표시되도록 [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다. 자산을 로컬에서 액세스할 수 없는 위치로 이동하는 경우 [!DNL Sites] 배포하면 Sites 배포에 자산이 표시되지 않습니다.

원격 DAM에서 자산에 대한 메타데이터 속성을 업데이트할 수도 있으며 변경 사항은 로컬에서 사용할 수 있습니다 [!DNL Sites] 배포.

[!DNL Sites] 작성자는 의 사용 가능한 업데이트를 미리 볼 수 있습니다. [!DNL Sites] 배포 후 변경 사항을 다시 게시하여 [!DNL Experience Manager] 게시 인스턴스.

[!DNL Experience Manager] 의 에셋에 만료된 상태 시각적 표시기를 표시합니다. `Remote Assets Content Finder` 사이트 작성자가에서 에셋을 사용하지 못하도록 하려면 [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다. 만료된 상태의 에셋을 사용하는 경우 [!DNL Sites] 페이지에서 에셋이 [!DNL Experience Manager] 게시 인스턴스.

## 자주 묻는 질문 {#frequently-asked-questions}

+++**에서 사용할 수 있는 자산을 사용해야 하는 경우 연결된 자산을 구성해야 합니까? [!DNL Sites] 배포?**

이 경우 연결된 에셋을 구성할 필요가 없습니다. 에서 사용할 수 있는 자산을 사용할 수 있습니다. [!DNL Sites] 배포.

+++

+++**연결된 자산 기능은 언제 구성해야 합니까?**

의 원격 DAM 배포에서 사용할 수 있는 자산을 사용해야 하는 경우에만 연결된 자산 기능을 구성합니다. [!DNL Sites] 배포.

+++

+++**여러 개를 연결할 수 있습니까 [!DNL Sites] 연결된 자산을 구성한 후 원격 DAM 배포에 배포**

예, 여러 개를 연결할 수 있습니다. [!DNL Sites] 연결된 자산을 구성한 후 원격 DAM 배포에 배포 자세한 내용은 [연결된 자산 아키텍처](#connected-assets-architecture).

+++

+++**몇 개의 원격 DAM 배포에 연결할 수 있는지 [!DNL Sites] 연결된 자산을 구성한 후 배포**

하나의 원격 DAM 배포를 [!DNL Sites] 연결된 자산을 구성한 후 배포합니다. 자세한 내용은 [연결된 자산 아키텍처](#connected-assets-architecture).

+++

+++**에서 Dynamic Media 에셋을 사용할 수 있습니까? [!DNL Sites] 연결된 자산을 구성한 후 배포**

연결된 자산을 구성한 후 [!DNL Dynamic Media] 에셋은에서 사용할 수 있습니다. [!DNL Sites] 읽기 전용 모드로 배포. 따라서 를 사용할 수 없습니다 [!DNL Dynamic Media] 에서 에셋을 처리하려면 [!DNL Sites] 배포. 자세한 내용은 [사이트와 Dynamic Media 배포 간 연결 구성](#dynamic-media-assets).

+++

+++**의 원격 DAM 배포에서 이미지 및 문서 형식 유형의 자산을 사용할 수 있습니까? [!DNL Sites] 연결된 자산을 구성한 후 배포**

예. 의 원격 DAM 배포에서 이미지 및 문서 형식 유형의 자산을 사용할 수 있습니다. [!DNL Sites] 연결된 자산을 구성한 후 배포합니다.

+++

+++**에서 원격 DAM 배포의 콘텐츠 조각 및 비디오 자산을 사용할 수 있습니까? [!DNL Sites] 연결된 자산을 구성한 후 배포**

아니요. 에서는 원격 DAM 배포의 콘텐츠 조각 및 비디오 자산을 사용할 수 없습니다. [!DNL Sites] 연결된 자산을 구성한 후 배포합니다.

+++

+++**의 원격 DAM 배포에서 Dynamic Media 자산을 사용할 수 있습니까? [!DNL Sites] 연결된 자산을 구성한 후 배포**

예. 의 원격 DAM 배포에서 Dynamic Media 이미지 자산을 구성하고 사용할 수 있습니다. [!DNL Sites] 연결된 자산을 구성한 후 배포합니다. 자세한 내용은 [사이트와 Dynamic Media 배포 간 연결 구성](#dynamic-media-assets).

+++

+++**연결된 에셋을 구성한 후 원격 DAM 에셋 또는 폴더에서의 작업을 업데이트하고, 삭제하고, 이름을 바꾸고, 이동할 수 있습니까?**

예. 연결된 에셋을 구성한 후 원격 DAM 에셋 또는 폴더에서의 작업을 업데이트하고, 삭제하고, 이름을 바꾸고, 이동 할 수 있습니다. 업데이트는 약간의 지연과 함께 Sites 배포에서 자동으로 사용할 수 있습니다. 자세한 내용은 [원격 DAM의 자산 업데이트 관리](#handling-updates-to-remote-assets).

+++

+++**연결된 에셋을 구성한 후에에서 에셋을 추가하거나 수정할 수 있습니까? [!DNL Sites] 배포하고 원격 DAM 배포에서 사용할 수 있도록 설정하시겠습니까?**

에셋을에 추가할 수 있습니다. [!DNL Sites] 그러나 이러한 에셋을 원격 DAM 배포에 사용할 수 없습니다.

+++

## 제한 사항 및 우수 사례 {#tip-and-limitations}

* 자산 사용에 대한 통찰력을 얻으려면 다음을 구성하십시오. [Assets Insight](/help/assets/asset-insights.md) 에 대한 기능 [!DNL Sites] 인스턴스.

* 원격 자산을 (으)로 끌 수 없습니다. [이미지 구성 요소 구성 대화 상자](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=en#configure-dialog). 그러나 를 클릭하지 않고 원격 자산을 사이트 페이지의 이미지 구성 요소로 직접 드래그할 수 있습니다. **[!UICONTROL 구성]**.

### 권한 및 자산 관리 {#permissions-and-managing-assets}

* 로컬 자산은 읽기 전용 복사본입니다. [!DNL Experience Manager] 구성 요소는 변경되지 않은 상태로 자산을 유지한 채 편집합니다. 다른 편집 작업은 허용되지 않습니다.
* 로컬로 가져온 자산은 작성용으로만 사용할 수 있습니다. 자산 업데이트 워크플로우를 적용할 수 없고 메타데이터를 편집할 수 없습니다.
* 이미지 및 나열된 문서 형식만 지원됩니다. [!DNL Content Fragments] 및 [!DNL Experience Fragments] 은(는) 지원되지 않습니다.
* [!DNL Experience Manager] 메타데이터 스키마를 가져오지 않습니다. 즉, 가져온 모든 메타데이터가 표시되지 않을 수 있습니다. 스키마가 다음에서 별도로 업데이트되는 경우 [!DNL Sites] 배포하면 모든 메타데이터 속성이 표시됩니다.
* 모두 [!DNL Sites] 작성자는 원격 DAM 배포에 액세스할 수 없는 경우에도 가져온 복사본에 대한 읽기 권한을 갖습니다.
* 통합을 사용자 지정할 수 있는 API 지원이 없습니다.
* 이 기능을 통해 원격 자산을 원활하게 검색하고 사용할 수 있습니다. 로컬 배포에서 많은 원격 자산을 한 번에 사용할 수 있도록 하려면 자산을 마이그레이션하는 것이 좋습니다. [자산 마이그레이션 안내서](assets-migration-guide.md)를 참조하십시오.
* 에서 원격 자산을 페이지 썸네일로 사용할 수 없습니다. [!UICONTROL 페이지 속성] 사용자 인터페이스. 다음 위치에서 웹 페이지의 썸네일을 설정할 수 있습니다. [!UICONTROL 페이지 속성] 의 사용자 인터페이스 [!UICONTROL 축소판] 다음을 클릭: [!UICONTROL 이미지 선택].

### 설정 및 라이선스 {#setup-licensing}

* [!DNL Assets] 배포 대상 [!DNL Adobe Managed Services] 은(는) 지원됩니다.
* [!DNL Sites] 하나에 연결 가능 [!DNL Assets] 한 번에 배포.
* 라이센스 [!DNL Assets] 원격 저장소로 작업해야 합니다.
* 하나 이상의 라이선스 [!DNL Sites] 로컬 작성 배포로 작업해야 합니다.

### 사용 {#usage}

* 작성할 때 원격 자산을 검색하고 로컬 페이지에서 드래그할 수 있습니다. 다른 기능은 지원되지 않습니다.
* 5초 후에 가져오기 작업 시간이 종료됩니다. 네트워크 문제가 있는 경우 작성자가 자산을 가져오는 데 문제가 있을 수 있습니다. 작성자가에서 원격 자산을 드래그하여 재시도할 수 있습니다. [!UICONTROL 콘텐츠 파인더] 끝 [!UICONTROL 페이지 편집기].
*  `Image` 구성 요소를 통해 지원되는 편집과 원본에 영향을 주지 않는 간단한 편집은 가져온 자산에서 수행할 수 있습니다. 자산은 읽기 전용입니다.
* 자산을 다시 가져오는 유일한 방법은 페이지에서 자산을 드래그하는 것입니다. API 지원 또는 업데이트할 에셋을 다시 가져오는 다른 방법은 없습니다.
* 자산이 DAM에서 서비스 해제된 경우에도 계속 사용할 수 있습니다 [!DNL Sites] 페이지.
* 자산의 원격 참조 항목을 비동기식으로 가져옵니다. 참조와 총 횟수는 실시간이 아니며, DAM 사용자가 참조를 조회하는 동안 사이트 작성자가 에셋을 사용하는 경우에는 차이가 있을 수 있습니다. DAM 사용자는 페이지를 새로 고치고 몇 분 후에 다시 시도하여 총 수를 가져올 수 있습니다.

## 문제 해결 {#troubleshoot}

일반적인 오류를 해결하려면 다음 단계를 수행합니다.

* 에서 원격 자산을 검색할 수 없는 경우 [!UICONTROL 콘텐츠 파인더]그런 다음 필요한 역할과 권한이 있는지 확인합니다.

* 하나 이상의 이유로 원격 DAM에서 가져온 자산은 웹 페이지에 게시되지 않을 수 있습니다. 원격 서버에 존재하지 않거나, 가져오기 위한 적절한 권한이 없거나, 네트워크 오류가 원인일 수 있습니다. 원격 DAM에서 자산이 제거되지 않았는지 확인합니다. 적절한 권한이 있고 사전 요구 사항이 충족되는지 확인하십시오. 에셋을 페이지에 다시 추가하고 다시 게시합니다. [비동기 작업 목록](/help/sites-administering/asynchronous-jobs.md)에서 자산 가져오기 오류를 확인합니다.

* 로컬에서 원격 DAM 배포에 액세스할 수 없는 경우 [!DNL Sites] 배포, 사이트 간 쿠키가 허용되는지 확인 및 [동일 사이트 쿠키 지원](/help/sites-administering/same-site-cookie-support.md) 이(가) 구성되었습니다. 사이트 간 쿠키가 다음의 배포를 차단하는 경우 [!DNL Experience Manager] 인증할 수 없습니다. 예를 들어, [!DNL Google Chrome] 시크릿 모드에서 서드파티 쿠키를 차단할 수 있습니다. 에서 쿠키를 허용하려면 [!DNL Chrome] 브라우저에서 주소 표시줄의 &#39;눈&#39; 아이콘을 클릭하고 다음 위치로 이동합니다. **사이트가 작동하지 않음** > **차단됨**&#x200B;를 클릭하고 원격 DAM URL을 선택한 다음 로그인 토큰 쿠키를 허용합니다. 또는 을 참조하십시오. [서드파티 쿠키를 활성화하는 방법](https://support.google.com/chrome/answer/95647).

  ![시크릿 모드의 Chrome 브라우저에서 쿠키 오류 발생](assets/chrome-cookies-incognito-dialog.png)

* Experience Manager Sites as a Cloud Service Sites 배포에서 Managed Services 원격 DAM 배포 Adobe에 액세스할 수 없는 경우 `aem_author.vhost` 파일, 사용 가능한 위치 `"/etc/httpd/conf.d/available_vhosts`, 원격 DAM의 경우 Dispatcher 구성에 다음 헤더를 포함합니다.

  ```xml
  Header Set Access-Control-Allow-Origin <Local Sites instance host>
  Header Set Access-Control-Allow-Credentials true
  ```

* 원격 참조가 검색되지 않고 오류 메시지가 표시되는 경우 다음을 확인하십시오. [!DNL Sites] 배포를 사용할 수 있으며, 네트워크 연결 문제가 있는지 확인합니다. 확인하려면 나중에 다시 시도하십시오. [!DNL Assets] 배포는 와 연결을 설정하려고 두 번 시도합니다. [!DNL Sites] 배포 후 오류를 보고합니다.

  ![자산 원격 참조를 검색하지 못했습니다.](assets/reference-report-failure.png)

* 쿠키가 Sites 서버에서 Google Chrome의 Assets 서버로 전송되지 않으면 Assets 연결이 HTTPS를 통해 전송되지 않기 때문입니다. Assets 인스턴스에서 HTTPS를 사용하지 않는 경우 `SameSite=None` assets 서버로 인증한 후에는 응답에 헤더를 추가할 수 없습니다.

