---
title: 양식 구성 기초
seo-title: 양식 구성 기초
description: 인터랙티브한 데이터 캡처 애플리케이션을 제작하는 데 도움이 되는 다양한 양식 서비스에 대해 알아봅니다.
seo-description: 인터랙티브한 데이터 캡처 애플리케이션을 제작하는 데 도움이 되는 다양한 양식 서비스에 대해 알아봅니다.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 양식 구성 기초 {#basics-of-configuring-forms}

Forms 서비스를 사용하면 Designer에서 만든 양식의 유효성 검사, 처리, 변환 및 전달을 위한 대화형 데이터 캡처 클라이언트 애플리케이션을 만들 수 있습니다. 양식 작성자는 양식 서비스가 다양한 형식으로 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.

* Adobe Reader 또는 브라우저에서 PDF로 변환
* 표준을 준수하는 XHTML 1.0 렌더링을 비롯한 다양한 브라우저 환경에서 HTML로 제작
* Adobe Flash Player를 지원하는 다양한 브라우저 환경에서 양식 가이드로 사용할 수 있습니다.

양식 서비스에 대한 자세한 내용은 서비스 [참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

관리 콘솔에서 양식 페이지를 사용하여 Forms 서비스의 동작을 구성할 수 있습니다. 이러한 설정은 서비스의 모든 호출에 적용됩니다. AEM 양식 SDK를 통해 전송된 모든 매개 변수는 관리 콘솔에서 설정한 설정을 덮어씁니다.그러나, 이러한 호출은 특정 호출에만 영향을 줍니다.

관리 콘솔에서 양식 설정을 변경한 후 저장을 클릭합니다. 변경 사항을 적용하려면 서버를 다시 시작할 필요가 없습니다. 그러나 캐시 모드 설정을 구성할 때 Forms 서비스를 중지하고 다시 시작해야 할 수 있습니다. (서비스 [시작 및 중지를](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)참조하십시오.)
