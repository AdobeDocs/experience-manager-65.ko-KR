---
title: AEM Forms용 Adobe Experience Manager(AEM) 데스크탑 앱
description: AEM Forms용 Adobe Experience Manager(AEM) 데스크탑 앱
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# AEM Forms용 Adobe Experience Manager(AEM) 데스크탑 앱 {#aem-desktop-app-for-aem-forms}

AEM Desktop App을 사용하면 Adobe Experience Manager(AEM) Assets 저장소 및 AEM Forms 바이너리 파일을 시스템의 네트워크 디렉토리에 매핑할 수 있습니다. 파일 탐색기에서 동기화된 에셋 및 이진 파일을 보고 다양한 앱을 사용하여 원하는 대로 파일을 편집할 수 있습니다. 파일을 보는 것 외에도 이진 파일을 만들고, 업로드하고, 삭제할 수도 있습니다. 소프트웨어에서 직접 파일을 열고 편집하고 저장할 수도 있습니다. 예를 들어 Designer에서 직접 XDP 파일을 열고 편집할 수 있습니다. 로컬에서 에셋을 변경하면 변경 사항이 AEM Assets 저장소 및 AEM Forms UI에 반영됩니다.

AEM 인스턴스에서 앱을 다운로드할 수 있습니다. 앱 다운로드에 대한 자세한 내용은 [AEM 데스크탑 앱 릴리스 노트](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en).

## AEM 데스크탑 앱에서 지원되는 AEM Forms 에셋 {#aem-forms-assets-supported-in-aem-desktop-app}

앱을 사용하여 다음 유형의 양식 서식 파일(.xdp), PDF 양식(.pdf), 문서(.pdf), 이미지, XML 스키마(.xsd), 스타일 시트(.xfs)의 AEM Forms 이진 파일을 동기화할 수 있습니다. 이 앱은 다른 모든 파일(지원되지 않는 파일)을 0바이트 파일로 나열합니다. 지원되지 않는 파일을 0바이트 파일로 나열하면 사용자가 AEM Forms 서버에서 사용할 수 있는 다른 에셋이 있는지 알 수 있습니다.

>[!NOTE]
>
>파일 이름에는 영숫자, 하이픈 또는 밑줄만 포함할 수 있습니다.

## AEM 데스크탑 앱용 AEM Forms 활성화 {#enable-aem-forms-for-aem-desktop-app}

AEM Desktop App은 Microsoft Windows의 WebDAV 프로토콜과 Mac OS X의 SMB1을 사용하여 AEM Forms 서버에 연결합니다. 기본적으로 AEM Forms 서버는 WebDAV 또는 SMB 클라이언트와 이진 파일 및 기타 자산을 동기화할 수 없습니다. AEM Forms for AEM 데스크탑 앱을 활성화하려면 다음 단계를 수행하십시오.

1. 관리자로 AEM Forms에 로그인합니다.
1. 작성자 인스턴스에서 ![adobeexperiencemanger](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > 도구]** ![망치](assets/hammer.png) **[!UICONTROL > 배포 > 작업 > 웹 콘솔]**. 웹 콘솔이 새 창에 열립니다.
1. 웹 콘솔 창에서 를 찾아 엽니다. **[!UICONTROL FormsManager 추가 기능 구성]** 옵션을 선택합니다.
1. FormsManager 추가 기능 구성 대화 상자에서 **[!UICONTROL 리소스를 비동기적으로 동기화]** 확인란을 선택하고 **[!UICONTROL 저장]**.
1. AEM Forms 서버를 다시 시작합니다. 다시 시작하면 AEM Forms 서버가 AEM 데스크탑 앱에서 콘텐츠를 수락하고 공유할 수 있도록 활성화됩니다.
1. 앱을 열고 AEM Forms 서버에 연결합니다.

   연결에 성공하면 앱이 `content/dam` 및 `content/dam/formsanddocuments` 개 폴더. 위 폴더에서 로컬 폴더로 파일을 이동할 수 있으며 반대로 앱을 사용하여 자동으로 채워진 폴더 간에 콘텐츠를 이동할 수 있습니다.
