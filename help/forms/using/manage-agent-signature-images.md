---
title: 에이전트 서명 이미지 관리
description: 편지 템플릿을 만든 후에는 데이터, 컨텐츠 및 첨부 파일을 관리하여 AEM Forms에서 서신을 만드는 데 사용할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: f044ed75-bb72-4be1-aef6-2fb3b2a2697b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 에이전트 서명 이미지 관리{#manage-agent-signature-images}

## 개요 {#overview}

서신 관리에서 이미지를 사용하여 에이전트 서명을 서신으로 렌더링할 수 있습니다. 편지를 작성하는 동안 에이전트 서명 이미지를 설정한 후 편지에 있는 에이전트 서명 이미지를 보낸 사람 에이전트의 서명으로 렌더링할 수 있습니다.

agentSignatureImage DDE는 에이전트의 서명 이미지를 나타내는 계산된 DDE입니다. 이 계산된 DDE에 대한 표현식은 표현식 관리자 빌딩 블록에 의해 노출된 새 사용자 정의 함수를 사용합니다. 이 사용자 지정 함수는 agentID 및 agentFolder를 입력 매개 변수로 사용하고, 이러한 매개 변수를 기반으로 이미지 컨텐츠를 가져옵니다. SystemContext 시스템 데이터 사전은 현재 시스템 컨텍스트의 정보에 대한 응답 관리 액세스 권한을 가진 문자를 제공합니다. 시스템 컨텍스트에는 현재 로그인한 사용자 및 활성 구성 매개변수에 대한 정보가 포함되어 있습니다.

cmuserroot 폴더 아래에 이미지를 추가할 수 있습니다. 위치 [서신 관리 구성 속성](/help/forms/using/cm-configuration-properties.md), CM 사용자 루트 속성을 사용하여 에이전트 서명 이미지를 선택하는 위치의 폴더를 변경할 수 있습니다.

agentFolder DDE의 값은 서신 관리 구성 속성에 대한 CMUserRoot 구성 매개 변수에서 가져온 것입니다. 기본적으로 이 구성 매개 변수는 CRX 저장소의/content/cmUserRoot를 가리킵니다. 구성 속성에서 CMUserRoot 구성의 값을 변경할 수 있습니다.
기본 사용자 지정 함수를 재정의하여 사용자 서명 이미지를 가져오기 위한 자체 논리를 정의할 수도 있습니다.

## 에이전트 서명 이미지 추가 중 {#adding-agent-signature-image}

1. 에이전트 서명 이미지의 이름이 사용자의 AEM 사용자 이름과 같은지 확인합니다. 이미지 파일 이름에는 확장명이 필요하지 않습니다.
1. CRX에서 다음 이름의 폴더를 만듭니다. `cmUserRoot` 컨텐츠 폴더에 있습니다.

   1. 다음으로 이동 `https://'[server]:[port]'/crx/de`. 필요한 경우 관리자로 로그인합니다.

   1. 마우스 오른쪽 단추 클릭 **콘텐츠** 폴더 및 선택 **만들기** > **폴더 만들기**.

      ![폴더 만들기](assets/1_createnode_cmuserroot.png)

   1. 폴더 만들기 대화 상자에서 폴더 이름을 로 입력합니다. `cmUserRoot`. **모두 저장**&#x200B;을 클릭합니다.

      >[!NOTE]
      >
      >cmUserRoot 는 AEM이 에이전트 서명 이미지를 찾는 기본 위치입니다. 그러나 의 CM 사용자 루트 속성을 편집하여 변경할 수 있습니다. [서신 관리 구성 속성](/help/forms/using/cm-configuration-properties.md).

1. 콘텐츠 탐색기에서 cmUserRoot 폴더로 이동하여 에이전트 서명 이미지를 추가합니다.

   1. 다음으로 이동 `https://'[server]:[port]'/crx/explorer/index.jsp`. 필요한 경우 관리자로 로그인합니다.
   1. 클릭 **콘텐츠 탐색기**. 콘텐츠 탐색기가 새 창에 열립니다.
   1. 콘텐츠 탐색기에서 cmUserRoot 폴더로 이동하여 선택합니다. 마우스 오른쪽 단추 클릭 **cmUserRoot** 폴더 및 선택 **새 노드**.

      ![cmUserRoot의 새 노드](assets/2_cmuserroot_newnode.png)

      새 노드의 행에서 다음 항목을 입력한 다음 녹색 확인 표시를 클릭합니다.

      **이름:** JohnDoe(또는 에이전트 서명 파일의 이름)

      **유형:** nt:file

      아래 `cmUserRoot` 폴더, 라는 새 폴더 `JohnDoe` (또는 이전 단계에서 지정한 이름이) 만들어집니다.

   1. 새로 만든 폴더(여기)를 클릭합니다. `JohnDoe`). 컨텐트 탐색기에는 폴더의 컨텐트가 흐리게 표시됩니다.

   1. 를 두 번 클릭합니다. **jcr:content** 속성, 해당 유형 설정 **nt:resource**&#x200B;을 클릭한 다음 녹색 확인 표시를 클릭하여 항목을 저장합니다.

      속성이 없으면 먼저 이름이 jcr:content인 속성을 만듭니다.

      ![jcr:content 속성](assets/3_jcrcontentntresource.png)

      jcr:content의 하위 속성 중에는 흐리게 표시되는 jcr:data가 있습니다. jcr:data를 두 번 클릭합니다. 속성을 편집할 수 있고 [파일 선택] 버튼이 항목에 나타납니다. 클릭 **파일 선택** 로고로 사용할 이미지 파일을 선택합니다. 이미지 파일에는 확장명이 필요하지 않습니다.

      ![JCR 데이터](assets/5_jcrdata.png)

   **모두 저장**&#x200B;을 클릭합니다.

1. 편지에서 사용하는 XDP\레이아웃에 서명 이미지를 렌더링할 이미지 필드가 왼쪽 아래에 있는지(또는 레이아웃을 통해 서명을 렌더링할 위치) 확인합니다.
1. 서신을 만드는 동안 데이터 탭에서 다음 단계를 사용하여 서명 이미지에 대한 이미지 필드를 선택합니다.

   1. 오른쪽 창의 [링크 유형] 팝업 메뉴에서 [시스템]을 선택합니다.

   1. SystemContext DD에 대한 데이터 요소 패널의 목록에서 agentSignatureImage DDE를 선택합니다.

   1. 편지를 저장합니다.

1. 문자가 렌더링되면 레이아웃에 따라 이미지 필드의 편지 미리 보기에서 서명을 볼 수 있습니다.

   ![편지의 에이전트 서명 이미지](assets/letterwithsignature.png)
