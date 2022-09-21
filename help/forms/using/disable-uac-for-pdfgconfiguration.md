---
title: JEE 및 OSGI에 적용할 수 있는 PDFG 구성에 대한 UAC 비활성화
description: PDFG 구성에 대한 UAC를 비활성화하는 절차
source-git-commit: f6dcb488c64dad2d65facc0e8e1d6685b7375a08
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# Windows Server에서 Word 또는 Excel 파일을 PDF으로 변환할 수 없습니다. {#unable-to-convert-word-excel-files-PDF}

## 문제 {#issue}

사용자가 Microsoft Windows Server에서 Word 또는 Excel 파일을 PDF으로 변환하려고 하면 다음과 같은 오류가 발생합니다.

*기본 변환기의 오류 메시지: ALC-PDG-015-003-The 시스템에서 입력 파일을 열 수 없습니다. 파일을 다시 제출하거나 시스템 관리자에게 문의하십시오.*


## 솔루션 {#solution}

문제를 해결하려면 다음 단계를 수행하십시오.
1. 시스템 구성 유틸리티에 액세스하려면 다음 위치로 이동하십시오. **[!UICONTROL 시작 > 실행]** 그런 다음 를 입력합니다. **[!UICONTROL MSCONFIG]**.
1. 을(를) 클릭합니다. **[!UICONTROL 도구]** 탭을 선택하고 아래로 스크롤한 다음 선택합니다. **[!UICONTROL UAC 설정 변경]**. 클릭 **[!UICONTROL Launch]** 새 창에서 명령을 실행하려면
1. 슬라이더를 [알림 안 함] 수준으로 조정합니다. 완료되면 명령 창을 닫고 시스템 구성 창을 닫습니다.
1. UAC에 대한 레지스트리 설정이 0으로 설정되어 있는지 확인합니다. 확인하려면 다음 단계를 수행하십시오.

   1. Microsoft®은 레지스트리를 수정하기 전에 이 레지스트리를 백업하는 것을 권장합니다. 자세한 단계는 [Windows에서 레지스트리를 백업 및 복원하는 방법](https://support.microsoft.com/en-us/help/322756).
   1. Microsoft® Windows 레지스트리 편집기를 엽니다. 레지스트리 편집기를 열려면 시작 > 실행으로 이동하여 regedit를 입력한 다음 확인을 클릭합니다.
   1. 다음으로 이동 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. EnableLUA 값이 0으로 설정되어 있는지 확인합니다.
   1. 값 확인 **EnableLUA** 이 0으로 설정되어 있습니다. 값이 0이 아니면 값을 0으로 변경합니다. 레지스트리 편집기를 닫습니다.

1. 컴퓨터를 다시 시작합니다.

## 적용 대상 {#appliesto}

이 솔루션은 다음과 같은 경우에 적용됩니다.
* JEE 서버의 AEM Forms
* OSGi 서버의 AEM Forms