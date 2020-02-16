---
title: AEM 번역 워크플로우를 사용하여 적응형 양식 및 기록 문서 현지화
seo-title: AEM 번역 워크플로우를 사용하여 적응형 양식 및 기록 문서 현지화
description: AEM 번역 워크플로우를 사용하여 적응형 양식 및 기록 문서를 현지화하는 방법을 학습합니다.
seo-description: AEM 번역 워크플로우를 사용하여 적응형 양식 및 기록 문서를 현지화하는 방법을 학습합니다.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# AEM 번역 워크플로우를 사용하여 적응형 양식 및 기록 문서 현지화 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

지역화된 양식을 통해 다양한 지역의 고객에게 전달할 수 있습니다. Adobe Experience Manager 번역 워크플로우를 통해 적응형 양식과 기록 문서를 현지화할 수 있습니다. 기계 **번역** 또는 **인간 변환기를** 사용하여 적응형 양식을 현지화할 수 있습니다.

이 문서에서는 적응형 양식 및 기록 문서와 함께 AEM 번역 워크플로우를 사용하는 프로세스에 대해 설명합니다.

## 기계 번역을 사용하여 적응형 양식 및 기록 문서 현지화 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

기계 번역 서비스는 즉시 적응형 양식과 기록 문서로 컨텐츠를 변환합니다. AEM Forms는 기계 번역에 Microsoft Translator 시험버전을 사용하도록 미리 구성되어 있습니다. 적응형 양식 및 기록 문서에 대해 기계 번역을 활성화하려면 다음 단계를 수행하십시오.

1. AEM Forms UI 파섹  ****
1. 번역 **프로젝트에 사전 추가** 화면에서 **새 번역 프로젝트** 만들기 또는 **기존 번역 프로젝트에** 추가 옵션을 선택합니다.
1. 프로젝트 **제목** 필드에서 제목을 지정합니다. 예, `Government Reference Site - German locale.`
1. 타겟 **언어** 필드에서 로케일(예: `German(de)`)을 지정하고 완료를 **클릭합니다**. 여러 로케일을 지정할 수 있습니다. 이 양식은 타겟 언어 필드에 지정된 모든 로캘로 **변환됩니다** .
1. 사전 추가됨 대화 상자에서 프로젝트 **열기를 클릭합니다**. 프로젝트 화면에서 새로 만든 프로젝트를 엽니다.
1. 번역 **요약** 타일 아래쪽에 있는 줄임표를 **클릭합니다** . 번역 요약 화면이 열립니다.
1. 번역 **요약** 화면 상단에 있는 **편집 아이콘을 클릭합니다** . 번역 **탭을 열고** 번역 방법 화면에서 기계 **번역을** 선택합니다. 적절한 번역 **제공업체** 및 클라우드 구성을 **선택합니다**. Click the **Done** icon at the top of the screen.
1. 번역 **작업** 타일에서 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 아이콘을 클릭하고 시작을 **클릭합니다**. 타일 상태가 초안으로 변경됩니다. 번역 완료 시 상태가 검토 **준비로**&#x200B;변경됩니다. 몇 분 후에 페이지를 새로 고치고 상태를 확인합니다.
1. 번역 작업 **타일에서 상태가 검토** 준비 **(** Ready for review)로 변경되면 브라우저 창에서 양식을 엽니다. 현지화된 버전의 양식이 표시됩니다.

   >[!NOTE]
   >
   >* 브라우저 창에서 현지화된 버전의 양식을 열기 전에 브라우저의 로케일이 양식의 로케일과 일치하도록 설정되어 있는지 확인합니다. 예를 들어, 양식이 독일어(de) 언어로 번역된 경우 브라우저의 로케일을 독일어(de)로 설정합니다.
   >* 적응형 양식 구성 요소는 오른쪽에서 왼쪽으로(RTL) 언어를 지원하지 않습니다. 예: 히브리어.


   적응형 양식과 함께 자동 생성된 기록 문서도 지역화되었습니다.

   기록 문서 설정 및 구성에 대한 자세한 내용은 다음을 참조하십시오.

   [기록 문서 템플릿 구성](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [기록 문서 설정](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [기록](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 문서의 브랜딩 정보를 사용자 정의하고 시스템 언어를 사용하여 적응형 양식을 현지화한 브라우저 로케일이 동일한 언어로 설정되어 있는지 확인합니다. 브라우저 로케일은 기록 문서에서 브랜딩 정보를 현지화하는 데 도움이 됩니다.
1. 지역화된 기록 문서를 보려면 미리 보기 생성을 누릅니다. PDF 기록 문서가 생성되고 브라우저의 새 탭에서 열립니다.

## Human Translation을 사용하여 적응형 양식 및 기록 문서 현지화 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Human Translation에서 컨텐츠는 번역 공급자로 전송되고 전문 번역가가 번역합니다. 완료되면 번역된 컨텐츠가 반환되고 AEM으로 가져오게 됩니다. 번역 공급자가 AEM과 통합되면 컨텐츠가 AEM과 번역 공급자 사이에 자동으로 전송됩니다.

번역 시 XLIFF 형식의 파일이 포함된 사전은 전문 번역자와 공유됩니다. 사전에는 각 로케일에 대해 별도의 XLIFF 파일이 포함되어 있습니다. 각 XLIFF 파일에는 최종 사용자에게 표시될 텍스트와 해당 지역화된 텍스트의 자리 표시자가 포함되어 있습니다.

인간 변환기를 사용하여 양식과 문서를 현지화하려면 다음 단계를 수행하십시오.

1. [번역 서비스 제공자와](/help/sites-administering/tc-tic.md) AEM을 연결하고 번역 통합 프레임워크 구성을 [만듭니다](/help/sites-administering/tc-tic.md).

1. [언어 마스터의](/help/sites-administering/tc-tic.md) 페이지를 번역 서비스 및 프레임워크 구성과 연결합니다.

1. [번역할 컨텐츠](/help/sites-administering/tc-rules.md) 유형을 확인합니다.

1. [언어 마스터를 작성하고 언어 사본의 루트 페이지를 만들어 번역](/help/sites-administering/tc-prep.md) 컨텐츠를 준비합니다.

1. [번역 프로젝트를](/help/sites-administering/tc-manage.md) 만들어 번역할 컨텐츠를 수집하고 번역 프로세스를 준비합니다.

1. 번역 프로젝트를 사용하여 컨텐츠 번역 프로세스를 [관리합니다](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* 적응형 양식 구성 요소는 오른쪽에서 왼쪽으로(RTL) 언어를 지원하지 않습니다. 예: 히브리어.
>



