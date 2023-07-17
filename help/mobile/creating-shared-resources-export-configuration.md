---
title: 공유 리소스 내보내기 구성 만들기
description: 이 페이지를 따라 Adobe Experience Manager(AEM)에서 AEM Mobile으로 업로드할 공유 리소스를 내보내는 방법에 대해 알아봅니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# 공유 리소스 내보내기 구성 만들기{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**전제 조건**:
>
>공유 리소스 만들기 및 수정에 대해 학습하기 전에 다음을 참조하십시오. [컨텐츠 동기화](/help/mobile/mobile-ondemand-contentsync.md) 기본 개념을 이해할 수 있습니다.

Adobe Experience Manager(AEM) 모바일 사용자는 컨텐츠 동기화를 사용하여 라이브 컨텐츠를 모바일 앱에서 사용할 수 있는 정적 컨텐츠로 내보내고 이 내보내기는 컨텐츠가 AEM Mobile에서 Mobile On-Demand Services로 업로드될 때 발생합니다.

속성 ***dps-exportTemplate*** 위의 표에 언급된 대로 앱의 내보내기 구성에 대한 경로를 정의합니다. 공유 리소스를 만들고 수정하려면 이 속성을 설정하십시오.

다음 리소스는 AEM Mobile에 업로드하기 위해 AEM에서 공유 리소스를 내보내는 방법에 대해 설명합니다.

공유 HTML 리소스를 통해 문서는 모든 문서에 대해 복제되는 HTML 리소스를 공유할 수 있으며 아이콘, 글꼴, JavaScript 및 css를 포함할 수 있습니다.

다음 위치에서 콘텐츠 동기화 구성 찾음: **&lt;dps-exporttemplate>/dps-HTMLResources>** 장치에서 속성 정적 렌더링에 필요한 모든 콘텐츠와 문서를 내보내도록 구성해야 합니다.

>[!CAUTION]
>
>다음 사항이 있는 경우에만 아래 단계를 수행하여 샘플 공유 리소스를 볼 수 있습니다.
>
>* 샘플 콘텐츠 설치
>* AEM 인스턴스 실행 중
>* 구성된 사용자 지정 컨텍스트 또는 다른 포트가 없음
>

샘플 공유 리소스를 보려면 아래 단계를 참조하십시오.

1. AEM 서버에서 CRXDE Lite을 엽니다.
1. 이 경로 찾아보기 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*&#x200B;을 클릭하여 샘플 공유 리소스를 확인합니다.

   아래 그림과 같이 공유 리소스를 만드는 데 필요한 모든 속성을 볼 수 있습니다.

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>공유 리소스가 변경되면 AEM Mobile On-demand Services에 공유 리소스를 업로드하거나 내보내야 합니다.
