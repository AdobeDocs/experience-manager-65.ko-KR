---
title: 구성 파일 가져오기 및 내보내기
description: 서버 환경 설정을 편집하거나 다른 AEM Forms 제품 인스턴스를 구성하기 위해 구성 파일을 가져오거나 내보내는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '264'
ht-degree: 100%

---

# 구성 파일 가져오기 및 내보내기 {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

수동 구성 페이지에서 구성 설정 사본을 XML 형식으로 다운로드합니다. 이 파일 설정에 따라 모든 서버 환경 설정이 제어됩니다. 그런 다음, 파일을 편집하여 다시 서버로 업로드할 수 있습니다. 이 파일을 사용하여 다른 AEM Forms 제품 인스턴스를 구성할 수도 있습니다.

보안 위험을 방지하기 위해 디렉터리 서버의 바인드 암호 값은 내보낸 구성 파일에 포함되지 않습니다. 새 시스템으로 파일을 가져오기 전에 XML 파일의 암호를 업데이트합니다.

>[!NOTE]
>
>구성 파일을 가져오면 파일 정보를 기반으로 AEM Forms가 재구성됩니다. AEM Forms 제품과 XML에 익숙한 시스템 관리자나 전문 서비스 컨설턴트만이 구성 파일을 수정하는 것을 고려해야 합니다. 예를 들어 손상된 설정을 재구성하기 위해 구성 파일을 편집해야 할 수도 있습니다.

**구성 정보 내보내기**

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다.
1. 내보내기를 클릭합니다. Microsoft Internet Explorer를 사용하는 경우 파일을 저장할 위치를 지정하라는 메시지가 표시됩니다. Firefox를 사용하는 경우 파일은 데스크탑에 저장됩니다.

**구성 정보 가져오기**

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다.
1. 찾아보기를 클릭하여 구성 파일을 찾은 후 가져오기를 클릭하고 확인을 클릭합니다.
