---
title: 제출 검토자와 양식 연결
seo-title: Associating submission reviewers with a form
description: AEM Forms에서 제출 검토자와 양식을 연결하는 방법을 알아봅니다. 관련 검토자는 양식 포털을 통해 제출된 양식을 검토합니다.
seo-description: Learn how to associate submission reviewers with a form in AEM Forms. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
feature: Adaptive Forms
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 제출 검토자와 양식 연결 {#associating-submission-reviewers-with-a-form}

양식을 만들 때 양식 포털을 통해 양식 제출을 검토하고 피드백을 제공하는 사용자를 지정할 수 있습니다. 조직은 제출된 양식에 대한 피드백 및 재작업을 수집할 수 있습니다.

AEM Forms에서는 검토자 그룹을 양식과 연결할 수 있습니다. 양식의 검토 그룹에 추가된 사용자는 이 양식의 제출을 보고 피드백을 제공합니다.

양식에 할당된 검토자 그룹은 지정된 양식의 제출만 검토할 수 있습니다.

## 전제 조건 {#prerequisite}

### 메타데이터 스키마 편집기를 사용하여 적응형 양식의 제출 검토자 그룹 속성을 활성화합니다 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

검토자 그룹을 양식에 연결하려면 적응형 양식의 메타데이터 스키마를 편집하십시오. 기본적으로 제출된 양식에 검토자 그룹을 추가할 수 없습니다.

메타데이터 스키마를 편집하려면 다음을 수행합니다.

1. 작성 모드의 Experience Manager에서 **도구** > **자산** > **메타데이터 스키마**.
1. 스키마 Forms 페이지에서 다음 위치로 이동합니다. **Forms** > **AEM에서 작성된 Forms.**

   페이지의 URL은 다음과 같습니다.

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 선택 **적응형 양식** 을(를) 클릭합니다. **편집**.
1. 양식 편집 페이지에서 **고급**.
1. 고급 탭에서 **단일 행 텍스트** 구성 요소는 빌드 양식에서 사용할 수 있습니다.
1. 추가된 텍스트 구성 요소를 선택하여 해당 설정을 확인합니다.

   설정에서 을 입력합니다. `./jcr:content/metadata/form-submission-reviewer-group` 속성 매핑 필드에서 참조할 수 있습니다.

   적응형 양식의 고급 속성의 제출 검토자 그룹 필드는 필드 레이블에서 지정하는 이름으로 활성화됩니다.

## 제출 검토자와 양식 연결 {#associating-submission-reviewers-with-a-form-1}

제출 검토자를 적응형 양식과 연결하려면 검토자 그룹을 만들고 사용자를 해당 검토자에 추가합니다. 양식의 고급 속성의 양식 제출 검토자 필드 아래에 생성된 검토자 그룹을 추가합니다.
사용자 그룹을 사용하면 서로 다른 전송 검토자 세트를 다른 적응형 양식과 연결할 수 있습니다. 이 기능은 권한이 없는 사용자로부터 제출 검토를 차단합니다.

다음 단계를 수행하기 전에 [전제 조건](../../forms/using/adding-reviewers-form.md#prerequisite).

그룹을 만들고 구성원을 추가하려면 다음 위치로 이동합니다. **도구** > **작업** > **보안** > **그룹**.
자세한 내용은 [사용자 관리 및 서비스](/help/sites-administering/security.md).
기본 사용자 그룹의 구성원으로 만든 그룹을 추가해야 합니다. **forms 제출 검토자**. 이 사용자 그룹은 AEM Forms과 함께 제공되며, 사용자가 제출 검토자로 추가되도록 합니다.

사용자 그룹을 적응형 양식과 연결하려면

1. 작성 모드에서 **Forms** > **Forms 및 문서**.
1. **선택 **옵션을 사용하여 적응형 양식을 선택하고 **속성 보기**.
1. 양식의 속성 창에서 **편집**&#x200B;를 클릭한 다음 **고급**.
1. 제출 검토자 그룹 필드에 그룹을 입력하고 **완료**.

   적응형 양식의 편집된 메타데이터 스키마에 지정한 이름과 함께 제출 검토자 그룹 필드가 나타납니다.

>[!NOTE]
>
>사용자 및 양식을 복제하여 AEM Forms의 원격 구현에서 사용자 및 양식의 가용성을 보장합니다.
>
>원격 구현에서 사용자 그룹의 구성원 검토로 모든 사용자가 복제되는지 확인합니다.
