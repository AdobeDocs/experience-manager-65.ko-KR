---
title: 대체 글꼴 구성
description: AEM Forms의 대체 글꼴을 구성하는 방법을 알아봅니다. FontManagerResources.properties 파일을 사용하면 기본 글꼴을 대체 글꼴에 수동으로 매핑할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '264'
ht-degree: 100%

---

# 대체 글꼴 구성 {#configuring-fallback-fonts}

서버에서 기본 글꼴을 사용할 수 없는 경우 기본 AEM Forms 글꼴을 대체(또는 교체) 글꼴에 매핑하도록 FontManagerResources. properties 파일을 수동으로 구성할 수 있습니다. 이 속성 파일은 adobe-fontmanager.jar 파일에 있습니다.

>[!NOTE]
>
>대체 글꼴 구성은 어셈블러 서비스에도 적용됩니다.

1. *`[aem-forms root]`*/configurationManager/export 디렉터리에 있는 adobe-livecycle-*`[appserver]`*.ear 파일로 이동하여 백업 사본을 만들고 원본의 압축을 풉니다.
1. adobe-fontmanager.jar 파일을 찾아 압축을 풉니다.
1. FontManagerResources.properties 파일을 찾아 텍스트 편집기에서 엽니다.
1. 필요에 따라 일반 글꼴 및 대체 글꼴 위치와 이름을 수정하고 파일을 저장합니다.

   FontManagerResources. properties 파일의 글꼴 항목은 *`[aem-forms root]`*/fonts 디렉터리를 기준으로 합니다. 기본 AEM Forms 글꼴이 아닌 글꼴을 지정하는 경우 해당 글꼴을 이 디렉터리 구조(기존 디렉터리 또는 새로 만든 디렉터리 내)에 설치해야 합니다.

   >[!NOTE]
   >
   >지정된 글꼴이나 기본 글꼴에 특정 유니코드 문자가 포함되어 있지 않거나 해당 문자를 사용할 수 없는 경우 다음 우선순위에 따라 대체 글꼴에서 문자를 가져옵니다.

   * 로케일별 글꼴
   * 로케일이 설정되지 않은 경우 ROOT 글꼴
   * 대체 테이블에 설정된 순서로 검색되는 일반 글꼴

1. adobe-fontmanager.jar 파일을 다시 패키징합니다.
1. adobe-livecycle-*`[appserver]`*.ear 파일을 다시 패키징한 후 구성 관리자를 실행하거나 수동으로 다시 배포합니다.

>[!NOTE]
>
>구성 관리자를 사용하여 adobe-livecycle-`[appserver]`.ear 파일을 다시 패키징하지 마십시오. 그러면 수정 사항이 AEM Forms 기본값으로 덮어쓰여집니다.
