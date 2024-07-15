---
title: 문서 내보내기 구성 만들기
description: 이 페이지를 따라 Adobe Experience Manager(AEM)에서 AEM Mobile으로 업로드할 콘텐츠를 내보내는 방법에 대해 알아보십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# 문서 내보내기 구성 만들기{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**필수 구성 요소**:
>
>공유 리소스 만들기 및 수정에 대한 자세한 내용은 [콘텐츠 동기화](/help/mobile/mobile-ondemand-contentsync.md)를 참조하여 기본 개념을 알아보십시오.

AEM Mobile 사용자는 Content Sync를 사용하여 모바일 앱에서 사용할 수 있는 정적 콘텐츠로 라이브 콘텐츠를 내보내고 AEM Mobile에서 Mobile On-Demand Services로 콘텐츠가 업로드되면 이 내보내기가 발생합니다.

위의 표에 언급된 속성 ***dps-exportTemplate***&#x200B;은(는) 앱의 내보내기 구성에 대한 경로를 정의합니다. 공유 리소스를 만들고 수정하려면 이 속성을 설정하십시오.

다음 리소스는 AEM Mobile에 업로드하기 위해 Adobe Experience Manager(AEM)에서 콘텐츠를 내보내는 방법에 대해 설명합니다.

문서에 내보내고 업로드해야 하는 콘텐츠가 있습니다. 이 콘텐츠 중 일부는 문서 간에 공유할 수 있습니다.

[ContentSync](/help/mobile/mobile-ondemand-contentsync.md)을(를) 사용하여 콘텐츠를 함께 수집하고 ***공유 리소스*** 패키지를 만듭니다.

**&lt;dps-exportTemplate>/dps-article>**&#x200B;에 있는 ContentSync 구성은 장치의 속성 정적 렌더링에 필요한 모든 콘텐츠 및 아티클을 내보내도록 구성해야 합니다.

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
1. 샘플 공유 리소스를 보려면 이 경로 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)로 이동하십시오.

   아래 그림과 같이 공유 리소스를 만드는 데 필요한 모든 속성을 볼 수 있습니다.

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>문서는 문서 컨텐츠가 변경될 때 AEM Mobile On-demand Services에 업로드하거나 내보내야 합니다.
