---
title: 연결된 자산을 사용하여 [!DNL Sites]에서 DAM 자산 공유
description: 원격 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 배포에서 사용할 수 있는 자산을 사용합니다.
contentOwner: AG
role: Business Practitioner, Administrator, Leader
feature: 연결된 자산, 사용자 및 그룹
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
source-git-commit: c07467feb96c25a4bac1916f88f04fdb37979ee1
workflow-type: tm+mt
source-wordcount: '2739'
ht-degree: 29%

---

# 연결된 자산을 사용하여 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}에서 DAM 자산 공유

대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 배포할 수 있습니다. 이러한 웹 사이트를 만드는 데 사용되는 웹 사이트 제작 기능과 디지털 자산이 서로 다른 배포에 있을 수 있습니다. 한 가지 이유는 함께 작업하는 데 필요한 기존 배포를 지리적으로 배포할 수 있습니다. 또 다른 이유는 모회사가 함께 사용하려는 이기종 인프라를 인수하는 것입니다.

사용자는 [!DNL Experience Manager Sites]에서 웹 페이지를 만들 수 있습니다. [!DNL Experience Manager Assets] 는 웹 사이트에 필요한 자산을 제공하는 DAM(디지털 자산 관리) 시스템입니다. [!DNL Experience Manager]는 이제 [!DNL Sites] 및 [!DNL Assets]을 통합하여 위의 사용 사례를 지원합니다. 

## 연결된 자산 개요 {#overview-of-connected-assets}

[!UICONTROL 페이지 편집기]의 페이지를 대상 대상으로 편집할 때 작성자는 자산의 소스 역할을 하는 다른 [!DNL Assets] 배포의 자산을 원활하게 검색, 탐색 및 포함할 수 있습니다. 관리자는 [!DNL Sites] 기능이 [!DNL Assets] 기능이 있는 [!DNL Experience Manager] 의 다른 배포와 함께 [!DNL Experience Manager] 배포의 일회성 통합을 만듭니다.

[!DNL Sites] 작성자의 경우 원격 자산을 읽기 전용 로컬 자산으로 사용할 수 있습니다. 이 기능은 한 번에 여러 개의 원격 자산을 원활하게 검색하고 사용할 수 있도록 지원합니다. 한 번에 [!DNL Sites] 배포에서 많은 원격 자산을 사용할 수 있도록 하려면 자산을 일괄적으로 마이그레이션하는 것이 좋습니다. [Experience Manager 자산 마이그레이션 안내서](/help/assets/assets-migration-guide.md)를 참조하십시오.

### 사전 요구 사항 및 지원되는 배포 {#prerequisites}

이 기능을 사용하거나 구성하기 전에 다음을 확인하십시오.

* 사용자는 각 배포에 적절한 사용자 그룹의 일부입니다.
* [!DNL Adobe Experience Manager] 배포 유형의 경우 지원되는 기준 중 하나가 충족됩니다. [!DNL Experience Manager] 6.5 [!DNL Assets] 는 Cloud Service [!DNL Experience Manager] 로 작동합니다. 이 기능이 [!DNL Experience Manager]에서 [!DNL Cloud Service]로 작동하는 방법에 대한 자세한 내용은 [에 연결된 자산 [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)을 참조하십시오. [!DNL Experience Manager] 

   |  | [!DNL Sites]로서의 [!DNL Cloud Service]  | [!DNL Experience Manager] AMS [!DNL Sites] 의 6.5 | [!DNL Experience Manager] 6.5  [!DNL Sites] 온-프레미스 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]로서의[!DNL Cloud Service]**  | 지원됨 | 지원됨 | 지원됨 |
   | **[!DNL Experience Manager]AMS [!DNL Assets] 의 6.5** | 지원됨 | 지원됨 | 지원됨 |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] 온-프레미스** | 지원되지 않음 | 지원되지 않음 | 지원되지 않음 |

### 지원되는 파일 형식 {#mimetypes}

작성자는 콘텐츠 파인더에서 이미지와 다음 유형의 문서를 검색하고 페이지 편집기에서 검색된 자산을 사용합니다. 문서가 `Download` 구성 요소에 추가되고 이미지가 `Image` 구성 요소에 추가됩니다. 작성자는 기본 `Download` 또는 `Image` 구성 요소를 확장하는 모든 사용자 지정 [!DNL Experience Manager] 구성 요소에 원격 자산을 추가합니다. 지원되는 형식은 다음과 같습니다.

* **이미지 형식**:이미지 구성 요소 [가 지원하는 ](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html) 형식입니다. [!DNL Dynamic Media] 이미지는 지원되지 않습니다.
* **문서 형식**:지원되는  [문서 형식을 참조하십시오](assets-formats.md#supported-document-formats).

### 관련 사용자 및 그룹 {#users-and-groups-involved}

기능 및 해당 사용자 그룹을 구성하고 사용하는 데 관련된 여러 가지 역할이 아래에 설명되어 있습니다. 로컬 범위는 작성자가 웹 페이지를 만드는 사용 사례에 사용됩니다. 원격 범위는 필요한 자산을 호스팅하는 DAM 배포에 사용됩니다. [!DNL Sites] 작성자가 이러한 원격 자산을 가져옵니다.

| 역할 | 범위 | 사용자 그룹 | 연습의 사용자 이름 | 요구 사항 |
|---|---|---|---|---|
| [!DNL Sites] administrator | 로컬 | [!DNL Experience Manager] `administrators` | `admin` | [!DNL Experience Manager]을 설정하고 원격 [!DNL Assets] 배포와의 통합을 구성합니다. |
| DAM 사용자 | 로컬 | `Authors` | `ksaner` | `/content/DAM/connectedassets/`에서 가져온 자산을 보고 복제하는 데 사용됩니다. |
| [!DNL Sites] 작성자 | 로컬 | <ul><li>`Authors` (원격 DAM에 대한 읽기 권한과 로컬 [!DNL Sites]에 대한 작성자 액세스 사용) </li> <li>`dam-users` 로컬  [!DNL Sites]</li></ul> | `ksaner` | 최종 사용자는 이 통합을 사용하여 컨텐츠 속도를 향상시키는 [!DNL Sites] 작성자입니다. 작성자는 로컬 웹 페이지에서 필요한 이미지를 사용하여 [!UICONTROL 컨텐츠 파인더]를 사용하여 원격 DAM에서 자산을 검색하고 찾아봅니다. `ksaner` DAM 사용자의 자격 증명이 사용됩니다. |
| [!DNL Assets] 관리자 | 원격 | [!DNL Experience Manager] `administrators` | `admin` 원격  [!DNL Experience Manager] | CORS(원본 간 리소스 공유)를 구성합니다. |
| DAM 사용자 | 원격 | `Authors` | `ksaner` 원격  [!DNL Experience Manager] | 원격 [!DNL Experience Manager] 배포에서 작성자 역할. [!UICONTROL 컨텐츠 파인더]를 사용하여 연결된 자산에서 자산을 검색하고 찾아봅니다. |
| DAM 배포자(기술 사용자) | 원격 | [!DNL Sites] `Authors` | `ksaner` 원격  [!DNL Experience Manager] | 원격 배포에 있는 이 사용자 역할은 [!DNL Sites] 작성자 역할이 아닌 [!DNL Experience Manager] 로컬 서버에서 [!DNL Sites] 작성자를 대신하여 원격 자산을 가져오는 데 사용됩니다. 이 역할은 위의 두 `ksaner` 역할과 동일하지 않으며 다른 사용자 그룹에 속합니다. |

## [!DNL Sites] 및 [!DNL Assets] 배포 {#configure-a-connection-between-sites-and-assets-deployments} 간의 연결을 구성합니다

[!DNL Experience Manager] 관리자가 이 통합을 만들 수 있습니다. 만들고 나면 사용자 그룹을 통해 사용 권한이 설정됩니다. 사용자 그룹은 [!DNL Sites] 배포 및 DAM 배포에 정의됩니다.

연결된 자산 및 로컬 [!DNL Sites] 연결을 구성하려면 다음 단계를 수행합니다.

1. 기존 [!DNL Sites] 배포에 액세스하거나 다음 명령을 사용하여 배포를 만듭니다.

   1. JAR 파일의 폴더에서 터미널에서 다음 명령을 실행하여 각 [!DNL Experience Manager] 서버를 만듭니다.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 몇 분 후에 [!DNL Experience Manager] 서버가 성공적으로 시작됩니다. 이 [!DNL Sites] 배포를 웹 페이지 작성을 위한 로컬 시스템으로 간주합니다(예: `https://[local_sites]:4502`).

1. 적절한 범위의 사용자 및 역할이 [!DNL Sites] 배포 및 AMS의 [!DNL Assets] 배포에 있는지 확인합니다. [!DNL Assets] 배포에서 기술 사용자를 만들고 [에 언급된 사용자 그룹](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)에 추가합니다.

1. `https://[local_sites]:4502`에서 로컬 [!DNL Sites] 배포에 액세스합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 연결된 자산 구성]**&#x200B;을 클릭하고 다음 값을 제공합니다.

   1. 구성의 **[!UICONTROL 제목]**&#x200B;입니다.
   1. **[!UICONTROL 원격 DAM]** URL은 형식의  [!DNL Assets] 위치 URL입니다 `https://[assets_servername]:[port]`.
   1. DAM 배포자의 자격 증명(기술 사용자)
   1. **[!UICONTROL 마운트 지점]** 필드에 자산을 가져오는 로컬 [!DNL Experience Manager] 경로를 입력합니다. [!DNL Experience Manager] 예를 들면 `remoteassets` 폴더를 입력합니다. DAM에서 가져온 자산은 [!DNL Sites] 배포의 이 폴더에 저장됩니다.
   1. **[!UICONTROL 로컬 사이트]** URL은 배포의  [!DNL Sites] 위치입니다. [!DNL Assets] 배포에서는 이 값을 사용하여 이 배포로 가져온 디지털 자산에 대한 참조를  [!DNL Sites] 유지합니다.
   1. [!DNL Sites] 기술 사용자의 자격 증명입니다.
   1. **[!UICONTROL 원본 이진 전송 최적화 임계값]** 필드의 값은 원본 자산(표현물 포함)이 동기적으로 전송되는지 여부를 지정합니다. 파일 크기가 작은 자산을 쉽게 가져올 수 있지만 파일 크기가 상대적으로 큰 자산은 비동기식으로 가장 잘 동기화됩니다. 값은 네트워크 기능에 따라 다릅니다.
   1. 데이터 저장소를 사용하여 자산을 저장하고 데이터 저장소가 두 배포의 공통 저장소인 경우 **[!UICONTROL 연결된 자산과 공유되는 데이터 저장소]**&#x200B;를 선택합니다. 이 경우 실제 자산 바이너리를 데이터 저장소에서 사용할 수 있고 전송되지 않으므로 임계값 제한은 문제가 되지 않습니다.

   ![연결된 자산 기능에 대한 일반적인 구성](assets/connected-assets-typical-config.png)

   *그림:연결된 자산 기능에 대한 일반적인 구성.*

1. [!DNL Assets] 배포의 기존 디지털 자산이 이미 처리되고 표현물이 생성됩니다. 이러한 표현물은 이 기능을 사용하여 가져오므로 표현물을 다시 생성할 필요가 없습니다. 표현물의 재생성을 방지하기 위해 워크플로우 런처를 비활성화합니다. ([!DNL Sites]) 배포에서 런처 구성을 조정하여 `connectedassets` 폴더를 제외합니다(이 폴더에서 자산을 가져옵니다).

   1. [!DNL Sites] 배포에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 런처]**&#x200B;를 클릭합니다.

   1. **[!UICONTROL DAM 자산 업데이트]** 및 **[!UICONTROL DAM 메타데이터 원본에 쓰기]**&#x200B;로 워크플로우를 사용하여 런처를 검색합니다.

   1. 워크플로우 런처를 선택하고 작업 표시줄에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

   1. [!UICONTROL 속성] 마법사에서 **[!UICONTROL 경로]** 필드를 다음 매핑으로 변경하여 마운트 지점 **[!UICONTROL connectedassets]**&#x200B;을 제외하도록 해당 정규식을 업데이트합니다.

   | 이전 | 이후 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >작성자가 자산을 가져올 때 원격 배포에서 사용할 수 있는 모든 렌디션을 가져옵니다. 가져온 자산의 렌디션을 더 만들려면 이 구성 단계를 건너뜁니다. [!UICONTROL DAM 자산 업데이트] 워크플로우가 트리거되어 더 많은 렌디션을 만듭니다. 이러한 렌디션은 로컬 [!DNL Sites] 배포에서만 사용할 수 있으며 원격 DAM 배포에서는 사용할 수 없습니다.

1. [!DNL Sites] 배포를 [!DNL Assets] 배포의 CORS 구성에서 허용된 원본으로 추가합니다. 자세한 내용은 [CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html) 이해 를 참조하십시오.

1. [동일한 사이트 쿠키 지원을 구성합니다](/help/sites-administering/same-site-cookie-support.md).

구성된 [!DNL Sites] 배포와 [!DNL Assets] 배포 간의 연결을 확인할 수 있습니다.

![구성된 연결된 자산에 대한 연결 테스트  [!DNL Sites]](assets/connected-assets-multiple-config.png)
*그림:구성된 연결된 자산에 대한 연결 테스트  [!DNL Sites].*

## 원격 자산 사용 {#use-remote-assets}

웹 사이트 작성자가 콘텐츠 파인더를 사용하여 DAM 배포에 연결합니다. 작성자는 구성 요소에서 원격 자산을 찾아보고 검색하고 드래그할 수 있습니다. 원격 DAM을 인증하려면 관리자가 제공한 DAM 사용자의 자격 증명을 가까이 보관합니다.

작성자는 로컬 DAM과 원격 DAM 배포에서 사용할 수 있는 자산을 단일 웹 페이지에서 사용할 수 있습니다. 콘텐츠 파인더를 사용하여 로컬 DAM을 검색하거나 원격 DAM을 검색합니다.

로컬 [!DNL Sites] 배포에서 사용할 수 있는 동일한 분류 계층 구조와 함께 정확한 해당 태그가 있는 원격 자산 태그만 가져옵니다. 다른 태그는 모두 무시됩니다. 작성자는 전체 텍스트 검색을 제공하므로 원격 [!DNL Experience Manager] 배포에 있는 모든 태그를 사용하여 원격 자산을 검색할 수 있습니다.

### 사용 연습 {#walk-through-of-usage}

위의 설정을 사용하여 작성 환경에서 기능이 어떻게 작동하는지 파악합니다. 원격 DAM 배포 시 원하는 문서 또는 이미지를 사용합니다.

1. [!DNL Experience Manager] 작업 영역에서 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**&#x200B;에 액세스하여 원격 배포의 [!DNL Assets] 인터페이스로 이동합니다. 또는 브라우저에서 `https://[assets_servername_ams]:[port]/assets.html/content/dam`에 액세스합니다. 선택한 자산을 업로드합니다.
1. [!DNL Sites] 배포의 오른쪽 위 모서리에 있는 프로필 활성자에서 **[!UICONTROL 가장 대상]**&#x200B;을 클릭합니다. `ksaner`를 사용자 이름으로 지정하고 제공된 옵션을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 사이트]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**&#x200B;에서 We.Retail 웹 사이트 페이지를 엽니다. 페이지를 편집합니다. 또는 브라우저에서 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`에 액세스하여 페이지를 편집합니다.

   페이지의 왼쪽 위 모서리에서 **[!UICONTROL 사이드 패널 전환]**&#x200B;을 클릭합니다.

1. [!UICONTROL Assets] 탭을 열고 **[!UICONTROL 연결된 자산에 로그인]**&#x200B;을 클릭합니다.
1. 자격 증명을 제공합니다(사용자 이름: `ksaner`, 암호: `password`). 이 사용자는 두 [!DNL Experience Manager] 배포에 대한 작성 권한이 있습니다.
1. DAM에 추가한 자산을 검색합니다. 원격 자산이 왼쪽 패널에 표시됩니다. 이미지 또는 문서를 필터링하고 지원되는 문서 유형을 추가로 필터링합니다. 이미지를 `Image` 구성 요소로, 문서를 `Download` 구성 요소로 드래그합니다.

   가져온 자산은 로컬 [!DNL Sites] 배포에서 읽기 전용입니다. [!DNL Sites] 구성 요소에서 제공하는 옵션을 사용하여 가져온 자산을 편집할 수도 있습니다. 구성 요소별 편집은 원본에 영향을 주지 않습니다.

   ![원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션](assets/filetypes_filter_connected_assets.png)

   *그림: 원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션.*

1. 자산을 비동기적으로 가져오는 경우 및 가져오기 작업이 실패할 경우 사이트 작성자에게 알립니다. 작성자는 작성 중이나 작성 후에도 [비동기 작업](/help/sites-administering/asynchronous-jobs.md) 사용자 인터페이스에서 가져오기 작업 및 오류에 대한 자세한 정보를 볼 수 있습니다.

   ![백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.](assets/assets_async_transfer_fails.png)

   *그림: 백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.*

1. 페이지를 게시할 때 [!DNL Experience Manager]은 페이지에 사용된 자산의 전체 목록을 표시합니다. 게시할 때 원격 자산을 성공적으로 가져오는지 확인합니다. 가져온 각 자산의 상태를 확인하려면 [비동기 작업](/help/sites-administering/asynchronous-jobs.md) 사용자 인터페이스를 참조하십시오.

   >[!NOTE]
   >
   >하나 이상의 원격 자산을 가져오지 않더라도 페이지가 게시됩니다. 원격 자산을 사용하는 구성 요소가 빈 채로 게시됩니다. [!DNL Experience Manager] 알림 영역에는 비동기 작업 페이지에 표시되는 오류에 대한 알림이 표시됩니다.

>[!CAUTION]
>
>가져온 원격 자산은 웹 페이지에서 사용한 경우 로컬 폴더에 액세스할 권한이 있는 모든 사람이 검색하고 사용할 수 있습니다. 가져온 자산은 로컬 폴더(`connectedassets` 위의 연습에서 )에 저장됩니다. 또한 자산은 [!UICONTROL 콘텐츠 파인더]를 통해 로컬 저장소에서 검색하고 볼 수 있습니다.

가져온 자산은 연결된 메타데이터를 편집할 수 없다는 점을 제외하고 다른 로컬 자산으로 사용할 수 있습니다.

### 웹 페이지에서 자산 사용 확인 {#asset-usage-references}

[!DNL Experience Manager] DAM 사용자가 자산에 대한 모든 참조를 확인할 수 있도록 해줍니다. 원격 [!DNL Sites] 및 복합 자산에 있는 자산의 사용을 이해하고 관리하는 데 도움이 됩니다. [!DNL Experience Manager Sites] 배포의 웹 페이지의 많은 작성자가 다른 웹 페이지의 원격 [!DNL Assets]에 있는 자산을 사용할 수 있습니다. 자산 관리를 단순화하고 끊어진 참조를 시작하지 않으려면 DAM 사용자가 로컬 및 원격 웹 페이지에서 자산의 사용을 확인하는 것이 중요합니다. 자산의 [!UICONTROL 속성] 페이지에 있는 [!UICONTROL 참조] 탭에는 자산의 로컬 및 원격 참조가 나열됩니다.

[!DNL Assets] 배포에서 참조를 보고 관리하려면 다음 단계를 수행합니다.

1. [!DNL Assets] 콘솔에서 자산을 선택하고 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 참조]** 탭을 클릭합니다. [!DNL Assets] 배포에서 자산을 사용하려면 **[!UICONTROL 로컬 참조]** 를 참조하십시오. 연결된 자산 기능을 사용하여 자산을 가져온 [!DNL Sites] 배포에서 자산을 사용하려면 **[!UICONTROL 원격 참조]을 참조하십시오.

   ![자산 속성 페이지의 원격 참조](assets/connected-assets-remote-reference.png)

1. [!DNL Sites] 페이지에 대한 참조는 각 로컬 [!DNL Sites]에 대한 총 참조 수를 표시합니다. 모든 참조를 찾고 총 참조 수를 표시하는 데 시간이 걸릴 수 있습니다.
1. 참조 목록은 대화형 이며 DAM 사용자는 참조를 클릭하여 참조 페이지를 열 수 있습니다. 어떤 이유로 원격 참조를 가져올 수 없는 경우 사용자에게 실패를 알리는 알림이 표시됩니다.
1. 사용자는 자산을 이동하거나 삭제할 수 있습니다. 자산을 이동하거나 삭제할 때 선택한 모든 자산/폴더의 총 참조 수가 경고 대화 상자에 표시됩니다. 참조가 아직 표시되지 않은 자산을 삭제하면 경고 대화 상자가 표시됩니다.

   ![강제 삭제 경고](assets/delete-referenced-asset.png)

## 제한 사항 및 우수 사례 {#tip-and-limitations}

* 자산 사용에 대한 통찰력을 얻으려면 [!DNL Sites] 인스턴스에서 [Assets Insight](/help/assets/asset-insights.md) 기능을 구성하십시오.

### 권한 및 자산 관리 {#permissions-and-managing-assets}

* 로컬 자산은 원격 배포의 원본 자산과 동기화되지 않습니다. DAM 배포에 대한 권한 편집, 삭제 또는 취소는 다운스트림으로 전파되지 않습니다.
* 로컬 자산은 읽기 전용 복사본입니다. [!DNL Experience Manager] 구성 요소는 변경되지 않은 상태로 자산을 유지한 채 편집합니다. 다른 편집 작업은 허용되지 않습니다.
* 로컬로 가져온 자산은 작성용으로만 사용할 수 있습니다. 자산 업데이트 워크플로우를 적용할 수 없고 메타데이터를 편집할 수 없습니다.
* 이미지 및 나열된 문서 형식만 지원됩니다. [!DNL Dynamic Media] 자산, 콘텐츠 조각 및 경험 구성요소는 지원되지 않습니다.
* [!DNL Experience Manager] 메타데이터 스키마를 가져오지 않습니다. 가져온 모든 메타데이터가 표시되지 않을 수 있음을 의미합니다. 스키마를 별도로 업데이트하면 모든 속성이 표시됩니다.
* 작성자가 원격 DAM 배포에 액세스할 수 없는 경우에도 모든 [!DNL Sites] 작성자는 가져온 복사본에 대한 읽기 권한을 갖습니다.
* 통합을 사용자 지정할 수 있는 API 지원이 없습니다.
* 이 기능을 통해 원격 자산을 원활하게 검색하고 사용할 수 있습니다. 로컬 배포에서 많은 원격 자산을 한 번에 사용할 수 있도록 하려면 자산을 마이그레이션하는 것이 좋습니다. [자산 마이그레이션 안내서](assets-migration-guide.md)를 참조하십시오.
* 원격 자산을 [!UICONTROL 페이지 속성] 사용자 인터페이스에서 페이지 축소판으로 사용할 수 없습니다. [!UICONTROL 이미지 선택]을 클릭하여 [!UICONTROL 페이지 속성] 사용자 인터페이스의 [!UICONTROL 축소판]에서 웹 페이지의 축소판을 설정할 수 있습니다.

### 설정 및 라이선스 {#setup-licensing}

* [!DNL Assets] 배포 [!DNL Adobe Managed Services] 가 지원됩니다.
* [!DNL Sites] 한 번에 하나의 저장소 [!DNL Assets] 에 연결할 수 있습니다.
* 원격 저장소로 작동하는 [!DNL Assets] 라이선스.
* 로컬 작성 배포로 작동하는 [!DNL Sites] 의 하나 이상의 라이선스.

### 사용량 {#usage}

* 사용자는 원격 자산을 검색하고 작성할 때 로컬 페이지에서 드래그할 수 있습니다. 다른 기능은 지원되지 않습니다.
* 5초 후에 가져오기 작업 시간이 종료됩니다. 네트워크 문제가 있는 경우 작성자가 자산을 가져오는 데 문제가 있을 수 있습니다. 작성자가 원격 자산을 [!UICONTROL 콘텐츠 파인더]에서 [!UICONTROL 페이지 편집기]로 드래그하여 다시 시도할 수 있습니다.
*  `Image` 구성 요소를 통해 지원되는 편집과 원본에 영향을 주지 않는 간단한 편집은 가져온 자산에서 수행할 수 있습니다. 자산은 읽기 전용입니다.
* 자산을 다시 가져오는 유일한 방법은 페이지에서 자산을 드래그하는 것입니다. 자산을 업데이트하기 위해 자산을 다시 가져오는 API 지원 또는 다른 방법이 없습니다.
* DAM에서 자산이 폐기된 경우 자산은 [!DNL Sites] 페이지에서 계속 사용됩니다.
* 자산의 원격 참조 항목을 비동기식으로 가져옵니다. DAM 사용자가 참조를 보는 동안 사이트 작성자가 자산을 사용하는 경우 참조 및 총 카운트가 실시간이 아니며 약간의 차이가 있을 수 있습니다. DAM 사용자는 페이지를 새로 고치고 몇 분 후에 다시 시도하여 총 개수를 가져올 수 있습니다.

## 문제 해결 {#troubleshoot}

일반적인 오류를 해결하려면 다음 단계를 수행합니다.

* [!UICONTROL 컨텐츠 파인더]에서 원격 자산을 검색할 수 없는 경우, 필요한 역할과 권한이 있는지 확인합니다.

* 원격 DAM에서 가져온 자산은 하나 이상의 이유로 웹 페이지에 게시되지 않을 수 있습니다. 원격 서버에 존재하지 않거나, 가져오기 위한 적절한 권한이 없거나, 네트워크 오류로 인해 발생할 수 있습니다. 원격 DAM에서 자산이 제거되지 않았는지 확인합니다. 적절한 권한이 있고 전제 조건이 충족되는지 확인하십시오. 페이지에 자산 추가를 다시 시도하고 다시 게시합니다. [비동기 작업 목록](/help/sites-administering/asynchronous-jobs.md)에서 자산 가져오기 오류를 확인합니다.

* 로컬 [!DNL Sites] 배포에서 원격 DAM 배포에 액세스할 수 없는 경우 사이트 간 쿠키가 허용되고 [동일한 사이트 쿠키 지원](/help/sites-administering/same-site-cookie-support.md)이 구성되어 있는지 확인하십시오. 사이트 간 쿠키가 차단되면 [!DNL Experience Manager] 배포가 인증되지 않을 수 있습니다. 예를 들어, Incognito 모드의 [!DNL Google Chrome]은 타사 쿠키를 차단할 수 있습니다. [!DNL Chrome] 브라우저에서 쿠키를 허용하려면 주소 표시줄에서 &#39;eye&#39; 아이콘을 클릭하고 **사이트가 작동하지 않음** > **차단됨**&#x200B;으로 이동한 다음 원격 DAM URL을 선택하고 로그인 토큰 쿠키를 허용합니다. 또는 [타사 쿠키를 활성화하는 방법](https://support.google.com/chrome/answer/95647)을 참조하십시오.

   ![Incognito 모드의 Chrome 브라우저에서 쿠키 오류](assets/chrome-cookies-incognito-dialog.png)

* 원격 참조가 검색되지 않고 오류 메시지가 표시되는 경우 [!DNL Sites] 배포를 사용할 수 있는지 확인하고 네트워크 연결 문제를 확인합니다. 나중에 다시 시도하여 확인합니다. [!DNL Assets] 배포는 배포에 대한 연결을 두 번  [!DNL Sites] 시도한 다음 오류를 보고합니다.

   ![자산 원격 참조를 검색하지 못했습니다.](assets/reference-report-failure.png)
