---
title: 초기 샌드박스 애플리케이션
seo-title: 초기 샌드박스 애플리케이션
description: 템플릿, 구성 요소 및 스크립트 만들기
seo-description: 템플릿, 구성 요소 및 스크립트 만들기
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---


# 초기 샌드박스 애플리케이션 {#initial-sandbox-application}

이 섹션에서 다음을 만듭니다.

* 예제 웹 사이트에서 컨텐츠 페이지를 만드는 데 사용할 **[템플릿입니다](#createthepagetemplate)** .
* 웹 사이트 페이지를 렌더링하는 데 사용할 **[구성 요소 및 스크립트](#create-the-template-s-rendering-component)** .

## 컨텐츠 템플릿 만들기 {#create-the-content-template}

템플릿은 새 페이지의 기본 컨텐츠를 정의합니다. 복잡한 웹 사이트에서는 여러 가지 템플릿을 사용하여 사이트에서 다양한 유형의 페이지를 만들 수 있습니다. 또한 템플릿 세트는 서버 클러스터에 변경 사항을 롤아웃하는 데 사용되는 청사진이 될 수 있습니다.

이 연습에서는 모든 페이지가 하나의 간단한 템플릿을 기반으로 합니다.

1. CRXDE Lite의 탐색기 창:

   * 선택 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 만들기]** > **[!UICONTROL 템플릿 만들기]**

1. 템플릿 만들기 대화 상자에서 다음 값을 입력한 다음 **[!UICONTROL 다음을 클릭합니다]**.

   * 레이블: `playpage`
   * 제목: `An SCF Sandbox Play Template`
   * 설명: `An SCF Sandbox template for play pages`
   * 리소스 유형: `an-scf-sandbox/components/playpage`
   * 등급:&lt;기본값으로 유지>

   Label은 노드 이름에 사용됩니다.

   리소스 유형이 `playpage`의 jcr:content 노드에 속성으로 나타납니다 `sling:resourceType`. 브라우저가 요청할 때 컨텐츠를 렌더링하는 구성 요소(리소스)를 식별합니다.

   이 경우 템플릿을 사용하여 만든 모든 페이지는 구성 요소에 의해 `playpage` 렌더링됩니다 `an-scf-sandbox/components/playpage` . 규칙으로 구성 요소의 경로는 상대 경로이므로 Sling은 폴더에서 먼저 리소스를 검색하고, 찾을 수 없으면 `/apps` `/libs` 폴더에서 리소스를 검색할 수 있습니다.

   ![create-content-template](assets/create-content-template-1.png)

1. 복사/붙여넣기를 사용하는 경우 리소스 유형 값에 선행 또는 후행 공백이 없는지 확인합니다.

   **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. &quot;허용되는 경로&quot;는 템플릿이 **[!UICONTROL 새 페이지 대화 상자에 나열되는 것과 같이 이 템플릿을 사용하는 페이지 경로를]** 나타냅니다.

   패스를 추가하려면 더하기 단추 `+` 를 클릭하고 나타나는 텍스트 상자 `/content(/.&ast;)?` 에 입력합니다. 복사/붙여넣기를 사용하는 경우 앞이나 뒤에 공백이 없어야 합니다.

   참고:허용되는 경로 속성의 값은 *정규식입니다*. 표현식과 일치하는 경로가 있는 컨텐츠 페이지에서는 템플릿을 사용할 수 있습니다. 이 경우 정규 표현식은 **/content** 폴더 경로 및 모든 하위 페이지와 일치합니다.

   작성자가 아래 페이지 `/content`를 만들면 사용할 수 있는 템플릿 목록에 &quot;SCF 샌드박스 페이지 템플릿&quot;이라는 `playpage` 템플릿이 나타납니다.

   템플릿에서 루트 페이지를 만든 후 정규 표현식에 루트 경로를 포함하도록 속성을 수정하여 템플릿에 대한 액세스가 이 웹 사이트로 제한될 수 있습니다.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   허용된 부모 **[!UICONTROL 패널]** 에서 **[!UICONTROL 다음을]** 클릭합니다.

   허용된 **[!UICONTROL 하위]** 패널 **[!UICONTROL 에서 [다음]을]** 클릭합니다.

   **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. 확인을 클릭하고 템플릿 작성을 완료하면 새 템플릿의 속성 탭 값 모서리에 빨간색 삼각형이 표시되는 것을 확인할 수 `playpage` 있습니다. 이러한 빨간색 삼각형은 저장하지 않은 편집을 나타냅니다.

   모두 **[!UICONTROL 저장을]** 클릭하여 새 템플릿을 저장소에 저장합니다.

   ![verify-content-template](assets/verify-content-template.png)

### 템플릿의 렌더링 구성 요소 만들기 {#create-the-template-s-rendering-component}

컨텐츠를 정의하고 *재생 페이지 템플릿을* 기반으로 만들어진 페이지를 렌더링하는 구성 요소를 [만듭니다](#createthepagetemplate).

1. CRXDE Lite에서 마우스 오른쪽 단추 **`/apps/an-scf-sandbox/components`** 를 클릭하고 **[!UICONTROL 만들기 > 구성 요소를 클릭합니다]**.
1. 노드 이름(레이블)을 *재생 페이지로*&#x200B;설정하면 구성 요소의 경로가

   `/apps/an-scf-sandbox/components/playpage`

   재생 페이지 템플릿의 리소스 유형에 해당하는 리소스 유형(선택 사항: 경로의 초기 **`/apps/`** 부분을 빼기).

   구성 요소 **[!UICONTROL 만들기]** 대화 상자에서 다음 속성 값을 입력합니다.

   * 레이블: **재생 페이지**
   * 제목: **SCF 샌드박스 재생 구성 요소**
   * 설명: **SCF 샌드박스 페이지의 컨텐츠를 렌더링하는 구성 요소입니다.**
   * 슈퍼 유형: *&lt;비워 두십시오>*
   * 그룹: *&lt;비워 두십시오>*

   ![create-template-component](assets/create-template-component.png)

1. 대화 상자 **[!UICONTROL 의]** 허용된 하위 **[!UICONTROL 패널이 나타날 때까지 다음을]** 클릭합니다.

   * **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
   * 모두 **[!UICONTROL 저장을 클릭합니다]**.

1. 템플릿에 대한 구성 요소 및 resourceType의 경로가 일치하는지 확인합니다.

   >[!CAUTION]
   >
   >재생 페이지 구성 요소의 경로와 재생 페이지 템플릿의 sling:resourceType 속성 간의 통신은 웹 사이트의 올바른 기능을 위해 중요합니다.

   ![verify-template-component](assets/verify-template-component.png)