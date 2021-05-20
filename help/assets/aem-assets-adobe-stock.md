---
title: 자산 관리 [!DNL Adobe Stock] 자산
description: ' [!DNL Adobe Experience Manager] 내에서 자산을 검색, 가져오기, 라이선스 및 관리합니다.  [!DNL Adobe Stock]  라이선스가 있는 자산을 다른 디지털 자산으로 사용합니다.'
contentOwner: AG
feature: 검색, Adobe Stock
role: Business Practitioner, Administrator
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
source-git-commit: a7a9a31364497ab67d805e45ba4fa03c927828ed
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}에서 [!DNL Adobe Stock] 자산 사용

조직은 [!DNL Adobe Stock] 엔터프라이즈 플랜을 [!DNL Experience Manager Assets]과 통합하여 라이선스가 있는 자산이 광고 및 마케팅 프로젝트에 폭넓게 사용 가능하고 [!DNL Experience Manager] 의 강력한 자산 관리 기능이 있는지 확인할 수 있습니다.

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다. [!DNL Experience Manager] 사용자는 인터페이스를 종료하지 않고도  [!DNL Adobe Stock] 에 저장된 자산을 빠르게 찾고, 미리 보고, 라이선스를 제공할  [!DNL Experience Manager]수  [!DNL Experience Manager] 있습니다.

## 전제 조건 {#prerequisites}

통합에는 [enterprise [!DNL Adobe Stock] 계획](https://stockenterprise.adobe.com/)이 필요합니다.

## [!DNL Experience Manager] 및 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock} 통합

[!DNL Experience Manager] 과 [!DNL Adobe Stock] 간의 통신을 허용하려면 [!DNL Experience Manager]에서 IMS 구성과 [!DNL Adobe Stock] 구성을 만드십시오.

>[!NOTE]
>
>조직에 대한 [!DNL Experience Manager] 관리자 및 [!DNL Admin Console] 관리자만 관리자 권한이 필요하므로 통합을 수행할 수 있습니다.

### IMS 구성 {#create-an-ims-configuration} 만들기

1. [!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL Adobe IMS 구성]**&#x200B;으로 이동합니다. **[!UICONTROL 만들기]**&#x200B;를 클릭하고 **[!UICONTROL 클라우드 솔루션]** > **[!UICONTROL Adobe Stock]**&#x200B;을 선택합니다.
1. 기존 인증서를 재사용하거나 **[!UICONTROL 새 인증서 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 인증서 만들기]**&#x200B;를 클릭합니다. 만든 후 공개 키를 다운로드합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다. [!UICONTROL Adobe IMS 기술 계정 구성] 화면을 열어 필요한 값을 곧 제공할 수 있습니다.
1. [Adobe 개발자 콘솔](https://console.adobe.io)에 액세스합니다. 통합이 필요한 조직에 대한 관리자 권한이 계정에 있는지 확인합니다.
1. **[!UICONTROL 새 프로젝트 만들기]**&#x200B;를 클릭하고 **[!UICONTROL API 추가]**&#x200B;를 클릭합니다. 사용 가능한 API 목록에서 **[!UICONTROL Adobe Stock]**&#x200B;을 선택합니다. [!UICONTROL OAUTH 2.0 Web]을 선택합니다.
1. **[!UICONTROL 기본 리디렉션 URI]** 및 **[!UICONTROL 리디렉션 URI 패턴]** 값을 제공합니다. **[!UICONTROL 구성된 API 저장]**&#x200B;을 클릭합니다. 생성된 ID와 암호를 복사합니다.
1. [!UICONTROL Adobe IMS 기술 계정 구성] 화면에서 **[!UICONTROL 제목]**, **[!UICONTROL 인증 서버]**, **[!UICONTROL API 키]**, **[!UICONTROL 클라이언트 암호]** 및 **[!UICONTROL 페이로드]**&#x200B;라는 상자에 값을 제공합니다. 이러한 값에 대한 자세한 내용은 [JWT 인증 빠른 시작](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)을 참조하십시오.

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}에서 [!DNL Adobe Stock] 구성을 만듭니다

1. [!DNL Experience Manager]도구&#x200B;]**>**[!UICONTROL  Cloud Services ]**>**[!UICONTROL  Adobe Stock ]**로 이동합니다.**[!UICONTROL 
1. **[!UICONTROL 만들기]**&#x200B;를 클릭하여 구성을 만들고 기존 IMS 구성과 연결합니다. `PROD` 을 환경 매개 변수로 선택합니다.
1. **[!UICONTROL 라이선스가 있는 자산 경로]** 필드에서 위치를 그대로 둡니다. [!DNL Adobe Stock] 자산을 저장할 위치를 변경하지 마십시오.
1. 필요한 모든 속성을 추가하여 만들기를 완료합니다. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.
1. 자산의 라이선스를 제공할 수 있는 [!DNL Experience Manager] 사용자 또는 그룹을 추가합니다.

>[!NOTE]
>
>[!DNL Adobe Stock] 구성이 여러 개 있는 경우 [!UICONTROL 사용자 환경 설정] 패널에서 원하는 구성을 선택합니다. [!DNL Experience Manager] 홈 페이지에서 패널에 액세스하려면 사용자 아이콘을 클릭한 다음 **[!UICONTROL 사용자 환경 설정]** > **[!UICONTROL Stock 구성]**&#x200B;을 클릭합니다.

## [!DNL Experience Manager]에서 [!DNL Adobe Stock] 자산 사용 및 관리 {#usemanage}

이 기능을 사용하면 조직에서 해당 사용자가 [!DNL Experience Manager Assets]에서 [!DNL Adobe Stock] 자산을 사용하여 작업할 수 있도록 허용할 수 있습니다. [!DNL Experience Manager] 사용자 인터페이스 내에서 사용자는 [!DNL Adobe Stock] 자산을 검색하고 필요한 자산에 대한 라이선스를 제공할 수 있습니다.

[!DNL Adobe Stock] 자산이 [!DNL Experience Manager]에서 라이선스가 부여되면 일반적인 자산처럼 사용하고 관리할 수 있습니다. [!DNL Experience Manager]에서 사용자는 자산을 검색하고 미리 볼 수 있습니다.자산을 복사하여 게시합니다.[!DNL Brand Portal]에서 자산 공유[!DNL Experience Manager] 데스크탑 앱을 통해 자산에 액세스하고 사용합니다.기타.

![작업  [!DNL Adobe Stock] 공간에서 자산 검색 및 결과  [!DNL Adobe Experience Manager] 필터링](assets/adobe-stock-search-results-workspace.png)

*그림:인터페이스에서  [!DNL Adobe Stock] 자산을 검색하고 결과를  [!DNL Experience Manager] 필터링합니다.*

**A.** ID가 제공된 자산과 유사한  [!DNL Adobe Stock] 자산을 검색합니다. **B.** 선택한 모양 또는 방향과 일치하는 자산을 검색합니다. **C.** 지원되는 자산 유형 중 하나 검색  **D.**  필터 창 열기 또는 축소  **예**  라이선스 및 선택한 자산을  [!DNL Experience Manager] **F에 저장** 워터마크  [!DNL Experience Manager] G. **선택한 자산과 유사한** 웹 사이트에서 자산 탐색 [!DNL Adobe Stock] H. **** 웹 사이트에서 선택한 자산 보기 [!DNL Adobe Stock] 웹 사이트 **I.** 검색 결과  **J.** 카드 보기와 목록 보기 간에 선택한 자산 수J.스위치

### 자산 찾기 {#find-assets}

[!DNL Experience Manager] 사용자는 [!DNL Experience Manager] 및 [!DNL Adobe Stock]에서 자산을 검색할 수 있습니다. 검색 위치가 [!DNL Adobe Stock]으로 제한되지 않으면 [!DNL Experience Manager] 및 [!DNL Adobe Stock]의 검색 결과가 표시됩니다.

* [!DNL Adobe Stock] 자산을 검색하려면 **[!UICONTROL 탐색]** > **[!UICONTROL 자산]** > **[!UICONTROL Adobe Stock]**&#x200B;을 클릭합니다.

* [!DNL Adobe Stock] 및 [!DNL Experience Manager Assets]에서 자산을 검색하려면 ![검색](assets/do-not-localize/search_icon.png)을 클릭합니다.

또는 검색 막대에 `Location: Adobe Stock` 을 입력하여 [!DNL Adobe Stock] 자산을 선택합니다. [!DNL Experience Manager] 에서는 검색된 자산에 고급 필터링 기능을 제공하여 사용자가 지원되는 자산 유형, 이미지 방향 및 라이선스가 있는 상태 등의 필터를 사용하여 필요한 자산을 빠르게 작성할 수 있도록 합니다.

>[!NOTE]
>
>[!DNL Adobe Stock]에서 검색된 자산은 [!DNL Experience Manager]에 표시됩니다. [!DNL Adobe Stock] 자산을 가져와서 사용자가 자산  [!DNL Experience Manager] 라이선스를  [저장하고 자산](/help/assets/aem-assets-adobe-stock.md#saveassets) 을  [저장한 후에만 저장소에 저장됩니다](/help/assets/aem-assets-adobe-stock.md#licenseassets). 쉽게 참조하고 액세스할 수 있도록 [!DNL Experience Manager]에 이미 저장된 자산이 표시되고 강조 표시됩니다. 또한 [!DNL Stock] 자산은 소스를 [!DNL Stock](으)로 나타내기 위해 일부 추가 메타데이터와 함께 저장됩니다.

![검색 결과에서  [!DNL Experience Manager] 및 강조 표시된  [!DNL Adobe Stock] 자산 검색 필터](assets/aem-search-filters2.jpg)

*그림:검색 결과에서 필터  [!DNL Experience Manager] 및 강조 표시된  [!DNL Adobe Stock] 자산을 검색합니다.*

### 필요한 자산을 저장하고 봅니다 {#saveassets}

[!DNL Experience Manager]에 저장할 자산을 선택합니다. 맨 위의 도구 모음에서 [!UICONTROL 저장] 을 클릭하고 자산의 이름과 위치를 제공합니다. 라이센스가 없는 자산은 워터마크로 로컬에 저장됩니다.

다음번에 자산을 검색할 때 저장된 자산이 배지로 강조 표시되어 이러한 자산을 [!DNL Experience Manager Assets]에서 사용할 수 있음을 나타냅니다.

>[!NOTE]
>
>최근에 추가된 자산에 라이센스 배지 대신 새 배지가 표시됩니다.

### 자산 라이선스 {#licenseassets}

사용자는 [!DNL Adobe Stock] 엔터프라이즈 계획의 할당량을 사용하여 [!DNL Adobe Stock] 자산에 대한 라이선스를 제공할 수 있습니다. 자산에 대한 라이선스를 부여하면 워터마크 없이 저장되며 [!DNL Experience Manager Assets]에서 검색하고 사용할 수 있습니다.

![자산에 라이센스를 부여하고 저장하는 대화  [!DNL Adobe Stock] 상자  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*그림:대화 상자에서 자산에 라이선스를  [!DNL Adobe Stock] 부여하고 저장할 수  [!DNL Experience Manager Assets]있습니다.*

### 메타데이터 및 자산 속성 {#access-metadata-and-asset-properties} 액세스

사용자는 [!DNL Experience Manager]에 저장된 자산에 대한 [!DNL Adobe Stock] 메타데이터 속성을 포함하여 메타데이터에 액세스하고 미리 볼 수 있으며, 자산에 대해 **[!UICONTROL 라이센스 참조]**&#x200B;를 추가할 수 있습니다. 그러나 라이센스 참조에 대한 업데이트는 [!DNL Experience Manager] 웹 사이트와 [!DNL Adobe Stock] 웹 사이트 간에 동기화되지 않습니다.

사용자는 라이선스가 있는 자산과 라이선스가 없는 자산 모두에 대한 속성을 볼 수 있습니다.

![저장된 자산의 메타데이터 및 라이선스 참조를 보고 액세스합니다](assets/metadata_properties.jpg)

*그림:저장된 자산의 메타데이터 및 라이선스 참조를 보고 액세스합니다.*

## 알려진 제한 사항 {#known-limitations}

* **편집 이미지 경고가 표시되지 않습니다**.이미지에 라이센스를 부여할 때 이미지가 편집 전용 인지 확인할 수 없습니다. 관리 관리자는 Admin Console에서 편집 자산에 대한 액세스를 중단할 수 있습니다.

* **잘못된 라이센스 유형이 표시됩니다**.자산에 대해 잘못된 라이선스 유형이  [!DNL Experience Manager] 에 표시될 수 있습니다. 사용자는 [!DNL Adobe Stock] 웹 사이트에 로그인하여 라이센스 유형을 확인할 수 있습니다.

* **참조 필드 및 메타데이터가 동기화되지 않습니다**.사용자가 라이센스 참조 필드를 업데이트하면 라이센스 참조 정보가 웹 사이트 [!DNL Experience Manager] 에서 업데이트되지만 웹 사이트에서는 업데이트되지  [!DNL Adobe Stock] 않습니다. 마찬가지로, 사용자가 [!DNL Adobe Stock] 웹 사이트의 참조 필드를 업데이트하면 업데이트가 [!DNL Experience Manager]에서 동기화되지 않습니다.

>[!MORELIKETHIS]
>
>* [와 함께 자산을  [!DNL Adobe Stock] 사용하는 방법에 대한 비디오 자습서 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] 엔터프라이즈 플랜 도움말](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/stock/faq.html)

