---
title: AEM 자산에서 Adobe Stock 자산 관리
description: AEM 내에서 Adobe Stock 에셋을 검색, 가져오기, 라이선스 부여 및 관리할 수 있습니다. 라이선스가 부여된 에셋을 다른 디지털 에셋으로 사용할 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68fb4c08b8093ff50e74dc9e29011325cdf7e7d7

---


# AEM Assets에서 Adobe Stock 자산 사용 {#use-adobe-stock-assets-in-aem-assets}

조직은 Adobe Stock 엔터프라이즈 플랜과 AEM Assets를 통합하여 AEM의 강력한 에셋 관리 기능을 통해 라이선스가 부여된 에셋을 크리에이티브 및 마케팅 프로젝트에 광범위하게 사용할 수 있도록 할 수 있습니다.

Adobe Stock 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다. AEM 사용자는 AEM 작업 영역을 벗어나지 않고도 AEM에 저장된 Adobe Stock 에셋을 신속하게 검색하고 미리 보고 라이선스를 부여할 수 있습니다.

## 전제 조건 {#prerequisites}

통합을 사용하려면 [엔터프라이즈 Adobe Stock 플랜](https://stockenterprise.adobe.com/) 및 AEM 6.5 이상이 필요합니다. AEM 6.5 서비스 팩 세부 정보는 이 [릴리스 노트를](/help/release-notes/sp-release-notes.md)참조하십시오.

## AEM 및 Adobe Stock 통합 {#integrate-aem-and-adobe-stock}

AEM과 Adobe Stock 간의 통신을 허용하려면 AEM에서 IMS 구성과 Adobe Stock 구성을 만드십시오.

>[!NOTE]
>
>조직의 AEM 관리자와 관리 콘솔 관리자만 관리자 권한이 필요하므로 통합을 수행할 수 있습니다.

### Create an IMS configuration {#create-an-ims-configuration}

1. AEM 로고를 클릭합니다. 도구 > **[!UICONTROL 보안]** > **[!UICONTROL Adobe]** IMS **[!UICONTROL 구성으로 이동합니다]**. 만들기를 **[!UICONTROL 클릭하고]** 클라우드 솔루션 **[!UICONTROL >]** Adobe **[!UICONTROL Stock을]**&#x200B;선택합니다.
1. 기존 인증서를 재사용하거나 새 인증서 **[!UICONTROL 만들기를]**&#x200B;선택합니다.
1. **[!UICONTROL 인증서 만들기]**&#x200B;를 클릭합니다. 만든 후 공개 키를 다운로드합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 제목, 권한 부여 서버 **[!UICONTROL ,]** API 키 **[!UICONTROL ,]**&#x200B;클라이언트 암호 **[!UICONTROL 값,]** Publicing Payload ********&#x200B;에 해당하는 필드를 제공합니다. Adobe [I/O에서 이러한 값을 가져오기 위한 자세한 내용은 JWT 인증 빠른 시작을](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)참조하십시오.
1. 다운로드한 공개 키를 Adobe I/O 서비스 계정에 추가합니다.

### AEM에서 Adobe Stock 구성 만들기 {#create-adobe-stock-configuration-in-aem}

1. AEM 사용자 인터페이스에서 도구 > 클라우드 **[!UICONTROL 서비스]** > **[!UICONTROL Adobe]** Stock **[!UICONTROL 으로]**&#x200B;이동합니다.
1. 만들기를 **[!UICONTROL 클릭하여]** 구성을 만들고 기존 IMS 구성과 연결합니다. 환경 매개 변수로 `PROD` 선택합니다.
1. 라이센스 **[!UICONTROL 자산 경로]** 필드에서 위치를 그대로 둡니다. Adobe Stock 에셋을 저장할 위치를 변경하지 마십시오.
1. 필요한 모든 속성을 추가하여 작성을 완료합니다. Click **[!UICONTROL Save &amp; Close]**.
1. 자산에 라이선스를 부여할 수 있는 AEM 사용자 또는 그룹을 추가합니다.

>[!NOTE]
>
>Adobe Stock 구성이 여러 개 있는 경우 AEM 사용자 인터페이스에서 [!UICONTROL AEM] 로고를 클릭하여 사용자 환경 설정 패널에서 원하는 구성을 선택합니다.

## AEM에서 Adobe Stock 에셋 사용 및 관리 {#usemanage}

조직은 이 기능을 사용하여 사용자가 AEM Assets에서 Adobe Stock 자산을 사용하여 작업할 수 있도록 허용할 수 있습니다. AEM 사용자 인터페이스 내에서 사용자는 Adobe Stock 자산을 검색하고 필요한 자산에 라이선스를 부여할 수 있습니다.

AEM에서 Adobe Stock 에셋에 라이선스가 부여되면 일반 자산처럼 사용하고 관리할 수 있습니다. AEM에서 사용자는 자산을 검색하고 미리 볼 수 있습니다.자산 복사 및 게시;브랜드 포털에서 자산 공유;aem 데스크탑 앱을 통해 에셋 액세스 및 사용기타 기능

![AEM 작업 영역에서 Adobe Stock 에셋 검색 및 결과 필터링](assets/adobe-stock-search-results-workspace.png)

*그림:AEM 작업 영역에서 Adobe Stock 에셋 검색 및 결과 필터링*

**A.** Adobe Stock ID가 제공된 자산과 유사한 에셋을 검색합니다. **B.** 선택한 모양 또는 방향과 일치하는 에셋을 검색할 수 있습니다. **C.** 지원되는 자산 유형 D 중 하나를 **검색합니다.** 필터 창 E를 열거나 **축소합니다.** 선택한 자산에 라이선스를 부여하고 AEM F에서 저장합니다 **.** 워터마크 G를 사용하여 자산을 AEM에 **저장합니다.** 선택한 자산 H와 유사한 Adobe Stock 웹 사이트의 에셋을 **살펴보십시오.** Adobe Stock 웹 사이트 I에서 선택한 에셋을 **봅니다.** 검색 결과 J에서 선택한 자산의 **수입니다.** 카드 보기와 목록 보기 간 전환

### 자산 찾기 {#find-assets}

AEM 사용자는 AEM 및 Adobe Stock에서 자산을 검색할 수 있습니다. 검색 위치가 Adobe Stock에 제한되지 않으면 AEM 및 Adobe Stock의 검색 결과가 표시됩니다.

* Adobe Stock 에셋을 검색하려면 탐색 > **[!UICONTROL 에셋]** > **[!UICONTROL Adobe Stock]** 검색을 **[!UICONTROL 클릭합니다]**.

* Adobe Stock 및 AEM 자산에서 자산을 검색하려면 검색 아이콘 ![search_icon](assets/search_icon.png)을 클릭합니다.

또는 검색 `Location: Adobe Stock` 표시줄에서 입력을 시작하여 Adobe Stock 에셋을 선택합니다.  AEM에서는 검색된 자산에 대한 고급 필터링 기능을 제공하므로 사용자는 지원되는 자산 유형, 이미지 방향 및 라이선스가 부여된 상태와 같은 필터를 사용하여 필요한 자산을 신속하게 이용할 수 있습니다.

>[!NOTE]
>
>Adobe Stock에서 검색된 자산은 AEM에 표시됩니다. Adobe Stock 자산은 사용자가 자산을 [](/help/assets/aem-assets-adobe-stock.md#saveassets) 저장하거나 자산을 [](/help/assets/aem-assets-adobe-stock.md#licenseassets)라이센스한 후에만 AEM 저장소에 보관됩니다. AEM에 이미 저장된 에셋이 쉽게 참조하고 액세스할 수 있도록 표시되고 강조 표시됩니다. 또한 이러한 에셋은 소스를 Adobe Stock으로 나타내기 위해 일부 추가 메타데이터와 함께 저장됩니다.

![AEM의 검색 필터 및 검색 결과에서 강조 표시된 Adobe Stock 에셋](assets/aem-search-filters2.jpg)

*그림:AEM의 검색 필터 및 검색 결과에서 강조 표시된 Adobe Stock 에셋*

### 필요한 에셋 저장 및 보기 {#saveassets}

AEM에서 저장할 자산을 선택합니다. 맨 위의 도구 모음에서 저장을 클릭하고 자산의 이름과 위치를 입력합니다. 라이센스가 없는 에셋은 워터마크를 사용하여 로컬에 저장됩니다.

다음 번에 자산을 검색할 때 저장된 자산은 배지로 강조 표시되어 해당 자산을 AEM 자산에서 사용할 수 있음을 나타냅니다.

>[!NOTE]
>
>최근에 추가된 에셋은 라이선스 배지 대신 새 배지가 표시됩니다.

### 라이선스 에셋 {#licenseassets}

사용자는 Adobe Stock 엔터프라이즈 플랜의 할당량을 사용하여 Adobe Stock 에셋에 라이선스를 부여할 수 있습니다. 자산 라이선스를 부여하면 워터마크 없이 저장되며 AEM 자산에서 검색하고 사용할 수 있습니다.

![AEM Assets에서 Adobe Stock 에셋에 라이선스를 부여하고 저장하는 대화 상자](assets/aem-stock_licenseandsave.jpg)

*그림:AEM Assets에서 Adobe Stock 에셋에 라이선스를 부여하고 저장하는 대화 상자*

### 메타데이터 및 자산 속성 액세스 {#access-metadata-and-asset-properties}

사용자는 AEM에 저장된 자산에 대한 Adobe Stock 메타데이터 속성을 비롯한 메타데이터에 액세스하고 미리 볼 수 있으며, 자산에 대한 라이센스 **[!UICONTROL 참조를]** 추가할 수 있습니다. 그러나 라이선스 참조에 대한 업데이트는 AEM과 Adobe Stock 웹 사이트 간에 동기화되지 않습니다.

사용자는 라이선스가 부여된 에셋과 라이선스가 없는 에셋 모두에 대한 속성을 볼 수 있습니다.

![저장된 에셋의 메타데이터 및 라이선스 참조 보기 및 액세스](assets/metadata_properties.jpg)

*그림:저장된 에셋의 메타데이터 및 라이선스 참조 보기 및 액세스*

## 알려진 제한 사항 {#known-limitations}

### 편집 이미지 경고가 표시되지 않음

이미지에 라이선스를 부여할 때 이미지가 편집 전용 이미지인지 확인할 수 없습니다. 이러한 오용을 방지하기 위해 관리자는 Admin Console에서 편집 자산에 대한 액세스를 끌 수 있습니다.

### 잘못된 라이선스 유형이 표시됩니다.

자산에 대해 AEM에 잘못된 라이선스 유형이 표시될 수 있습니다. 사용자는 Adobe Stock 웹 사이트에 로그인하여 라이선스 유형을 확인할 수 있습니다.

### 참조 필드 및 메타데이터가 동기화되지 않음

사용자가 라이센스 참조 필드를 업데이트하면 라이센스 참조 정보는 AEM에서 업데이트되지만 Adobe Stock 웹 사이트에서는 업데이트되지 않습니다. 마찬가지로 사용자가 Adobe Stock 웹 사이트의 참조 필드를 업데이트하면 업데이트가 AEM에서 동기화되지 않습니다.

>[!MORELIKETHIS]
>
>* [AEM 자산과 함께 Adobe Stock 에셋 사용에 대한 비디오 자습서](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)
>* [Adobe Stock 엔터프라이즈 플랜 도움말](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock FAQ](https://helpx.adobe.com/stock/faq.html)

