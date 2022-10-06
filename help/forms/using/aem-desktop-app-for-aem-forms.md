---
title: AEM Forms용 AEM 데스크탑 앱
seo-title: AEM desktop app for AEM Forms
description: AEM Forms용 AEM 데스크탑 앱
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# AEM Forms용 AEM 데스크탑 앱 {#aem-desktop-app-for-aem-forms}

AEM 데스크탑 앱을 사용하면 Adobe Experience Manager(AEM) Assets 저장소 및 AEM Forms 이진 파일을 시스템의 네트워크 디렉토리에 매핑할 수 있습니다. 파일 탐색기에서 동기화된 자산 및 이진 파일을 보고 다양한 앱을 사용하여 원하는 대로 파일을 편집할 수 있습니다. 파일을 보는 것 외에도 이진 파일을 만들고 업로드하고 삭제할 수도 있습니다. 또한 소프트웨어에서 파일을 직접 열고 편집하고 저장할 수 있습니다. 예를 들어 디자이너에서 직접 XDP 파일을 열고 편집할 수 있습니다. 로컬로 자산에 대한 변경 사항이 AEM Assets 저장소 및 AEM Forms UI에 반영됩니다.

AEM 인스턴스에서 앱을 다운로드할 수 있습니다. 앱 다운로드에 대한 자세한 내용은 [AEM 데스크탑 앱 릴리스 노트](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## AEM 데스크탑 앱에서 지원되는 AEM Forms 자산 {#aem-forms-assets-supported-in-aem-desktop-app}

이 앱을 사용하여 다음 유형의 AEM Forms 이진 파일(.xdp), PDF 양식(.pdf), 문서(.pdf), 이미지, XML 스키마(.xsd), 스타일 시트(.xfs)를 동기화할 수 있습니다. 앱에는 다른 모든 파일(지원되지 않는 파일)이 0바이트 파일로 나열됩니다. 지원되지 않는 파일을 0바이트 파일로 나열하면 AEM Forms 서버에서 사용할 수 있는 다른 자산이 있는지 사용자가 알 수 있습니다.

>[!NOTE]
>
>파일 이름에는 영숫자, 하이픈 또는 밑줄만 사용할 수 있습니다.

## AEM용 AEM Forms 데스크탑 앱 활성화 {#enable-aem-forms-for-aem-desktop-app}

AEM Desktop App은 Microsoft Windows의 WebDAV 프로토콜 및 Mac OS X의 SMB1을 사용하여 AEM Forms 서버에 연결합니다. 기본적으로 AEM Forms 서버는 이진 파일 및 기타 자산을 WebDAV 또는 SMB 클라이언트와 동기화하도록 활성화되지 않습니다. AEM용 AEM Forms 데스크탑 앱을 활성화하려면 다음 단계를 수행하십시오.

1. 관리자로 AEM Forms에 로그인합니다.
1. 작성자 인스턴스에서 를 클릭합니다. ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > 도구]** ![망치](assets/hammer.png) **[!UICONTROL > 배포 > 작업 > 웹 콘솔]**. 웹 콘솔이 새 창에 열립니다.
1. 웹 콘솔 창에서 **[!UICONTROL FormsManager 추가 기능 구성]** 선택 사항입니다.
1. FormsManager 추가 기능 구성 대화 상자에서 **[!UICONTROL 비동기적 동기화 리소스]** 확인란을 선택하고 를 클릭합니다. **[!UICONTROL 저장]**.
1. AEM Forms 서버를 다시 시작합니다. 다시 시작한 후 AEM Forms 서버가 콘텐츠를 수락하고 AEM 데스크탑 앱과 공유할 수 있도록 활성화됩니다.
1. 앱을 열고 AEM Forms 서버에 연결합니다.

   연결에 성공하면 앱이 `content/dam` 및 `content/dam/formsanddocuments` 폴더. 위의 폴더에서 로컬 폴더로 파일을 이동하고 그 반대로 앱을 사용하여 자동 채워진 폴더 간에 컨텐츠를 이동할 수 있습니다.
