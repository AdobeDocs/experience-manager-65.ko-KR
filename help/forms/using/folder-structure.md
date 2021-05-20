---
title: 폴더 구조 이해
seo-title: 폴더 구조 이해
description: 사용자 지정할 AEM Forms 작업 공간 소스 코드의 폴더 구조를 이해하는 방법입니다.
seo-description: 사용자 지정할 AEM Forms 작업 공간 소스 코드의 폴더 구조를 이해하는 방법입니다.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 폴더 구조 이해 {#understanding-the-folder-structure}

AEM Forms 작업 공간 구성 요소는 백본을 사용하여 MVC 아키텍처로 디자인됩니다. 각 구성 요소에는 다음에 대한 파일이 있습니다.

* 비즈니스 논리를 포함하는 모델.
* 템플릿: 인터페이스 컨트롤이 포함된 HTML 파일입니다.
* 템플릿에 대한 컨트롤러 클래스 역할을 하는 보기.

모든 구성 요소의 자산은 아래에 설명된 폴더 구조에 배치됩니다. 자산에 액세스하려면 CRXDE Lite에 로그인하고 `/libs/ws/js/runtime/`으로 이동합니다.

**** models백본 모델을 포함합니다.

**** view백본 보기를 포함합니다.

**** 템플릿: 구성 요소에 대한 HTML 템플릿만 포함합니다.

**** route유니버설 경로를 포함합니다. 경로 내의 템플릿 폴더에는 HTML 코드와 구성 요소에 대한 참조가 포함되어 있습니다.

**** servicesREST 종단점에서 Adobe Experience Manager 서버 API를 호출하기 위한 서비스 인터페이스를 포함합니다.

**** util여러 구성 요소에서 사용할 수 있는 일반 유틸리티를 포함합니다.
