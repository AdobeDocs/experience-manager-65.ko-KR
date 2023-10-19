---
title: 초기 샌드박스 애플리케이션
description: 콘텐츠 페이지를 만드는 데 사용되는 콘텐츠 템플릿과 웹 사이트 페이지를 렌더링하는 데 사용되는 구성 요소 및 스크립트를 사용하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---

# 초기 샌드박스 애플리케이션 {#initial-sandbox-application}

이 섹션에서는 다음을 만듭니다.

* 다음 **[템플릿](#createthepagetemplate)** 예제 웹 사이트에서 컨텐츠 페이지를 만드는 데 사용됩니다.
* 다음 **[구성 요소 및 스크립트](#create-the-template-s-rendering-component)** 웹 사이트 페이지를 렌더링하는 데 사용됩니다.

## 콘텐츠 템플릿 만들기 {#create-the-content-template}

템플릿은 새 페이지의 기본 콘텐츠를 정의합니다. 복잡한 웹 사이트에서는 사이트에서 서로 다른 유형의 페이지를 만들기 위해 여러 템플릿을 사용할 수 있습니다. 또한 템플릿 세트는 서버 클러스터에 대한 변경 사항을 롤아웃하는 데 사용되는 블루프린트가 될 수 있습니다.

이 연습에서는 모든 페이지가 하나의 간단한 템플릿을 기반으로 합니다.

1. CRXDE Lite의 탐색기 창에서 다음을 수행합니다.

   * 선택 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 만들기]** > **[!UICONTROL 템플릿 만들기]**

1. 템플릿 만들기 대화 상자에서 다음 값을 입력한 다음 **[!UICONTROL 다음]**:

   * 레이블: `playpage`
   * 제목: `An SCF Sandbox Play Template`
   * 설명: `An SCF Sandbox template for play pages`
   * 리소스 유형: `an-scf-sandbox/components/playpage`
   * 순위: &lt;leave as=&quot;&quot; default=&quot;&quot;>

   노드 이름에는 레이블 이 사용됩니다.

   리소스 유형이 다음에 나타납니다. `playpage`의 `jcr:content` 노드를 속성으로 `sling:resourceType`. 브라우저가 요청할 때 콘텐츠를 렌더링하는 구성 요소(리소스)를 식별합니다.

   이 경우 모든 페이지는 `playpage` 템플릿은 `an-scf-sandbox/components/playpage` 구성 요소. 규칙에 따라 구성 요소에 대한 경로는 상대적이므로 Sling은에서 먼저 리소스를 검색할 수 있습니다. `/apps` 폴더 및 을(를) 찾을 수 없는 경우 `/libs` 폴더를 삭제합니다.

   ![create-content-template](assets/create-content-template-1.png)

1. 복사/붙여넣기를 사용하는 경우 리소스 유형 값에 선행 또는 후행 공백이 없는지 확인합니다.

   **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. &quot;허용된 경로&quot;는 이 템플릿을 사용하는 페이지의 경로를 나타내므로 다음에 대한 템플릿 목록이 표시됩니다. **[!UICONTROL 새 페이지]** 대화 상자.

   경로를 추가하려면 더하기 버튼을 클릭합니다 `+` 및 유형 `/content(/.&ast;)?` 표시되는 텍스트 상자에 입력합니다. 복사/붙여넣기를 사용하는 경우 선행 또는 후행 공백이 없는지 확인합니다.

   참고: 허용되는 경로 속성의 값은 입니다. *정규 표현식*. 표현식과 일치하는 경로가 있는 콘텐츠 페이지는 템플릿을 사용할 수 있습니다. 이 경우 정규 표현식은 의 경로와 일치합니다 **/content** 폴더와 모든 하위 페이지.

   작성자가 아래에 페이지를 만들 때 `/content`, `playpage` 제목이 &quot;SCF 샌드박스 페이지 템플릿&quot;인 템플릿이 사용할 수 있는 템플릿 목록에 나타납니다.

   템플릿에서 루트 페이지를 만든 후 속성을 편집하여 정규 표현식에 루트 경로를 포함시켜 템플릿에 대한 액세스를 이 웹 사이트로 제한할 수 있습니다.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   클릭 **[!UICONTROL 다음]** 다음에서 **[!UICONTROL 허용된 상위]** 패널.

   클릭 **[!UICONTROL 다음]** 다음에서 **[!UICONTROL 허용된 하위]** 패널.

   **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. 확인(OK)을 클릭하고 템플릿 생성을 완료한 후 새 템플릿의 속성(Properties) 탭 값 모서리에 표시되는 빨간색 삼각형을 확인합니다 `playpage` 템플릿. 이러한 빨간색 삼각형은 저장되지 않은 편집 내용을 나타냅니다.

   클릭 **[!UICONTROL 모두 저장]** 저장소에 새 템플릿을 저장합니다.

   ![verify-content-template](assets/verify-content-template.png)

### 템플릿의 렌더링 구성 요소 만들기 {#create-the-template-s-rendering-component}

만들기 *구성 요소* 콘텐츠를 정의하고 를 기반으로 생성된 모든 페이지를 렌더링합니다. [playpage 템플릿](#createthepagetemplate).

1. CRXDE Lite에서 마우스 오른쪽 단추 클릭 **`/apps/an-scf-sandbox/components`** 및 클릭 **[!UICONTROL 만들기 > 구성 요소]**.
1. 노드의 이름(레이블)을 *playpage*: 구성 요소에 대한 경로는 입니다.

   `/apps/an-scf-sandbox/components/playpage`

   재생 페이지 템플릿의 리소스 유형(선택적으로 초기 항목 제외)에 해당합니다. **`/apps/`** 경로의 일부).

   다음에서 **[!UICONTROL 구성 요소 만들기]** 대화 상자에서 다음 속성 값을 입력합니다.

   * 레이블: **playpage**
   * 제목: **SCF 샌드박스 재생 구성 요소**
   * 설명: **SCF 샌드박스 페이지에 대한 콘텐츠를 렌더링하는 구성 요소입니다.**
   * 상위 유형: *&lt;leave blank=&quot;&quot;>*
   * 그룹: *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. 클릭 **[!UICONTROL 다음]** 종료 시간: **[!UICONTROL 허용된 하위]** 대화 상자의 패널이 표시됩니다.

   * **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
   * **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. 구성 요소에 대한 경로와 템플릿에 대한 resourceType이 일치하는지 확인합니다.

   >[!CAUTION]
   >
   >재생 페이지 구성 요소 경로 및 `sling:resourceType` playpage 템플릿의 속성은 웹 사이트의 올바른 기능에 매우 중요합니다.

   ![verify-template-component](assets/verify-template-component.png)
