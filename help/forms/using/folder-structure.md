---
title: 폴더 구조 이해
description: 맞춤화할 AEM Forms 작업 영역 소스 코드의 폴더 구조를 이해하는 방법입니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 폴더 구조 이해 {#understanding-the-folder-structure}

AEM Forms 작업 영역 구성 요소는 백본을 사용하여 MVC 아키텍처에서 설계되었습니다. 각 구성 요소에는 다음 파일을 위한 파일이 있습니다.

* 비즈니스 논리가 포함된 모델.
* 템플릿(인터페이스 컨트롤이 포함된 HTML 파일)
* 템플릿 컨트롤러 클래스로 사용되는 보기입니다.

모든 구성 요소의 에셋은 아래에 설명된 폴더 구조에 배치됩니다. 에셋에 액세스하려면 CRXDE Lite에 로그인하여 `/libs/ws/js/runtime/`(으)로 이동하십시오.

**모델**&#x200B;에 백본 모델이 포함되어 있습니다.

**보기**&#x200B;에 백본 보기가 포함되어 있습니다.

**템플릿** 구성 요소에 대한 HTML 템플릿만 포함합니다.

**경로**&#x200B;에 범용 경로가 있습니다. 경로 내의 HTML 폴더에는 템플릿 코드와 구성 요소에 대한 참조가 포함됩니다.

**서비스** REST 끝점에서 Adobe Experience Manager 서버 API를 호출하는 서비스 인터페이스를 포함합니다.

**util** 여러 구성 요소에서 사용할 수 있는 일반 유틸리티가 포함되어 있습니다.
