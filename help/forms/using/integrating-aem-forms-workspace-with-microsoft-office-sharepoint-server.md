---
title: AEM forms 작업 영역과 Microsoft Office SharePoint Server 통합
description: AEM Forms 작업 영역을 Microsoft Office SharePoint Server와 통합할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# AEM forms 작업 영역과 Microsoft Office SharePoint Server 통합{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- 요구 사항**

**전제 조건 지식**
AEM Forms Workspace를 SharePoint Server에 추가하려면 먼저 적절한 권한이 있는 SharePoint Server에 액세스할 수 있어야 하며 Workspace에 액세스하려면 URL을 알고 있어야 합니다. 아래 단계에서는 SharePoint 서버에 대해 잘 알고 있다고 가정합니다. SharePoint Server의 웹 파트에 대한 자세한 내용은 Windows SharePoint Services의 웹 파트를 참조하십시오.

**사용자 수준**
시작

AEM Forms Workspace를 Microsoft Office SharePoint Server(예: Microsoft Office SharePoint Server 2007)에서 웹 파트로 사용할 수 있습니다. 사용자는 웹 브라우저를 사용하여 AEM Forms Server에 연결하여 통합 환경을 제공하여 SharePoint Workspace에 액세스할 수 있습니다. 이 문서에서는 Microsoft Office SharePoint Server에서 AEM Forms Workspace를 웹 파트로 표시하는 기본 단계에 대해 알아봅니다. 이 문서에 설명된 단계를 수행하여 SharePoint 서버에 연결하는 사용자가 동일한 포트에서 AEM Forms Workspace에 액세스할 수 있도록 통합 환경을 제공할 수 있습니다.

>[!NOTE]
>
>이 문서에 나열된 단계는 특정 Microsoft SharePoint Server 2007입니다. 지원되는 다른 버전의 Microsoft SharePoint을 사용하여 HTML 작업 영역을 구성할 수도 있습니다.

## AEM Forms Workspace와 Microsoft Office SharePoint Server 2007 통합 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

AEM Forms 작업 영역을 웹 파트에 통합하려면 다음 단계를 수행하십시오.

1. 웹 브라우저에서 다음과 같은 SharePoint 사이트로 이동합니다. `https://[myMOSSserver]:44299/default.aspx` 위치 `[myMOSSserver]` 은 Sharepoint 서버의 이름 또는 IP 주소입니다.

   >[!NOTE]
   >
   >44299은 SharePoint 서버의 기본 포트 번호입니다. 포트 번호는 SharePoint 서버 설치에 따라 다릅니다.

1. 웹 페이지의 오른쪽 상단에서 **사이트 작업** 및 선택 **페이지 편집**.
1. 다음을 클릭합니다. **웹 파트 추가** 단추를 클릭합니다.
1. 웹 파트 추가 - 웹 페이지 대화 상자의 기타에서 **페이지 뷰어 웹 파트** 그런 다음 을 클릭합니다. **추가**.
1. 페이지 뷰어 웹 파트 상자에서 **편집** 및 선택 **공유 웹 파트 수정**.

   >[!NOTE]
   >
   >페이지 뷰어 웹 파트 상자가 **웹 파트 추가** 다음 그림과 같이 3단계에서 클릭한 단추(그림 1):

   ![Microsoft Office SharePoint 서버의 페이지 뷰어 웹 파트 상자입니다.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   그림 1. - Microsoft Office SharePoint 서버의 페이지 뷰어 웹 파트 상자

1. 페이지 뷰어 페이지에서 다음 작업을 수행합니다.

   1. 링크 상자에 다음과 같은 AEM Forms 작업 영역의 URL을 입력합니다. `https://[AEM_forms_Server]:8080/lc/ws` 위치 `[AEM_forms_Server]` 는 AEM Forms 서버의 IP 또는 이름을 나타냅니다.
   1. 클릭 **모양** 전체 Workspace 사용자 인터페이스를 볼 수 있도록 높이, 너비 및 제목을 수정하십시오. 예를 들어 높이와 너비를 각각 6인치와 11인치로 설정할 수 있습니다.
   1. 클릭 **테스트 링크**. 작업 영역이 표시된 새 웹 브라우저 창이 나타납니다.
   1. (선택 사항) **레이아웃** 웹 파트에서 작업 영역의 레이아웃을 수정할 수 있습니다.
   1. (선택 사항) **고급** 또한 설명 및 웹 파트에서 작업 영역을 최소화하거나 닫을 수 있는지 여부와 같은 다른 설정을 수정합니다.

      **적용**&#x200B;을 클릭합니다.

1. 클릭 **편집 모드 종료** 작업 영역에 액세스할 수 있는지 확인합니다.

위의 단계를 완료하면 SharePoint 사이트가 다음 그림과 비슷하게 표시됩니다(그림 2).

![Microsoft Office SharePoint Server와 통합된 AEM Forms 작업 영역](assets/aem-forms-workspace.jpg)

그림 2 - Microsoft Office SharePoint Server와 통합된 AEM Forms 작업 영역
