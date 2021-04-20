---
title: 대용량 보안 정보 전달
seo-title: 대용량 보안 정보 전달
description: 문서 보안은 대량 제작 환경에서 문서가 아닌 사용자를 위한 라이선스 연결을 지원합니다.
seo-description: 문서 보안은 대량 제작 환경에서 문서가 아닌 사용자를 위한 라이선스 연결을 지원합니다.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# 대용량 보안 정보 배달 {#high-volume-secure-information-delivery}

통신 회사에 대한 안전한 월별 송장을 생성하는 것과 같은 대량 생산 환경에서는 각 문서에 맞는 라이선스를 만드는 것이 리소스 사용량이 많은 프로세스가 될 수 있습니다. 이러한 경우 문서 보안은 문서가 아닌 사용자에 대한 라이센스 연결을 지원합니다. 사용자에 대해 생성된 라이센스는 해당 사용자에 대해 보호되는 모든 문서에 사용됩니다.

이 방식의 한 가지 이점은 문서 보안 데이터베이스 크기가 사용자 수가 아니라 문서와 선형으로 확장되지 않는다는 것입니다. 또한 사용자에 대해 라이선스를 한 번만 만들어야 하므로 이후 이러한 정책을 통해 문서를 더욱 빠르게 보호할 수 있습니다. 이러한 모든 문서에는 오프라인 액세스, 문서 만료 및 취소와 같은 기능이 지원됩니다.

문서 보안은 추상 정책도 지원합니다. 추상 정책은 문서 보안 설정 및 사용 권한과 같은 모든 정책 속성을 포함하지만 주체 목록을 포함하지 않는 정책 템플릿입니다. 관리자는 추상 정책에서 문서에 액세스할 수 있는 주도자가 다른 정책을 원하는 개수만큼 만들 수 있습니다. 추상 정책의 변경 사항은 추상 정책으로부터 생성된 실제 정책에 영향을 주지 않습니다.

통신 회사의 월별 송장 생성 경우 개요 정책을 만들고 사용자를 생성한 다음 각 사용자에 대한 고유한 라이센스를 생성합니다. 라이선스는 나중에 각 사용자를 위한 문서에 적용됩니다.

추상 정책 만들기는 문서 보안 Java SDK를 통해서만 지원됩니다. 그러나 문서 보안 웹 페이지에서 추상 정책으로 만든 정책을 관리할 수는 있습니다. 이 방법을 사용하여 만든 정책은 문서 보안 웹 페이지에서 만든 정책과 동일합니다.

자세한 내용은 [AEM 양식 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)을 참조하십시오.
