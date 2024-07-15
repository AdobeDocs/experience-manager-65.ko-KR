---
title: 초기 샌드박스 애플리케이션
description: 콘텐츠 페이지를 만드는 데 사용되는 콘텐츠 템플릿과 웹 사이트 페이지를 렌더링하는 데 사용되는 구성 요소 및 스크립트를 사용하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# 초기 샌드박스 애플리케이션 {#initial-sandbox-application}

이 섹션에서는 다음을 만듭니다.

* 예제 웹 사이트에서 콘텐츠 페이지를 만드는 데 사용되는 **[template](#createthepagetemplate)**.
* 웹 사이트 페이지를 렌더링하는 데 사용되는 **[구성 요소 및 스크립트](#create-the-template-s-rendering-component)**.

## 콘텐츠 템플릿 만들기 {#create-the-content-template}

템플릿은 새 페이지의 기본 콘텐츠를 정의합니다. 복잡한 웹 사이트에서는 사이트에서 서로 다른 유형의 페이지를 만들기 위해 여러 템플릿을 사용할 수 있습니다. 또한 템플릿 세트는 서버 클러스터에 대한 변경 사항을 롤아웃하는 데 사용되는 블루프린트가 될 수 있습니다.

이 연습에서는 모든 페이지가 하나의 간단한 템플릿을 기반으로 합니다.

1. CRXDE Lite의 탐색기 창에서 다음을 수행합니다.

   * `/apps/an-scf-sandbox/templates` 선택
   * **[!UICONTROL 만들기]** > **[!UICONTROL 템플릿 만들기]**

1. 템플릿 만들기 대화 상자에서 다음 값을 입력한 다음 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   * 레이블: `playpage`
   * 제목: `An SCF Sandbox Play Template`
   * 설명: `An SCF Sandbox template for play pages`
   * 리소스 종류: `an-scf-sandbox/components/playpage`
   * 순위: &lt;기본값으로 유지>

   노드 이름에는 레이블 이 사용됩니다.

   리소스 유형이 `playpage`의 `jcr:content` 노드에 속성 `sling:resourceType`(으)로 나타납니다. 브라우저가 요청할 때 콘텐츠를 렌더링하는 구성 요소(리소스)를 식별합니다.

   이 경우 `playpage` 템플릿을 사용하여 만든 모든 페이지가 `an-scf-sandbox/components/playpage` 구성 요소에 의해 렌더링됩니다. 규칙에 따라 구성 요소에 대한 경로는 상대적입니다. 따라서 Sling은 `/apps` 폴더에서 먼저 리소스를 검색하고, 찾을 수 없는 경우 `/libs` 폴더에서 리소스를 검색할 수 있습니다.

   ![create-content-template](assets/create-content-template-1.png)

1. 복사/붙여넣기를 사용하는 경우 리소스 유형 값에 선행 또는 후행 공백이 없는지 확인합니다.

   **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. &quot;허용된 경로&quot;는 이 템플릿을 사용하는 페이지의 경로를 나타내므로 해당 템플릿은 **[!UICONTROL 새 페이지]** 대화 상자에 나열됩니다.

   경로를 추가하려면 더하기 단추 `+`을(를) 클릭하고 나타나는 텍스트 상자에 `/content(/.&ast;)?`을(를) 입력하십시오. 복사/붙여넣기를 사용하는 경우 선행 또는 후행 공백이 없는지 확인합니다.

   참고: 허용되는 경로 속성의 값은 *정규 표현식*&#x200B;입니다. 표현식과 일치하는 경로가 있는 콘텐츠 페이지는 템플릿을 사용할 수 있습니다. 이 경우 정규식은 **/content** 폴더 및 모든 하위 페이지의 경로와 일치합니다.

   작성자가 `/content` 아래에 페이지를 만들면 &quot;SCF 샌드박스 페이지 템플릿&quot;이라는 `playpage` 템플릿이 사용할 수 있는 템플릿 목록에 나타납니다.

   템플릿에서 루트 페이지를 만든 후 속성을 편집하여 정규 표현식에 루트 경로를 포함시켜 템플릿에 대한 액세스를 이 웹 사이트로 제한할 수 있습니다.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   **[!UICONTROL 허용된 부모]** 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   **[!UICONTROL 허용된 자식]** 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. [확인]을 클릭하고 템플릿 만들기를 마치면 새 `playpage` 템플릿에 대한 속성 탭 값의 모서리에 표시되는 빨간색 삼각형이 표시됩니다. 이러한 빨간색 삼각형은 저장되지 않은 편집 내용을 나타냅니다.

   저장소에 새 템플릿을 저장하려면 **[!UICONTROL 모두 저장]**&#x200B;을 클릭하십시오.

   ![verify-content-template](assets/verify-content-template.png)

### 템플릿의 렌더링 구성 요소 만들기 {#create-the-template-s-rendering-component}

콘텐츠를 정의하고 [playpage 템플릿](#createthepagetemplate)을(를) 기반으로 만들어진 페이지를 렌더링하는 *구성 요소*&#x200B;를 만듭니다.

1. CRXDE Lite에서 **`/apps/an-scf-sandbox/components`**&#x200B;을(를) 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 만들기 > 구성 요소]**&#x200B;를 클릭합니다.
1. 노드의 이름(레이블)을 *playpage*(으)로 설정하면 구성 요소에 대한 경로가 다음과 같습니다.

   `/apps/an-scf-sandbox/components/playpage`

   플레이페이지 템플릿의 리소스 유형(선택적으로 경로의 초기 **`/apps/`** 부분 제외)에 해당합니다.

   **[!UICONTROL 구성 요소 만들기]** 대화 상자에서 다음 속성 값을 입력합니다.

   * 레이블: **playpage**
   * 제목: **SCF 샌드박스 재생 구성 요소**
   * 설명: **SCF 샌드박스 페이지의 콘텐츠를 렌더링하는 구성 요소입니다.**
   * 상위 유형: *&lt;비워 둠>*
   * 그룹: *&lt;비워 둠>*

   ![create-template-component](assets/create-template-component.png)

1. 대화 상자의 **[!UICONTROL 허용된 하위 항목]** 패널이 나타날 때까지 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   * **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
   * **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. 구성 요소에 대한 경로와 템플릿에 대한 resourceType이 일치하는지 확인합니다.

   >[!CAUTION]
   >
   >재생 페이지 구성 요소에 대한 경로와 재생 페이지 템플릿의 `sling:resourceType` 속성 간의 대응은 웹 사이트의 올바른 기능에 중요합니다.

   ![verify-template-component](assets/verify-template-component.png)
