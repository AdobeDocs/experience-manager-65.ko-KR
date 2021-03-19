---
title: AEM Forms용 AEM 데스크탑 앱
seo-title: AEM Forms용 AEM 데스크탑 앱
description: AEM Forms용 AEM 데스크탑 앱
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# AEM Forms용 AEM 데스크탑 앱 {#aem-desktop-app-for-aem-forms}

AEM 데스크탑 앱을 사용하면 Adobe Experience Manager(AEM) 자산 저장소 및 AEM Forms 이진 파일을 시스템의 네트워크 디렉토리에 매핑할 수 있습니다. 파일 탐색기에서 동기화된 에셋과 바이너리 파일을 보고 다양한 앱을 사용하여 원하는 대로 파일을 편집할 수 있습니다. 파일을 보는 것 외에도 이진 파일을 만들고 업로드 및 삭제할 수 있습니다. 또한 소프트웨어에서 직접 파일을 열고 편집 및 저장할 수 있습니다. 예를 들어 Designer에서 XDP 파일을 직접 열고 편집할 수 있습니다. 자산을 로컬로 변경한 내용은 AEM Assets 저장소 및 AEM Forms UI에 반영됩니다.

AEM 인스턴스에서 앱을 다운로드할 수 있습니다. 앱 다운로드에 대한 자세한 내용은 [AEM 데스크탑 앱 릴리스 노트](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html)를 참조하십시오.

## AEM 데스크탑 앱 {#aem-forms-assets-supported-in-aem-desktop-app}에서 지원되는 AEM Forms 에셋

이 앱을 사용하여 다음 유형의 양식 템플릿(.xdp), PDF 양식(.pdf), 문서(.pdf), 이미지, XML 스키마(.xsd), 스타일 시트(.xfs)의 AEM Forms 이진 파일을 동기화할 수 있습니다. 앱은 다른 모든 파일(지원되지 않는 파일)을 0바이트 파일로 나열합니다. 지원되지 않는 파일을 0바이트 파일로 나열하면 AEM Forms 서버에서 사용할 수 있는 다른 에셋이 있는지 알 수 있습니다.

>[!NOTE]
>
>파일 이름은 영숫자, 하이픈 또는 밑줄만 포함할 수 있습니다.

## AEM 데스크탑 앱용 AEM Forms 활성화 {#enable-aem-forms-for-aem-desktop-app}

AEM 데스크탑 앱은 Microsoft Windows의 경우 WebDAV 프로토콜을 사용하고 Mac OS X의 경우 SMB1을 사용하여 AEM Forms 서버에 연결합니다. 기본적으로 AEM Forms 서버는 WebDAV 또는 SMB 클라이언트와 이진 파일 및 기타 에셋을 동기화할 수 없습니다. AEM 데스크탑 앱용 AEM Forms을 활성화하려면 다음 단계를 수행하십시오.

1. AEM Forms에 관리자로 로그인합니다.
1. 작성자 인스턴스에서 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > 도구]** ![ 망치](assets/hammer.png) **[!UICONTROL 배포 > 작업 > 웹 콘솔]**&#x200B;을 클릭합니다. 웹 콘솔이 새 창에 열립니다.
1. 웹 콘솔 창에서 **[!UICONTROL FormsManager AddOn 구성]** 옵션을 찾아 엽니다.
1. FormsManager AddOn 구성 대화 상자에서 **[!UICONTROL 비동기식으로 리소스 동기화]** 확인란을 선택 취소하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
1. AEM Forms 서버를 다시 시작합니다. 다시 시작한 후 AEM Forms 서버가 AEM 데스크탑 앱과 컨텐츠를 승인하고 공유할 수 있도록 활성화됩니다.
1. 앱을 열고 AEM Forms 서버에 연결합니다.

   성공적으로 연결되면 앱이 `content/dam` 및 `content/dam/formsanddocuments` 폴더를 채웁니다. 위의 폴더에서 로컬 폴더로 파일을 이동하고, 그 반대로 파일을 이동하면 이 앱을 사용하여 자동 채워진 폴더 간에 컨텐츠를 이동할 수 있습니다.

