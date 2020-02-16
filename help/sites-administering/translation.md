---
title: 다국어 사이트의 컨텐츠 번역
seo-title: 다국어 사이트의 컨텐츠 번역
description: 다국어 사이트의 컨텐츠를 변환하는 방법을 살펴볼 수 있습니다.
seo-description: 다국어 사이트의 컨텐츠를 변환하는 방법을 살펴볼 수 있습니다.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# 다국어 사이트의 컨텐츠 번역 {#translating-content-for-multilingual-sites}

페이지 컨텐츠, 자산 및 사용자 생성 컨텐츠의 번역 과정을 자동화하여 다국어 웹 사이트를 제작하고 유지 관리할 수 있습니다. 번역 워크플로우를 자동화하기 위해 번역 서비스 제공업체를 AEM과 통합하고 컨텐츠를 여러 언어로 번역하는 프로젝트를 제작할 수 있습니다. AEM은 인간 및 기계 번역 워크플로우를 지원합니다.

* 인간 번역:컨텐츠는 번역 공급자로 전송되며 전문 번역가가 번역합니다. 완료되면 번역된 컨텐츠가 반환되고 AEM으로 가져오게 됩니다. 번역 공급자가 AEM과 통합되면 컨텐츠가 AEM과 번역 공급자 사이에 자동으로 전송됩니다.
* 기계 번역:기계 번역 서비스는 컨텐츠를 즉시 변환합니다.

컨텐츠를 번역하려면 다음 단계를 수행하십시오.

1. [번역 서비스 제공자와](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) AEM을 연결하고 번역 통합 프레임워크 구성을 [만듭니다](/help/sites-administering/tc-tic.md).
1. [언어 마스터의](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) 페이지를 번역 서비스 및 프레임워크 구성과 연결합니다.
1. [번역할 컨텐츠](/help/sites-administering/tc-rules.md) 유형을 확인합니다.
1. [언어 마스터를 작성하고 언어 사본의 루트 페이지를 만들어 번역](/help/sites-administering/tc-prep.md) 컨텐츠를 준비합니다.
1. [번역 프로젝트를](/help/sites-administering/tc-manage.md) 만들어 번역할 컨텐츠를 수집하고 번역 프로세스를 준비합니다.
1. 번역 프로젝트를 사용하여 컨텐츠 번역 프로세스를 [관리합니다](/help/sites-administering/tc-manage.md).

번역 서비스 공급자가 AEM과의 통합을 위한 커넥터를 제공하지 않는 경우 AEM은 XML 형식으로 번역 컨텐츠의 수동 추출 및 재삽입을 지원합니다.

>[!NOTE]
>
>사용자는 언어 복사 기능을 사용하려면 프로젝트 관리자 그룹의 구성원이어야 합니다.

## 우수 사례 {#best-practices}

번역 [우수 사례](/help/sites-administering/tc-bp.md) 페이지에는 구현과 관련된 중요한 정보가 들어 있습니다.
