---
title: 자격 증명 사용 정보 검토
description: 자격 증명 사용 정보를 검토하는 방법을 알아봅니다. 사용을 설명하는 자격 증명 사용 정보는 Acrobat Reader 확장을 통해 액세스할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-wordcount: '196'
ht-degree: 4%
---
# 자격 증명 사용 정보 검토 {#review-credential-use-information}

자격 증명에는 Acrobat Reader DC 확장 최종 사용자 웹 응용 프로그램을 통해 액세스할 수 있는 해당 용도를 설명하는 정보가 포함되어 있습니다. 이 정보를 사용하여 설치된 자격 증명의 유형(평가 또는 프로덕션)과 유효 날짜를 확인할 수 있습니다.

1. 웹 브라우저를 열고 다음 URL을 입력합니다.

   http://localhost:port/ReaderExtensions (여기서 *port*&#x200B;은(는) 응용 프로그램 서버의 포트 번호입니다.)

1. 기본 사용자 이름 및 암호를 사용하여 로그인합니다.

   사용자 이름: 관리자

   암호: 암호

   >[!NOTE]
   >
   >기본 사용자 이름 및 암호를 사용하여 로그인하려면 관리자 또는 수퍼유저 권한이 있어야 합니다. 다른 사용자가 Acrobat Reader DC 확장 기능에 액세스할 수 있도록 하려면 사용자 관리에서 사용자 계정을 만들고 사용자에게 Acrobat Reader DC 확장 웹 애플리케이션 역할을 부여합니다.

1. 자격 증명 선택 목록에서 자격 증명 별칭을 선택하고 만료 날짜 및 사용 예정 알림에 포함된 정보를 검토합니다.

>[!NOTE]
>
>자격 증명의 만료 날짜는 관리 콘솔의 설정 > Trust Store Management > 로컬 자격 증명 페이지 만료 날짜에서도 사용할 수 있습니다.
