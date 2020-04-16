---
title: 연결된 자산을 사용하여 Adobe Experience Manager Sites 작성 워크플로우에서 DAM 자산 공유
description: 다른 Experience Manager Site 배포에서 웹 페이지를 만들 때 원격 Adobe Experience Manager Assets 배포에서 사용할 수 있는 자산을 사용합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7628b5edd52a144aa4f92f8145493b9b927aeda0

---


# 연결된 자산을 사용하여 AEM Sites에서 DAM 자산 공유 {#use-connected-assets-to-share-dam-assets-in-aem-sites}

대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 배포할 수 있습니다. 이러한 웹 사이트를 만드는 데 사용되는 웹 사이트 제작 기능과 디지털 자산이 서로 다른 배포에 있을 수 있습니다. 서로 다른 배포에 있는 이유는 모회사가 함께 사용하려는 형식이 다른 인프라로 이어질 수 있는 탠덤 또는 고객 확보 작업에 필요한 기존 배포가 지리적으로 분산되었기 때문일 수 있습니다.

AEM Sites는 웹 페이지를 구축하는 기능을 제공하며, AEM Assets은 웹 사이트에 필요한 자산을 제공하는 디지털 자산 관리(DAM) 시스템입니다. AEM은 AEM Sites 및 AEM Assets를 통합하여 위의 사용 사례를 지원합니다.

## 연결된 자산 개요 {#overview-of-connected-assets}

페이지 편집기에서 페이지를 편집할 때 작성자가 다른 AEM Assets 배포의 자산을 원활하게 검색, 탐색 및 포함할 수 있습니다. AEM 관리자 작업을 수행하려면 AEM Assets의 다른(원격) 배포를 통해 AEM Sites의 로컬 배포에 대한 일회성 통합을 수행합니다.

Sites 작성자의 경우 원격 자산을 읽기 전용 로컬 자산으로 사용할 수 있습니다. 이 기능은 한 번에 여러 개의 원격 자산을 원활하게 검색하고 사용할 수 있도록 지원합니다. 로컬 배포에서 많은 원격 자산을 한 번에 사용할 수 있도록 하려면 자산을 일괄적으로 마이그레이션하는 것이 좋습니다. [자산 마이그레이션 안내서](/help/assets/assets-migration-guide.md)를 참조하십시오.

### 사전 요구 사항 및 지원되는 배포 {#prerequisites}

이 기능을 사용하거나 구성하기 전에 다음을 확인하십시오.

* 사용자 각 배포에 적절한 사용자 그룹에 포함됩니다.
* Adobe Experience Manager 배포 유형이 지원되는 기준 중 하나를 충족합니다. AEM 6.5 자산은 AEM에서 클라우드 서비스로 작동합니다. 자세한 내용은 AEM에서 [클라우드 서비스로 연결된 자산 기능을 참조하십시오](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | 클라우드 서비스로서의 AEM Sites  | AMS의 AEM 6.5 Sites | AEM 6.5 Sites 온-프레미스 |
   |---|---|---|---|
   | **클라우드 서비스로서의 AEM Assets** | 지원됨 | 지원됨 | 지원됨 |
   | **AMS의 AEM 6.5 Assets** | 지원됨 | 지원됨 | 지원됨 |
   | **AEM 6.5 Assets 온프레미스** | 지원되지 않음 | 지원되지 않음 | 지원되지 않음 |

### 지원되는 파일 형식 {#mimetypes}

작성자는 콘텐츠 파인더에서 이미지와 다음 유형의 문서를 검색하고 페이지 편집기에서 검색된 자산을 사용할 수 있습니다. 문서를 `Download` 구성 요소에 추가할 수 있고 이미지를 `Image` 구성 요소에 추가할 수 있습니다. 작성자가 기본 `Download` 또는 `Image` 구성 요소를 확장하는 모든 사용자 지정 AEM 구성 요소에 원격 자산을 추가할 수도 있습니다. 지원되는 형식 목록은 다음과 같습니다.

* **이미지 형식**:이미지 구성 요소에서 지원하는 이미지 [형식은 연결된](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/components/image.html) 자산에서 지원됩니다. Dynamic Media 이미지는 지원되지 않습니다.
* **문서 형식**: [연결된 자산에서 지원하는 문서 형식](assets-formats.md#supported-document-formats)을 참조하십시오.

### 관련 사용자 및 그룹 {#users-and-groups-involved}

기능 및 해당 사용자 그룹을 구성하고 사용하는 데 관련된 여러 가지 역할이 아래에 설명되어 있습니다. 로컬 범위는 작성자가 웹 페이지를 만드는 사용 사례에 사용됩니다. 원격 범위는 필요한 자산을 호스팅하는 DAM 배포에 사용됩니다. 사이트 작성자가 이러한 원격 자산을 가져옵니다.

| 역할 | 범위 | 사용자 그룹 | 연습의 사용자 이름 | 요구 사항 |
|---|---|---|---|---|
| AEM Sites 관리자 | 로컬 | AEM 관리자 | `admin` | AEM을 설정하고 원격 자산 배포와의 통합을 구성합니다. |
| DAM 사용자 | 로컬 | 작성 | `ksaner` | `/content/DAM/connectedassets/`에서 가져온 자산을 보고 복제하는 데 사용됩니다. |
| AEM Sites 작성자 | 로컬 | 작성자(원격 DAM에 대한 읽기 권한과 로컬 사이트에 대한 작성자 권한을 가짐) | `ksaner` | 최종 사용자는 이 통합을 사용하여 콘텐츠 속도를 향상시키는 사이트 작성자입니다. 작성자는 로컬 웹 페이지에서 필요한 이미지를 사용하고 콘텐츠 파인더를 사용하여 원격 DAM에서 자산을 검색하고 찾아봅니다. `ksaner` DAM 사용자의 자격 증명이 사용됩니다. |
| AEM Assets 관리자 | 원격 | AEM 관리자 | 원격 AEM의 `admin` | CORS(원본 간 리소스 공유)를 구성합니다. |
| DAM 사용자 | 원격 | 작성 | 원격 AEM의 `ksaner` | 원격 AEM 배포에서 작성자 역할. 콘텐츠 파인더를 사용하여 연결된 자산에서 자산을 검색하고 찾아봅니다. |
| DAM 배포자(기술 사용자) | 원격 | 패키지 빌더 및 사이트 작성자 | 원격 AEM의 `ksaner` | 원격 배포에 있는 이 사용자 역할은 AEM 로컬 서버(사이트 작성자 역할 아님)에서 사이트 작성자를 대신하여 원격 자산을 가져오는 데 사용됩니다. 이 역할은 위의 두 `ksaner` 역할과 동일하지 않으며 다른 사용자 그룹에 속합니다. |

## 사이트 및 자산 배포 간 연결 구성 {#configure-a-connection-between-sites-and-assets-deployments}

AEM 관리자가 이 통합을 만들 수 있습니다. 통합을 만들면 이 통합을 사용하는 데 필요한 권한이 사이트 배포 및 DAM 배포에 정의된 사용자 그룹을 통해 설정됩니다.

연결된 자산 및 로컬 사이트 연결을 구성하려면 다음 단계를 따르십시오.

1. 기존 AEM Sites 배포에 액세스하거나 다음 명령을 사용하여 배포를 만듭니다.

   1. JAR 파일의 폴더에서 터미널에서 다음 명령을 실행하여 각 AEM 서버를 만듭니다.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 몇 분 후에 AEM 서버가 성공적으로 시작됩니다. 이 AEM Sites 배포를 웹 페이지 작성을 위한 로컬 시스템으로 간주합니다(예: `https://[local_sites]:4502`).

1. 로컬 범위의 사용자 및 역할이 AEM Sites 배포 및 AMS의 AEM Assets 배포에 있는지 확인합니다. 자산 배포에 대한 기술 사용자를 만들고 [관련 사용자 및 그룹](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)에 언급된 사용자 그룹에 추가합니다.

1. `https://[local_sites]:4502`에서 로컬 AEM Sites 배포에 액세스합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 연결된 자산 구성]**&#x200B;을 클릭하고 다음 값을 제공합니다.

   1. AEM Assets 위치는 `https://[assets_servername_ams]:[port]`입니다.
   1. DAM 배포자의 자격 증명(기술 사용자)
   1. **[!UICONTROL 마운트 지점]** 필드에 AEM이 자산을 가져오는 로컬 AEM 경로를 입력합니다. 예를 들면 `remoteassets` 폴더를 입력합니다.
   1. 네트워크에 따라 **[!UICONTROL 원본 이진 전송 최적화 임계값]**&#x200B;의 값을 조정합니다. 이 임계값보다 크기가 큰 자산 렌디션은 비동기적으로 전송됩니다.
   1. 데이터 저장소를 사용하여 자산을 저장하고 데이터 저장소가 두 AEM 배포의 공통 저장소인 경우 **[!UICONTROL 연결된 자산과 공유되는 데이터 저장소]**를 선택합니다. 이 경우 실제 자산 바이너리가 데이터 저장소에 있고 전송되지 않으므로 임계값 제한은 문제가 되지 않습니다.
      ![연결된 자산에 대한 일반적인 구성](assets/connected-assets-typical-config.png)
   *그림: 연결된 자산에 대한 일반적인 구성*

1. 자산이 이미 처리되고 렌디션을 가져올 때 워크플로우 런처를 비활성화합니다. 로컬(AEM Sites) 배포에서 런처 구성을 조정하여 원격 자산을 가져오는 `connectedassets` 폴더를 제외합니다.

   1. AEM Sites 배포에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 런처]**&#x200B;를 클릭합니다.

   1. **[!UICONTROL DAM 자산 업데이트]** 및 **[!UICONTROL DAM 메타데이터 원본에 쓰기]**&#x200B;로 워크플로우를 사용하여 런처를 검색합니다.

   1. 워크플로우 런처를 선택하고 작업 표시줄에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

   1. 속성 마법사에서 **[!UICONTROL 경로]** 필드를 다음 매핑으로 변경하여 마운트 지점 **[!UICONTROL connectedassets]**&#x200B;을 제외하도록 해당 정규식을 업데이트합니다.
   | 이전 | 이후 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >작성자가 자산을 가져올 때 원격 AEM 배포에서 사용할 수 있는 모든 렌디션을 가져옵니다. 가져온 자산의 렌디션을 더 만들려면 이 구성 단계를 건너뜁니다. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. AEM Sites 인스턴스를 원격 AEM Assets의 CORS 구성에서 **[!UICONTROL 허용된 원본]** 중 하나로 추가합니다.

   1. 관리자 자격 증명을 사용하여 로그인합니다. 원본을 서로 검색합니다. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에 액세스합니다.

   1. AEM Sites 인스턴스에 대한 CORS 구성을 만들려면 ![Adobe Granite CORS(원본 간 리소스 공유) 정책](assets/aem_assets_add_icon.png) 옆에 있는 **[!UICONTROL aem_assets_add_icon]** 아이콘을 클릭합니다.

   1. **[!UICONTROL 허용된 원본]** 필드에 로컬 사이트의 URL(`https://[local_sites]:[port]`)을 입력합니다. 구성을 저장합니다.

## 원격 자산 사용 {#use-remote-assets}

웹 사이트 작성자가 콘텐츠 파인더를 사용하여 DAM 인스턴스에 연결합니다. 작성자는 구성 요소에서 원격 자산을 찾아보고 검색하고 드래그할 수 있습니다. 원격 DAM을 인증하려면 관리자가 제공한 DAM 사용자의 자격 증명을 가까이 보관합니다.

작성자는 로컬 DAM 인스턴스와 원격 DAM 인스턴스에서 모두 사용할 수 있는 자산을 단일 웹 페이지에서 사용할 수 있습니다. 콘텐츠 파인더를 사용하여 로컬 DAM을 검색하거나 원격 DAM을 검색합니다.

로컬 사이트 인스턴스에서 사용할 수 있는 동일한 분류 계층과 함께 정확한 해당 태그가 있는 원격 자산의 태그만 가져옵니다. 다른 태그는 모두 무시됩니다. AEM에서 전체 텍스트 검색을 제공하므로 작성자는 원격 AEM 배포에 있는 모든 태그를 사용하여 원격 자산을 검색할 수 있습니다.

### 사용 연습 {#walk-through-of-usage}

위의 설정을 사용하여 작성 환경에서 기능이 어떻게 작동하는지 파악합니다. 원격 DAM 배포 시 원하는 문서 또는 이미지를 사용합니다.

1. AEM 작업 공간에서 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**&#x200B;에 액세스하여 원격 배포의 자산 UI로 이동합니다. 또는 브라우저에서 `https://[assets_servername_ams]:[port]/assets.html/content/dam`에 액세스합니다. 선택한 자산을 업로드합니다.
1. 사이트 인스턴스의 오른쪽 상단 모서리에 있는 프로필 활성자에서 **[!UICONTROL 가장 대상]**&#x200B;을 클릭합니다. `ksaner`를 사용자 이름으로 지정하고 제공된 옵션을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 사이트]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**&#x200B;에서 We.Retail 웹 사이트 페이지를 엽니다. 페이지를 편집합니다. 또는 브라우저에서 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`에 액세스하여 페이지를 편집합니다.

   페이지의 왼쪽 위 모서리에서 **[!UICONTROL 사이드 패널 전환]**&#x200B;을 클릭합니다.

1. 자산 탭을 열고 **[!UICONTROL 연결된 자산에 로그인]**&#x200B;을 클릭합니다.
1. 자격 증명을 제공합니다(사용자 이름: `ksaner`, 암호: `password`). 이 사용자는 두 AEM 배포에 대한 작성 권한이 있습니다.
1. DAM에 추가한 자산을 검색합니다. 원격 자산이 왼쪽 패널에 표시됩니다. 이미지 또는 문서를 필터링하고 지원되는 문서 유형을 추가로 필터링합니다. 이미지를 `Image` 구성 요소로, 문서를 `Download` 구성 요소로 드래그합니다.

   가져온 자산은 로컬 AEM Sites 배포에서 읽기 전용입니다. AEM Sites 구성 요소에서 제공하는 옵션을 사용하여 가져온 자산을 편집할 수도 있습니다. 구성 요소별 편집은 원본에 영향을 주지 않습니다.

   ![원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션](assets/filetypes_filter_connected_assets.png)

   *그림: 원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션*

1. 자산을 비동기적으로 가져오는 경우 및 가져오기 작업이 실패할 경우 사이트 작성자에게 알립니다. 작성자는 작성 중이나 작성 후에도 [비동기 작업](/help/assets/asynchronous-jobs.md) 사용자 인터페이스에서 가져오기 작업 및 오류에 대한 자세한 정보를 볼 수 있습니다.

   ![백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.](assets/assets_async_transfer_fails.png)

   *그림: 백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림*

1. 페이지를 게시할 때 AEM은 페이지에 사용된 자산의 전체 목록을 표시합니다. 게시할 때 원격 자산을 성공적으로 가져오는지 확인합니다. 가져온 각 자산의 상태를 확인하려면 [비동기 작업](/help/assets/asynchronous-jobs.md) 사용자 인터페이스를 참조하십시오.

   >[!NOTE]
   >
   >하나 이상의 원격 자산을 가져오지 않더라도 페이지가 게시됩니다. 원격 자산을 사용하는 구성 요소가 빈 채로 게시됩니다. AEM 알림 영역에는 비동기 작업 페이지에 표시되는 오류에 대한 알림이 표시됩니다.

>[!CAUTION]
>
>가져온 원격 자산은 웹 페이지에서 사용한 경우 가져온 자산이 저장된 로컬 폴더에 액세스할 권한이 있는 모든 사람이 검색하고 사용할 수 있습니다(위의 연습에서 `connectedassets`). 또한 자산은 [!UICONTROL 콘텐츠 파인더]를 통해 로컬 저장소에서 검색하고 볼 수 있습니다.

가져온 자산은 연결된 메타데이터를 편집할 수 없다는 점을 제외하고 다른 로컬 자산으로 사용할 수 있습니다.

## 제한 사항 {#limitations}

**권한 및 자산 관리**

* 로컬 자산은 원격 배포의 원본 자산과 동기화되지 않습니다. DAM 배포에 대한 권한 편집, 삭제 또는 취소는 다운스트림으로 전파되지 않습니다.
* 로컬 자산은 읽기 전용 복사본입니다. AEM 구성 요소는 변경되지 않은 상태로 자산을 유지한 채 편집합니다. 다른 편집 작업은 허용되지 않습니다.
* 로컬로 가져온 자산은 작성용으로만 사용할 수 있습니다. 자산 업데이트 워크플로우를 적용할 수 없고 메타데이터를 편집할 수 없습니다.
* 이미지 및 나열된 문서 형식만 지원됩니다. Dynamic Media 자산, 콘텐츠 조각 및 경험 구성요소는 지원되지 않습니다.
* 메타데이터 스키마를 가져오지 않았습니다.
* 모든 사이트 작성자는 원격 DAM 배포에 액세스할 권한이 없어도 가져온 복사본에 대한 읽기 권한을 갖습니다.
* 통합을 사용자 지정할 수 있는 API 지원이 없습니다.
* 이 기능을 통해 원격 자산을 원활하게 검색하고 사용할 수 있습니다. 로컬 배포에서 많은 원격 자산을 한 번에 사용할 수 있도록 하려면 자산을 마이그레이션하는 것이 좋습니다. [자산 마이그레이션 안내서](assets-migration-guide.md)를 참조하십시오.
* 페이지 속성 사용자 인터페이스에서 원격 자산을 페이지 축소판으로 사용할 [!UICONTROL 수] 없습니다. 이미지 선택을 클릭하여 페이지 속성 [!UICONTROL 사용자 인터페이스에서] 웹 페이지의 축소판을 설정할 [!UICONTROL 수] 있습니다.

**설정 및 라이선스**

* AMS에서의 AEM Assets 배포가 지원됩니다.
* AEM Sites에서 한 번에 하나의 AEM Assets 저장소에 연결할 수 있습니다.
* 원격 저장소로 작동하는 AEM Assets의 라이선스.
* 로컬 작성 배포로 작동하는 AEM Sites에 대한 한 개 이상의 라이선스.

**사용량**

* 로컬 페이지에서 원격 자산을 검색하고 원격 자산을 작성자 콘텐츠로 드래그하는 기능만 지원됩니다.
* 5초 후에 가져오기 작업 시간이 종료됩니다. 네트워크 문제가 있는 경우 작성자가 자산을 가져오는 데 문제가 있을 수 있습니다. 작성자가 [!UICONTROL 콘텐츠 파인더]에서 [!UICONTROL 페이지 편집기]로 원격 자산을 드래그하여 다시 시도할 수 있습니다.
* AEM `Image` 구성 요소를 통해 지원되는 편집과 원본에 영향을 주지 않는 간단한 편집은 가져온 자산에서 수행할 수 있습니다. 자산은 읽기 전용입니다.

## 문제 해결 {#troubleshoot}

일반적인 오류 시나리오에 대한 문제를 해결하려면 다음 단계를 따르십시오.

* 콘텐츠 파인더에서 원격 자산을 검색할 수 없는 경우 다시 확인하고 필요한 역할과 권한이 있는지 확인합니다.
* 원격 사이트에 존재하지 않거나, 가져오기 위한 적절한 권한이 없거나, 네트워크 오류로 인해 원격 DAM에서 가져온 자산은 웹 페이지에 게시되지 않을 수 있습니다. 원격 DAM에서 자산이 제거되지 않았거나 권한이 변경되지 않았는지, 적절한 사전 요구 사항을 충족하는지 확인하고 자산을 페이지에 추가해 본 다음 다시 게시합니다. [비동기 작업 목록](/help/assets/asynchronous-jobs.md)에서 자산 가져오기 오류를 확인합니다.
