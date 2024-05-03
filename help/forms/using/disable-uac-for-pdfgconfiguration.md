---
title: JEE와 OSGI 모두에 적용할 수 있는 PDFG 구성에 대한 UAC를 비활성화합니다.
description: PDFG 구성에 대한 UAC를 비활성화하여 Word에서 PDF으로 변환하는 방법에 대해 알아봅니다.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Windows Server에서 Word 또는 Excel 파일을 PDF으로 변환할 수 없음 {#unable-to-convert-word-excel-files-PDF}

## 문제 {#issue}

사용자가 Microsoft® Windows Server에서 Word 또는 Excel 파일을 PDF으로 변환하려고 할 때 다음과 같은 오류가 발생합니다.

*기본 변환기의 오류 메시지:*
*ALC-PDG-015-003-시스템이 입력 파일을 열 수 없습니다. 파일을 다시 제출하거나 시스템 관리자에게 문의하십시오.*


## 솔루션 {#solution}

다음 작업을 수행합니다.

1. 시스템 구성 유틸리티에 액세스하려면 **[!UICONTROL 시작 > 실행]** 입력한 다음 **[!UICONTROL MSCONFIG]**.
1. 다음을 클릭합니다. **[!UICONTROL 도구]** 탭을 누르고 아래로 스크롤한 다음 선택 **[!UICONTROL UAC 설정 변경]**. 클릭 **[!UICONTROL 시작]** 새 창에서 명령을 실행할 수 있습니다.
1. 슬라이더를 알림 안 함 레벨로 조정합니다. 완료되면 명령 창을 닫고 시스템 구성 창을 닫습니다.
1. UAC에 대한 레지스트리 설정이 0으로 설정되어 있는지 확인하십시오. 다음 단계를 수행하여 확인합니다.

   1. Microsoft®는 레지스트리를 수정하기 전에 백업하는 것을 권장합니다. 자세한 단계는 를 참조하십시오. [Windows에서 레지스트리를 백업 및 복원하는 방법](https://support.microsoft.com/en-us/help/322756).
   1. Microsoft® Windows 레지스트리 편집기를 엽니다. 레지스트리 편집기를 열려면 시작 > 실행으로 이동하고 regedit 를 입력한 다음 확인 을 클릭합니다.
   1. 다음으로 이동 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. EnableLUA 값이 0(영)으로 설정되어 있는지 확인합니다.
   1. 값 확인 **EnableLUA** 0으로 설정되어 있습니다. 값이 0이 아니면 값을 0으로 변경합니다. 레지스트리 편집기를 닫습니다.

1. 컴퓨터를 다시 시작합니다.

## 적용 대상 {#appliesto}

이 솔루션은 JEE 서버의 AEM Forms 및 OSGi 서버의 AEM Forms에 적용됩니다.
