---
title: Adobe Creative Cloud 우수 사례와 통합
description: 자산 전송 워크플로우를 간소화하고 높은 컨텐츠 속도를 달성하는 데 도움이 되는 통합 [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] 에 대한 우수 사례입니다.
contentOwner: AG
role: Business Practitioner, Administrator
feature: 공동 작업,Adobe 자산 링크,데스크탑 앱
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
source-git-commit: c4cfb709162ca8f8f6e8508516c39542347c6bc4
workflow-type: tm+mt
source-wordcount: '3254'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 및  [!DNL Creative Cloud] 통합 우수 사례  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] 는 DAM 사용자가 크리에이티브 팀과 함께 작업할 수  [!DNL Adobe Creative Cloud] 있도록 과 통합하여 컨텐츠 작성 프로세스에서 간소화된 공동 작업을 수행할 수 있는 DAM(디지털 자산 관리) 솔루션입니다.

[!DNL Adobe Creative Cloud] 는 크리에이티브 팀이 디지털 자산을 만드는 데 도움이 되는 솔루션 및 서비스의 에코시스템을 제공합니다. 데스크탑 및 모바일 애플리케이션, 데스크탑 동기화 또는 웹 경험이 포함된 스토리지와 같은 클라우드 서비스, [!DNL Adobe Stock] 등의 마켓플레이스 등이 포함되어 있습니다.

사용 사례를 기반으로 데스크탑과 엔터프라이즈급 DAM 간에 어떤 통합을 선택하고 연결 워크플로우에 대한 관련 모범 사례는 무엇입니까? 를 참조하십시오.

>[!NOTE]
>
>[!DNL Experience Manager] 폴더  [!DNL Creative Cloud] 공유는 더 이상 사용되지 않으며 더 이상 이 안내서에서 다루지 않습니다. Adobe은 [Adobe 자산 링크](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) 또는 [Experience Manager 데스크탑 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html)과 같은 최신 기능을 사용하여 크리에이티브 사용자에게 [!DNL Experience Manager]에서 관리되는 자산에 대한 액세스 권한을 제공할 것을 권장합니다.

## 크리에이티브, 마케터 및 DAM 사용자의 공동 작업 요구 사항 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 요구 사항 | 사용 사례 | 관련 서피스 |
|---|---|---|
| 데스크탑에서 크리에이티브 환경 간소화 | 크리에이티브 전문가를 위한 DAM([!DNL Experience Manager Assets])에서 자산에 대한 액세스를 간소화하거나, 기본 자산 작성 애플리케이션에서 작업하는 데스크탑의 사용자를 보다 폭넓게 활용할 수 있습니다. 이 솔루션은 [!DNL Experience Manager]에 변경 내용을 검색, 사용(열기)하고 편집 및 저장하고 새 파일을 업로드하는 쉽고 간단한 방법이 필요합니다. | Win 또는 Mac 데스크탑[!DNL Creative Cloud] 앱 |
| [!DNL Adobe Stock]에서 고품질의 즉시 사용할 수 있는 자산 제공 | 마케터는 자산 소싱 및 검색을 지원하여 컨텐츠 작성 프로세스를 가속화할 수 있습니다. 크리에이티브 전문가가 크리에이티브 도구 내에서 바로 승인된 자산을 사용합니다. | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] marketplace;메타데이터 필드 |
| 조직별 자산 분배 및 공유 | 내부 부서/지역 분기 및 외부 파트너, 배포자 및 에이전시는 상위 조직에서 공유한 승인된 자산을 사용합니다. 조직은 더 광범위한 재사용을 위해 생성된 자산을 안전하고 원활하게 공유하려고 합니다. | Brand Portal, Asset Share Commons |

## 공동 작업을 지원하기 위한 Adobe 제공 요구 사항 {#adobe-offerings-to-support-the-collaboration-need}

| 관련 성향에 대한 가치 제안 | Adobe 제공 | 관련 서피스 |
|---|---|---|
| 크리에이티브 사용자는 [!DNL Creative Cloud] 앱을 종료하지 않고 [!DNL Experience Manager]에서 자산을 찾고, 열고 사용하고, 변경 사항을 편집 및 [!DNL Experience Manager]에 업로드하고, 새 파일을 [!DNL Experience Manager]에 업로드합니다. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], 및 [!DNL Adobe InDesign]. |
| 비즈니스 사용자는 자산을 열고 사용, 변경 내용을 [!DNL Experience Manager]에 편집 및 업로드하고, 데스크탑 환경에서 [!DNL Experience Manager]에 새 파일을 업로드하는 작업을 단순화합니다. 일반 통합을 사용하여 비Adobe을 포함하여 기본 데스크탑 애플리케이션에서 자산 유형을 엽니다. | [Experience Manager 데스크탑 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win 및 Mac 데스크탑의 데스크탑 앱 |
| 마케터와 비즈니스 사용자는 [!DNL Experience Manager] 내에서 [!DNL Adobe Stock] 자산을 검색, 미리 보기, 라이선스 및 저장 및 관리합니다. 라이선스와 저장된 자산은 더 나은 거버넌스를 위해 선택 [!DNL Adobe Stock] 메타데이터를 제공합니다. | [Experience Manager 및 Adobe Stock 통합](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 웹 인터페이스 |

이 문서는 주로 공동 작업 요구 사항의 첫 두 가지 측면에 중점을 둡니다. 사용 사례로는 자산의 분포 및 소싱이 간략하게 언급되어 있습니다. 이러한 요구 사항을 해결하려면 Brand Portal Adobe 또는 Asset Share Commons를 고려하십시오. [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 등의 대체 솔루션, [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 구성 요소를 기반으로 빌드할 수 있는 솔루션, [Link Share](/help/assets/link-sharing.md)와 같은 대체 솔루션은 특정 요구 사항에 따라 검토해야 합니다.[](/help/assets/manage-assets.md)

![Experience Manager에 대한 연결 Creative Cloud, 사용할 기능 결정](assets/creative-connections-aem.png)

### 사용 사례 및 Adobe 솔루션 매핑 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 사용 사례 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 데스크탑 앱 | 비고/기타 해결 방법 |
|---|---|---|---|
| 검색 - DAM 폴더 찾아보기 | 예 | [!DNL Experience Manager] 웹 인터페이스 및 데스크톱 작업 |  |
| 검색 - DAM 컬렉션 액세스 | 예 | [!DNL Experience Manager] 웹 인터페이스 및 데스크톱 작업 |  |
| 검색 - DAM에서 자산 검색 | 예 | [!DNL Experience Manager] 웹 인터페이스 및 데스크톱 작업 |  |
| 사용 - 자산 열기 | 예 | 예 | [Finder에서 웹 ](manage-assets.md#previewing-assets) 인터페이스에서 열기 |
| 사용 - DAM의 자산을 문서에 배치 | 예 - 포함 | 예 - 연결 또는 포함 | [!DNL Experience Manager] 데스크탑 앱에서는 로컬 파일 시스템에서 자산으로 자산에 대한 액세스를 제공합니다. 기본 앱의 이러한 링크는 로컬 경로로 표시됩니다. |
| 편집 - 열어서 편집합니다. | 예 - 체크아웃 작업 | 예 - 열린 작업(네트워크 공유에서) | [AAL에서 ](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html) 체크아웃하면 기본적으로 자산을 사용자의 Creative Cloud 저장소 계정(Creative Cloud 앱별로 동기화)에 저장합니다. |
| 편집 - DAM 외부에서 진행 중 | 예 - 데스크탑에 동기화된 사용자의 Creative Cloud 저장소 계정에서 사용할 수 있는 자산입니다. | 예 |  |
| 편집 - 변경 내용 업로드 | 예 - [체크 인 작업](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)(선택적 주석 포함) | 예 |  |
| 업로드 - 단일 파일 | 예 - 현재 활성 문서 업로드 | 예 | [웹 인터페이스를 통해 업로드](manage-assets.md#uploading-assets) |
| 업로드 - 여러 파일/계층 폴더 구조 | 아니오 | 예 | [웹 인터페이스 또](manage-assets.md#uploading-assets) 는 사용자 정의 스크립팅 또는 도구를 통해 업로드합니다. |
| 기타 - 사용자 및 로그인 | Creative Cloud 사용자가 Creative Cloud 데스크탑 앱에 로그인되어 인식됨(SSO) | [!DNL Experience Manager] 사용자 및 자격 증명 | 두 솔루션의 사용자는 [!DNL Experience Manager] 사용자 할당량에 따라 계산됩니다. |
| 기타 - 네트워크 및 액세스 | 네트워크를 통해 [!DNL Experience Manager] 배포에 대한 사용자의 데스크탑에 대한 액세스 필요 | 네트워크를 통해 [!DNL Experience Manager] 배포에 대한 사용자의 데스크탑에 대한 액세스 필요 | [!DNL Adobe Asset Link] 네트워크 프록시 환경을 공유하지 않습니다. |
| 기타 - 많은 수의 자산 마이그레이션 | 아니오 | 아니오 | [자산 마이그레이션 안내서](assets-migration-guide.md) |

자산 분배 사용 사례를 지원하려면 다른 솔루션을 고려해야 합니다.

* [Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portal을 사용하여 자산을 게시할 수  [!DNL Experience Manager Assets] 있는 구성 가능한 SaaS 추가 기능입니다.
* 사용자 지정 솔루션은 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 코드 베이스를 기반으로 만들어집니다.
* [!DNL Experience Manager] [링크를 ](/help/assets/link-sharing.md) 사용하여 자산을 ad hoc으로 공유하도록 링크를 공유하십시오.
* [Experience Manager Assets 웹 인터페이스](/help/assets/manage-assets.md) 는  [!DNL Experience Manager] 액세스 제어 설정에 의해 보안되고 필요한 IT/네트워크 구성 조정을 통해 보안된 외부 당사자를 위한 영역과 상호 작용하여 이러한 외부 사용자에게 액세스 권한을  [!DNL Experience Manager].

## 주요 개념 및 사용 사례 {#key-concepts-and-use-cases}

### 일반 용어 {#glossary-of-common-terms} 용어집

* **진행 중 또는 WIP(Creative Work-in-Progress):**  자산이 여러 변경 작업을 수행하고 일반적으로 더 광범위한 팀과 공유할 준비가 되지 않은 자산 라이프사이클의 단계입니다.
* **크리에이티브 지원 자산:** [!DNL Assets] 더 광범위한 팀과 공유할 준비가 되었거나, 마케팅 또는 LOB 팀과 공유할 크리에이티브 팀이 선택하거나 승인했습니다.
* **자산 승인:** DAM에 이미 업로드된 자산에 대해 실행되는 승인 프로세스로, 일반적으로 브랜드 승인, 법적 승인 등이 포함됩니다.
* **최종 자산:** 모든 승인/메타데이터 태깅을 거친 자산이며 광범위한 팀에서 사용할 준비가 된 자산입니다. 이러한 자산은 DAM에 저장되며 모든(또는 모든 관심 있는) 사용자가 사용할 수 있습니다. 마케팅 채널이나 크리에이티브 팀이 디자인을 만드는 데 사용할 수 있습니다.
* **사소한 자산 업데이트/변경 :** 디지털 자산에 대한 빠르고 작은 변경 사항입니다. 이는 종종 수정 또는 작은 편집 요청, 자산 검토 또는 승인(예: 위치 변경, 텍스트 크기 변경, 채도/명도 조정, 색상 조정)에 응답하여 수행됩니다.
* **주요 자산 업데이트/변경 :** 상당한 작업이 필요하고 경우에 따라 긴 기간 동안 수행해야 하는 디지털 자산에 대한 변경 사항입니다. 일반적으로 여러 변경 사항이 포함됩니다. 자산을 업데이트하는 동안 여러 번 저장해야 합니다. 주요 자산 갱신으로 인해 일반적으로 자산이 WIP 단계에 들어갑니다.
* **DAM:** 디지털 자산 관리. 이 문서에서 별도로 언급되지 않는 한 [!DNL Experience Manager Assets]과 동의됩니다.
* **크리에이티브 사용자:** Creative Cloud 앱 및 서비스를 사용하여 디지털 자산을 만드는 크리에이티브 전문가. 경우에 따라 크리에이티브 사용자는 Creative Cloud을 사용할 수 있지만 디지털 자산을 만들지 않는 크리에이티브 팀의 구성원일 수 있습니다(예: 크리에이티브 디렉터 또는 크리에이티브 팀 관리자).
* **DAM 사용자:** DAM 시스템의 일반적인 사용자. 조직에 따라 DAM 사용자는 마케팅 또는 비마케팅 사용자일 수 있습니다. 예를 들어 LOB(Line-of-Business) 사용자, 도서관, 영업 사원 등이 있습니다.

### [!DNL Experience Manager] 및 [!DNL Creative Cloud] 통합 {#considerations-when-using-aem-and-creative-cloud-integration} 사용 시 고려 사항

* [데스크탑 앱 우수 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles) 를 참조하십시오
* [Adobe Stock 통합](aem-assets-adobe-stock.md)을 참조하십시오
* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)를 참조하십시오

[!DNL Experience Manager] 및 [!DNL Creative Cloud] 통합에 대한 모범 사례에 대한 간단한 요약입니다. 이 문서의 나머지 부분을 읽어 자세한 내용을 파악합니다.

* **Photoshop, InDesign 또는 Illustrator에서 작업하는 크리에이티브 사용자의 경우,** Adobe 자산 링크는 [!DNL Experience Manager]에서 체크 아웃된 자산에 대해 진행 중인 작업을 깨끗한 처리하는 등 최상의 사용자 경험을 제공합니다.
* **모든 일반 파일 형식 또는 응용 프로그램에 대해 데스크탑에서 자산에 대한 액세스를 간소화하기 위해**  [!DNL Experience Manager] 데스크탑 앱을 사용합니다.
* **DAM에 자산을 저장하는 이유 및 시기 이해:**  조직의 광범위한 팀이 사용할 수 있도록 업데이트하는 이유입니다.
* **공유된 자산의 볼륨에 주의하십시오.** 사용 사례가 자산 배포라면, 거버넌스 및 보안이 가장 중요한 측면일 수 있습니다. Brand Portal과 같이 규모에 맞게 제작된 도구를 사용해 보십시오.
* **자산 라이프사이클 이해:** 여러 팀이 조직에서 자산을 처리하는 방법을 알아봅니다
* **자산을 신중하게 자주 저장하는 작업을 처리합니다.** Adobe 자산 링크는 PS, AI 및 ID로 자산을 처리합니다. 다른 응용 프로그램의 경우 DAM에서 모든 변경 사항이 필요하지 않은 한 매핑된/공유 폴더에서 진행 중인 작업을 수행하지 마십시오

### [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}에서 [!DNL Adobe Stock] 자산에 액세스

[Experience Manager 및 Adobe Stock ](/help/assets/aem-assets-adobe-stock.md) 통합은  [!DNL Experience Manager] 사용자에게 자산 [!DNL Adobe Stock] 을  [!DNL Experience Manager]로 검색, 미리 보기, 라이선스 및 저장할 수 있는 기능을 제공합니다. 라이선스 및 저장된 [!DNL Stock] 자산이 [!DNL Stock] 메타데이터를 선택했으며, 이 메타데이터를 추가 필터로 검색하는 데 사용할 수 있습니다.

이 통합에 대한 몇 가지 중요한 사항:

* Adobe 스톡의 자산을 [!DNL Experience Manager]에 저장하면 일반 [!DNL Assets]이 되고 바이너리가 [!DNL Experience Manager] 저장소에 저장됩니다. [!DNL Adobe Stock]과 관련된 일부 메타데이터는 [!DNL Experience Manager]의 자산에 대해 저장되며, 그렇지 않으면 수집 프로세스가 다른 파일과 동일하게 표시됩니다. 예를 들어, 스마트 태그가 활성화되어 있으면 저장 시 태그가 이러한 자산에 추가됩니다.
* [!DNL Experience Manager]에 저장된 자산은 복사이며, 다시 [!DNL Adobe Stock]에 연결되는 링크가 아닙니다.

**에서 로 저장된 자산 [!DNL Adobe Stock] 을 사용하여  [!DNL Experience Manager] 작업[!DNL Creative Cloud]**. 이 통합은 [!DNL Adobe Asset Link]와는 다르지만, [!DNL Adobe Asset Link]은 [!DNL Stock]에서 저장된 이러한 자산을 이러한 방식으로 인식하고, [!DNL Photoshop], [!DNL Illustrator] 또는 [!DNL InDesign]에서 [!DNL Adobe Asset Link] 확장 UI에 이러한 자산에 대한 추가 메타데이터 및 [!DNL Adobe Stock] 로고를 표시합니다. 파일은 [!DNL Experience Manager]에 저장할 때 일반 자산이므로 찾아보기, 열기 등에 사용할 수 있습니다.
[!DNL Adobe Asset Link] 확장이 있는 [!DNL Creative Cloud] 앱에서 작업하는 크리에이티브 사용자는 [!DNL Adobe Stock]에서 [!DNL Experience Manager]로 이미 라이선스가 부여된 자산에 액세스할 수 있을 뿐만 아니라 [!DNL Creative Cloud] 라이브러리 패널을 사용하여 [!DNL Adobe Stock] 자산을 검색, 미리 보기 및 라이선스를 제공할 수도 있습니다.
[!DNL Assets]  [!DNL Adobe Stock] 라이선스가  [!DNL Experience Manager] 있고 [!DNL Experience Manager Assets] 에 저장되면 배포에 액세스하는 더 광범위한 팀에서 사용할 수 있지만 라이브러리 패널을  [!DNL Adobe Stock] 통해  [!DNL Creative Cloud] 제공되는 크리에이티브 라이선스 자산은 기본적으로  [!DNL Creative Cloud] 해당 계정에서만 사용할 수 있습니다.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## DAM에 자산 저장 정보 {#about-storing-assets-in-a-dam}

크리에이티브 및 마케팅/LOB(Line of Business) 팀 간의 효율적인 워크플로우를 설계하고 최상의 지원 기능을 선택하려면 DAM에 자산이 저장되는 시기와 이유를 이해하는 것이 중요합니다.

### 자산이 DAM {#why-assets-are-stored-in-dam}에 저장되는 이유

DAM에 자산을 저장하면 쉽게 액세스하고 이를 완료할 수 있습니다. Launch를 사용하면 파트너, 고객 등을 포함하는 조직 또는 에코시스템에서 다양한 사용자가 자산을 활용할 수 있습니다.

대부분의 조직은 다운스트림 마케팅/LOB 프로세스와 관련된 자산만 저장하도록 선택합니다([!DNL Experience Manager Sites] 또는 Adobe Experience Cloud에서 제공하는 기타 채널 - Marketing Cloud, Advertising Cloud을 통해 웹 채널에 게시, 사용자/파트너에게 제공 등). 또한 조직은 DAM에서 검토/승인 프로세스를 수행할 수 있는 자산을 저장합니다. 이 방법으로 DAM은 주로 자산을 활용할 가능성이 높고 유휴 자산을 저장하지 않는 자산을 저장합니다.

자산을 저장하는 것은 기술 및 리소스 활용률 고려도 받습니다. DAM은 메타데이터 추출, 버전 관리, 미리 보기/코드 변환 생성, 참조 관리, 액세스 제어 정보 추가 등 저장된 자산에 대한 추가 서비스를 제공합니다. 이러한 서비스는 추가 시간과 인프라 자원을 사용합니다.

모든 자산과 업데이트를 저장하는 것은 권장되지 않는 경우가 많습니다. 예를 들어 특정 자산에 대한 업데이트가 품질이 좋지 않고 과도한 리소스를 소비하는 경우 자산이 DAM에 저장되지 않을 수 있습니다.

#### 자산이 DAM {#when-assets-are-stored-in-dam}에 저장되는 경우

광고 팀(및 조직)은 일반적으로 자산 라이프사이클의 각 단계에서 자산을 저장하는 것에 관심이 없습니다. 예를 들어 다음과 같은 경우 자산이 저장되지 않습니다.

* 아직 확정되지 않았거나 실험대상이 되는 자산입니다.
* 크리에이티브/내부 팀 검토 주기를 통과하지 못하는 자산.
* 해당 자산과 비교하여 외부 팀에 자신들의 일을 대표할 더 나은 후보가 있다.

일반적으로 다음 클래스 자산은 DAM에 저장됩니다.

* 특정 성숙기에 도달했고 공유할 준비가 된 자산입니다.
* 크리에이티브 팀이 미리 선택한 자산입니다.
* 특정 계약이나 계약(예: RAW 파일에서 변환된 JPG 파일, PSD 원본에서 TIFF/이미지)에 따라 마케팅에서 사용하거나 요청한 특정 자산 형식.

#### 자산 업데이트가 DAM {#when-updates-to-assets-are-stored-in-dam}에 저장되는 경우

일반적으로, DAM 사용자 광범위한 세트와 관련된 자산만 DAM에 저장해야 합니다. 이렇게 하면 사용자(마케팅 및 유사한 기능)가 DAM 자산 타임라인에서 관련 버전만 볼 수 있습니다.

일반적으로 자산 라이프사이클의 주요 이정표에 관련된 변경 사항입니다. 예를 들어, 크리에이티브 팀이 제공하는 요청/검토를 기반으로 한 초기 마케팅 준비가 완료된 자산이나 공식 업데이트는 DAM에서 저장하고 버전을 지정해야 합니다.

DAM에서 기존 자산의 변경 요청 이후 마케팅 팀이 검토하도록 업데이트되는 크리에이티브 팀의 업데이트는 관련 업데이트의 예입니다. 추가 참조나 이전 버전으로 되돌리려면 DAM에서 저장 및 버전을 지정해야 합니다.

다음은 일반적으로 관련이 없는 업데이트의 예입니다.

* 마케팅 리뷰를 준비하기 전에 업로드된 자산의 이전 버전
* 크리에이티브 및 마케팅 팀이 자산이 준비되었다고 결정하기 전에 진행 중인 작업 단계에서 자산을 자주 크리에이티브 방식으로 변경합니다

### DAM {#user-access-to-dam}에 대한 사용자 액세스

[!DNL Assets] 에서는 배포에 대한 액세스 권한에 따라 두 가지 유형의 사용자를  [!DNL Assets] 지원합니다. 일반적으로 엔터프라이즈 네트워크(방화벽) 내의 사용자는 DAM에 직접 액세스할 수 있습니다. 엔터프라이즈 네트워크 외부의 다른 사용자는 직접 액세스할 수 없습니다. 사용자 유형은 기술 관점에서 사용할 수 있는 통합을 결정합니다.

#### DAM {#creative-users-with-direct-access-to-dam}에 직접 액세스할 수 있는 크리에이티브 사용자

일반적으로 내부 크리에이티브 팀 또는 내부 네트워크에 온보딩된 에이전시/크리에이티브 전문가가 [!DNL Experience Manager] 로그인을 포함하여 DAM 배포에 액세스할 수 있습니다. [!DNL Experience Manager] 또한 네트워크 인프라를 설정하여 외부 당사자에 직접 액세스할 수 있도록 설정할 수 있습니다. 대개 클라이언트를 위해 일하는 에이전시와 같이 신뢰할 수 있는 조직은 네트워크를  [!DNL Experience Manager] 통해 액세스할 수 있습니다. 예를 들면 VPN 또는 IP 허용 목록 등을 통해 액세스할 수 있습니다.

이러한 경우 Adobe 자산 링크 또는 [!DNL Experience Manager] 데스크탑 앱을 사용하면 최종/승인된 자산에 쉽게 액세스할 수 있고, 크리에이티브 자산을 DAM에 저장할 수 있습니다.

#### DAM {#creative-users-without-access-to-dam}에 액세스할 수 없는 크리에이티브 사용자

DAM 배포에 직접 액세스할 수 없는 외부 에이전시 및 프리랜서는 승인된 자산에 액세스해야 하거나 DAM에 새 디자인을 추가해야 할 수 있습니다.

다음 전략을 사용하여 최종/승인된 자산에 대한 액세스 권한을 제공합니다.

* Asset Link가 작동하지 않는 경우 데스크탑 앱을 사용합니다.
* 자산을 외부 파트너에게 안전하게 분배하려면 [Assets Brand Portal Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)을 사용하십시오
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)를 기반으로 하는 배포 및 소싱 포털의 사용자 지정 구현 사용
* [!DNL Experience Manager]에 설정된 액세스 제어 및 필요한 네트워크 인프라(예: VPN 및 IP 허용 목록)을 사용하여 외부 당사자에게 DAM의 전용 컨텐츠 영역에 액세스할 수 있도록 합니다. [!DNL Experience Manager] 웹 UI를 사용하여 자산을 가져오고 새 컨텐츠를 DAM에 업로드할 수 있습니다.

#### [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}의 자산에 대해 진행 중

이 문서에서 설명한 대로 로컬 파일에 모든 편집 내용을 저장하지 않고 작업 진행 중이라고도 하는 자산에 대한 주요 업데이트를 수행하는 것이 좋습니다. 또한 변경 사항으로 [!DNL Experience Manager]에도 업로드됩니다. 따라서 데스크탑 사용자의 작업 속도를 높이고, 사용되는 네트워크 대역폭을 제한하며, 자산 타임라인을 깔끔하고 제어된 주요 업데이트에 주력합니다.

Adobe 자산 링크는 이 사용 사례를 지원합니다.

* [!DNL Photoshop], [!DNL InDesign] 또는 [!DNL Illustrator]의 사용자가 파일을 편집하려고 하면 지정된 자산에서 체크아웃 작업을 실행합니다
* 자산이 백그라운드에서 다운로드되고, Creative Cloud 데스크탑 앱별로 디스크에 동기화된 사용자 Creative Cloud 계정에 배치되며, 체크아웃 플래그가 자산의 [!DNL Experience Manager]에 전환되어 편집 충돌을 최소화합니다
* 여기서 사용자는 동기화된 위치에 로컬로 저장된 파일에서 작업하며 필요한 빈도대로 필요한 변경 사항을 계속 작업하고 저장할 수 있습니다
* 또한, 자산이 Creative Cloud 계정에 있으므로 사용자가 보유하고 있는 다른 장치(예: 전용 Creative Cloud 모바일 앱에서 열거나 편집할 수 있음)에서도 사용할 수 있으며, 공동 작업을 위해 다른 Creative Cloud 사용자와 공유할 수 있습니다.
* 크리에이티브 사용자가 변경 작업을 완료하면 Creative Cloud 애플리케이션에서 해당 파일에 대한 체크 인 작업을 실행할 수 있으며 주석도 선택 가능합니다. [!DNL Experience Manager]의 해당 자산에 버전이 지정되고 새 바이너리로 업데이트됩니다. [!DNL Experience Manager] 마케터나 LOB 사용자와 같은 사용자는  [!DNL Experience Manager] 자산 타임라인 UI를 통해 주요 자산 변경 사항 또는 이정표에 액세스할 수 있습니다.

[!DNL Experience Manager] 데스크탑 앱에서는 기본 앱에서 열린 자산에 대한 네트워크 공유를 제공합니다. 기본적으로 로컬에서 수행한 모든 변경 사항은 잠시 후 자동으로 [!DNL Experience Manager]에 업로드됩니다. 이러한 구성을 사용하면 작업 진행 중 빈번한 저장 작업이 [!DNL Experience Manager]에 업로드되고 버전이 지정되므로, 네트워크 트래픽과 잠재적인 확장성 문제가 많이 발생하고, [!DNL Experience Manager]에서 불필요한 버전은 물론,

여기에서 권장되는 접근 방법은 [!DNL Experience Manager] 데스크탑 앱의 옵션을 사용하여 자동화된 업데이트를 비활성화하고, 변경 사항을 [!DNL Experience Manager]에 수동으로 업로드하여 앱의 자산 상태 UI에서 변경 사항 업로드 작업을 활용하는 것입니다.

#### DAM {#bulk-upload-to-dam}에 벌크 업로드

다음과 같은 일부 시나리오에서 많은 수의 파일을 동시에 DAM에 업로드해야 할 필요가 있을 수 있습니다.

* 사진 촬영 또는 더 큰 프로젝트의 결과 업로드
* 크리에이티브 에이전시에서 제공한 자산 업로드
* DAM 외부에서 선택 작업이 수행된 경우 더 큰 세트에서 선택한 자산 업로드

설명은 데스크탑 사용자 워크플로우의 일반적인 일부로서 파일을 작동(예: 매주 또는 모든 사진 촬영)하여 업로드하는 것을 의미합니다. 대규모 자산 마이그레이션은 여기에서 다루지 않습니다.

다음 업로드 기능을 활용할 수 있습니다.

* 대용량/계층 폴더를 벌크로 업로드하려면 [폴더 업로드](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem) 기능을 제공하는 [!DNL Experience Manager] 데스크탑 앱을 사용합니다. 계층 폴더 구조를 업로드할 수도 있습니다. [!DNL Assets] 업로드되므로 웹 브라우저 세션에 연결되어 있지 않습니다
* 단일 폴더에서 몇 개의 파일을 업로드하려면 파일을 웹 인터페이스로 직접 드래그하거나 [!DNL Assets] 웹 인터페이스에서 만들기 옵션을 사용합니다.
* 비즈니스 요구 사항에 따라 사용자 정의 업로더를 사용할 수도 있습니다.

#### 데스크탑에서 직접 디지털 자산 관리 {#managing-digital-assets-directly-from-desktop}

네트워크 파일 공유를 사용하여 디지털 자산을 관리하는 경우, [!DNL Experience Manager] 데스크탑 앱에서 매핑한 네트워크 공유를 사용하는 것만으로 편리한 대체용으로 볼 수 있습니다. 네트워크 파일 공유에서 전환할 때 [!DNL Experience Manager] 웹 인터페이스는 네트워크 공유(검색, 컬렉션, 메타데이터, 공동 작업, 미리 보기 등)에서 가능한 것 이상으로 풍부한 디지털 자산 관리 기능 세트를 제공하며, [!DNL Experience Manager] 데스크탑 앱은 서버측 DAM 저장소를 데스크탑의 작업과 연결하는 편리한 링크를 제공합니다.

[!DNL Experience Manager] 데스크탑 앱을 사용하여 [!DNL Assets]의 네트워크 공유에서 직접 자산을 관리하지 마십시오. 예를 들어 [!DNL Experience Manager] 데스크탑 앱을 사용하여 여러 파일을 이동/복사하지 마십시오. 대신 [!DNL Assets] 인터페이스를 사용하여 Finder/Explorer에서 네트워크 공유로 폴더를 드래그하거나 [!DNL Assets] 폴더 업로드 기능을 사용하십시오.

#### 자산 마이그레이션 {#asset-migration}

기존 시스템에서 새 시스템으로 자산 마이그레이션을 계획하거나 서버에 저장된 많은 자산의 마이그레이션을 실행하려면 [마이그레이션 안내서](/help/assets/assets-migration-guide.md)를 참조하십시오. [!DNL Experience Manager] 데스크탑 앱  [!DNL Experience Manager] 및  [!DNL Creative Cloud] 통합은 이러한 마이그레이션을 지원하지 않습니다. 수집할 자산의 양이 많고 메타데이터 매핑, 변환 및 섭취 관련 추가 요구 사항으로 인해 마이그레이션은 다양한 도구와 접근 방식을 사용하여 처리해야 합니다.

>[!MORELIKETHIS]
>
>* [Adobe 자산 링크](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Manager 데스크탑 앱 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Brand Portal Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager 및 Adobe Stock 통합](aem-assets-adobe-stock.md)

