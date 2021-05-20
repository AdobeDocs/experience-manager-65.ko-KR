---
title: 컬렉션 관리
seo-title: 컬렉션 관리
description: 컬렉션은 덮개의 테마에 맞는 문서 또는 배너와 같은 콘텐츠로 채워진 잘 정의된 버킷을 나타냅니다. 자세한 내용은 이 페이지를 참조하십시오.
seo-description: 컬렉션은 덮개의 테마에 맞는 문서 또는 배너와 같은 콘텐츠로 채워진 잘 정의된 버킷을 나타냅니다. 자세한 내용은 이 페이지를 참조하십시오.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---

# 컬렉션 관리{#managing-collections}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

컨텐츠 관리 작업은 애플리케이션 내에서 컨텐츠를 만들고 관리하는 데 도움이 되는 기본 구성단위입니다. 애플리케이션 내의 컨텐츠에 대해 다음 작업이 수행됩니다.

## 컬렉션 개요 {#collections-overview}

컬렉션은 덮개의 테마에 맞는 문서 또는 배너와 같은 컨텐츠로 채워진 잘 정의된 *버킷*&#x200B;을 나타냅니다.

>[!NOTE]
>
>AEM Mobile 앱의 다음 항목에 대해 알려면 온라인 도움말의 다음 리소스를 참조하십시오.
>
>* [디자인 고려 사항](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [컬렉션 관리](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)

>



## 컬렉션 만들기 {#creating-a-collection}

컬렉션을 만드는 일반적인 워크플로우는 다음과 같습니다.

1. 사이드 레일에서 **모바일**&#x200B;을 선택합니다.
1. 모바일의 카탈로그에서 Mobile On-Demand 앱을 선택합니다.
1. **컬렉션 관리** 타일의 오른쪽 위 모서리에 있는 아래쪽 화살표를 클릭합니다.
1. 마법사의 각 단계에서 작업하여 새 문서 만들기를 계속합니다.
1. 준비가 되면 **만들기**&#x200B;를 클릭합니다.
1. 새 문서가 **컬렉션 관리** 타일에 나타납니다.

![chlimage_1-1](assets/chlimage_1-1.gif)

## 새 컬렉션 가져오기 {#importing-a-new-collection}

기존 Mobile On-Demand 콘텐츠는 Mobile On-Demand에서 AEM으로 다운로드(가져옴)할 수 있습니다. 이렇게 하면 로컬 컨텐츠를 편집하고 볼 수 있습니다.

>[!NOTE]
>
>가져오기에 이미지가 포함되지 않습니다.

새 컬렉션을 가져오는 워크플로우

1. 모바일의 카탈로그에서 Mobile On-Demand 앱을 선택합니다.
1. **컬렉션 관리** 타일의 오른쪽 위 모서리에 있는 아래쪽 화살표를 클릭하고 컬렉션 가져오기를 선택합니다.
1. 대화 상자에서 **컬렉션 가져오기**&#x200B;를 클릭한 다음 닫기를 클릭합니다.
1. 이제 모바일 온디맨드 컬렉션이 **컬렉션 관리** 타일에 나타납니다.

>[!CAUTION]
>
>먼저 Mobile On-Demand 연결을 연결해야 합니다.

## 컬렉션 편집 {#editing-a-collection}

기본 제공 AEM 드래그 앤 드롭 편집기를 사용하여 문서를 추가하거나 변경합니다. 텍스트 및 이미지와 같은 구성 요소를 추가/제거할 수 있습니다. DAM 자산의 이미지를 삽입할 수 있습니다.

컬렉션을 편집하는 워크플로우:

1. 모바일의 카탈로그에서 Mobile On-Demand 앱을 선택합니다.
1. **컬렉션 관리** 타일에서 AEM 소스 문서를 선택합니다.
1. 목록 보기에서 강조 표시된 컬렉션을 클릭하여 콘텐츠 편집기에서 엽니다.
1. 콘텐츠 편집기를 사용하여 컬렉션 콘텐츠(원고, 이미지, 텍스트 등)를 끌어서 놓습니다.

### 컬렉션 {#viewing-and-editing-the-metadata-within-a-collection} 내의 메타데이터 보기 및 편집

컬렉션에는 제목, 설명, 이미지 등의 다양한 속성이 있습니다. 이 작업은 이러한 속성을 보고 수정하는 데 사용됩니다. 선택적으로, 이러한 변경 사항은 저장 시 Mobile On-Demand에 업로드할 수 있습니다.

컬렉션을 보거나 편집하는 일반 워크플로우입니다.

1. 모바일의 카탈로그에서 Mobile On-Demand 앱을 선택합니다.
1. **컬렉션 관리** 타일에서 컬렉션을 선택합니다.

1. 작업 표시줄에서 **속성**&#x200B;을 선택합니다.
1. 해당 문서에 대해 사용 가능한 모든 메타 데이터를 표시합니다.
1. 원하는 경우 메타 데이터를 편집하고 완료되면 **저장**&#x200B;을 클릭합니다.
1. 원할 경우, 변경 사항을 즉시 Mobile On-Demand에 업로드합니다.

## 컬렉션 업로드 {#uploading-a-collection}

업로드 작업은 선택한 컨텐츠를 복사하고 Mobile On-Demand 프로젝트에 추가합니다. 이미 기존 Mobile On-Demand 콘텐츠가 새 버전으로 대체되었습니다.

컬렉션을 업로드하는 일반 워크플로우입니다.

1. **모바일**&#x200B;에서 카탈로그에서 모바일 온디맨드 앱을 선택합니다.
1. **컬렉션 관리** 타일에서 Mobile On-Demand에 업로드할 문서를 선택합니다.
1. 필요한 경우 목록 보기에서 컬렉션을 더 추가합니다.
1. 작업 표시줄에서 **업로드**&#x200B;를 선택한 다음 대화 상자에서 업로드 를 클릭합니다.
1. 이제 컬렉션이 Mobile On-Demand에 업로드됩니다.

## 컬렉션 {#deleting-a-collection} 삭제

이 작업은 Mobile On-Demand에서 선택한 컬렉션을 삭제하고 선택적으로 로컬 AEM 인스턴스에서 삭제합니다.

컬렉션을 삭제하는 일반 워크플로우입니다.

1. 모바일의 카탈로그에서 Mobile On-Demand 앱을 선택합니다.
1. **컬렉션 관리** 타일에서 삭제할 문서를 선택합니다.
1. 목록에서 선택되었는지 확인합니다(필요에 따라 삭제할 다른 항목 선택).
1. 작업 표시줄에서 **삭제**&#x200B;를 클릭합니다.
1. AEM 및 Mobile On-Demand에서 삭제할 것인지 확인하십시오.
1. **삭제**&#x200B;를 클릭합니다. 
1. 이제 컬렉션이 목록에서 제거됩니다.

## 컬렉션에 컨텐츠 추가 {#adding-content-to-collections}

컬렉션은 기본적으로 관련 컨텐츠의 카테고리입니다. 이들은 문서, 배너와 같은 컨텐츠를 앱의 탐색 구조를 정의하는 패키지로 수집합니다. 컬렉션은 중첩될 수 있습니다.

>[!NOTE]
>
>콘텐츠를 컬렉션에 추가하려면 먼저 Mobile On-Demand에 업로드해야 합니다.

컬렉션은 기본적으로 관련 컨텐츠의 카테고리입니다.이들은 문서, 배너와 같은 컨텐츠를 앱의 탐색 구조를 정의하는 패키지로 수집합니다. 컬렉션은 중첩될 수 있습니다.

1. 모바일의 카탈로그에서 Mobile On-Demand 앱을 선택합니다.
1. 이전에 업로드한 문서(또는 배너/컬렉션)를 선택합니다
1. 작업 표시줄에서 추가 대상 을 선택합니다.
1. 대화 상자에서 이전에 업로드한 컬렉션을 선택합니다.
1. **업데이트**&#x200B;를 클릭하여 컬렉션에 콘텐츠를 추가합니다.

![chlimage_1-2](assets/chlimage_1-2.gif)

### 다음 단계 {#the-next-steps}

컬렉션 관리에 대해 알고 싶은 사람은

* [배너 관리](/help/mobile/mobile-on-demand-managing-banners.md)
* [문서 관리](/help/mobile/mobile-on-demand-managing-articles.md)
* [공유 리소스 업로드](/help/mobile/mobile-on-demand-shared-resources.md)
* [컨텐츠 게시/게시 취소](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [프리플라이트 사용 미리 보기](/help/mobile/aem-mobile-manage-ondemand-services.md)
