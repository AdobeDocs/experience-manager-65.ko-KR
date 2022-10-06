---
title: HTML 5 양식 우수 사례
seo-title: Best practices for HTML5 forms
description: 최상의 성능을 위해 XFA 기반 HTML5 Forms을 조정하십시오.
seo-description: Learn how to tune your XFA-based HTML5 Forms for best performance.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 1%

---

# HTML 5 양식 우수 사례{#best-practices-for-html-forms}

## 개요 {#overview}

AEM Forms에는 HTML 5 양식이라는 구성 요소가 있습니다. 기존 XFA 기반 PDF forms(XDP 파일)를 HTML5 형식으로 렌더링하는 데 도움이 됩니다. 이 문서에서는 로드 시간을 줄이고 모바일 장치에서 HTML5 양식의 성능을 개선하기 위한 지침과 권장 사항을 제공합니다.

대부분의 모바일 장치에는 제한된 처리 성능과 메모리 기능이 있습니다. 모바일 장치의 대기 시간을 개선하는 데 도움이 됩니다. 모바일 장치에서 실행되는 웹 브라우저는 제한된 리소스(메모리 및 처리 기능이 제한됨)에 액세스할 수 있습니다. 제한에 도달하면 브라우저 동작이 느려집니다. 이 문서에서는 HTML5 양식의 크기를 확인하는 권장 사항을 제공합니다. 더 작은 형태는 장치의 메모리 및 처리 전력 제한을 위반하지 않으며 원활한 경험을 제공합니다.

이 문서에서 설명한 권장 사항은 HTML5 양식을 대상으로 하지만 XFA 기반 PDF forms에도 동일하게 적용됩니다. 이러한 우수 사례는 HTML5 양식의 전반적인 성능에 종합적으로 기여합니다. 효율적이고 생산적인 양식을 개발하기 위해서는 신중한 계획이 필요하다. 시작하기:

## 노드는 HTML 5 양식의 통화이며 현명하게 사용합니다 {#nodes-are-currency-of-html-forms-spend-them-wisely}

일반적으로 XFA 양식에는 여러 요소가 있습니다. 예를 들어, 표, 텍스트 필드 및 이미지가 있습니다. 모든 요소에는 요소의 동작과 모양을 제어하는 여러 개의 속성이 있습니다. XFA 양식을 HTML5 형식으로 렌더링하면 모든 XFA 요소 및 해당 속성이 모델 또는 HTML DOM 노드로 변환됩니다. 이러한 노드는 DOM의 크기와 복잡성에 추가됩니다. HTML5를 느리게 만들어 렌더링합니다.

브라우저가 보다 쉽게 대여 DOM을 렌더링할 수 있습니다. 따라서 XFA 양식에서 다음 최적화를 수행하여 노드 수를 줄일 수 있습니다. 따라서 린 DOM 구조를 생성합니다.

* 캡션 속성을 사용하여 필드에 레이블을 추가합니다. 별도의 텍스트 요소를 사용하여 레이블을 추가하지 마십시오. 체중이 줄면 효과가 생기고 실적도 향상된다. 레이아웃 문제를 방지하는 데에도 도움이 됩니다.
* 양식의 텍스트 요소 수를 최소로 유지합니다. 그리기 요소는 가독성과 모양을 개선하는 데 도움이 되지만 정보 저장 기능은 없습니다. 여러 그리기 텍스트 요소를 단일 그리기 텍스트 요소에 병합하는 것이 좋습니다. 돌을 던지지 않고 마르지 않도록 해라.

## Lite 양식은 리소스를 압축하여 유지합니다 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5 양식에는 이미지, JavaScript 및 CSS 파일과 같은 여러 외부 리소스가 포함될 수 있습니다. 브라우저가 양식을 요청할 때마다 외부 리소스가 네트워크를 통해 전송됩니다. 네트워크를 통해 이동하는 데 필요한 시간은 파일 크기와 직접 같습니다.

따라서, 외부 자원의 크기를 줄이고 절대적으로 필요한 리소스만 사용하는 것이 양식의 성능을 향상시키는 바람직한 방법입니다. XFA 양식에서 다음 최적화를 수행하여 양식의 외부 리소스 크기를 줄일 수 있습니다.

* 사용 [압축 이미지](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). 양식을 렌더링하는 데 필요한 네트워크 작업 및 메모리 양을 줄입니다. 따라서 양식 로드 시간이 크게 줄어듭니다.
* AEM 구성 관리자(Day CQ HTML 라이브러리 관리자)의 축소 옵션을 사용하여 JavaScript 및 CSS 파일을 압축합니다. 자세한 내용은 [OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md).
* 웹 압축을 활성화합니다. 양식에서 시작된 요청 및 응답 크기를 줄입니다. 자세한 내용은 [AEM Forms 서버의 성능 조정](https://helpx.adobe.com/kr/aem-forms/6-3/performance-tuning-aem-forms.html).

## 관심 영역을 활성화하여 필수 필드만 표시  {#keep-the-interest-alive-show-only-required-fields}

HTML5 양식은 수백 개의 페이지로 실행될 수 있습니다. 필드가 많은 양식이 브라우저에서 느리게 로드됩니다. XFA 양식에서 다음 최적화를 수행하여 많은 필드 및 페이지로 양식을 최적화할 수 있습니다.

* 큰 양식을 여러 양식으로 분할하는 것을 평가합니다. 또한 양식 세트를 사용하여 모든 작은 양식을 함께 그룹화하여 하나의 단위로 표시할 수도 있습니다. 양식 세트는 필요한 양식만 로드합니다. 또한 양식 세트에서 데이터 바인딩을 공유하도록 여러 양식의 공통 필드를 구성할 수 있습니다. 데이터 바인딩은 사용자가 일반적인 정보를 한 번만 채우는 데 도움이 됩니다. 이 정보는 후속 양식에 자동으로 입력되므로 성능이 크게 개선됩니다. 양식 세트에 대한 자세한 내용은 [AEM 양식의 양식 세트](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* 섹션을 분할하고 각 섹션을 다른 페이지로 이동하는 것을 고려해 보십시오. HTML5 forms는 페이지 스크롤 요청 시 각 페이지를 동적으로 로드합니다. 스크롤된 페이지(표시되는 페이지 및 앞에 오는 페이지)만 메모리에 저장됩니다. 나머지 페이지는 필요에 따라 로드됩니다. 따라서 고유한 페이지의 섹션을 분할하고 이동하면 양식을 로드하는 데 필요한 시간이 줄어듭니다. 양식의 첫 번째 페이지를 랜딩 페이지로 사용할 수도 있습니다. 이는 책의 목차(TOC)와 유사합니다. 양식의 랜딩 페이지에는 양식의 다른 섹션에 대한 링크만 포함되어 있습니다. 양식 첫 페이지의 로드 시간이 크게 개선되어 사용자 경험이 개선됩니다.
* 기본적으로 조건부 섹션을 숨겨진 상태로 유지합니다. 특정 조건이 충족될 경우에만 이러한 섹션을 볼 수 있습니다. DOM의 크기를 최소로 유지하는 데 도움이 됩니다. 탭 탐색을 사용하여 한 번에 하나의 섹션만 표시할 수도 있습니다.

## 페이지 수가 적을수록 페이지 수가 줄어듭니다 {#less-is-more-reduce-the-number-of-pages}

HTML5 양식에는 데이터 기반 필드(표 및 하위 양식)가 포함될 수 있습니다. 이러한 필드는 런타임에 양식 크기를 확장합니다. 예를 들어 HTML5 양식의 데이터 기반 테이블은 수천 개의 행에 걸쳐 있을 수 있습니다. 이러한 표로 인해 레이아웃과 성능이 저하될 수 있습니다. 아래 제안된 최적화는 데이터 기반 필드를 사용하여 HTML5 양식의 로드 시간을 줄이는 데 도움이 될 수 있습니다.

* XFA 스크립팅을 사용하여 데이터 기반 필드(테이블 및 하위 양식)를 표시할 수 있는 페이징된 탐색을 만들 수 있습니다. 페이지 탐색에서는 특정 데이터만 페이지에 표시됩니다. 한 번에 표시되는 필드로 브라우저 페인트 작업을 제한하므로 양식을 쉽게 탐색할 수 있습니다. 또한 모바일 장치의 사용자는 데이터 하위 집합에만 관심이 있습니다. 우수한 사용자 경험을 제공하고 필요한 데이터를 로드하는 데 필요한 시간을 줄이는 데 도움이 됩니다. 한 가지 가격에 두 가지 해결책을 얻을 수 있습니다.  또한 페이지 탐색은 즉시 사용할 수 없습니다. XFA 스크립팅을 사용하여 페이지 탐색 기능을 개발할 수 있습니다.

* 여러 읽기 전용 열을 하나의 열에 병합하는 것을 평가합니다. 양식을 표시하는 데 필요한 메모리가 줄어듭니다. 또한 사용자의 입력이 필요하지 않은 열을 표시하지 마십시오.
* 데이터 기반 양식을 [양식 세트](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)위의 제안에서 많은 개선 사항을 제공하지 않는 경우. 예를 들어 테이블에 행이 1000개를 초과하는 경우 100개 행마다 다른 형식으로 이동합니다. 양식의 로드 시간과 성능을 개선하는 데 도움이 됩니다.  또한 양식 세트는 모든 양식에 대해 통합된 제출 XML을 생성합니다. 모든 양식의 데이터를 구분하려면 다른 데이터 루트를 사용하십시오. 자세한 내용은 [AEM Forms의 양식 세트](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## DOR(Document of Record)에 대한 2의 힘 {#power-of-two-for-document-of-record-dor}

XFA 양식에는 DOR(Document of Record)에 대해서만 많은 수의 섹션이 포함될 수 있습니다. 노드 수를 줄이고 이러한 양식의 성능을 향상시키기 위해 양식의 다른 복사본을 유지 관리할 수 있습니다. 이 사본은 양식을 채우는 사본, 다른 사본은 서버에서 기록 문서를 생성합니다. XFA 양식을 채울 복사본에 데이터를 캡처하는 데만 필요한 필드가 표시됩니다. XFA 생성 생성에서 양식의 인쇄 출력에만 필요한 필드를 유지합니다. 제안된 접근 방식을 선택하기 전에 성능 향상 및 유지 관리 오버헤드를 평가하십시오.

## 권장 읽기  {#recommended-reads}

Adobe Experience Manager (AEM) 양식을 사용하면 복잡한 트랜잭션을 간편하고 쾌적한 디지털 경험으로 변환할 수 있습니다. 그러나 효율적이고 생산적인 양식을 개발하기 위해서는 공동 노력이 필요합니다. 다음은 HTML5 Forms 외에도 일반적인 AEM 우수 사례에 대해 권장되는 몇 가지 읽기입니다.

* [AEM 배포 및 유지 관리에 대한 우수 사례](/help/sites-deploying/best-practices.md)
* [컨텐츠 작성 우수 사례](/help/sites-authoring/best-practices.md)
* [AEM 관리에 대한 우수 사례](/help/sites-administering/administer-best-practices.md)
* [솔루션 개발을 위한 우수 사례](/help/sites-developing/best-practices.md)
* [적응형 양식 작업을 위한 우수 사례](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms 서버가 동적 PDF 양식에 글꼴을 포함하지 않습니다](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 빠른 참조 카드 {#quick-reference-card}

다음 카드(고해상도 버전을 다운로드하려면 카드 클릭)를 인쇄하고 빠른 참조를 위해 책상에 보관하십시오.
[ ![HTML5 Forms 우수 사례 빠른 참조 카드](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
