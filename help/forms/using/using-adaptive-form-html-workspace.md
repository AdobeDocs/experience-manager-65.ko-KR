---
title: HTML 작업 영역에서 적응형 양식 사용
seo-title: Using an adaptive form in HTML Workspace
description: HTML 작업 영역에서 적응형 양식 사용
seo-description: Using an adaptive form in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# HTML 작업 영역에서 적응형 양식 사용{#using-an-adaptive-form-in-html-workspace}

JEE의 AEM Forms에서는 HTML 작업 영역에서 적응형 양식을 사용할 수 있는 기능을 제공합니다.

프로세스 설계 중에 XDP를 선택할 수 있으므로 기존 적응형 양식 AEM 저장소에서 검색하는 기능이 추가되었습니다. 이 기능을 사용하면 프로세스 디자이너가 시작 지점 및 작업에서 적응형 양식을 구성할 수 있습니다.

## 프로세스 디자인 경험 {#process-design-experience}

적응형 양식을 프로세스 디자인에 사용할 수 있도록 하려면 다음을 수행하십시오.

* 작업 및 시작 지점 할당에서 작업에 양식 자산을 할당할 때 CRX 저장소의 적응형 양식 자산을 찾을 수 있습니다.
* 작업/시작 지점 지정 속성 시트에서 적응형 양식의 최상위/글로벌 도구 모음을 숨길 수 있습니다.
* 적응형 양식의 렌더링 및 제출 작업에 새 작업 프로필을 사용할 수 있습니다.

### LiveCycle 응용 프로그램 내보내기 및 가져오기 {#livecycle-application-export-and-import}

적응형 양식은 AEM 저장소에 있으므로 LiveCycle 애플리케이션 내보내기에는 사용된 적응형 양식에 대한 참조만 포함됩니다. 따라서 LiveCycle 애플리케이션의 내보내기 및 가져오기는 2단계 프로세스입니다. LiveCycle 응용 프로그램에는 프로세스 정의 등이 포함됩니다. 적응형 양식이 포함된 별도의 패키지는 AEM에서 ZIP 파일로 내보내집니다. 가져오는 동안 LiveCycle 응용 프로그램은 Workbench를 통해 가져오고 적응형 양식은 AEM을 통해 가져옵니다.

## Analysis Workspace에서 적응형 양식의 HTML 경험 {#user-experience-of-adaptive-form-in-html-workspace}

HTML 작업 영역에서는 모바일 양식에 사용할 수 있는 컨트롤 외에도 일부 적응형 양식별 컨트롤을 제공합니다. 사용자가 작업 또는 시작 지점을 열 때 HTML 작업 영역에서 첨부 파일을 추가하고, 저장하고, 서명하고, 제출하고, 적응형 양식을 탐색할 수 있습니다. 세부 사항은 다음과 같습니다.

1. 모바일 Forms의 경우와 마찬가지로 파일을 첨부하려면 작업 첨부 파일을 사용합니다. 적응형 양식의 모든 파일 첨부 유형 버튼은 숨겨집니다.

1. 적응형 양식을 저장하려면 **저장**, 모바일 Forms의 경우와 같습니다. 적응형 양식의 모든 저장 유형 버튼은 숨겨집니다.

1. 적응형 양식을 제출하려면 **제출** Mobile Forms의 경우와 마찬가지로 단추 또는 경로 작업을 사용할 수 있습니다. 적응형 양식의 모든 제출 유형 버튼은 숨겨집니다.

1. **적응형 양식 전역 도구 모음 가시성**: 프로세스 디자이너가 전역/최상위 도구 모음, 도구 모음 및 단추를 숨기는 경우 적응형 양식에 해당 단추가 표시되지 않습니다.

1. **적응형 Forms을 위한 작업 영역 탐색 제어** HTML : Analysis Workspace의 적응형 양식에 대한 저장, 제출 및 경로 지정 작업 버튼과 함께 다음/이전 버튼을 사용할 수 있습니다. 다음/이전 단추를 클릭하여 HTML 작업 영역에서 적응형 양식의 패널을 탐색합니다. 다음/이전 단추는 적응형 양식의 모바일 보기에서 탐색 컨트롤과 유사한 딥 탐색을 제공합니다.

1. **적응형 양식의 전자 서명 서비스 및 요약 구성 요소** HTML : Analysis Workspace에서 요약 구성 요소가 작동하지 않습니다. 즉, 적응형 양식에 요약 구성 요소가 있으면 작업 영역에 표시되지 않습니다. Workspace 사용자는 디자인 구성 요소에서 자동 제출 대신 HTML Workspace에서 제출 또는 경로 작업을 클릭합니다. 문서에 서명한 후에는 플랫 서명된 문서로 표시됩니다. 클릭 **제출** 또는 경로 작업을 사용하여 작업 또는 시작점을 닫거나 완료할 수 있습니다.\
   서명된 문서는 eSign 서비스 서버에서 수집되고 데이터 xml 파일은 프로세스의 다음 단계로 전달됩니다.

## 프로세스 디자인에서 적응형 양식을 사용하는 단계 {#steps-to-use-adaptive-forms-in-process-design}

1. Adobe Experience Manager Forms Workbench를 엽니다.

1. 다음으로 이동 **파일 > 새로 만들기 > 응용 프로그램** 또는 기존 응용 프로그램을 사용하여 응용 프로그램을 만듭니다.

   ![새 애플리케이션 만들기](assets/create_new_appl.png)

   새 애플리케이션 만들기

1. 응용 프로그램에서 프로세스를 만들거나 기존 프로세스를 사용합니다.

   ![새 프로세스 만들기](assets/create_new_process.png)

   새 프로세스 만들기

1. 시작 지점 또는 작업 할당을 만들고 두 번 클릭합니다.
1. 아래 **[!UICONTROL 프레젠테이션 및 데이터]** 섹션, 선택 **[!UICONTROL crx 자산 사용]** 에셋 앞에 있는 생략 부호를 클릭합니다.

   ![CRX 자산 사용](assets/use_crx_asset.png)

   CRX 자산 사용

1. 자산 관리 UI를 통해 생성된 적응형 양식을 선택하고 **[!UICONTROL 확인]**.

   ![적응형 양식 선택](assets/selecting_form.png)

   적응형 양식 선택

   >[!NOTE]
   >
   >적응형 양식 만들기에 대한 자세한 내용은 [적응형 양식 만들기](../../forms/using/creating-adaptive-form.md).
   >
   >
   >프로세스 만들기에 대한 자세한 내용은 [프로세스 만들기 및 관리](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
