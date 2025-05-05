---
title: 제출 서류 검토자를 양식과 연결
description: AEM Forms에서 제출 서류 검토자를 양식과 연결하는 방법을 알아봅니다. 관련 검토자는 Forms 포털을 통해 제출된 양식을 검토합니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# 제출 서류 검토자를 양식과 연결 {#associating-submission-reviewers-with-a-form}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

양식을 만들 때 양식 포털을 통해 양식 제출을 검토하고 피드백을 제공하는 사용자를 지정할 수 있습니다. 조직은 피드백을 수집하고 제출된 양식에 대해 다시 작업할 수 있습니다.

AEM Forms을 사용하면 검토자 그룹을 양식과 연결할 수 있습니다. 양식의 검토 그룹에 추가된 사용자는 이 양식의 제출 사항을 보고 피드백을 제공합니다.

양식에 할당된 검토자 그룹은 지정된 양식의 제출만 검토할 수 있습니다.

## 전제 조건 {#prerequisite}

### 메타데이터 스키마 편집기를 사용하여 적응형 양식에 대한 제출 검토자 그룹 속성 활성화 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

검토자 그룹을 양식에 연결하려면 적응형 양식의 메타데이터 스키마를 편집합니다. 기본적으로 제출된 양식에 검토자 그룹을 추가할 수 없습니다.

메타데이터 스키마를 편집하려면:

1. 작성자 모드의 Experience Manager에서 **도구** > **Assets** > **메타데이터 스키마**&#x200B;를 클릭합니다.
1. 스키마 Forms 페이지에서 **Forms** > **AEM에서 작성된 Forms**&#x200B;으로 이동합니다.

   페이지의 URL은 다음과 같습니다.

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. **적응형 양식**&#x200B;을 선택하고 **편집**&#x200B;을 클릭합니다.
1. 양식 편집 페이지에서 **고급**&#x200B;을 클릭합니다.
1. 고급 탭에서 빌드 양식에서 사용할 수 있는 **한 줄 텍스트** 구성 요소를 드래그 앤 드롭합니다.
1. 추가된 텍스트 구성 요소를 선택하여 해당 설정을 확인합니다.

   [설정] 아래의 [속성에 매핑] 필드에 `./jcr:content/metadata/form-submission-reviewer-group`을(를) 입력합니다.

   적응형 양식의 고급 속성에 있는 제출 검토자 그룹 필드는 필드 레이블 아래에 지정한 이름으로 활성화됩니다.

## 제출 서류 검토자를 양식과 연결 {#associating-submission-reviewers-with-a-form-1}

제출 검토자를 적응형 양식과 연결하려면 검토자 그룹을 만들고 사용자를 추가하십시오. 양식의 고급 속성에서 양식 제출 검토자 필드 아래에 작성된 검토자 그룹을 추가합니다.
사용자 그룹을 사용하면 다양한 제출 검토자 세트를 다른 적응형 양식에 연결할 수 있습니다. 이 기능은 권한이 없는 사용자의 제출 검토를 방지합니다.

다음 단계를 수행하기 전에 [필수 구성 요소](../../forms/using/adding-reviewers-form.md#prerequisite)를 참조하십시오.

그룹을 만들고 구성원을 추가하려면 **도구** > **작업** > **보안** > **그룹**(으)로 이동합니다.
자세한 내용은 [사용자 관리 및 서비스](/help/sites-administering/security.md)를 참조하십시오.
만든 그룹을 기본 제공 사용자 그룹 **forms-submission-reviewers**&#x200B;의 구성원으로 추가했는지 확인하십시오. 이 사용자 그룹은 AEM Forms과 함께 제공되며 사용자가 제출 검토자로 추가되었는지 확인합니다.

사용자 그룹을 적응형 양식과 연결하려면 다음 작업을 수행하십시오.

1. 작성 모드에서 **Forms** > **Forms 및 문서**(으)로 이동합니다.
1. **선택**&#x200B;옵션을 사용하여 적응형 양식을 선택하고 **속성 보기**&#x200B;를 클릭하세요.
1. 양식의 속성 창에서 **편집**&#x200B;을 클릭한 다음 **고급**&#x200B;을 클릭합니다.
1. 제출 검토자 그룹 필드에 그룹을 입력하고 **완료**&#x200B;를 클릭합니다.

   제출 검토자 그룹 필드가 적응형 양식의 편집된 메타데이터 스키마에 지정한 이름으로 나타납니다.

>[!NOTE]
>
>AEM Forms의 원격 구현에서 사용자 및 양식의 가용성을 보장하기 위해 사용자 및 양식을 복제합니다.
>
>모든 사용자가 원격 구현에서 사용자 그룹의 구성원을 검토하는 것으로 복제되는지 확인하십시오.
