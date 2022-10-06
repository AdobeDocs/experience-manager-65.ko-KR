---
title: AEM 번역 워크플로우를 사용하여 적응형 양식 및 레코드 문서를 현지화합니다
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: AEM 번역 워크플로우를 사용하여 적응형 양식 및 레코드 문서를 현지화하는 방법을 알아봅니다.
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 15%

---

# AEM 번역 워크플로우를 사용하여 적응형 양식 및 레코드 문서를 현지화합니다 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

현지화된 양식은 여러 지리적 위치에서 더 넓은 대상을 제공하는 데 도움이 됩니다. Adobe Experience Manager 번역 워크플로우는 적응형 양식 및 해당 레코드 문서를 현지화하는 데 도움이 됩니다. 다음을 사용할 수 있습니다 **기계 번역** 또는 **인간 번역가** 적응형 양식을 현지화하는 중입니다.

이 문서에서는 적응형 양식 및 레코드 문서에서 AEM 번역 워크플로우를 사용하는 프로세스에 대해 설명합니다.

## 기계 번역을 사용하여 적응형 양식 및 레코드 문서 현지화 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

기계 번역 서비스는 콘텐츠를 즉시 적응형 양식 및 레코드 문서로 변환합니다. AEM Forms은 기계 번역에 Microsoft Translator 평가판을 사용하도록 사전 구성되어 있습니다. 적응형 양식 및 레코드 문서에 대해 기계 번역을 활성화하려면 다음 단계를 수행하십시오.

1. AEM Forms UI에서 양식을 선택하고 **사전 추가** 선택 사항입니다.
1. in **번역 프로젝트에 사전 추가** 화면에서 을 선택합니다. **새 번역 프로젝트 만들기** 또는 **기존 번역 프로젝트에 추가** 선택 사항입니다.
1. 에서 **프로젝트 제목** 필드에서 제목을 지정합니다. 예, `Government Reference Site - German locale.`
1. 에서 **Target 언어** 필드에서 로케일을 지정합니다(예: `German(de)`). **완료**. 여러 로케일을 지정할 수 있습니다. 양식은 **Target 언어** 필드.
1. 추가된 사전 대화 상자에서 **프로젝트 열기**. 프로젝트 화면에서 새로 만든 프로젝트를 엽니다.
1. 을(를) 클릭합니다. **줄임표** 맨 아래 **번역 요약** 타일. 번역 요약 화면이 열립니다.
1. 을(를) 클릭합니다. **편집** 아이콘을 클릭합니다 **번역 요약** 화면. 를 엽니다. **번역** 탭을 선택하고 **번역 방법** 화면. 적절한 **번역 공급자** 및 **클라우드 구성**. 을(를) 클릭합니다. **완료** 아이콘을 클릭합니다.
1. 설정 **번역 작업** 타일에서 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 아이콘을 클릭하고 **시작**. 타일의 상태가 초안으로 변경됩니다. 번역이 완료되면 상태가 **검토 준비**. 몇 분 후에 페이지를 새로 고침하고 상태를 확인합니다.
1. 상태가 **검토 준비** on **번역 작업** 타일에서 브라우저 창에서 양식을 엽니다. 현지화된 버전의 양식이 표시됩니다.

   >[!NOTE]
   >
   >* 브라우저 창에서 현지화된 버전의 양식을 열기 전에 브라우저의 로케일이 양식의 로케일과 일치하도록 설정되어 있는지 확인하십시오. 예를 들어, 양식이 독일어(de) 언어로 번역되는 경우 브라우저의 로케일을 독일어(de)로 설정합니다.
   >* 적응형 양식 구성 요소는 오른쪽에서 왼쪽(RTL) 언어를 지원하지 않습니다. 예를 들면 히브리어입니다.


   적응형 양식과 함께 자동 생성된 레코드 문서도 현지화됩니다.

   레코드 설정 및 구성 문서에 대한 자세한 내용은 다음을 참조하십시오.

[기록 문서 템플릿 구성](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[레코드 설정 문서](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [레코드 문서의 브랜딩 정보 사용자 정의](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 시스템 언어를 사용하여 적응형 양식을 현지화한 브라우저 로케일이 동일한 언어로 설정되어 있는지 확인합니다. 브라우저 로케일은 기록 문서에서 브랜딩 정보를 현지화하는 데 도움이 됩니다.
1. 현지화된 기록 문서를 보려면 미리 보기 생성을 누릅니다. 레코드 PDF 문서가 생성되고 브라우저의 새 탭에서 열립니다.

## Human Translation을 사용하여 적응형 양식 및 해당 레코드 문서 현지화 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

인간 번역에서 컨텐츠는 번역 공급자에게 전송되고 전문 번역자가 번역합니다. 번역이 완료되면 번역된 콘텐츠는 반환되어 AEM으로 가져와집니다. 번역 공급업체를 AEM과 통합하면 콘텐츠는 자동으로 AEM과 번역 공급업체 간 전송됩니다.

번역을 위해 XLIFF 형식의 파일이 포함된 사전은 전문 번역자와 공유됩니다. 사전에는 각 로케일에 대한 별도의 XLIFF 파일이 포함되어 있습니다. 각 XLIFF 파일에는 최종 사용자에게 표시될 텍스트와 해당 지역화된 텍스트의 자리 표시자가 포함되어 있습니다.

Human Translator를 사용하여 양식 및 기록 문서를 현지화하려면 다음 단계를 수행합니다.

1. [AEM과 번역 서비스 공급업체를 연결](/help/sites-administering/tc-tic.md)한 다음 [번역 통합 프레임워크 구성을 만듭니다](/help/sites-administering/tc-tic.md).

1. 번역 서비스 및 프레임워크 구성과 [언어 마스터의 페이지를 연결](/help/sites-administering/tc-tic.md)합니다.

1. 번역할 [콘텐츠의 유형을 식별](/help/sites-administering/tc-rules.md)합니다.

1. 언어 마스터를 작성하고 언어 사본의 루트 페이지를 만들어 [번역할 콘텐츠를 준비](/help/sites-administering/tc-prep.md)합니다.

1. [번역 프로젝트를 제작하여](/help/sites-administering/tc-manage.md) 번역할 콘텐츠를 수집하고 번역 프로세스를 준비합니다.

1. 번역 프로젝트를 사용하여 [콘텐츠 번역 프로세스를 관리](/help/sites-administering/tc-manage.md)합니다.

>[!NOTE]
>
>* 적응형 양식 구성 요소는 오른쪽에서 왼쪽(RTL) 언어를 지원하지 않습니다. 예를 들면 히브리어입니다.
>

