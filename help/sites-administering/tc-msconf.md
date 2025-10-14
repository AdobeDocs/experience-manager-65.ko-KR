---
title: Microsoft Translator에 연결
description: AEM을 Microsoft Translator에 연결하여 번역 워크플로를 자동화하는 방법에 대해 알아봅니다.
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3bb516289dbff4fb3b94685b9e25360e7717776e
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 63%

---

# Microsoft Translator에 연결 {#connecting-to-microsoft-translator}

AEM은 [Microsoft Translator](https://www.microsoft.com/en-us/translator/business/)에서 페이지 콘텐츠 또는 에셋을 번역할 수 있는 기본 제공 커넥터를 제공합니다. Microsoft에서 Microsoft Translator 사용 라이선스를 받은 후 이 페이지의 지침에 따라 커넥터를 구성하십시오.

| 속성 | 설명 |
|---|---|
| 번역 레이블 | 번역 서비스의 표시 이름 |
| 번역 속성 | (선택 사항) 사용자 생성 콘텐츠의 경우, 번역된 텍스트 옆에 표시되는 속성(예: `Translations by Microsoft`) |
| 작업 영역 ID | (옵션) 사용할 맞춤화된 Microsoft Translator 엔진의 ID |
| 구독 키 | Microsoft Translator에 대한 Microsoft 구독 키 |

다음 절차를 통해 Microsoft Translator 구성이 생성됩니다.

1. [탐색 패널에서 &#x200B;](/help/sites-authoring/basic-handling.md#first-steps)을(를) 클릭합니다. **도구** > **Cloud Service** > **번역 Cloud Service**.
1. 구성을 만들고자 하는 위치로 이동합니다. 일반적으로 이는 사이트 루트에 있거나 전역 기본 구성일 수 있습니다.
1. **만들기** 단추를 클릭합니다.
1. 구성을 정의합니다.
   1. 드롭다운 목록에서 **Microsoft Translator**&#x200B;를 선택합니다.
   1. 구성의 제목을 입력합니다. 제목을 통해 클라우드 서비스 콘솔 및 페이지 속성 드롭다운 목록에서 구성을 식별합니다.
   1. 필요한 경우 구성을 저장하는 저장소 노드에 사용할 이름을 입력합니다.

   ![번역 구성 만들기](assets/create-translation-config.png)

1. **만들기**&#x200B;를 클릭합니다.
1. **구성 편집** 창에서 이전 표에서 설명된 번역 서비스에 대한 값을 입력합니다.

   ![번역 구성 편집](assets/msft-config-ui.png)

1. 연결을 확인하려면 **연결**&#x200B;을 클릭하세요.
1. **저장 및 닫기**&#x200B;를 클릭합니다.

## Translator 서비스 구성 게시 {#publishing-the-translator-service-configurations}

마지막 단계로 [트리 게시](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) 작업을 사용하여 게시된 번역된 콘텐츠를 지원하도록 Microsoft Translator 구성을 게시하십시오.
