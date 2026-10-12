---
title: 대용량 보안 정보 전송
description: 문서 보안은 대량 프로덕션 환경에서 문서가 아닌 사용자에게 라이선스를 연결하는 기능을 지원합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%
---
# 대용량 보안 정보 전송 {#high-volume-secure-information-delivery}

통신 회사에서 보안이 적용된 월별 청구서를 생성하는 환경과 같은 대량 프로덕션 환경에서는 각 문서에만 적용되는 라이선스를 만드는 작업이 리소스를 많이 사용하는 프로세스가 될 수 있습니다. 이 경우 문서 보안은 문서가 아닌 사용자에게 라이선스를 연결하는 기능을 지원합니다. 사용자를 위해 생성된 라이선스는 해당 사용자를 위해 보호되는 모든 문서에 사용됩니다.

이 접근 방식의 장점 중 하나는 문서 보안 데이터베이스 크기가 문서 수에 따라 선형적으로 커지지 않고 사용자 수에 따라 커진다는 점입니다. 또한 사용자당 라이선스를 한 번만 만들면 되므로 이후에 해당 정책을 통해 문서를 보호하는 속도가 더 빨라집니다. 모든 문서에는 오프라인 액세스, 문서 만료, 취소와 같은 기능이 지원됩니다.

문서 보안은 추상 정책도 지원합니다. 추상 정책은 문서 보안 설정 및 사용 권한과 같은 모든 정책 속성을 포함하되 주체 목록은 포함하지 않는 정책 템플릿입니다. 관리자는 문서에 액세스할 수 있어야 하는 서로 다른 주체를 지정하여 추상 정책에서 원하는 수만큼 정책을 만들 수 있습니다. 추상 정책에서 수행되는 변경 사항은 추상 정책에서 생성된 실제 정책에 영향을 미치지 않습니다.

통신 회사에서 월별 청구서를 생성하는 경우 추상 정책과 사용자를 만든 후 각 사용자에게 고유한 라이선스를 생성합니다. 이 라이선스는 나중에 각 사용자의 문서에 적용됩니다.

추상 정책 생성은 문서 보안 Java SDK를 통해서만 지원됩니다. 하지만 문서 보안 웹 페이지에서 추상 정책으로 만든 정책을 관리할 수는 있습니다. 이 방법을 사용하여 생성된 정책은 문서 보안 웹 페이지에서 생성된 정책과 동작이 동일합니다.

자세한 내용은 [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)을 참조하십시오.
