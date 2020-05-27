---
title: Use Connected Assets to share DAM assets in [!DNL Adobe Experience Manager Sites] authoring workflow.
description: 원격 배포에서 사용할 수 있는 자산을 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 사용합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 50%

---


# Use Connected Assets to share DAM assets in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 배포할 수 있습니다. 이러한 웹 사이트를 만드는 데 사용되는 웹 사이트 제작 기능과 디지털 자산이 서로 다른 배포에 있을 수 있습니다. 동시에 작업하는 데 필요한 기존 배포가 지리적으로 분산되어 있는 이유 중 하나가 있습니다. 또 다른 이유는 모회사가 함께 사용하고자 하는 이기종 인프라를 유도하기 위한 인수입니다.

사용자는 웹 페이지를 만들 수 있습니다 [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] 는 웹 사이트에 필요한 자산을 제공하는 디지털 자산 관리(DAM) 시스템입니다. [!DNL Experience Manager]는 이제 [!DNL Sites] 및 [!DNL Assets]을 통합하여 위의 사용 사례를 지원합니다. 

## 연결된 자산 개요 {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. 관리자는 배포의 다른(원격) [!DNL Sites] 배포를 한 번만 통합합니다 [!DNL Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. 이 기능은 한 번에 여러 개의 원격 자산을 원활하게 검색하고 사용할 수 있도록 지원합니다. To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk. Experience [Manager 자산 마이그레이션 가이드를 참조하십시오](/help/assets/assets-migration-guide.md).

### 사전 요구 사항 및 지원되는 배포 {#prerequisites}

이 기능을 사용하거나 구성하기 전에 다음을 확인하십시오.

* 사용자 각 배포에 적절한 사용자 그룹에 포함됩니다.
* Adobe Experience Manager 배포 유형의 경우 지원되는 기준 중 하나가 충족됩니다. [!DNL Experience Manager] 6.5 [!DNL Assets] 는 클라우드 서비스 [!DNL Experience Manager] 로 작동합니다. 자세한 내용은 Experience Manager [의 클라우드 서비스로 연결된 자산 기능을 참조하십시오](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] 클라우드 서비스로 | [!DNL Experience Manager] 6.5 [!DNL Sites] AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] 온-프레미스 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]클라우드 서비스로&#x200B;** | 지원됨 | 지원됨 | 지원됨 |
   | **[!DNL Experience Manager]6.5[!DNL Assets]AMS ** | 지원됨 | 지원됨 | 지원됨 |
   | **[!DNL Experience Manager]6.5[!DNL Assets]온-프레미스&#x200B;** | 지원되지 않음 | 지원되지 않음 | 지원되지 않음 |

### 지원되는 파일 형식 {#mimetypes}

작성자는 콘텐츠 파인더에서 이미지와 다음 유형의 문서를 검색하고 페이지 편집기에서 검색된 자산을 사용할 수 있습니다. 문서를 `Download` 구성 요소에 추가할 수 있고 이미지를 `Image` 구성 요소에 추가할 수 있습니다. Authors can also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. 지원되는 형식은 다음과 같습니다.

* **이미지 형식**: 이미지 구성 요소에서 [지원하는](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/components/image.html) 형식입니다. [!DNL Dynamic Media] 이미지는 지원되지 않습니다.
* **문서 포맷**: 연결된 자산 [에서 지원하는 문서 형식을 참조하십시오](assets-formats.md#supported-document-formats).

### 관련 사용자 및 그룹 {#users-and-groups-involved}

기능 및 해당 사용자 그룹을 구성하고 사용하는 데 관련된 여러 가지 역할이 아래에 설명되어 있습니다. 로컬 범위는 작성자가 웹 페이지를 만드는 사용 사례에 사용됩니다. 원격 범위는 필요한 자산을 호스팅하는 DAM 배포에 사용됩니다. The [!DNL Sites] author fetches these remote assets.

| 역할 | 범위 | 사용자 그룹 | 연습의 사용자 이름 | 요구 사항 |
|---|---|---|---|---|
| [!DNL Sites] administrator | 로컬 | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| DAM 사용자 | 로컬 | `Authors` | `ksaner` | `/content/DAM/connectedassets/`에서 가져온 자산을 보고 복제하는 데 사용됩니다. |
| [!DNL Sites] 작성자 | 로컬 | `Authors` (원격 DAM에 대한 읽기 액세스 및 로컬에 대한 작성자 액세스 [!DNL Sites]사용) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. `ksaner` DAM 사용자의 자격 증명이 사용됩니다. |
| [!DNL Assets] administrator | 원격 | [!DNL Experience Manager] `administrators` | `admin` 원격 [!DNL Experience Manager] | CORS(원본 간 리소스 공유)를 구성합니다. |
| DAM 사용자 | 원격 | `Authors` | `ksaner` 원격 [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| DAM 배포자(기술 사용자) | 원격 | [!DNL Sites] `Authors` | `ksaner` 원격 [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. 이 역할은 위의 두 `ksaner` 역할과 동일하지 않으며 다른 사용자 그룹에 속합니다. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Sites] deployment at `https://[local_sites]:4502`. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 연결된 자산 구성]**&#x200B;을 클릭하고 다음 값을 제공합니다.

   1. [!DNL Assets] 위치는 입니다 `https://[assets_servername_ams]:[port]`.
   1. DAM 배포자의 자격 증명(기술 사용자)
   1. In **[!UICONTROL Mount Point]** field, enter the local [!DNL Experience Manager] path where [!DNL Experience Manager] fetches the assets. 예를 들면 `remoteassets` 폴더를 입력합니다.
   1. 네트워크에 따라 **[!UICONTROL 원본 이진 전송 최적화 임계값]**&#x200B;의 값을 조정합니다. 이 임계값보다 크기가 큰 자산 렌디션은 비동기적으로 전송됩니다.
   1. 데이터 저장소를 사용하여 자산을 저장하고 데이터 저장소가 두 배포의 공통 저장소인 경우 **[!UICONTROL 연결된 자산과 공유되는 데이터 저장소]**를 선택합니다. 이 경우 실제 자산 바이너리가 데이터 저장소에 있고 전송되지 않으므로 임계값 제한은 문제가 되지 않습니다.
      ![연결된 자산에 대한 일반적인 구성](assets/connected-assets-typical-config.png)
   *그림: 연결된 자산에 대한 일반적인 구성.*

1. 자산이 이미 처리되고 렌디션을 가져올 때 워크플로우 런처를 비활성화합니다. Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. **[!UICONTROL DAM 자산 업데이트]** 및 **[!UICONTROL DAM 메타데이터 원본에 쓰기]**&#x200B;로 워크플로우를 사용하여 런처를 검색합니다.

   1. 워크플로우 런처를 선택하고 작업 표시줄에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.
   | 이전 | 이후 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >작성자가 자산을 가져올 때 원격 배포에서 사용할 수 있는 모든 렌디션을 가져옵니다. 가져온 자산의 렌디션을 더 만들려면 이 구성 단계를 건너뜁니다. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Assets'] CORS configuration.

   1. 관리자 자격 증명을 사용하여 로그인합니다. Search for `Cross-Origin`. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에 액세스합니다.

   1. To create a CORS configuration for [!DNL Sites] instance, click ![aem_assets_add_icon](assets/do-not-localize/aem_assets_add_icon.png) icon next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. 구성을 저장합니다.

## 원격 자산 사용 {#use-remote-assets}

웹 사이트 작성자가 콘텐츠 파인더를 사용하여 DAM 인스턴스에 연결합니다. 작성자는 구성 요소에서 원격 자산을 찾아보고 검색하고 드래그할 수 있습니다. 원격 DAM을 인증하려면 관리자가 제공한 DAM 사용자의 자격 증명을 가까이 보관합니다.

작성자는 단일 웹 페이지에서 로컬 DAM 및 원격 DAM 인스턴스에서 사용할 수 있는 자산을 사용할 수 있습니다. 콘텐츠 파인더를 사용하여 로컬 DAM을 검색하거나 원격 DAM을 검색합니다.

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. 다른 태그는 모두 무시됩니다. Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### 사용 연습 {#walk-through-of-usage}

위의 설정을 사용하여 작성 환경에서 기능이 어떻게 작동하는지 파악합니다. 원격 DAM 배포 시 원하는 문서 또는 이미지를 사용합니다.

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. 또는 브라우저에서 `https://[assets_servername_ams]:[port]/assets.html/content/dam`에 액세스합니다. 선택한 자산을 업로드합니다.
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. `ksaner`를 사용자 이름으로 지정하고 제공된 옵션을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 사이트]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**&#x200B;에서 We.Retail 웹 사이트 페이지를 엽니다. 페이지를 편집합니다. 또는 브라우저에서 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`에 액세스하여 페이지를 편집합니다.

   페이지의 왼쪽 위 모서리에서 **[!UICONTROL 사이드 패널 전환]**&#x200B;을 클릭합니다.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. 자격 증명을 제공합니다(사용자 이름: `ksaner`, 암호: `password`). This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. DAM에 추가한 자산을 검색합니다. 원격 자산이 왼쪽 패널에 표시됩니다. 이미지 또는 문서를 필터링하고 지원되는 문서 유형을 추가로 필터링합니다. 이미지를 `Image` 구성 요소로, 문서를 `Download` 구성 요소로 드래그합니다.

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. 구성 요소별 편집은 원본에 영향을 주지 않습니다.

   ![원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션](assets/filetypes_filter_connected_assets.png)

   *그림: 원격 DAM에서 자산을 검색할 때 문서 유형 및 이미지를 필터링하는 옵션.*

1. 자산을 비동기적으로 가져오는 경우 및 가져오기 작업이 실패할 경우 사이트 작성자에게 알립니다. 작성자는 작성 중이나 작성 후에도 [비동기 작업](/help/assets/asynchronous-jobs.md) 사용자 인터페이스에서 가져오기 작업 및 오류에 대한 자세한 정보를 볼 수 있습니다.

   ![백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.](assets/assets_async_transfer_fails.png)

   *그림: 백그라운드에서 발생하는 자산의 비동기적 가져오기에 대한 알림.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. 게시할 때 원격 자산을 성공적으로 가져오는지 확인합니다. 가져온 각 자산의 상태를 확인하려면 [비동기 작업](/help/assets/asynchronous-jobs.md) 사용자 인터페이스를 참조하십시오.

   >[!NOTE]
   >
   >하나 이상의 원격 자산을 가져오지 않더라도 페이지가 게시됩니다. 원격 자산을 사용하는 구성 요소가 빈 채로 게시됩니다. The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>가져온 원격 자산은 웹 페이지에서 사용한 경우 가져온 자산이 저장된 로컬 폴더에 액세스할 권한이 있는 모든 사람이 검색하고 사용할 수 있습니다(위의 연습에서 `connectedassets`). 또한 자산은 [!UICONTROL 콘텐츠 파인더]를 통해 로컬 저장소에서 검색하고 볼 수 있습니다.

가져온 자산은 연결된 메타데이터를 편집할 수 없다는 점을 제외하고 다른 로컬 자산으로 사용할 수 있습니다.

## 제한 사항 {#limitations}

### 권한 및 자산 관리 {#permissions-and-managing-assets}

* 로컬 자산은 원격 배포의 원본 자산과 동기화되지 않습니다. DAM 배포에 대한 권한 편집, 삭제 또는 취소는 다운스트림으로 전파되지 않습니다.
* 로컬 자산은 읽기 전용 복사본입니다. [!DNL Experience Manager] 구성 요소는 변경되지 않은 상태로 자산을 유지한 채 편집합니다. 다른 편집 작업은 허용되지 않습니다.
* 로컬로 가져온 자산은 작성용으로만 사용할 수 있습니다. 자산 업데이트 워크플로우를 적용할 수 없고 메타데이터를 편집할 수 없습니다.
* 이미지 및 나열된 문서 형식만 지원됩니다. [!DNL Dynamic Media] 자산, 콘텐츠 조각 및 경험 구성요소는 지원되지 않습니다.
* 메타데이터 스키마를 가져오지 않았습니다.
* All [!DNL Sites] authors have read permissions on the fetched copies, even if authors do not have access to the remote DAM deployment.
* 통합을 사용자 지정할 수 있는 API 지원이 없습니다.
* 이 기능을 통해 원격 자산을 원활하게 검색하고 사용할 수 있습니다. 로컬 배포에서 많은 원격 자산을 한 번에 사용할 수 있도록 하려면 자산을 마이그레이션하는 것이 좋습니다. [자산 마이그레이션 안내서](assets-migration-guide.md)를 참조하십시오.
* 원격 자산을 페이지 속성 사용자 인터페이스에서 페이지 축소판으로 사용할 [!UICONTROL 수] 없습니다. 이미지 선택을 클릭하여 [!UICONTROL 페이지 속성] 사용자 인터페이스에서 웹 페이지의 축소판을 설정할 수 [!UICONTROL 있습니다] .

### 설정 및 라이선스 {#setup-licensing}

* [!DNL Assets] 배포 [!DNL Adobe Managed Services] 가 지원됩니다.
* [!DNL Sites] 한 번에 단일 [!DNL Assets] 저장소에 연결할 수 있습니다.
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### 사용량 {#usage}

* 로컬 페이지에서 원격 자산을 검색하고 원격 자산을 작성자 콘텐츠로 드래그하는 기능만 지원됩니다.
* 5초 후에 가져오기 작업 시간이 종료됩니다. 네트워크 문제가 있는 경우 작성자가 자산을 가져오는 데 문제가 있을 수 있습니다. Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
*  `Image` 구성 요소를 통해 지원되는 편집과 원본에 영향을 주지 않는 간단한 편집은 가져온 자산에서 수행할 수 있습니다. 자산은 읽기 전용입니다.

## 문제 해결 {#troubleshoot}

일반적인 오류 시나리오에 대한 문제를 해결하려면 다음 단계를 따르십시오.

* If you cannot search for remote assets from the [!UICONTROL Content Finder] then ensure that the required roles and permissions are in place.
* 원격 댐에서 가져온 에셋이 하나 이상의 이유로 웹 페이지에 게시되지 않을 수 있습니다. 원격 서버에 존재하지 않거나 해당 서버에 가져올 권한이 없거나 네트워크 오류가 원인일 수 있습니다. 원격 DAM에서 자산이 제거되지 않았는지 확인합니다. 적절한 권한이 제자리에 있고 사전 요구 사항을 충족하는지 확인합니다. 자산을 페이지에 추가하고 다시 게시합니다. [비동기 작업 목록](/help/assets/asynchronous-jobs.md)에서 자산 가져오기 오류를 확인합니다.
