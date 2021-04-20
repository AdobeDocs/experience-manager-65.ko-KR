---
title: ' [!DNL Adobe Stock] 자산 관리'
description: ' [!DNL Adobe Experience Manager] 내에서  [!DNL Adobe Stock] 자산을 검색, 가져오기, 라이센스 부여 및 관리합니다. 라이선스가 부여된 자산을 다른 디지털 자산으로 사용하십시오.'
contentOwner: AG
feature: Search, Adobe Stock
role: Business Practitioner, Administrator
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
translation-type: tm+mt
source-git-commit: a7a9a31364497ab67d805e45ba4fa03c927828ed
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}에서 [!DNL Adobe Stock] 에셋 사용

조직은 [!DNL Adobe Stock] 엔터프라이즈 플랜을 [!DNL Experience Manager Assets]과 통합하여 라이선스 에셋을 크리에이티브 및 마케팅 프로젝트에 광범위하게 사용할 수 있도록 하고 [!DNL Experience Manager]의 강력한 에셋 관리 기능을 활용할 수 있습니다.

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다. [!DNL Experience Manager] 사용자는 인터페이스를 종료하지 않고도  [!DNL Adobe Stock] 저장된 에셋을 신속하게 검색하고 미리 보고 라이선스를 부여할  [!DNL Experience Manager]수  [!DNL Experience Manager] 있습니다.

## 전제 조건 {#prerequisites}

통합에는 [enterprise [!DNL Adobe Stock] 계획](https://stockenterprise.adobe.com/)이 필요합니다.

## [!DNL Experience Manager] 및 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock} 통합

[!DNL Experience Manager]과 [!DNL Adobe Stock] 간의 통신을 허용하려면 [!DNL Experience Manager]에서 IMS 구성과 [!DNL Adobe Stock] 구성을 만듭니다.

>[!NOTE]
>
>조직에 대한 [!DNL Experience Manager] 관리자와 [!DNL Admin Console] 관리자만 관리자 권한이 필요하므로 통합을 수행할 수 있습니다.

### IMS 구성 {#create-an-ims-configuration} 만들기

1. [!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL Adobe IMS 구성]**&#x200B;으로 이동합니다. **[!UICONTROL 만들기]**&#x200B;를 클릭하고 **[!UICONTROL 클라우드 솔루션]** > **[!UICONTROL Adobe Stock]**&#x200B;을 선택합니다.
1. 기존 인증서를 재사용하거나 **[!UICONTROL 새 인증서 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 인증서 만들기]**&#x200B;를 클릭합니다. 만든 후 공개 키를 다운로드합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다. [!UICONTROL Adobe IMS 기술 계정 구성] 화면을 열어 필요한 값을 곧 제공할 수 있습니다.
1. [Adobe 개발자 콘솔](https://console.adobe.io)에 액세스합니다. 통합이 필요한 조직에 대한 관리자 권한이 계정에 있는지 확인합니다.
1. **[!UICONTROL 새 프로젝트 만들기]**&#x200B;를 클릭하고 **[!UICONTROL API 추가]**&#x200B;를 클릭합니다. 사용 가능한 API 목록에서 **[!UICONTROL Adobe Stock]**&#x200B;을 선택합니다. [!UICONTROL OAUTH 2.0 Web]을 선택합니다.
1. **[!UICONTROL 기본 리디렉션 URI]** 및 **[!UICONTROL 리디렉션 URI 패턴]** 값을 제공합니다. **[!UICONTROL 구성된 API 저장]**&#x200B;을 클릭합니다. 생성된 ID 및 암호를 복사합니다.
1. [!UICONTROL Adobe IMS. 기술 계정 구성] 화면에서 **[!UICONTROL 제목]**, **[!UICONTROL 인증 서버]**, **[!UICONTROL API 키]**, **[!UICONTROL 클라이언트 암호]** 및 **[!UICONTROL 페이로드]**. 이러한 값에 대한 자세한 내용은 [JWT 인증 빠른 시작](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)을 참조하십시오.

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}에서 [!DNL Adobe Stock] 구성 만들기

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**&#x200B;으로 이동합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭하여 구성을 만들고 기존 IMS 구성과 연결합니다. 환경 매개 변수로 `PROD`을 선택합니다.
1. **[!UICONTROL 라이센스 자산 경로]** 필드에서 위치를 그대로 두십시오. [!DNL Adobe Stock] 자산을 저장할 위치를 변경하지 마십시오.
1. 필요한 모든 속성을 추가하여 작성을 완료합니다. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.
1. 자산에 라이선스를 부여할 수 있는 [!DNL Experience Manager] 사용자 또는 그룹을 추가합니다.

>[!NOTE]
>
>[!DNL Adobe Stock] 구성이 여러 개 있는 경우 [!UICONTROL 사용자 환경 설정] 패널에서 원하는 구성을 선택합니다. [!DNL Experience Manager] 홈 페이지에서 패널에 액세스하려면 사용자 아이콘을 클릭한 다음 **[!UICONTROL 사용자 환경 설정]** > **[!UICONTROL Stock 구성]**&#x200B;을 클릭합니다.

## [!DNL Experience Manager] {#usemanage}에서 [!DNL Adobe Stock] 에셋 사용 및 관리

조직은 이 기능을 사용하여 사용자가 [!DNL Experience Manager Assets]의 [!DNL Adobe Stock] 자산을 사용하여 작업하도록 허용할 수 있습니다. [!DNL Experience Manager] 사용자 인터페이스 내에서 사용자는 [!DNL Adobe Stock] 자산을 검색하고 필요한 자산에 라이선스를 부여할 수 있습니다.

[!DNL Adobe Stock] 에셋에 라이선스가 부여되면 일반 자산처럼 사용하고 관리할 수 있습니다. [!DNL Experience Manager] [!DNL Experience Manager]에서는 사용자가 자산을 검색하고 미리 볼 수 있습니다.에셋 복사 및 게시;[!DNL Brand Portal];에서 자산 공유[!DNL Experience Manager] 데스크탑 앱을 통해 에셋 액세스 및 사용;기타 여러 가지 기능.

![작업 영역에서  [!DNL Adobe Stock] 에셋 검색 및 결과  [!DNL Adobe Experience Manager] 필터링](assets/adobe-stock-search-results-workspace.png)

*그림:인터페이스에서  [!DNL Adobe Stock] 자산을 검색하고 결과를  [!DNL Experience Manager] 필터링합니다.*

**A.** ID가 제공되는 자산과 유사한  [!DNL Adobe Stock] 자산을 검색합니다. **B. 선택한 모양 또는 방향과 일치하는 에셋을** 검색합니다. **C.** 지원되는 자산 유형  **D.** D.Open 또는 필터 중 하나 검색E. **E.License를** 검색하고 선택한 자산을 F.F. [!DNL Experience Manager] **F.F.F.F.** 선택한 자산에 저장 워터마크K를 사용하여 자산 저장G.J.웹 사이트에서 선택한 자산 탐색H와 유사한 에셋를 선택합니다. 선택한 에셋 탐색H선택한 에셋를 선택한 에셋 [!DNL Experience Manager]   ****   [!DNL Adobe Stock]   ****   [!DNL Adobe Stock]   ****   **** 를 선택한 에셋를 선택한 에셋를 선택한 에셋N를 선택한NNHN를NNNNNNNN.View검색 결과에서 선택한 자산 번호J.List카드 보기 및 목록 간 전환

### 자산 {#find-assets} 찾기

[!DNL Experience Manager] 사용자는 [!DNL Experience Manager] 및 [!DNL Adobe Stock]의 두 가지 모두에서 자산을 검색할 수 있습니다. 검색 위치가 [!DNL Adobe Stock]으로 제한되지 않으면 [!DNL Experience Manager] 및 [!DNL Adobe Stock]의 검색 결과가 표시됩니다.

* [!DNL Adobe Stock] 자산을 검색하려면 **[!UICONTROL 탐색]** > **[!UICONTROL 자산]** > **[!UICONTROL Adobe Stock 검색]**&#x200B;을 클릭합니다.

* [!DNL Adobe Stock] 및 [!DNL Experience Manager Assets]에서 자산을 검색하려면 ![검색](assets/do-not-localize/search_icon.png)을 클릭합니다.

또는 검색 표시줄에 `Location: Adobe Stock`을 입력하여 [!DNL Adobe Stock] 자산을 선택합니다. [!DNL Experience Manager] 검색된 자산에 고급 필터링 기능을 제공하여 지원되는 에셋 유형, 이미지 방향 및 라이선스 상태 등의 필터를 사용하여 필요한 에셋을 신속하게 0으로 필터링할 수 있습니다.

>[!NOTE]
>
>[!DNL Adobe Stock]에서 검색된 자산은 [!DNL Experience Manager]에 표시됩니다. [!DNL Adobe Stock] 에셋은 사용자가 에셋 또는  [!DNL Experience Manager] 라이선스를  [저장하고 에셋](/help/assets/aem-assets-adobe-stock.md#saveassets) 을  [저장한 후에만 보관됩니다](/help/assets/aem-assets-adobe-stock.md#licenseassets). 참조와 액세스가 용이하도록 [!DNL Experience Manager]에 이미 저장된 에셋이 표시되고 강조 표시됩니다. 또한 [!DNL Stock] 에셋은 소스를 [!DNL Stock]으로 나타내기 위해 일부 추가 메타데이터와 함께 저장됩니다.

![검색 결과에서 검색 필터  [!DNL Experience Manager] 및 강조 표시된  [!DNL Adobe Stock] 에셋 검색](assets/aem-search-filters2.jpg)

*그림:검색 결과에서 검색 필터 [!DNL Experience Manager] 와 강조 표시된  [!DNL Adobe Stock] 에셋을 검색합니다.*

### 필요한 자산 {#saveassets} 저장 및 보기

[!DNL Experience Manager]에 저장할 자산을 선택합니다. 맨 위의 도구 모음에서 [!UICONTROL 저장]을 클릭하고 자산의 이름과 위치를 입력합니다. 라이선스가 없는 에셋은 워터마크와 함께 로컬에 저장됩니다.

다음 번에 에셋을 검색할 때 저장된 에셋은 [!DNL Experience Manager Assets]에서 해당 에셋을 사용할 수 있음을 나타내는 배지로 강조 표시됩니다.

>[!NOTE]
>
>최근에 추가된 에셋에는 라이선스 배지 대신 새 배지가 표시됩니다.

### 라이선스 에셋 {#licenseassets}

사용자는 [!DNL Adobe Stock] 엔터프라이즈 플랜의 할당량을 사용하여 [!DNL Adobe Stock] 자산에 라이선스를 부여할 수 있습니다. 에셋에 라이선스를 부여하면 워터마크 없이 저장되며 [!DNL Experience Manager Assets]에서 검색하고 사용할 수 있습니다.

![에셋에 라이선스를 부여하고 저장할  [!DNL Adobe Stock] 대화 상자  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*그림:에셋에 라이선스를 부여하고 저장할  [!DNL Adobe Stock] 수 있는 대화  [!DNL Experience Manager Assets]상자*

### 메타데이터 및 자산 속성 {#access-metadata-and-asset-properties} 액세스

사용자는 [!DNL Experience Manager]에 저장된 에셋에 대한 [!DNL Adobe Stock] 메타데이터 속성을 비롯한 메타데이터를 액세스하고 미리 볼 수 있으며 에셋에 대해 **[!UICONTROL 라이선스 참조]**&#x200B;를 추가할 수 있습니다. 그러나 라이선스 참조에 대한 업데이트는 [!DNL Experience Manager]과 [!DNL Adobe Stock] 웹 사이트 간에 동기화되지 않습니다.

사용자는 라이선스가 부여된 에셋과 라이선스가 없는 에셋 모두에 대한 속성을 볼 수 있습니다.

![저장된 에셋의 메타데이터 및 라이선스 참조 보기 및 액세스](assets/metadata_properties.jpg)

*그림:저장된 에셋의 메타데이터 및 라이선스 참조를 보고 액세스합니다.*

## 알려진 제한 사항 {#known-limitations}

* **편집 이미지 경고가 표시되지 않습니다**.이미지 라이선스를 부여할 때 이미지가 편집 전용 이미지인지 확인할 수 없습니다. 악용 가능성을 방지하기 위해 관리자는 Admin Console에서 편집 자산에 대한 액세스를 끌 수 있습니다.

* **잘못된 라이센스 유형이 표시됩니다**.에셋에 대해 잘못된 라이선스 유형 [!DNL Experience Manager] 이 표시될 수 있습니다. 사용자는 [!DNL Adobe Stock] 웹 사이트에 로그인하여 라이센스 유형을 확인할 수 있습니다.

* **참조 필드 및 메타데이터는 동기화되지** 않습니다.사용자가 라이센스 참조 필드를 업데이트하면 라이센스 참조 정보가 웹 사이트 [!DNL Experience Manager] 에서 업데이트되지만 웹 사이트에서는 업데이트되지  [!DNL Adobe Stock] 않습니다. 마찬가지로 사용자가 [!DNL Adobe Stock] 웹 사이트의 참조 필드를 업데이트하면 업데이트가 [!DNL Experience Manager]에서 동기화되지 않습니다.

>[!MORELIKETHIS]
>
>* [자산 사용에 대한 비디오  [!DNL Adobe Stock] 자습서 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] 엔터프라이즈 플랜 도움말](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/stock/faq.html)

