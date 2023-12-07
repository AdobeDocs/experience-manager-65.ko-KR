---
title: 자격 증명 사용 정보 검토
description: 자격 증명 사용 정보를 검토하는 방법을 알아봅니다. 사용을 설명하는 자격 증명 사용 정보는 Acrobat Reader 확장을 통해 액세스할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 자격 증명 사용 정보 검토 {#review-credential-use-information}

자격 증명에는 Acrobat Reader DC 확장 최종 사용자 웹 애플리케이션을 통해 액세스할 수 있는 의도된 사용을 설명하는 정보가 포함되어 있습니다. 이 정보를 사용하여 설치된 자격 증명의 유형(평가 또는 프로덕션)과 유효 날짜를 확인할 수 있습니다.

1. 웹 브라우저를 열고 다음 URL을 입력합니다.

   http://localhost:port/ReaderExtensions (여기서 *포트* 은 애플리케이션 서버의 포트 번호입니다.

1. 기본 사용자 이름 및 암호를 사용하여 로그인합니다.

   사용자 이름: 관리자

   암호: 암호

   >[!NOTE]
   >
   >기본 사용자 이름 및 암호를 사용하여 로그인하려면 관리자 또는 수퍼유저 권한이 있어야 합니다. 다른 사용자가 Acrobat Reader DC 확장에 액세스할 수 있도록 하려면 사용자 관리에서 사용자 계정을 만들고 사용자에게 Acrobat Reader DC 확장 웹 애플리케이션 역할을 부여합니다.

1. 자격 증명 선택 목록에서 자격 증명 별칭을 선택하고 만료 날짜 및 사용 예정 알림에 포함된 정보를 검토합니다.

>[!NOTE]
>
>자격 증명의 만료 날짜는 관리 콘솔의 설정 > Trust Store Management > 로컬 자격 증명 페이지 만료 날짜에서도 사용할 수 있습니다.
