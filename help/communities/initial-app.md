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
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# 초기 샌드박스 응용 프로그램 {#initial-sandbox-application}

이 섹션에서 다음을 생성합니다.

* 예제 웹 사이트에서 컨텐츠 페이지를 만드는 데 사용할 **[템플릿](#createthepagetemplate)**.
* 웹 사이트 페이지를 렌더링하는 데 사용할 **[구성 요소 및 스크립트](#create-the-template-s-rendering-component)**.

## 컨텐츠 템플릿 {#create-the-content-template} 만들기

템플릿은 새 페이지의 기본 컨텐츠를 정의합니다. 복잡한 웹 사이트에서는 사이트에서 다른 유형의 페이지를 만드는 데 여러 템플릿을 사용할 수 있습니다. 또한 템플릿 세트가 서버 클러스터에 변경 사항을 롤아웃하는 데 사용되는 블루프린트가 될 수 있습니다.

이 연습에서는 모든 페이지가 하나의 간단한 템플릿을 기반으로 합니다.

1. CRXDE Lite의 탐색기 창에서 다음을 수행합니다.

   * 선택 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 만들기]**  >  **[!UICONTROL 템플릿 만들기]**

1. 템플릿 만들기 대화 상자에서 다음 값을 입력한 다음 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   * 레이블: `playpage`
   * 제목: `An SCF Sandbox Play Template`
   * 설명: `An SCF Sandbox template for play pages`
   * 리소스 유형: `an-scf-sandbox/components/playpage`
   * 등급:&lt;기본값으로 유지>

   노드 이름에 레이블이 사용됩니다.

   리소스 유형이 `playpage`의 jcr:content 노드에 속성 `sling:resourceType`으로 나타납니다. 브라우저에서 요청할 때 컨텐츠를 렌더링하는 구성 요소(리소스)를 식별합니다.

   이 경우 `playpage` 템플릿을 사용하여 만든 모든 페이지가 `an-scf-sandbox/components/playpage` 구성 요소에 의해 렌더링됩니다. 규칙에 따라 구성 요소의 경로가 상대적이므로 Sling은 `/apps` 폴더에서 먼저 리소스를 검색하고, 찾을 수 없는 경우 `/libs` 폴더에서 리소스를 검색할 수 있습니다.

   ![create-content-template](assets/create-content-template-1.png)

1. 복사/붙여넣기를 사용하는 경우 리소스 유형 값에 선행 또는 후행 공백이 없는지 확인하십시오.

   **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. &quot;허용된 경로&quot;는 **[!UICONTROL 새 페이지]** 대화 상자에 템플릿이 나열되도록 이 템플릿을 사용하는 페이지 경로를 나타냅니다.

   경로를 추가하려면 더하기 단추 `+`를 클릭하고 나타나는 텍스트 상자에 `/content(/.&ast;)?`을 입력합니다. 복사/붙여넣기를 사용하는 경우 선행 또는 후행 공백이 없는지 확인하십시오.

   참고:허용되는 경로 속성의 값은 *정규 표현식*&#x200B;입니다. 표현식과 일치하는 경로가 있는 컨텐츠 페이지에서 템플릿을 사용할 수 있습니다. 이 경우 정규 표현식은 **/content** 폴더의 경로와 모든 하위 페이지와 일치합니다.

   작성자가 `/content` 아래에 페이지를 만들면 &quot;SCF 샌드박스 페이지 템플릿&quot;이라는 `playpage` 템플릿이 사용할 수 있는 템플릿 목록에 표시됩니다.

   템플릿에서 루트 페이지를 만든 후 일반 표현식에 루트 경로를 포함하도록 속성을 수정하여 템플릿에 대한 액세스를 이 웹 사이트로 제한할 수 있습니다.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   **[!UICONTROL 허용되는 부모]** 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   **[!UICONTROL 허용되는 하위]** 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. 확인 을 클릭하고 템플릿 만들기를 마치면 새 `playpage` 템플릿에 대한 속성 탭 값의 모서리에 빨간색 삼각형이 표시됩니다. 이러한 빨간색 삼각형은 저장되지 않은 편집 내용을 나타냅니다.

   **[!UICONTROL 모두 저장]**&#x200B;을 클릭하여 새 템플릿을 저장소에 저장합니다.

   ![verify-content-template](assets/verify-content-template.png)

### 템플릿의 렌더링 구성 요소 {#create-the-template-s-rendering-component} 만들기

컨텐츠를 정의하고 [재생 페이지 템플릿](#createthepagetemplate)을(를) 기반으로 만들어진 페이지를 렌더링하는 *구성 요소*&#x200B;를 만듭니다.

1. CRXDE Lite에서 **`/apps/an-scf-sandbox/components`** 을 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 만들기 > 구성 요소]** 를 클릭합니다.
1. 노드의 이름(레이블)을 *playpage*&#x200B;로 설정하면 구성 요소의 경로가 다음과 같습니다

   `/apps/an-scf-sandbox/components/playpage`

   플레이페이지 템플릿의 리소스 유형에 해당합니다(선택적으로 경로의 초기 **`/apps/`** 부분을 빼기).

   **[!UICONTROL 구성 요소 만들기]** 대화 상자에서 다음 속성 값을 입력합니다.

   * 레이블:**playpage**
   * 제목:**SCF 샌드박스 재생 구성 요소**
   * 설명:**SCF 샌드박스 페이지의 컨텐츠를 렌더링하는 구성 요소입니다.**
   * 수퍼 유형:*&lt;비워 두십시오>*
   * 그룹:*&lt;비워 두십시오>*

   ![create-template-component](assets/create-template-component.png)

1. 대화 상자의 **[!UICONTROL 허용되는 하위]** 패널이 나타날 때까지 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   * **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
   * **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. 구성 요소의 경로와 템플릿에 대한 resourceType이 일치하는지 확인합니다.

   >[!CAUTION]
   >
   >플레이페이지 구성 요소에 대한 경로와 플레이페이지 템플릿의 sling:resourceType 속성 간의 서신은 웹 사이트의 올바른 기능에 매우 중요합니다.

   ![verify-template-component](assets/verify-template-component.png)
