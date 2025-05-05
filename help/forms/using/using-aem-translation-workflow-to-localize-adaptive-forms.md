---
title: AEM 번역 워크플로를 사용하여 적응형 양식 및 기록 문서 현지화
description: AEM 번역 워크플로를 사용하여 적응형 양식 및 기록 문서를 현지화하는 방법에 대해 알아봅니다.
content-type: reference
topic-tags: develop
noindex: true
feature: Adaptive Forms,Foundation Components
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 20%

---

# AEM 번역 워크플로를 사용하여 적응형 양식 및 기록 문서 현지화 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

현지화된 양식을 통해 전 세계 다양한 지역의 대상자를 지원할 수 있습니다. Adobe Experience Manager 번역 워크플로를 통해 적응형 양식 및 해당 기록 문서 를 현지화할 수 있습니다. **기계 번역** 또는 **사람 번역자**&#x200B;를 사용하여 적응형 양식을 지역화할 수 있습니다.

이 문서에서는 적응형 양식 및 기록 문서와 함께 AEM 번역 워크플로를 사용하는 프로세스에 대해 설명합니다.

## 기계 번역을 사용하여 적응형 양식 및 기록 문서 현지화 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

기계 번역 서비스는 콘텐츠를 적응형 양식 및 기록 문서로 즉시 번역합니다. AEM Forms은 기계 번역을 위해 Microsoft Translator의 체험판을 사용하도록 사전 구성되어 있습니다. 다음 단계를 수행하여 적응형 양식 및 기록 문서에 대한 기계 번역을 활성화합니다.

1. AEM Forms UI에서 양식을 선택하고 **사전 추가** 옵션을 선택합니다.
1. **번역 프로젝트에 사전 추가** 화면에서 **새 번역 프로젝트 만들기** 또는 **기존 번역 프로젝트에 추가** 옵션을 선택합니다.
1. **프로젝트 제목** 필드에서 제목을 지정합니다. 예, `Government Reference Site - German locale.`
1. **타겟 언어** 필드에서 로케일(예: `German(de)`)을 지정하고 **완료**&#x200B;를 클릭합니다. 여러 로케일을 지정할 수 있습니다. 양식이 **타겟 언어** 필드에 지정된 모든 로케일로 번역됩니다.
1. [사전 추가] 대화 상자에서 **프로젝트 열기**&#x200B;를 클릭합니다. 프로젝트 화면에서 새로 만든 프로젝트를 엽니다.
1. **번역 요약** 타일 하단의 **생략 부호**&#x200B;를 클릭합니다. 번역 요약 화면이 열립니다.
1. **번역 요약** 화면 상단에 있는 **편집** 아이콘을 클릭합니다. **번역** 탭을 열고 **번역 방법** 화면에서 기계 번역을 선택합니다. 적절한 **번역 공급자** 및 **클라우드 구성**&#x200B;을 선택하십시오. 화면 상단의 **완료** 아이콘을 클릭합니다.
1. **번역 작업** 타일에서 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 아이콘을 클릭하고 **시작**&#x200B;을 클릭합니다. 타일의 상태가 초안으로 변경됩니다. 번역을 완료하면 상태가 **검토 준비됨**(으)로 변경됩니다. 몇 분 후 페이지를 새로 고치고 상태를 확인합니다.
1. **번역 작업** 타일에서 상태가 **검토 준비됨**(으)로 변경된 후 브라우저 창에서 양식을 여십시오. 지역화된 버전의 양식이 표시됩니다.

   >[!NOTE]
   >
   >* 브라우저 창에서 지역화된 버전의 양식을 열기 전에 브라우저의 로케일이 양식의 로케일과 일치하도록 설정되어 있는지 확인하십시오. 예를 들어, 양식이 독일어(de)로 번역된 경우 브라우저의 로케일을 독일어(de)로 설정합니다.
   >* 적응형 양식 구성 요소는 RTL(오른쪽에서 왼쪽) 언어를 지원하지 않습니다. 예를 들면, 히브리어.

   적응형 양식과 함께 자동 생성된 기록 문서도 현지화됩니다.

   기록 문서 설정 및 구성에 대한 자세한 내용은 다음을 참조하십시오.

[기록 문서 템플릿 구성](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[기록 문서 설정](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [기록 문서의 브랜딩 정보를 사용자 지정합니다](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md). 브라우저 로케일이 컴퓨터 언어를 사용하여 적응형 양식을 지역화한 언어와 동일한 언어로 설정되어 있는지 확인하십시오. 브라우저 로케일은 기록 문서의 브랜딩 정보를 현지화하는 데 도움이 됩니다.
1. 현지화된 기록 문서를 보려면 미리보기 생성을 선택합니다. 기록 문서 PDF이 생성되고 브라우저의 새 탭에서 열립니다.

## 사람 번역을 사용하여 적응형 양식 및 해당 기록 문서 현지화 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

사람 번역에서는 콘텐츠를 전문 번역사가 번역할 수 있도록 번역 공급업체로 보냅니다. 번역이 완료되면 번역된 콘텐츠는 반환되어 AEM으로 가져와집니다. 번역 공급업체를 AEM과 통합하면 콘텐츠는 자동으로 AEM과 번역 공급업체 간 전송됩니다.

번역을 위해 XLIFF 형식의 파일이 포함된 사전을 전문 번역자와 공유합니다. 사전에는 각 로케일에 대한 별도의 XLIFF 파일이 포함되어 있습니다. 각 XLIFF 파일에는 최종 사용자와 해당 지역화된 텍스트의 자리 표시자에 표시될 텍스트가 포함되어 있습니다.

사람 번역기를 사용하여 양식 및 해당 기록 문서를 현지화하려면 다음 단계를 수행하십시오.

1. [AEM과 번역 서비스 공급업체를 연결](/help/sites-administering/tc-tic.md)한 다음 [번역 통합 프레임워크 구성을 만듭니다](/help/sites-administering/tc-tic.md).

1. 번역 서비스 및 프레임워크 구성과 [언어 마스터의 페이지를 연결](/help/sites-administering/tc-tic.md)합니다.

1. 번역할 [콘텐츠의 유형을 식별](/help/sites-administering/tc-rules.md)합니다.

1. 언어 마스터를 작성하고 언어 사본의 루트 페이지를 만들어 [번역할 콘텐츠를 준비](/help/sites-administering/tc-prep.md)합니다.

1. [번역 프로젝트를 제작하여](/help/sites-administering/tc-manage.md) 번역할 콘텐츠를 수집하고 번역 프로세스를 준비합니다.

1. 번역 프로젝트를 사용하여 [콘텐츠 번역 프로세스를 관리](/help/sites-administering/tc-manage.md)합니다.

>[!NOTE]
>
>* 적응형 양식 구성 요소는 RTL(오른쪽에서 왼쪽) 언어를 지원하지 않습니다. 예를 들면, 히브리어.
>
