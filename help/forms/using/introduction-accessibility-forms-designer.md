---
title: 양식 디자이너에서 양식을 만들기 위한 액세스 가능성 모범 사례 소개
description: Forms Designer 사용을 위한 최상의 접근성 사례에 대해 알아봅니다
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
exl-id: 646cfe47-b11f-45bb-a3f9-3dfc2043146e
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 1af3c3d4-88d7-5e0f-813c-eb70824bfcdd
    internal-label: Forms Designer
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%
---
# Forms Designer의 접근성 모범 사례 소개

액세스 가능한 양식은 컴퓨터 화면에서 양식과 상호 작용할 수 있는 방법에 영향을 주는 장애가 있는 사용자를 포함하여 거의 모든 사용자가 사용할 수 있는 양식입니다. 예를 들어, 시각 장애가 있거나 이동성이 감소된 사용자는 여전히 액세스 가능한 양식을 사용할 수 있습니다.

Adobe LiveCycle Designer에는 다양한 장애가 있는 사용자를 위한 양식의 유용성을 높이고 양식 작성자가 장애가 있는 사용자가 보다 쉽게 액세스할 수 있는 PDF forms을 만들 수 있도록 지원하는 다양한 기능이 포함되어 있습니다.

양식에 액세스 가능성을 구축하면 가능한 광범위한 컨텐츠 대상을 확보할 수 있을 뿐만 아니라 액세스 가능성 표준 준수가 필요한 지역에 문서를 제공할 때 필수 사항입니다. 예를 들어, 미국에서는 재활 법 제508조와 같은 접근성 표준이 존재하여 정부 서비스를 소비하는 장애가 있는 공무원 및 장애를 가진 공공 장애인을 포함한 모든 사용자가 정보 기술을 사용할 수 있도록 합니다.

LiveCycle Designer은 개발자가 접근성 표준에서 지정한 요구 사항을 준수할 수 있도록 지원합니다. 구성 요소 기반 접근 방식을 통해 양식 빌더는 내장된 접근성 기능을 활용할 수 있습니다. LiveCycle Designer은 또한 액세스 가능한 XHTML 파일(LiveCycle Forms 사용) 및 PDF forms을 만들 수 있도록 지원합니다. 액세스 가능한 PDF forms에는 전체 논리 구조와 문서 컨텐츠에 대한 추가 정보가 포함되어 있어 액세스 가능성을 높일 수 있습니다.
Adobe의 접근성 솔루션에 대한 자세한 내용은 접근성 리소스 센터(www.adobe.com/accessibility)를 참조하십시오.
