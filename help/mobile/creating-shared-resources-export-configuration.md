---
title: 공유 리소스 내보내기 구성 만들기
seo-title: 공유 리소스 내보내기 구성 만들기
description: AEM Mobile에 업로드할 Adobe Experience Manager(AEM)에서 공유 리소스를 내보내는 방법에 대해 알려면 이 페이지를 따르십시오.
seo-description: AEM Mobile에 업로드할 Adobe Experience Manager(AEM)에서 공유 리소스를 내보내는 방법에 대해 알려면 이 페이지를 따르십시오.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---

# 공유 리소스 내보내기 구성 만들기{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**전제 조건**:
>
>공유 리소스를 만들고 수정하는 방법에 대한 자세한 내용은 [컨텐츠 동기화](/help/mobile/mobile-ondemand-contentsync.md)를 참조하십시오.

AEM Mobile 사용자는 컨텐츠 동기화를 사용하여 모바일 앱에서 사용할 정적 컨텐츠로 라이브 컨텐츠를 내보내고 AEM Mobile에서 Mobile On-Demand Services로 컨텐츠가 업로드되면 내보내집니다.

위의 표에 언급된 속성 ***dps-exportTemplate***&#x200B;은 앱 내보내기 구성의 경로를 정의합니다. 공유 리소스를 만들고 수정하려면 이 속성을 설정하십시오.

다음 리소스는 AEM Mobile으로 업로드할 Adobe Experience Manager(AEM)에서 공유 리소스를 내보내는 방법에 대해 설명합니다.

공유 HTML 리소스를 사용하면 문서가 모든 문서에 대해 복제해야 하는 HTML 리소스를 공유할 수 있으며 아이콘, 글꼴, Javascript 및 css를 포함할 수 있습니다.

**&lt;dps-exportTemplate>/dps-HTMLRessources>**&#x200B;에 있는 컨텐츠 동기화 구성은 장치의 속성 정적 렌더링에 필요한 모든 컨텐츠와 문서를 내보내도록 구성해야 합니다.

>[!CAUTION]
>
>다음 권한이 있는 경우에만 아래 단계를 수행하여 샘플 공유 리소스를 볼 수 있습니다.
>
>* 샘플 컨텐츠 설치
>* AEM 인스턴스 실행
>* 구성된 사용자 지정 컨텍스트 또는 다른 포트 없음

>



샘플 공유 리소스를 보려면 아래 단계를 참조하십시오.

1. AEM 서버에서 CRXDE Lite을 엽니다.
1. 샘플 공유 리소스를 보려면 이 경로 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLRessources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*&#x200B;로 이동하십시오.

   아래 그림과 같이 공유 리소스를 만드는 데 필요한 모든 속성을 볼 수 있습니다.

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>공유 리소스가 변경되면 AEM Mobile On-demand Services으로 공유 리소스를 업로드하거나 내보내야 합니다.
