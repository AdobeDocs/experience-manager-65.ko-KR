---
title: 대용량 보안 정보 제공
description: Document Security는 대량 프로덕션 환경의 문서가 아닌 사용자에게 라이선스를 연결할 수 있도록 지원합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 대용량 보안 정보 제공 {#high-volume-secure-information-delivery}

통신사에 대한 보안 월별 송장을 생성하는 것과 같은 대량 생산 환경에서는 각 문서에 고유한 라이센스를 만드는 것이 자원 집약적인 프로세스가 될 수 있습니다. 이러한 경우 document security는 문서가 아닌 사용자에게 라이선스를 연결할 수 있도록 지원합니다. 사용자에 대해 생성된 라이선스는 해당 사용자의 보호를 받는 모든 문서에 사용됩니다.

이 접근 방식의 한 가지 장점은 문서 보안 데이터베이스 크기가 사용자 수가 아니라 문서에 따라 선형적으로 증가하지 않는다는 것입니다. 또한 사용자를 위해 라이센스를 한 번만 만들면 되므로 이러한 정책을 통해 문서를 보다 신속하게 보호할 수 있습니다. 오프라인 액세스, 문서 만료 및 해지 등의 기능은 이러한 모든 문서에 대해 지원됩니다.

Document Security는 추상 정책도 지원합니다. 추상 정책은 문서 보안 설정 및 사용 권한과 같은 모든 정책 속성을 포함하지만 주체 목록은 포함하지 않는 정책 템플릿입니다. 관리자는 문서에 액세스할 수 있어야 하는 서로 다른 주도자를 사용하여 추상적인 정책에서 원하는 수의 정책을 만들 수 있습니다. 추상적 정책에 대한 변경은 추상적 정책으로부터 생성되는 실제 정책에는 영향을 미치지 않는다.

통신사에 대한 월별 청구서가 생성되면 추상적인 정책을 생성하고 사용자를 생성한 다음 각 사용자에 대해 고유한 라이센스를 생성합니다. 라이센스는 나중에 각 사용자의 문서에 적용됩니다.

추상 정책 생성은 Document Security Java SDK를 통해서만 지원됩니다. 그러나 document security 웹 페이지의 추상 정책에서 생성하는 정책을 관리할 수 있습니다. 이 방법을 사용하여 만든 정책은 문서 보안 웹 페이지에서 만든 정책과 동작이 동일합니다.

다음을 참조하십시오 [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63) 추가 정보.
