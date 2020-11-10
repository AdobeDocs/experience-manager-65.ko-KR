---
title: Manage [!DNL Adobe Stock] assets
description: 내부에서 자산을 검색, 가져오기, 라이선스 부여 및 [!DNL Adobe Stock] 관리할 수 있습니다 [!DNL Adobe Experience Manager]. 라이선스가 부여된 자산을 다른 디지털 자산으로 사용하십시오.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 3%

---


# Use [!DNL Adobe Stock] assets in [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

조직은 엔터프라이즈 플랜과 [!DNL Adobe Stock] 통합하여 크리에이티브 및 마케팅 프로젝트 [!DNL Experience Manager Assets] 에서 라이선스가 부여된 에셋을 광범위한 에셋 관리 기능과 함께 사용할 수 있도록 할 수 있습니다. 강력한 에셋 관리 기능은 다음과 같습니다 [!DNL Experience Manager].

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다. [!DNL Experience Manager] 사용자는 [!DNL Adobe Stock] [!DNL Experience Manager][!DNL Experience Manager] 인터페이스 내에서 저장한 에셋을 신속하게 찾아 미리 보고 라이선스를 부여할 수 있습니다.

## 전제 조건 {#prerequisites}

통합을 위해서는 [ [!DNL Adobe Stock] 엔터프라이즈 플랜이 필요합니다](https://stockenterprise.adobe.com/).

## 통합 [!DNL Experience Manager] 및 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

에서 통신 [!DNL Experience Manager] 을 허용하려면 에서 IMS 구성 [!DNL Adobe Stock]과 구성을 [!DNL Adobe Stock] 만듭니다 [!DNL Experience Manager].

>[!NOTE]
>
>조직의 [!DNL Experience Manager] 관리자 및 [!DNL Admin Console] 관리자만 관리자 권한이 필요하므로 통합을 수행할 수 있습니다.

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. 만들기 **[!UICONTROL 를]** 클릭하고 **[!UICONTROL 클라우드 솔루션]** > **[!UICONTROL Adobe Stock을 선택합니다]**.
1. 기존 인증서를 재사용하거나 새 인증서 **[!UICONTROL 만들기를 선택합니다]**.
1. **[!UICONTROL 인증서 만들기]**&#x200B;를 클릭합니다. 생성된 공개 키를 다운로드합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 다운로드한 공개 키를 [!DNL Adobe Developer Console] 서비스 계정에 추가합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다. IMS [!UICONTROL 기술 계정 구성] 화면을 열어 값을 바로 제공할 수 있습니다.
1. Adobe 개발자 [콘솔에 액세스합니다](https://console.adobe.io). 통합이 필요한 조직에 대한 관리자 권한이 계정에 있는지 확인합니다.
1. 새 프로젝트 **[!UICONTROL 만들기를]** 클릭하고 **[!UICONTROL API 추가를 클릭합니다]**. 사용 가능한 API 목록에서 **[!UICONTROL Adobe Stock]** 를 선택합니다. OAUTH [!UICONTROL 2.0 Web을 선택합니다]. 표시된 다양한 값을 구성하고 복사합니다.
1. 제목, 권한 부여 서버 [!DNL Experience Manager] 라는 필드 **[!UICONTROL 에]** API 키 **[!UICONTROL ,]** API Client Secret **[!UICONTROL , 및 Facebook Payload라는 값을]**********&#x200B;입력합니다. 이러한 값에 대한 자세한 내용은 [JWT 인증 빠른 시작](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)을 참조하십시오.

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### 구성 [!DNL Adobe Stock] 을 [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. 에서 [!DNL Experience Manager]도구 **[!UICONTROL > Cloud Services]** **[!UICONTROL >]** Adobe Stock으로 **[!UICONTROL 이동합니다]**.
1. 만들기 **[!UICONTROL 를]** 클릭하여 구성을 만들고 기존 IMS 구성에 연결합니다. 환경 매개 변수 `PROD` 로 선택합니다.
1. 라이센스 **[!UICONTROL 자산 경로]** 필드에서 위치를 그대로 두십시오. 자산을 저장할 위치를 변경하지 [!DNL Adobe Stock] 마십시오.
1. 필요한 모든 속성을 추가하여 작성을 완료합니다. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.
1. 자산에 라이선스를 부여할 수 있는 사용자 또는 그룹을 추가합니다. [!DNL Experience Manager]

>[!NOTE]
>
>여러 [!DNL Adobe Stock] 구성이 있는 경우 [사용자 환경 설정] 패널에서 원하는 구성을 [!UICONTROL 선택합니다] . 홈 [!DNL Experience Manager] 페이지에서 패널에 액세스하려면 사용자 아이콘을 클릭한 다음 **[!UICONTROL 사용자 환경 설정]** > **[!UICONTROL 스톡 구성을 클릭합니다]**.

## 자산 사용 및 [!DNL Adobe Stock] 관리 [!DNL Experience Manager] {#usemanage}

조직은 이 기능을 사용하여 사용자가 자신의 [!DNL Adobe Stock] 자산을 사용하여 작업할 수 있도록 허용할 수 [!DNL Experience Manager Assets]있습니다. 사용자 인터페이스 내에서 [!DNL Experience Manager] [!DNL Adobe Stock] 사용자는 자산을 검색하고 필요한 자산의 라이선스를 부여할 수 있습니다.

에셋에 라이선스가 부여되면 일반적인 에셋처럼 사용하고 관리할 수 [!DNL Adobe Stock] [!DNL Experience Manager]있습니다. 에서 [!DNL Experience Manager]사용자는 자산을 검색하고 미리 볼 수 있습니다.자산 복사 및 게시;자산을 공유할 수 [!DNL Brand Portal]있습니다.데스크탑 앱을 통해 에셋 액세스 및 [!DNL Experience Manager] 사용다양한 기능을 사용할 수 있습니다.

![작업 공간에서 [!DNL Adobe Stock] 자산 검색 및 결과 [!DNL Adobe Experience Manager] 필터링](assets/adobe-stock-search-results-workspace.png)

*그림:인터페이스에서 자산 [!DNL Adobe Stock] 을 검색하고 결과를 필터링합니다 [!DNL Experience Manager] .*

**A.** ID가 제공되는 자산과 유사한 [!DNL Adobe Stock] 자산을 검색합니다. **B.** 선택한 모양 또는 방향과 일치하는 에셋을 검색합니다. **C.** C. **D.** Open 또는 **D.** 지원되는 자산 유형 중 하나를 검색하십시오. [!DNL Experience Manager] 라이센스와 선택한 자산을 창 **에 저장합니다.** 워터마크 [!DNL Experience Manager] 가 있는 F.Save 자산을 저장합니다.F.E **의 워터마크E와 함께 저장합니다.G는 선택한 자산이 비슷한 웹 사이트의 자산을 탐색합니다.** [!DNL Adobe Stock] **** [!DNL Adobe Stock] **** **** 선택한 웹 사이트에서 선택한 자산을 축소합니다.H. 검색 결과 - 카드 보기 및 카드 목록 보기 간 J.Switch

### 자산 찾기 {#find-assets}

사용자 [!DNL Experience Manager] 는 및 모두에서 자산을 검색할 수 [!DNL Experience Manager] 있습니다 [!DNL Adobe Stock]. 검색 위치가 다음으로 제한되지 않으면 [!DNL Adobe Stock]검색 결과 [!DNL Experience Manager] 가 표시되고 [!DNL Adobe Stock] 표시됩니다.

* 자산을 검색하려면 [!DNL Adobe Stock] 탐색 **[!UICONTROL >]** 자산 **** > Adobe Stock ****&#x200B;검색을 클릭합니다.

* 여러 [!DNL Adobe Stock] 가지 [!DNL Experience Manager Assets]에서 자산을 검색하려면 ![검색을 클릭합니다](assets/do-not-localize/search_icon.png).

또는 검색 막대 `Location: Adobe Stock` 에 입력하기 시작하여 자산을 [!DNL Adobe Stock] 선택합니다. [!DNL Experience Manager] 검색된 자산에 고급 필터링 기능을 제공하여 지원되는 에셋 유형, 이미지 방향 및 라이선스 상태 등의 필터를 사용하여 필요한 에셋을 신속하게 이용할 수 있습니다.

>[!NOTE]
>
>검색된 자산 [!DNL Adobe Stock] [!DNL Experience Manager]은 [!DNL Adobe Stock] 에셋은 사용자가 에셋 [!DNL Experience Manager] 또는 [라이선스를](/help/assets/aem-assets-adobe-stock.md#saveassets) 저장하고 에셋을 저장한 후에만 보관됩니다 [](/help/assets/aem-assets-adobe-stock.md#licenseassets). 이미 저장된 에셋이 [!DNL Experience Manager] 표시되고 강조 표시되므로 쉽게 참조하고 액세스할 수 있습니다. 또한, [!DNL Stock] 자산은 소스를 나타내는 일부 추가 메타데이터와 함께 저장됩니다 [!DNL Stock].

![검색 결과에서 검색 필터 [!DNL Experience Manager] 와 강조 표시된 [!DNL Adobe Stock] 자산](assets/aem-search-filters2.jpg)

*그림:검색 결과에서 필터 [!DNL Experience Manager] 와 강조 표시된 [!DNL Adobe Stock] 에셋을 검색합니다.*

### 필요한 자산 저장 및 보기 {#saveassets}

저장할 자산을 선택합니다 [!DNL Experience Manager]. 상단에 있는 [!UICONTROL 도구 모음에서 저장을] 클릭하고 자산의 이름과 위치를 입력합니다. 라이센스가 없는 에셋은 워터마크를 사용하여 로컬에 저장됩니다.

다음 번에 에셋을 검색할 때 저장된 에셋이 배지로 강조 표시되어 해당 에셋을 사용할 수 있음을 나타냅니다 [!DNL Experience Manager Assets].

>[!NOTE]
>
>최근에 추가된 에셋에는 라이선스 배지 대신 새 배지가 표시됩니다.

### 라이선스 에셋 {#licenseassets}

사용자는 기업 계획의 할당량을 사용하여 [!DNL Adobe Stock] 자산에 대한 라이선스를 부여할 수 [!DNL Adobe Stock] 있습니다. 에셋에 라이선스를 부여하면 워터마크 없이 저장되며 에서 검색하고 사용할 수 있습니다 [!DNL Experience Manager Assets].

![에셋에 라이선스를 부여하고 저장할 수 있는 대화 [!DNL Adobe Stock] 상자 [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*그림:에셋에 라이선스를 부여하고 저장할 수 있는 대화 [!DNL Adobe Stock] 상자 [!DNL Experience Manager Assets].*

### 메타데이터 및 자산 속성 액세스 {#access-metadata-and-asset-properties}

사용자는 에셋에 저장된 에셋의 [!DNL Adobe Stock] 메타데이터 속성을 비롯한 메타데이터에 액세스하고 미리 볼 수 [!DNL Experience Manager]있으며 **[!UICONTROL 에셋에 대한 라이센스 참조]** 사항을 추가할 수 있습니다. 그러나 라이선스 참조에 대한 업데이트는 [!DNL Experience Manager] 웹 사이트와 [!DNL Adobe Stock] 웹 사이트 간에 동기화되지 않습니다.

사용자는 라이선스가 부여된 에셋과 라이선스가 없는 에셋의 속성을 볼 수 있습니다.

![저장된 에셋의 메타데이터 및 라이선스 참조 보기 및 액세스](assets/metadata_properties.jpg)

*그림:저장된 에셋의 메타데이터 및 라이선스 참조를 보고 액세스합니다.*

## 알려진 제한 사항 {#known-limitations}

* **편집 이미지 경고가 표시되지 않습니다**.이미지 라이선스를 부여할 때 이미지가 편집 전용 이미지인지 확인할 수 없습니다. 오용 가능성을 방지하기 위해 관리자는 Admin Console에서 편집 자산에 대한 액세스를 끌 수 있습니다.

* **잘못된 라이선스 유형이 표시됩니다**.에셋에 대해 잘못된 라이선스 유형 [!DNL Experience Manager] 이 표시될 수 있습니다. 사용자는 [!DNL Adobe Stock] 웹 사이트에 로그인하여 라이센스 유형을 볼 수 있습니다.

* **참조 필드 및 메타데이터는 동기화되지 않습니다**.사용자가 라이센스 참조 필드를 업데이트하면 라이센스 참조 정보가 웹 사이트 [!DNL Experience Manager] 에서 업데이트되지만 [!DNL Adobe Stock] 웹 사이트에서는 업데이트되지 않습니다. 마찬가지로 사용자가 웹 사이트의 참조 필드를 업데이트하면 [!DNL Adobe Stock] 업데이트가 에서 동기화되지 않습니다 [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [에셋을 [!DNL Adobe Stock] 사용하는 방법에 대한 비디오 자습서 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] 엔터프라이즈 플랜 도움말](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/stock/faq.html)

