---
title: 대체 글꼴 구성
seo-title: 대체 글꼴 구성
description: 대체 글꼴을 구성하는 방법을 알아봅니다.
seo-description: 대체 글꼴을 구성하는 방법을 알아봅니다.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 대체 글꼴 구성 {#configuring-fallback-fonts}

기본 글꼴을 서버에서 사용할 수 없는 경우 기본 AEM 양식 글꼴을 폴백(또는 대체)으로 매핑하도록 FontManagerResources.properties 파일을 수동으로 구성할 수 있습니다. 이 속성 파일은 adobe-fontmanager.jar 파일에 있습니다.

>[!NOTE]
>
>대체 글꼴 구성은 어셈블러 서비스에도 적용됩니다.

1. /configurationManager/export 디렉토리에서 adobe-livecycle-*`[appserver]`*.ear 파일을 *`[aem-forms root]`*&#x200B;찾아 백업 복사본을 만들고 원본 파일의 압축을 해제합니다.
1. adobe-fontmanager.jar 파일을 찾아 압축을 해제합니다.
1. FontManagerResources.properties 파일을 찾아 텍스트 편집기에서 엽니다.
1. 필요에 따라 일반 및 폴백 글꼴 위치와 이름을 수정하고 파일을 저장합니다.

   FontManagerResources.properties 파일의 글꼴 항목은 *`[aem-forms root]`*/fonts 디렉토리에 상대적입니다. 기본 AEM 양식 글꼴이 아닌 글꼴을 지정하는 경우 이 디렉토리 구조 내에 해당 글꼴을 설치해야 합니다(기존 디렉토리 내 또는 새로 만든 글꼴).

   >[!NOTE]
   >
   >지정된 글꼴 또는 기본 글꼴에 특정 유니코드 문자가 포함되어 있지 않거나 사용할 수 없는 경우, 다음 우선 순위에 따라 대체 글꼴에서 문자를 가져옵니다.

   * 로케일별 글꼴
   * 로케일이 설정되지 않은 경우 ROOT 글꼴
   * 대체 테이블에서 순서 설정으로 검색된 일반 글꼴

1. adobe-fontmanager.jar 파일을 다시 패키지합니다.
1. adobe-livecycle-*`[appserver]`*.ear 파일을 다시 패키지한 다음 수동으로 또는 Configuration Manager를 실행하여 다시 배포합니다.

>[!NOTE]
>
>Configuration Manager를 사용하여 adobe-livecycle-`[appserver]`.ear 파일을 다시 패키징하면 AEM 양식 기본값으로 수정 내용을 덮어쓸 수 있습니다.

