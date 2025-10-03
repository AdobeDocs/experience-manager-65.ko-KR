---
title: 양식 구성의 기본 사항
description: 대화형 데이터 캡처 애플리케이션을 만드는 데 도움이 되는 다양한 양식 서비스를 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '197'
ht-degree: 100%

---

# 양식 구성의 기본 사항 {#basics-of-configuring-forms}

Forms 서비스를 사용하면 일반적으로 Designer에서 만든 양식의 유효성을 검사하고 해당 양식을 처리, 변환 및 전달하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만들 수 있습니다. 양식 작성자는 다음과 같이 Forms 서비스가 다양한 형식으로 렌더링하는 단일 양식 디자인을 개발합니다.

* Adobe Reader 또는 브라우저에서 사용 가능한 PDF
* 호환되는 XHTML 1.0 렌더링을 포함한 다양한 브라우저 환경에서 사용 가능한 HTML
* Adobe Flash Player를 지원하는 다양한 브라우저 환경에서 사용 가능한 양식 Guides

Forms 서비스에 대한 자세한 내용은 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

관리 콘솔의 Forms 페이지에서 Forms 서비스 동작을 구성할 수 있습니다. 해당 설정은 모든 서비스 호출에 적용됩니다. AEM Forms SDK를 통해 전송된 모든 매개변수는 관리 콘솔에서 설정한 설정을 재정의하지만, 해당 호출에만 영향을 미칩니다.

관리 콘솔에서 Forms 설정을 변경한 후 저장을 클릭합니다. 서버를 다시 시작하지 않아도 변경 사항이 적용됩니다. 하지만 캐시 모드 설정을 구성할 때는 Forms 서비스를 중지했다가 다시 시작해야 할 수도 있습니다. ([서비스 시작 및 중지](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)를 참조하십시오.)
