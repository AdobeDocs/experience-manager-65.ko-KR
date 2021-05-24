---
title: 다국어 사이트의 컨텐츠 번역
seo-title: 다국어 사이트의 컨텐츠 번역
description: 다국어 사이트의 콘텐츠를 번역하는 방법을 알아봅니다.
seo-description: 다국어 사이트의 콘텐츠를 번역하는 방법을 알아봅니다.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: 언어 복사
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# 다국어 사이트 {#translating-content-for-multilingual-sites} 컨텐츠 번역

페이지 컨텐츠, 자산 및 사용자 생성 컨텐츠를 자동으로 변환하여 다국어 웹 사이트를 제작 및 유지 관리할 수 있습니다. 번역 워크플로우를 자동화하기 위해 번역 서비스 공급자를 AEM과 통합하고 컨텐츠를 여러 언어로 번역할 프로젝트를 만듭니다. AEM은 사람 및 기계 번역 워크플로우를 지원합니다.

* 인간 번역:컨텐츠는 번역 공급자에게 전송되고 전문 번역가가 번역합니다. 완료되면 번역된 컨텐츠가 반환되고 AEM으로 가져옵니다. 번역 공급자가 AEM과 통합되면 AEM과 번역 공급자 간에 콘텐츠가 자동으로 전송됩니다.
* 기계 번역:기계 번역 서비스는 콘텐츠를 즉시 번역합니다.

컨텐츠를 번역하려면 다음 단계가 포함됩니다.

1. [AEM을 번역 서비스 ](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) 공급자와 연결하고  [번역 통합 프레임워크 구성을 만듭니다](/help/sites-administering/tc-tic.md).
1. [언어 마스터의 페이지](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) 를 번역 서비스 및 프레임워크 구성과 연결합니다.
1. [변환할 컨텐츠의 ](/help/sites-administering/tc-rules.md) 유형을 확인합니다.
1. [언어 마스터를 ](/help/sites-administering/tc-prep.md) 작성하고 언어 사본의 루트 페이지를 만들어 번역 컨텐츠를 준비합니다.
1. [번역 ](/help/sites-administering/tc-manage.md) 프로젝트를 만들어 번역할 컨텐츠를 수집하고 번역 프로세스를 준비합니다.
1. 번역 프로젝트를 사용하여 [컨텐츠 번역 프로세스를 관리합니다](/help/sites-administering/tc-manage.md).

번역 서비스 공급자가 AEM과의 통합에 커넥터를 제공하지 않는 경우 AEM에서는 XML 형식으로 번역 컨텐츠를 수동으로 추출하고 다시 삽입할 수 있습니다.

>[!NOTE]
>
>언어 사본 기능을 사용하려면 사용자가 프로젝트 관리자 그룹의 구성원이어야 합니다.

## 우수 사례 {#best-practices}

[번역 우수 사례](/help/sites-administering/tc-bp.md) 페이지에는 구현과 관련된 중요한 정보가 포함되어 있습니다.
