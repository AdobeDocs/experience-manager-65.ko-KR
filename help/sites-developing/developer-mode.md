---
title: 개발자 모드
seo-title: 개발자 모드
description: 개발자 모드에서는 개발자에게 현재 페이지에 대한 정보를 제공하는 여러 탭이 있는 사이드 패널을 엽니다
seo-description: 개발자 모드에서는 개발자에게 현재 페이지에 대한 정보를 제공하는 여러 탭이 있는 사이드 패널을 엽니다
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---

# 개발자 모드{#developer-mode}

AEM에서 페이지를 편집할 때 개발자 모드를 포함하여 몇 가지 [모드](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui)를 사용할 수 있습니다. 이렇게 하면 개발자에게 현재 페이지에 대한 정보를 제공하는 여러 탭이 있는 사이드 패널이 열립니다. 세 개의 탭은 다음과 같습니다.

* **[](#components)** 구조 및 성능 정보를 보기 위한 구성 요소입니다.
* **[](#tests)** 테스트 실행 및 결과 분석을 위한 테스트입니다.
* **[](#errors)** 발생한 문제를 확인하는 동안 오류가 발생했습니다.

개발자는 다음 작업을 수행할 수 있습니다.

* 검색:어떤 페이지로 구성됩니까?
* 디버그:어디에서 언제 그리고 언제 무슨 일이 일어나는가 하는 것은 문제를 해결하는 데 도움이 됩니다.
* 테스트:응용 프로그램이 예상대로 작동합니까?

>[!CAUTION]
>
>개발자 모드:
>
>* 터치 활성화 UI에서만 사용할 수 있습니다(페이지를 편집할 때).
>* 모바일 장치나 데스크탑의 작은 창에서 사용할 수 없습니다(공간 제한 때문에).

   >
   >   
   * 너비가 1024px 미만인 경우 발생합니다.
>* `administrators` 그룹의 구성원인 사용자만 사용할 수 있습니다.


>[!CAUTION]
>
>개발자 모드는 nosamplecontent 실행 모드를 사용하지 않는 표준 작성자 인스턴스에서만 사용할 수 있습니다.
>
>필요한 경우 다음을 사용하도록 구성할 수 있습니다.
>
>* nosamplecontent 실행 모드를 사용하는 작성자 인스턴스
>* 게시 인스턴스

>
>
사용 후 다시 비활성화해야 합니다.

>[!NOTE]
>
>다음을 참조하십시오.
>
>* 기술 자료 문서, [AEM TouchUI 문제 해결](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html) 을 참조하십시오.
>* AEM Gems 세션 [AEM 6.0 개발자 모드](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)에 대한 .

>



## 개발자 모드 열기 {#opening-developer-mode}

개발자 모드가 페이지 편집기에 사이드 패널로 구현됩니다. 패널을 열려면 페이지 편집기의 도구 모음에서 모드 선택기에서 **개발자** 를 선택합니다.

![chlimage_1-11](assets/chlimage_1-11.png)

패널은 다음 두 개의 탭으로 나뉘어 있습니다.

* **[구성 요소](/help/sites-developing/developer-mode.md#components)**  - 작성자의  [컨텐츠 트리](/help/sites-authoring/author-environment-tools.md#content-tree) 와 유사한 구성 요소 트리가 표시됩니다

* **[오류](/help/sites-developing/developer-mode.md#errors)**  - 문제가 발생하면 각 구성 요소에 대한 세부 정보가 표시됩니다.

### 구성 요소 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

다음과 같은 구성 요소 트리가 표시됩니다.

* 페이지에서 렌더링되는 구성 요소 및 템플릿 체인(SLY, JSP 등)에 대해 설명합니다. 트리를 확장하여 계층 내에 컨텍스트를 표시할 수 있습니다.
* 구성 요소를 렌더링하는 데 필요한 서버측 계산 시간을 표시합니다.
* 트리를 확장하고 트리 내에서 특정 구성 요소를 선택할 수 있습니다. 선택 사항에서는 구성 요소 세부 사항에 액세스할 수 있습니다.예:

   * 저장소 경로
   * 스크립트에 대한 링크(CRXDE Lite에서 액세스)

* 선택한 구성 요소(컨텐츠 플로우에서 파란색 테두리로 표시됨)가 컨텐츠 트리에 강조 표시됩니다. 그 반대의 경우도 마찬가지입니다.

이를 통해 다음을 수행할 수 있습니다.

* 구성 요소당 렌더링 시간을 결정하고 비교합니다.
* 계층 구조를 보고 이해합니다.
* 느린 구성 요소를 찾아 페이지 로드 시간을 파악하고 개선합니다.

각 구성 요소 항목에는 (예:) 다음 항목이 표시될 수 있습니다.

![chlimage_1-13](assets/chlimage_1-13.png)

* **세부 사항 보기**:다음을 보여주는 목록에 대한 링크:

   * 구성 요소를 렌더링하는 데 사용되는 모든 구성 요소 스크립트.
   * 이 특정 구성 요소의 저장소 컨텐츠 경로입니다.

   ![chlimage_1-14](assets/chlimage_1-14.png)

* **스크립트 편집**:링크:

   * CRXDE Lite에서 구성 요소 스크립트를 엽니다.

* 구성 요소 항목(화살표 헤드)을 확장하면 다음 내용이 표시될 수도 있습니다.

   * 선택한 구성 요소 내의 계층 입니다.
   * 격리된 선택한 구성 요소의 렌더링 시간, 구성 요소 내에 중첩된 개별 구성 요소 및 결합된 합계입니다.

   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>일부 링크는 `/libs` 아래의 스크립트를 가리킵니다. 그러나 이러한 매개 변수는 참조용이므로 **이 `/libs` 아래에 있는 것은 편집하지 않아야 합니다. 변경한 내용이 손실될 수 있습니다.** 이는 핫픽스/기능 팩을 업그레이드하거나 적용할 때마다 이 분기가 변경 사항에 영향을 주기 때문입니다. 필요한 모든 변경 사항은 `/apps`오버레이 및 무시](/help/sites-developing/overlays.md)를 참조하십시오.[

### 오류 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

바라건대 **오류** 탭은 항상 비어 있기를(위와 같이) 하지만 문제가 발생하면 각 구성 요소에 대해 다음 세부 정보가 표시됩니다.

* 구성 요소가 오류 로그에 항목을 기록하고 오류 세부 정보와 CRXDE Lite 내의 해당 코드에 대한 직접 링크가 있는 경우 경고.
* 구성 요소에서 관리 세션을 여는 경우 경고.

예를 들어 정의되지 않은 메서드가 호출되는 경우 결과 오류가 **오류** 탭에 표시됩니다.

![chlimage_1-17](assets/chlimage_1-17.png)

구성 요소 탭의 트리에 있는 구성 요소 항목에도 오류가 발생할 때 표시기가 표시됩니다.

### 테스트 {#tests}

>[!CAUTION]
>
>AEM 6.2에서 개발자 모드의 테스트 기능이 독립형 도구 애플리케이션으로 다시 구현되었습니다.
>
>자세한 내용은 [UI 테스트](/help/sites-developing/hobbes.md)를 참조하십시오.
