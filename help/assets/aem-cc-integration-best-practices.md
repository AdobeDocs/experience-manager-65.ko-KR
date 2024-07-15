---
title: Adobe Creative Cloud 우수 사례와 통합
description: 자산 전송 워크플로우를 간소화하고 컨텐츠 속도를 높이기 위해  [!DNL Adobe Experience Manager] 을(를)  [!DNL Adobe Creative Cloud] 과(와) 통합하는 우수 사례입니다.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: a144f7cc75b1a5cdb45d2aaf90e87013ac68a431
workflow-type: tm+mt
source-wordcount: '3173'
ht-degree: 11%

---

# [!DNL Adobe Experience Manager] 및 [!DNL Creative Cloud] 통합 모범 사례 {#aem-and-creative-cloud-integration-best-practices}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager Assets]은(는) [!DNL Adobe Creative Cloud]과(와) 통합할 수 있는 DAM(디지털 에셋 관리) 솔루션으로서, DAM 사용자가 크리에이티브 팀과 함께 작업할 수 있도록 지원하여 콘텐츠 만들기 프로세스에서 공동 작업을 간소화합니다.

[!DNL Adobe Creative Cloud]은(는) 크리에이티브 팀에 디지털 자산을 만드는 데 도움이 되는 솔루션 및 서비스 에코시스템을 제공합니다. 여기에는 데스크톱 및 모바일 응용 프로그램, 데스크톱 동기화나 웹 환경을 사용하는 저장소 등의 클라우드 서비스, [!DNL Adobe Stock]과(와) 같은 마켓플레이스가 포함됩니다.

사용 사례에 따라 데스크탑과 엔터프라이즈급 DAM 간에 선택해야 할 통합과 연결 워크플로우에 대한 관련 모범 사례는 무엇인지 계속 읽으십시오.

>[!NOTE]
>
>[!DNL Experience Manager]에서 [!DNL Creative Cloud] 폴더 공유는 더 이상 사용되지 않으며 더 이상 이 안내서에서 다루지 않습니다. Adobe은 [!DNL Experience Manager]에서 관리되는 에셋에 대한 액세스 권한을 크리에이티브 사용자에게 제공하기 위해 [Adobe 에셋 링크](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) 또는 [Experience Manager 데스크톱 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html)과 같은 최신 기능을 사용할 것을 권장합니다.

## 크리에이티브, 마케터 및 DAM 사용자의 Collaboration 요구 사항 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 요구 사항 | 사용 사례 | 관련 표면 |
|---|---|---|
| 데스크탑에서 크리에이티브를 위한 경험 단순화 | 크리에이티브 전문가 또는 더 광범위하게 기본 자산 만들기 애플리케이션에서 작업하는 데스크탑의 사용자를 위해 DAM([!DNL Experience Manager Assets])에서 자산에 대한 액세스를 간소화합니다. [!DNL Experience Manager]에 대한 검색, 사용(열기), 변경 내용 편집 및 저장, 새 파일 업로드를 쉽고 간단하게 수행할 수 있는 방법이 필요합니다. | Win 또는 Mac 데스크톱; [!DNL Creative Cloud]개 앱 |
| [!DNL Adobe Stock]에서 바로 사용할 수 있는 고품질 자산 제공 | 마케터는 자산 소싱 및 검색을 지원하여 콘텐츠 작성 프로세스를 가속화합니다. 크리에이티브 전문가는 크리에이티브 도구 내에서 승인된 에셋을 바로 사용합니다. | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] 마켓플레이스; 메타데이터 필드 |
| 조직별 자산 분배 및 공유 | 내부 부서/로컬 지점과 외부 파트너, 배포자 및 에이전시는 상위 조직이 공유하는 승인된 자산을 사용합니다. 이 조직은 생성된 자산을 보다 광범위한 재사용을 위해 안전하고 원활하게 공유하고자 합니다. | Brand Portal, Asset Share Commons |

## 공동 작업 요구 사항을 지원하는 Adobe 서비스 {#adobe-offerings-to-support-the-collaboration-need}

| 관련된 담당자에 대한 가치 제안 | Adobe 제공 | 관련 표면 |
|---|---|---|
| 크리에이티브 사용자는 [!DNL Creative Cloud] 앱을 종료하지 않고 [!DNL Experience Manager]에서 에셋을 검색하고, 열어 사용하고, [!DNL Experience Manager]에 대한 변경 내용을 편집하고 업로드하고, [!DNL Experience Manager]에 새 파일을 업로드합니다. | [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] 및 [!DNL Adobe InDesign]입니다. |
| 비즈니스 사용자는 데스크톱 환경에서 자산 열기 및 사용, [!DNL Experience Manager]에 변경 내용 편집 및 업로드, [!DNL Experience Manager]에 새 파일 업로드를 단순화합니다. Adobe이 아닌 자산 유형을 포함하여 기본 데스크탑 애플리케이션에서 모든 자산 유형을 열기 위해 일반 통합을 사용합니다. | [Experience Manager 데스크톱 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Win 및 Mac 데스크톱에서 [!DNL Experience Manager] 데스크톱 앱 사용 |
| 마케터와 비즈니스 사용자는 [!DNL Experience Manager] 내에서 [!DNL Adobe Stock] 자산을 검색, 미리 보기, 라이선스 부여 및 관리하고 있습니다. 라이선스가 부여되고 저장된 자산은 더 나은 거버넌스를 위해 선택한 [!DNL Adobe Stock] 메타데이터를 제공합니다. | [Experience Manager 및 Adobe Stock 통합](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 웹 인터페이스 |

This article focuses primarily on the first two aspects of the collaboration needs. Distribution and sourcing of assets at scale is briefly mentioned as a use case. For such needs solutions, consider Adobe Brand Portal or Asset Share Commons. [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 구성 요소, [Link Share](/help/assets/link-sharing.md)를 기반으로 빌드할 수 있는 솔루션, [Experience Manager Assets](/help/assets/manage-assets.md)을(를) 사용하는 솔루션 등의 대체 솔루션은 특정 요구 사항을 기반으로 검토해야 합니다.

Experience Manager에 대한 ![Creative Cloud 연결, 사용할 기능 결정](assets/creative-connections-aem.png)

### 사용 사례 및 Adobe 솔루션 매핑 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 사용 사례 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 데스크탑 앱 | 설명 / 기타 솔루션 |
|---|---|---|---|
| 검색 - DAM 폴더 찾아보기 | 예 | [!DNL Experience Manager] 웹 인터페이스 및 데스크톱 작업 | |
| 검색 - DAM 컬렉션 액세스 | 예 | [!DNL Experience Manager] 웹 인터페이스 및 데스크톱 작업 | |
| 검색 - DAM에서 에셋 검색 | 예 | [!DNL Experience Manager] 웹 인터페이스 및 데스크톱 작업 | |
| 사용 - 에셋 열기 | 예 | 예 | [웹 인터페이스에서 열기](manage-assets.md#previewing-assets) 또는 Finder에서 열기 |
| 사용 - DAM의 에셋을 문서에 배치 | 예 - 포함 | 예 - 연결 또는 포함 | [!DNL Experience Manager] 데스크톱 앱에서 로컬 파일 시스템의 파일로 자산에 액세스할 수 있습니다. 기본 앱의 이러한 링크는 로컬 경로로 표시됩니다. |
| 편집 - 편집을 위해 열기 | 예 - 체크아웃 작업 | 예 - 열기 작업(네트워크 공유에서) | [AAL에서 체크 아웃](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html)하면 기본적으로 사용자의 creative cloud 저장소 계정(Creative Cloud 앱에 의해 동기화됨)에 자산이 저장됩니다. |
| 편집 - DAM 외부에서 진행 중인 작업 | 예 - 데스크탑에 동기화된 사용자의 Creative Cloud 스토리지 계정에서 사용할 수 있는 자산입니다. | 예 | |
| 편집 - 변경 사항 업로드 | 예 - 선택적 댓글이 포함된 [체크 인 동작](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html) | 예 | |
| 업로드 - 단일 파일 | 예 - 현재 활성 문서를 업로드합니다 | 예 | [웹 인터페이스를 통해 업로드](manage-assets.md#uploading-assets) |
| 업로드 - 여러 파일/계층 폴더 구조 | 아니요 | 예 | [웹 인터페이스](manage-assets.md#uploading-assets) 또는 사용자 지정 스크립팅 또는 도구를 통해 업로드합니다. |
| 기타 - 사용자 및 로그인 | Creative Cloud 데스크톱 앱에 로그인한 Creative Cloud 사용자가 인식됩니다(SSO) | [!DNL Experience Manager] 사용자 및 자격 증명 | 두 솔루션의 사용자는 [!DNL Experience Manager] 사용자 할당량에 포함됩니다. |
| 기타 - 네트워크 및 액세스 | 사용자의 데스크톱에서 네트워크를 통해 [!DNL Experience Manager] 배포에 액세스해야 합니다. | 사용자의 데스크톱에서 네트워크를 통해 [!DNL Experience Manager] 배포에 액세스해야 합니다. | [!DNL Adobe Asset Link]이(가) 네트워크 프록시 환경을 공유하지 않습니다. |
| 기타 - 많은 수의 에셋 마이그레이션 | 아니요 | 아니요 | [자산 마이그레이션 안내서](assets-migration-guide.md) |

자산 배포 사용 사례를 지원하기 위해 다른 솔루션을 고려해야 합니다.

* 자산을 게시하기 위해 [!DNL Experience Manager Assets]에 구성 가능한 SaaS 추가 기능을 위한 [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html).
* 사용자 지정 솔루션은 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 코드 베이스를 기반으로 만들어집니다.
* [!DNL Experience Manager] [링크 공유](/help/assets/link-sharing.md)를 통해 링크를 사용하여 주문형 자산을 공유할 수 있습니다.
* [!DNL Experience Manager] 액세스 제어 설정 및 필요한 IT/네트워크 구성 조정으로 보호되는 외부 대상의 영역이 있는 [Experience Manager Assets 웹 인터페이스](/help/assets/manage-assets.md)를 통해 이러한 외부 사용자에게 [!DNL Experience Manager]에 대한 액세스 권한을 제공합니다.

## 주요 개념 및 사용 사례 {#key-concepts-and-use-cases}

### 공통 용어 용어집 {#glossary-of-common-terms}

* **Work-in-progress or creative work-in-progress (WIP):** A phase in asset lifecycle where an asset undergoes multiple changes and is typically not yet ready to be shared with broader teams.
* **크리에이티브 지원 에셋:** [!DNL Assets] 더 광범위한 팀과 공유할 준비가 되었거나 마케팅 또는 LOB 팀과 공유하기 위해 크리에이티브 팀이 선택 또는 승인한 에셋입니다.
* **Asset approvals:** The approval process that runs for assets already uploaded to DAM, which typically includes brand approvals, legal approvals, and so on.
* **최종 자산:** 모든 승인/메타데이터 태그 지정을 거쳤으며 더 광범위한 팀에서 사용할 준비가 된 자산입니다. Such an asset is stored in DAM and made available to all (or all interested) users. It can be used in marketing channels or by creative teams to create designs.
* **사소한 자산 업데이트/변경 :** 디지털 자산에 대한 빠르고 작은 변경입니다. It is often made in response to a retouching or minor editing request, asset review, or approval (for example, reposition, change text size, adjust saturation/brightness, color, and so on).
* **주요 에셋 업데이트/변경 :** 디지털 에셋을 변경하는 데 상당한 작업이 필요하며 때로는 더 오랜 기간에 걸쳐 수행해야 합니다. It typically includes multiple changes. The asset must be saved multiple times while being updated. Major asset updates typically cause the asset to enter a WIP stage.
* **DAM:** Digital asset management. 이 문서에서 특별히 언급되지 않는 한 [!DNL Experience Manager Assets]과(와) 동의어입니다.
* **Creative user:** A creative professional, who creates digital assets using Creative Cloud apps and services. In some cases, a creative user may be a member of a creative team who may use Creative Cloud, but does not create digital assets (like a creative director or creative team manager).
* **DAM user:** A typical user of a DAM system. 조직에 따라 DAM 사용자는 마케팅 또는 비마케팅 사용자(예: LOB(Line of Business) 사용자, 라이브러리 관리자, 영업 담당자 등)가 될 수 있습니다.

### [!DNL Experience Manager] 및 [!DNL Creative Cloud] 통합 사용 시 고려 사항 {#considerations-when-using-aem-and-creative-cloud-integration}

* [데스크톱 앱 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)를 참조하세요.
* [Adobe Stock 통합](aem-assets-adobe-stock.md)을 참조하세요.
* [자산 링크 Adobe](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html)을 참조하세요.

[!DNL Experience Manager] 및 [!DNL Creative Cloud] 통합에 대한 모범 사례를 간략하게 요약한 것입니다. 이 문서의 나머지 부분을 읽고 자세한 내용을 이해하십시오.

* **Photoshop, InDesign 또는 Illustrator에서 작업하는 크리에이티브 사용자의 경우:** Adobe 에셋 링크에서는 [!DNL Experience Manager]에서 체크 아웃한 에셋에 대해 진행 중인 작업을 깔끔하게 처리하는 등 최상의 사용자 환경을 제공합니다.
* **일반 파일 형식 또는 응용 프로그램의 데스크톱에서 자산에 대한 액세스를 단순화하려면** [!DNL Experience Manager] 데스크톱 앱을 사용하십시오.
* **DAM에 자산을 저장하는 이유와 시기를 이해합니다.** 조직의 더 광범위한 팀에서 사용할 수 있는 업데이트를 제공합니다.
* **Mind the volume of assets shared:** If your use case is asset distribution, governance and security might be the most important aspects. Consider using tools built for doing that at scale, like Brand Portal.
* **Understand asset lifecycle:** Know how assets are handled in your organization by different teams
* **Handle frequent saves to assets with care:** Adobe Asset Link takes care of that for you with PS, AI, ID. 다른 애플리케이션의 경우 DAM에서 모든 변경 사항이 필요하지 않은 경우 매핑된/공유 폴더에서 진행 중인 작업을 수행하지 마십시오

### [!DNL Assets]에서 [!DNL Adobe Stock]개 자산에 액세스 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager 및 Adobe Stock 통합](/help/assets/aem-assets-adobe-stock.md)은(는) [!DNL Experience Manager]명의 사용자에게 [!DNL Adobe Stock]의 자산을 [!DNL Experience Manager]에 검색, 미리 보기, 라이선스 및 저장할 수 있는 기능을 제공합니다. 라이센스가 부여되고 저장된 [!DNL Stock]개의 자산이 추가 필터로 검색할 수 있는 [!DNL Stock]개의 메타데이터를 선택했습니다.

이 통합에 대한 몇 가지 중요한 사항은 다음과 같습니다.

* Adobe 스톡의 자산이 [!DNL Experience Manager]에 저장되면 [!DNL Experience Manager] 저장소에 저장된 바이너리를 사용하는 일반 [!DNL Assets]이(가) 됩니다. [!DNL Adobe Stock]과(와) 관련된 일부 메타데이터가 [!DNL Experience Manager]의 에셋에 대해 저장되었습니다. 그렇지 않으면 수집 프로세스는 다른 파일과 동일하게 표시됩니다. 예를 들어 스마트 태그가 활성화되어 있으면 저장할 때 태그가 이러한 에셋에 추가됩니다.
* [!DNL Experience Manager]에 저장된 자산은 복사본이 아니며 [!DNL Adobe Stock]에 다시 연결되는 링크가 아닙니다.

**자산을 [!DNL Adobe Stock]에서[!DNL Creative Cloud]**&#x200B;의 [!DNL Experience Manager](으)로 저장한 상태로 작업. 이 통합은 [!DNL Adobe Asset Link]과(와) 독립적이지만 [!DNL Adobe Asset Link]은(는) 이러한 방식으로 [!DNL Stock]에서 저장된 이러한 자산을 인식하고 [!DNL Photoshop], [!DNL Illustrator] 또는 [!DNL InDesign]의 [!DNL Adobe Asset Link] 확장 UI에서 이러한 자산에 추가 메타데이터 및 [!DNL Adobe Stock] 로고를 표시합니다. 파일은 [!DNL Experience Manager]에 저장될 때 일반 자산이므로 탐색, 열기 등에 사용할 수 있습니다.
[!DNL Creative Cloud] 앱에서 [!DNL Adobe Asset Link] 확장을 사용하여 작업하는 크리에이티브 사용자는 [!DNL Adobe Stock]에서 [!DNL Experience Manager](으)로 이미 라이선스가 부여된 자산에 액세스할 수 있을 뿐만 아니라 [!DNL Creative Cloud] 라이브러리 패널을 사용하여 [!DNL Adobe Stock] 자산을 검색, 미리 보기 및 라이선스할 수도 있습니다.
[!DNL Adobe Stock]의 [!DNL Assets] 라이선스가 부여되고 [!DNL Experience Manager]에 저장된 값은 [!DNL Experience Manager Assets] 배포에 액세스하는 더 광범위한 팀에서 사용할 수 있게 되지만 [!DNL Adobe Stock]에서 [!DNL Creative Cloud] 라이브러리 패널을 통해 자산을 라이선스하는 크리에이티브 팀은 기본적으로 [!DNL Creative Cloud] 계정에서만 사용할 수 있도록 합니다.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## DAM에 에셋 저장 기본 정보 {#about-storing-assets-in-a-dam}

크리에이티브 팀과 마케팅/사업부(LOB) 팀 간의 효율적인 워크플로우를 디자인하고 최상의 지원 기능을 선택하려면 자산이 DAM에 저장되는 시기와 이유를 이해하는 것이 중요합니다.

### 자산이 DAM에 저장되는 이유 {#why-assets-are-stored-in-dam}

DAM에 에셋을 저장하면 에셋에 쉽게 액세스하고 검색할 수 있습니다. 파트너, 고객 등을 포함하여 조직 또는 생태계 전반에 걸쳐 수많은 사용자가 에셋을 사용할 수 있도록 합니다.

대부분의 조직은 다운스트림 마케팅/LOB 프로세스와 관련된 자산만 저장하도록 선택합니다. [!DNL Experience Manager Sites]을(를) 통해 웹 채널과 같은 채널에 게시하거나, Adobe Experience Cloud에서 제공하는 다른 채널(Marketing Cloud, Advertising Cloud 및 Analytics Cloud에서 측정한 채널, 사용자/파트너에게 제공하는 채널 등)은 다음과 같습니다. 또한 조직에서는 검토/승인 프로세스가 수행될 수 있는 에셋을 DAM에 저장합니다. 이처럼 DAM은 활용 가능성이 높은 자산을 대부분 저장하고, 유휴 자산의 저장을 회피한다.

에셋 저장에도 기술 및 리소스 사용률 고려 사항이 적용됩니다. DAM은 메타데이터 추출, 버전 관리, 미리보기/트랜스코딩 생성, 참조 관리 및 액세스 제어 정보 추가 등 저장된 에셋에 대한 추가 서비스를 제공합니다. 이러한 서비스는 추가 시간 및 인프라 리소스를 사용합니다.

모든 에셋과 업데이트를 저장하는 것은 바람직하지 않은 경우가 많습니다. 예를 들어 특정 자산에 대한 업데이트의 품질이 낮고 리소스를 과도하게 사용하는 경우 자산이 DAM에 저장되지 않을 수 있습니다.

#### 자산이 DAM에 저장되는 경우 {#when-assets-are-stored-in-dam}

크리에이티브 팀(및 조직)은 일반적으로 에셋 수명주기의 각 단계에서 에셋을 저장하는 데 관심이 없습니다. 예를 들어 다음과 같은 경우에는 에셋을 저장하지 않습니다.

* 아직 확정되지 않았거나 실험이 필요한 Assets.
* 크리에이티브/내부 팀 검토 주기를 통과하지 못한 Assets.
* 해당 에셋에 비해 팀은 외부 팀에 자신의 작업을 대표하는 더 나은 후보자를 보유하고 있습니다.

일반적으로 다음 클래스 자산은 DAM에 저장됩니다.

* 일정 성숙도에 도달하여 공유할 준비가 된 것으로 간주되는 Assets
* 크리에이티브 팀이 사전 선택한 Assets.
* 특정 계약 또는 계약에 따라 마케팅에서 사용할 수 있거나 요청한 특정 에셋 형식(예: RAW 파일에서 변환된 JPG 파일, PSD 원본의 TIFF/이미지).

#### 자산 업데이트가 DAM에 저장되는 경우 {#when-updates-to-assets-are-stored-in-dam}

일반적으로 광범위한 DAM 사용자 세트와 관련된 에셋에 대한 업데이트만 DAM에 저장해야 합니다. 이를 통해 사용자(마케팅 및 유사한 기능)가 DAM 에셋 타임라인에서 관련 버전만 볼 수 있습니다.

일반적으로 자산 라이프사이클의 주요 이정표와 관련된 변경 사항입니다. 예를 들어 크리에이티브 팀이 제공한 요청/검토를 기반으로 한 초기 마케팅 준비 에셋 또는 공식 업데이트는 DAM에 저장 및 버전 관리되어야 합니다.

DAM의 기존 에셋에 대한 변경 요청 후 마케팅 팀이 검토하도록 크리에이티브 팀이 업데이트하는 것은 관련 업데이트의 예입니다. 추가 참조 또는 이전 버전으로 되돌리기 위해 DAM에 저장하고 버전을 지정해야 합니다.

다음은 일반적으로 관련성이 없는 업데이트의 예입니다.

* 마케팅 검토를 위해 준비되기 전에 업로드된 자산의 초기 버전
* 크리에이티브 및 마케팅 팀에서 에셋이 준비되었다고 결정하기 전에 진행 중인 작업 단계에서 에셋에 대한 빈번한 크리에이티브 변경

### DAM에 대한 사용자 액세스 {#user-access-to-dam}

[!DNL Assets]은(는) [!DNL Assets] 배포에 대한 액세스 권한에 따라 두 가지 유형의 사용자를 지원합니다. 일반적으로 엔터프라이즈 네트워크(방화벽) 내의 사용자는 DAM에 직접 액세스할 수 있습니다. 엔터프라이즈 네트워크 외부의 다른 사용자는 직접 액세스할 수 없습니다. 사용자 유형은 기술적 관점에서 사용할 수 있는 통합을 결정합니다.

#### DAM에 직접 액세스할 수 있는 크리에이티브 사용자 {#creative-users-with-direct-access-to-dam}

일반적으로 내부 네트워크에 온보딩된 사내 크리에이티브 팀 또는 에이전시/크리에이티브 전문가는 [!DNL Experience Manager] 로그인을 포함하여 DAM 배포에 액세스할 수 있습니다. [!DNL Experience Manager]과(와) 네트워크 인프라를 설정하여 외부 당사자(일반적으로 클라이언트 에이전시와 같은 신뢰할 수 있는 조직)에 직접 액세스하여 VPN 또는 IP 허용 목록 등을 통해 네트워크를 통해 [!DNL Experience Manager]에 액세스할 수 있도록 할 수 있습니다.

이러한 경우 Asset Link 또는 [!DNL Experience Manager] 데스크톱 앱을 Adobe 하면 최종/승인된 자산에 쉽게 액세스할 수 있으며 크리에이티브 준비가 완료된 자산을 DAM에 저장할 수 있습니다.

#### DAM에 액세스할 수 없는 크리에이티브 사용자 {#creative-users-without-access-to-dam}

DAM 배포에 직접 액세스할 수 없는 외부 에이전시와 프리랜서는 승인된 자산에 액세스해야 하거나 새 디자인을 DAM에 추가하려고 할 수 있습니다.

다음 전략을 사용하여 최종/승인된 에셋에 액세스할 수 있습니다.

* Asset Link가 작동하지 않는 경우 데스크탑 앱을 사용하십시오.
* 자산을 외부 파트너에게 안전하게 배포하려면 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)을(를) 사용하십시오.
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)을(를) 기반으로 배포 및 소싱 포털의 사용자 지정 구현 사용
* [!DNL Experience Manager]에 설정된 액세스 제어 및 필요한 네트워크 인프라(예: VPN 및 IP 허용 목록)를 사용하여 외부 당사자에게 DAM의 전용 콘텐츠 영역에 대한 액세스 권한을 부여합니다. [!DNL Experience Manager] 웹 UI를 사용하여 자산을 가져오고 새 콘텐츠를 DAM에 업로드할 수 있습니다.

#### [!DNL Experience Manager]에서 에셋에 대한 작업 진행 중 {#work-in-progress-on-assets-from-aem}

이 문서에서 설명한 대로 로컬 파일에 저장된 모든 편집 내용을 변경 내용으로 [!DNL Experience Manager]에 업로드하지 않고도 자산(예: 작업 진행 중)에 대한 주요 업데이트를 수행하는 것이 좋습니다. 이렇게 하면 데스크탑 사용자의 작업 속도가 빨라지고, 사용되는 네트워크 대역폭이 제한되며, 자산 타임라인을 깔끔하게 유지하고, 통제되는 주요 업데이트에 집중할 수 있습니다.

Adobe 에셋 링크는 이 사용 사례에 대한 유용한 지원을 제공합니다.

* [!DNL Photoshop], [!DNL InDesign] 또는 [!DNL Illustrator]의 사용자가 파일을 편집하려고 할 때 지정된 에셋에서 체크 아웃 작업을 실행합니다
* 에셋이 백그라운드로 다운로드되고, Creative Cloud 데스크톱 앱에서 디스크에 동기화되는 Creative Cloud 계정에 추가되며, 편집 충돌을 최소화하기 위해 에셋의 [!DNL Experience Manager]에서 체크아웃 플래그가 전환됩니다
* 이제부터 사용자는 동기화된 위치에 로컬로 저장된 파일에서 작업하며 필요한 빈도에 따라 작업을 계속하고 필요한 변경 사항을 저장할 수 있습니다
* 또한 에셋은 Creative Cloud 계정에 있으므로 사용자가 보유할 수 있는 다른 장치에서도 사용할 수 있으며(예: 전용 Creative Cloud 모바일 앱에서 열거나 편집할 수 있음), 공동 작업 목적으로 다른 Creative Cloud 사용자와 공유할 수 있습니다.
* 크리에이티브 사용자가 변경을 완료하면 Creative Cloud 애플리케이션에서 선택적 주석을 사용하여 해당 파일에 대한 체크 인 작업을 실행할 수 있습니다. [!DNL Experience Manager]의 해당 에셋은 새 바이너리로 버전이 지정되고 업데이트됩니다. 마케터 또는 LOB 사용자와 같은 [!DNL Experience Manager] 사용자는 [!DNL Experience Manager] 자산 타임라인 UI를 통해 주요 자산 변경 또는 마일스톤에 액세스할 수 있습니다.

[!DNL Experience Manager] 데스크톱 앱은 기본 앱에서 연 에셋에 대한 네트워크 공유를 제공합니다. 기본적으로 로컬에서 수행된 모든 변경 내용은 잠시 후 자동으로 [!DNL Experience Manager]에 업로드됩니다. 이러한 구성을 통해 진행 중인 단계 동안 자주 저장하는 작업은 모두 [!DNL Experience Manager]에 업로드되어 많은 네트워크 트래픽 및 잠재적인 확장성 문제를 해결합니다. [!DNL Experience Manager]의 불필요한 버전은 말할 것도 없습니다.

여기에서는 [!DNL Experience Manager] 데스크톱 앱의 옵션을 사용하여 자동 업데이트를 끄고 앱의 자산 상태 UI에서 변경 내용 업로드 작업을 사용하여 자산에 대한 변경 내용을 [!DNL Experience Manager]에 수동으로 업로드하는 것이 좋습니다.

#### DAM에 일괄 업로드 {#bulk-upload-to-dam}

다음과 같은 일부 시나리오에서는 더 많은 수의 파일을 동시에 DAM에 업로드해야 할 필요가 있습니다.

* 사진 촬영 또는 더 큰 프로젝트의 결과 업로드
* 크리에이티브 에이전시에서 제공하는 에셋 업로드
* DAM 외부에서 선택한 경우 더 큰 세트에서 선택한 에셋 업로드

이 설명은 데스크탑 사용자의 워크플로의 일반적인 일부로서, 작동적으로(예: 매주 또는 사진 촬영 시) 파일을 업로드하는 것을 말합니다. 대규모 자산 마이그레이션은 여기에서 다루지 않습니다.

다음과 같은 업로드 기능을 사용할 수 있습니다.

* 대형/계층적 폴더를 일괄 업로드하려면 [폴더 업로드](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) 기능을 제공하는 [!DNL Experience Manager] 데스크톱 앱을 사용하세요. 계층적 폴더 구조를 업로드할 수도 있습니다. [!DNL Assets]이(가) 백그라운드에서 업로드되므로 웹 브라우저 세션에 연결되어 있지 않습니다.
* 단일 폴더에서 몇 개의 파일을 업로드하려면 파일을 웹 인터페이스로 직접 끌어 놓거나 [!DNL Assets] 웹 인터페이스의 만들기 옵션을 사용합니다.
* 비즈니스 요구 사항에 따라 사용자 정의 업로더를 사용할 수도 있습니다.

#### 데스크탑에서 직접 디지털 자산 관리 {#managing-digital-assets-directly-from-desktop}

네트워크 파일 공유를 사용하여 디지털 자산을 관리하는 경우 [!DNL Experience Manager] 데스크톱 앱에서 매핑된 네트워크 공유를 사용하면 편리하게 대체할 수 있습니다. 네트워크 파일 공유에서 전환할 때 [!DNL Experience Manager] 웹 인터페이스는 네트워크 공유에서 가능한 기능(검색, 컬렉션, 메타데이터, 공동 작업, 미리 보기 등)을 훨씬 능가하는 다양한 디지털 자산 관리 기능을 제공하며 [!DNL Experience Manager] 데스크톱 앱은 서버측 DAM 저장소를 데스크톱의 작업과 연결하는 편리한 링크를 제공합니다.

[!DNL Experience Manager] 데스크톱 앱을 사용하여 [!DNL Assets]의 네트워크 공유에서 직접 자산을 관리하지 마십시오. 예를 들어 [!DNL Experience Manager] 데스크톱 앱을 사용하여 여러 파일을 이동/복사하지 마십시오. 대신 [!DNL Assets] 인터페이스를 사용하여 폴더를 Finder/Explorer에서 네트워크 공유로 드래그하거나 [!DNL Assets] 폴더 업로드 기능을 사용하십시오.

#### 자산 마이그레이션 {#asset-migration}

기존 시스템에서 새 시스템으로의 자산 마이그레이션 또는 서버에 저장된 대량의 자산 마이그레이션을 계획 및 실행하려면 [마이그레이션 안내서](/help/assets/assets-migration-guide.md)를 참조하십시오. [!DNL Experience Manager] 데스크톱 앱과 [!DNL Experience Manager]에서 [!DNL Creative Cloud] 간 통합은 이러한 마이그레이션을 지원하지 않습니다. 수집할 자산의 양이 많고 메타데이터 매핑, 변환 및 수집과 관련된 추가 요구 사항 때문에 마이그레이션은 다양한 툴과 접근 방식을 사용하여 처리해야 합니다.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html)
>* [Experience Manager 데스크톱 앱 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Brand Portal Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager 및 Adobe Stock 통합](aem-assets-adobe-stock.md)
