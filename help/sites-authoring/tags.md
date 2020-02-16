---
title: 태그 사용
seo-title: 태그 사용
description: 태그는 웹 사이트에 포함된 컨텐츠를 빠르고 손쉽게 분류할 수 있는 방법입니다.
seo-description: 태그는 웹 사이트에 포함된 컨텐츠를 빠르고 손쉽게 분류할 수 있는 방법입니다.
uuid: 5d922443-f924-426e-acf4-27dffd1053f6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9fb6d603-eb17-4192-bfa6-6c316f14ac7d
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# 태그 사용{#using-tags}

태그는 웹 사이트에 포함된 컨텐츠를 빠르고 손쉽게 분류할 수 있는 방법입니다. 태그는 검색을 통해 해당 컨텐츠 및 관련 컨텐츠를 찾을 수 있도록 하기 위해 페이지, 자산 또는 컨텐츠에 첨부할 수 있는 키워드 또는 레이블이라고 할 수 있습니다.

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## 태깅을 사용해야 하는 10가지 이유 {#ten-reasons-to-use-tagging}

1. **컨텐츠 구성** - 태깅을 사용하면 간단하게 컨텐츠를 신속하게 구성할 수 있으므로 보다 손쉽게 작업할 수 있습니다.
1. **태그 구성** - 태그는 컨텐츠를 구성하는 동안 계층 구조 분류/네임스페이스가 태그를 구성합니다.
1. **심층적인 구성** 태그 - 태그와 하위 태그를 만들 수 있으므로 전체 분류 체계 시스템, 상위 용어, 하위 개념 및 이들의 관계를 표현할 수 있습니다. 이를 통해 정식 계층 구조 이외에 두 번째 또는 세 번째 컨텐츠 계층 구조를 만들 수 있습니다.
1. **제어된 태깅** - 태그 및/또는 네임스페이스에 권한을 적용하여 태그 생성 및 애플리케이션을 제어함으로써 태깅을 제어할 수 있습니다.
1. **유연한 태깅** - 태그에는 다음과 같은 이름과 얼굴이 많이 있습니다.태그, 분류 용어, 카테고리, 레이블 등 따라서 다양한 컨텐츠 모델에서 다양한 방식으로 태그를 사용할 수 있습니다. 예를 들어 타겟 인구집단을 선정하거나, 컨텐츠를 분류하거나, 컨텐츠에 등급을 매기거나, 두 번째 컨텐츠 계층 구조를 만들 수 있습니다.
1. **향상된 검색** - AEM의 기본 검색 구성 요소에는 만든 태그 및 필터를 적용하여 관련 있는 태그로 결과 범위를 좁힐 수 있는 적용된 태그가 광범위하게 포함됩니다.
1. **SEO 활성화** - 페이지 속성으로 적용된 태그는 페이지의 메타태그에 자동으로 표시되므로 검색 엔진에 표시됩니다.
1. **간단한 정교함** - 태그를 단어와 버튼 터치만으로 간단하게 만들 수 있습니다. 그런 다음, 제목, 설명 및 무제한 레이블을 추가하여 태그에 더 많은 의미 체계를 제공할 수 있습니다.
1. **핵심 일관성** - 태깅 시스템은 AEM의 핵심 구성 요소이며 모든 AEM 기능에서 컨텐츠를 분류하는 데 사용됩니다. 또한 태깅 API는 개발자가 동일한 분류법에 액세스할 수 있는 태깅 지원 애플리케이션을 작성하는 데 사용할 수 있습니다.
1. **구조 및 유연성 결합** - AEM은 페이지와 경로가 중첩되어 구조화된 정보를 사용하여 작업하는 데 이상적입니다. 전체 텍스트 검색 기능이 내장되어 있으므로 비구조적인 정보로 작업할 때에도 동일한 성능을 발휘합니다. 태깅은 구조 및 유연성의 장점을 결합합니다.

사이트의 컨텐츠 구조 및 자산의 메타데이터 스키마를 디자인할 때는 태깅이 제공하는 액세스 가능한 간단한 접근 방법을 고려하십시오.

## 태그 적용 {#applying-tags}

In the author environment, authors may apply tags by accessing the page properties and entering one or more tags in the **Tags/Keywords** field.

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window. The **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy.

![chlimage_1-41](assets/chlimage_1-41.png)

### 태그 게시 {#publishing-tags}

페이지와 마찬가지로 태그 및 네임스페이스에 대해 다음 작업을 수행할 수 있습니다.

**활성화**

* 개별 태그를 활성화합니다.

   페이지와 마찬가지로 새로 만든 태그를 활성화해야 게시 환경에서 사용할 수 있습니다.

>[!NOTE]
>
>페이지를 활성화하면 대화 상자가 자동으로 열리고 해당 페이지에 속하는 활성화되지 않은 태그를 활성화할 수 있습니다.

**비활성화**

* 선택한 태그를 비활성화합니다.
