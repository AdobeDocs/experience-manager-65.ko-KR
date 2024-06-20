---
title: 구성 파일 가져오기 및 내보내기
description: 구성 파일을 가져오고 내보내 서버 환경 설정을 편집하거나 다른 AEM Forms 제품 인스턴스를 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 구성 파일 가져오기 및 내보내기 {#importing-and-exporting-the-configuration-file}

[수동 구성] 페이지에서는 XML 형식의 구성 설정 사본을 다운로드할 수 있습니다. 이 파일의 설정은 모든 서버 기본 설정을 제어합니다. 그런 다음 파일을 편집하고 다시 서버에 업로드할 수 있습니다. 파일을 사용하여 다른 AEM forms 제품 인스턴스를 구성할 수도 있습니다.

보안 위험을 방지하기 위해 디렉터리 서버의 바인드 암호 값은 내보낸 구성 파일에 포함되지 않습니다. 파일을 새 시스템으로 가져오기 전에 XML 파일의 암호를 업데이트합니다.

>[!NOTE]
>
>구성 파일을 가져오면 파일의 정보를 기반으로 AEM 양식이 다시 구성됩니다. AEM Forms 제품 및 XML에 익숙한 시스템 관리자 또는 전문 서비스 컨설턴트만 구성 파일 수정을 고려해야 합니다. 손상된 설정을 다시 구성하기 위해 구성 파일을 편집해야 할 수 있습니다.

**구성 정보 내보내기**

1. Administration Console에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기 를 클릭합니다.
1. 내보내기를 클릭합니다. Microsoft Internet Explorer를 사용하는 경우 파일을 저장할 위치를 지정하라는 메시지가 표시됩니다. Firefox를 사용하는 경우 파일이 데스크탑에 저장됩니다.

**구성 정보 가져오기**

1. Administration Console에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기 를 클릭합니다.
1. 찾아보기를 클릭하여 구성 파일을 찾고 가져오기를 클릭한 다음 확인을 클릭합니다.
