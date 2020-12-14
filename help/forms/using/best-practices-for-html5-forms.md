---
title: HTML5 양식 우수 사례
seo-title: HTML5 양식 우수 사례
description: 최상의 성능을 위해 XFA 기반의 HTML5 Forms을 조정할 수 있습니다.
seo-description: 최상의 성능을 위해 XFA 기반 HTML5 Forms을 조정하는 방법을 알아봅니다.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
translation-type: tm+mt
source-git-commit: b6c013a31b70166cba80fea53dffc3794ffee5b8
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 1%

---


# HTML5 양식에 대한 우수 사례{#best-practices-for-html-forms}

## 개요 {#overview}

AEM Forms에는 HTML5 양식이라는 구성 요소가 있습니다. HTML5 형식으로 기존 XFA 기반 PDF forms(XDP 파일)을 렌더링하는 데 도움이 됩니다. 이 문서는 모바일 장치에서 로드 시간을 줄이고 HTML5 양식의 성능을 개선하기 위한 지침과 권장 사항을 제공합니다.

대부분의 모바일 장치는 처리 능력과 메모리 기능이 제한되어 있습니다. 모바일 장치의 대기 시간을 개선하는 데 도움이 됩니다. 모바일 장치에서 실행되는 웹 브라우저는 제한된 리소스(메모리 및 처리 기능 제한)에 액세스할 수 있습니다. 제한에 도달하면 브라우저 동작이 느려집니다. 이 문서에서는 HTML5 양식의 크기를 확인할 수 있도록 권장 사항을 제공합니다. 작은 형식은 장치의 메모리 및 처리 성능 제한을 위반하지 않으며, 원활한 환경을 제공합니다.

이 문서에서 설명한 권장 사항은 HTML5 양식을 대상으로 하지만 XFA 기반 PDF forms에도 동일하게 적용됩니다. 이러한 우수 사례는 HTML5 양식의 전반적인 성능에 종합적으로 기여합니다. 효율적이고 생산적인 양식을 개발하기 위해서는 신중한 계획이 필요하다. 시작하기:

## 노드는 HTML5 양식의 통화이므로 현명하게 {#nodes-are-currency-of-html-forms-spend-them-wisely} 사용합니다.

일반적으로 XFA 양식에는 여러 요소가 있습니다. 표, 텍스트 필드, 이미지 등 다양한 요소를 사용할 수 있습니다. 모든 요소에는 요소의 비헤이비어와 모양을 제어할 수 있는 많은 속성이 있습니다. XFA 양식이 HTML5 형식으로 렌더링되면 모든 XFA 요소와 해당 속성이 모델 또는 HTML DOM 노드로 변환됩니다. 이러한 노드는 DOM의 크기와 복잡성에 추가됩니다. HTML5 양식을 렌더링하는 속도가 느려집니다.

브라우저가 보다 간단하게 학습용 DOM을 렌더링할 수 있습니다. XFA 양식에서 다음과 같은 최적화를 수행하여 노드 수를 줄일 수 있습니다. 따라서, 린 DOM 구조를 생성합니다.

* caption 속성을 사용하여 필드에 레이블을 추가합니다. 별도의 텍스트 요소를 사용하여 레이블을 추가하지 마십시오. 이것은 추가 체중을 줄이는 데 도움이 되며, 성과를 얻게 된다. 또한 레이아웃 문제를 방지할 수 있습니다.
* 양식의 Draw 텍스트 요소 수를 최소한으로 유지합니다. 그리기 요소는 가독성과 모양을 향상시키는 데 유용하지만 정보 저장 기능은 없습니다. 여러 Draw 텍스트 요소를 하나의 Draw 텍스트 요소로 병합하는 것이 좋습니다. 돌 하나도 바싹 구워 주지 말고, 좀 더 배어지게 해라.

## lite 양식을 사용하면 리소스를 압축된 상태로 유지 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5 양식에는 이미지, JavaScript 및 CSS 파일과 같은 여러 외부 리소스가 포함될 수 있습니다. 브라우저가 양식을 요청할 때마다 외부 리소스가 네트워크를 통해 전송됩니다. 네트워크를 통해 이동하는 데 필요한 시간은 파일 크기에 비례합니다.

따라서 외부 리소스의 크기를 줄이고 필수 리소스만 사용하는 것이 양식 성능을 향상시키는 기본 방법입니다. XFA 양식에서 다음과 같은 최적화를 수행하여 양식의 외부 리소스 크기를 줄일 수 있습니다.

* [압축된 이미지](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md)를 사용합니다. 양식을 렌더링하는 데 필요한 네트워크 활동과 메모리 양이 줄어듭니다. 따라서 양식 로드 시간은 상당히 줄어듭니다.
* AEM Configuration Manager(Day CQ HTML Library Manager)의 축소 옵션을 사용하여 JavaScript 및 CSS 파일을 압축합니다. 자세한 내용은 [OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md)을 참조하십시오.
* 웹 압축을 활성화합니다. 양식에서 시작된 요청 및 응답 크기를 줄입니다. 자세한 내용은 AEM 양식 서버[의 성능 조정을 참조하십시오.](https://helpx.adobe.com/kr/aem-forms/6-3/performance-tuning-aem-forms.html)

## 관심 영역을 활성 상태로 유지하고 필수 필드 {#keep-the-interest-alive-show-only-required-fields}만 표시합니다.

HTML5 양식은 수백 개의 페이지에 실행될 수 있습니다. 필드가 많이 있는 양식이 브라우저에서 느리게 로드됩니다. XFA 양식에서 다음과 같은 최적화를 수행하여 많은 수의 필드와 페이지로 양식을 최적화할 수 있습니다.

* 큰 양식을 여러 개의 양식으로 분할할 수 있는지 평가합니다. 또한 양식 세트를 사용하여 모든 작은 양식을 함께 그룹화하여 하나의 단위로 표시할 수 있습니다. 양식 세트는 필요한 양식만 로드합니다. 또한 양식 세트에서 데이터 바인딩을 공유하도록 여러 양식의 공통 필드를 구성할 수 있습니다. 데이터 바인딩을 사용하면 일반적인 정보를 한 번만 채울 수 있습니다.정보가 후속 양식에 자동으로 입력되므로 성능이 크게 향상됩니다. 양식 세트에 대한 자세한 내용은 AEM 양식[의 양식 세트를 참조하십시오.](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)
* 섹션을 분할하고 각 섹션을 다른 페이지로 이동하는 것을 고려합니다. HTML5 양식은 페이지 스크롤 요청에서 각 페이지를 동적으로 로드합니다. 스크롤된 페이지(표시되는 페이지 및 앞에 있는 페이지)만 메모리에 저장됩니다.나머지 페이지는 주문형 로드됩니다. 따라서 페이지에서 섹션을 직접 분할하고 이동하면 양식을 로드하는 데 필요한 시간이 줄어듭니다. 양식의 첫 페이지를 랜딩 페이지로 사용할 수도 있습니다. 이는 책의 목차(TOC)와 유사합니다. 양식의 랜딩 페이지에는 양식의 다른 섹션에 대한 링크만 들어 있습니다. 양식 첫 페이지의 로드 시간이 크게 개선되고 사용자 환경이 개선됩니다.
* 기본적으로 조건부 섹션을 숨겨진 상태로 유지합니다. 특정 조건이 충족될 때만 이러한 섹션을 볼 수 있도록 합니다. DOM의 크기를 최소로 유지하는 데 도움이 됩니다. 탭 방식의 탐색을 사용하여 한 번에 하나의 섹션만 표시할 수도 있습니다.

## 적은 수의 경우 {#less-is-more-reduce-the-number-of-pages} 페이지 수를 줄입니다.

HTML5 양식에는 데이터 기반 필드(테이블 및 하위 양식)가 포함될 수 있습니다. 이러한 필드는 런타임에 양식 크기를 확장합니다. 예를 들어 HTML5 양식의 데이터 기반 표는 수천 개의 행으로 확장할 수 있습니다. 이러한 표로 인해 레이아웃과 성능이 저하될 수 있습니다. 아래에 제안된 최적화는 데이터 기반 필드를 사용하여 HTML5 양식의 로드 시간을 줄이는 데 도움이 될 수 있습니다.

* XFA 스크립팅을 사용하여 페이징된 탐색을 수행하여 데이터 기반 필드(테이블 및 하위 양식)를 표시할 수 있습니다. 페이지 탐색 시 특정 데이터만 페이지에 표시됩니다. 브라우저 페인트 작업을 한 번에 표시되는 필드로 제한하므로 양식을 쉽게 탐색할 수 있습니다. 또한 모바일 디바이스의 사용자는 데이터 하위 세트에만 관심이 있습니다. 뛰어난 사용자 경험을 제공하고 필요한 데이터를 로드하는 데 소요되는 시간을 줄일 수 있습니다. 하나의 가격에 두 가지 솔루션을 사용할 수 있습니다.  페이지 탐색은 즉시 사용할 수 없습니다. XFA 스크립팅을 사용하여 페이징된 탐색을 개발할 수 있습니다.

* 여러 읽기 전용 열을 하나의 열로 병합하는 방법을 평가할 수 있습니다. 양식을 표시하는 데 필요한 메모리가 줄어듭니다. 또한 사용자의 입력이 필요하지 않은 열을 표시하지 않습니다.
* 위의 제안에서 많은 개선이 이루어지지 않는 경우 데이터 기반 양식을 [양식 세트](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)로 분할할 것을 평가합니다. 예를 들어 표에 행이 1,000개가 넘는 경우 100개 행마다 다른 형식으로 이동합니다. 양식의 로드 시간과 성능을 개선하는 데 도움이 됩니다.  또한 양식 세트는 모든 양식에 대해 통합된 제출 XML을 생성합니다. 모든 양식의 데이터를 차별화하려면 다른 데이터 루트를 사용하십시오. 자세한 내용은 AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)의 [양식 세트를 참조하십시오.

## 기록 문서(DOR) {#power-of-two-for-document-of-record-dor}에 대한 2의 성능

XFA 양식에는 DOR(Document of Record) 전용 섹션 수가 많을 수 있습니다. 노드 수를 줄이고 이러한 양식의 성능을 향상시키기 위해 양식의 사본을 서로 다르게 유지할 수 있습니다. 이 사본은 양식을 채울 사본 한 개, 서버에서 기록 문서를 생성하는 사본 한 개를 유지합니다. XFA 양식을 채울 복사본에는 데이터를 캡처하는 데만 필요한 필드가 표시됩니다. 기록 문서 XFA 생성 위치에서 양식 인쇄 출력에만 필요한 필드를 유지합니다. 제안된 방법을 선택하기 전에 성능 상승과 유지 관리 간접비를 평가하십시오.

## 권장 읽기: {#recommended-reads}

AEM(Adobe Experience Manager) 양식을 사용하면 복잡한 트랜잭션을 간단하고 매력적인 디지털 경험으로 탈바꿈시킬 수 있습니다. 그러나 효율적이고 생산적인 양식을 개발하기 위해서는 여러 노력이 필요합니다. 다음은 HTML5 Forms 외에도 일반적인 AEM 우수 사례를 위한 몇 가지 권장 사항입니다.

* [AEM 배포 및 유지 관리를 위한 모범 사례](/help/sites-deploying/best-practices.md)
* [컨텐츠 작성 우수 사례](/help/sites-authoring/best-practices.md)
* [AEM 관리에 대한 우수 사례](/help/sites-administering/administer-best-practices.md)
* [솔루션 개발을 위한 모범 사례](/help/sites-developing/best-practices.md)
* [적응형 양식 작업을 위한 우수 사례](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms Server는 동적 PDF 양식에 글꼴을 포함하지 않습니다.](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 빠른 참조 카드 {#quick-reference-card}

다음 카드를 인쇄(고해상도 버전을 다운로드하려면 카드 클릭)하고 빠른 참조를 위해 책상에 보관하십시오.
[ ![HTML5 Forms 우수 사례 빠른 참조 카드](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
