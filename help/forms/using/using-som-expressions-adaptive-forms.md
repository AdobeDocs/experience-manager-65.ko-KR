---
title: 적응형 양식의 SOM 표현식 사용
seo-title: 적응형 양식의 SOM 표현식 사용
description: 응용 양식 패널의 SOM 표현식을 추출하는 방법을 알아봅니다.
seo-description: 응용 양식 패널의 SOM 표현식을 추출하는 방법을 알아봅니다.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: e5c2385c29e2d20d453e2d1496f7d459d1c55876
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 응용 양식에 SOM 표현식 사용{#using-som-expressions-in-adaptive-forms}

적응형 양식은 AEM 저장소에서 JCR 컨텐츠 구조로 표시되는 AEM 페이지로 모델링됩니다. 콘텐츠 구조의 주요 요소는 guideContainer 노드입니다. guideContainer 아래에는 중첩된 패널과 필드가 포함될 수 있는 rootPanel이 있습니다.

SOM(스크립팅 개체 모델)을 사용하여 특정 문서 개체 모델(DOM) 내의 값, 속성 및 메서드를 참조할 수 있습니다. DOM은 트리 계층 구조의 메모리 개체와 속성을 구성합니다. SOM 표현식은 필드/그리기 요소 및 패널을 참조합니다.

다음 이미지는 구성 요소를 양식에 추가할 때 적응형 양식이 변환하는 노드 구조를 나타냅니다. 예를 들어, 런타임 시 DOM으로 변형되는 패널과 패널의 라디오 단추를 루트 패널에 추가할 수 있습니다. 응용 형식의 라디오 단추 필드에 대한 SOM 표현식은 `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`으로 지정됩니다.

![DOM 트리](assets/hierarchy.png)

DOM 트리

응용 양식의 모든 요소에 대한 SOM 표현식은 `guide[0].guide1[0]`에 의해 접두사로 추가됩니다. 노드 구조 계층 구조에서 구성 요소의 위치는 SOM 표현식을 파생하는 데 사용됩니다.

![라디오 단추가 2개인 DOM 트리](assets/hierarchy_radio_button.png)

라디오 단추가 2개인 DOM 트리

SOM 표현식은 적응형 양식의 라디오 단추 위치를 변경할 때 변경됩니다. 작성 모드에서 SOM 표현식 보기 옵션을 사용하여 AEM Forms 내의 필드 또는 요소의 SOM 표현식을 볼 수 있습니다. 옵션이 패널에 표시되고 필드나 요소를 마우스 오른쪽 단추로 클릭하면 표시됩니다.

![적응형 양식의 SOM 표현식 추출](assets/som-expressions.png)

적응형 양식의 SOM 표현식 추출

패널 내에서 패널 도구 모음에서 기능에 액세스할 수 있습니다. 이 기능은 적응형 양식 작성자의 스크립팅을 용이하게 합니다.

![패널 도구 모음을 사용하여 SOM 표현식 추출](assets/som-expression.png)

패널 도구 모음을 사용하여 SOM 표현식 추출

[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)에 나열된 일부 API는 요소의 SOM 표현식을 사용합니다. 예를 들어 적응형 양식의 특정 필드에 포커스를 표시하려면 해당 SOM 표현식을 `guideBridge`의 `getFocus`API에 전달합니다.
