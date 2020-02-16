---
title: 제출 검토자를 양식과 연결
seo-title: 제출 검토자를 양식과 연결
description: AEM Forms에서 제출 검토자를 양식과 연결하는 방법을 알아봅니다. 관련 검토자는 양식 포털을 통해 제출된 양식을 검토합니다.
seo-description: AEM Forms에서 제출 검토자를 양식과 연결하는 방법을 알아봅니다. 관련 검토자는 양식 포털을 통해 제출된 양식을 검토합니다.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
translation-type: tm+mt
source-git-commit: 55c12683ba66b3aace07ea83931c9c32ea65663e

---


# 제출 검토자를 양식과 연결 {#associating-submission-reviewers-with-a-form}

양식을 만들 때, 양식 포털을 통해 양식의 제출을 검토하는 사용자를 지정하고 피드백을 제공할 수 있습니다. 조직은 제출된 양식에 대한 피드백 및 재작업을 수집할 수 있습니다.

AEM Forms를 사용하면 검토자 그룹을 양식과 연결할 수 있습니다. 양식의 검토 그룹에 추가된 사용자는 이 양식의 제출 내용을 보고 피드백을 제공합니다.

양식에 지정된 검토자 그룹은 지정된 양식의 제출물만 검토할 수 있습니다.

## 전제 조건 {#prerequisite}

### 메타데이터 스키마 편집기를 사용하여 응용 양식에 대한 제출 검토자 그룹 속성 활성화 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

검토자 그룹을 양식과 연결하려면 적응형 양식의 메타데이터 스키마를 편집합니다. 기본적으로 검토자 그룹은 제출된 양식에 추가할 수 없습니다.

메타데이터 스키마를 편집하려면:

1. 작성 모드의 Experience Manager에서 도구 > **자산** > **메타데이터** 스키마를 **클릭합니다**.
1. 스키마 양식 페이지에서 양식 > **AEM에서** 작성한 **양식으로 이동합니다.**

   페이지의 URL은 다음과 같습니다.

   ```
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 적응형 **양식을** 선택하고 편집을 **클릭합니다**.
1. 양식 편집 페이지에서 고급을 **클릭합니다**.
1. 고급 탭에서 양식 작성 아래에서 **사용할 수 있는 단일 행 텍스트** 구성 요소를 드래그하여 놓습니다.
1. 추가된 텍스트 구성 요소를 선택하여 해당 설정을 확인합니다.

   설정에서 속성에 매핑 `./jcr:content/metadata/form-submission-reviewer-group` 필드에 입력합니다.

   적응형 양식의 고급 속성에 있는 제출 검토자 그룹 필드는 필드 레이블에서 지정한 이름으로 활성화됩니다.

## 제출 검토자를 양식과 연결 {#associating-submission-reviewers-with-a-form-1}

제출 검토자를 적응형 양식과 연결하려면 검토자 그룹을 만들어 사용자를 추가합니다. 양식의 고급 속성에 양식 제출 검토자 필드 아래에 작성된 검토자 그룹을 추가합니다.
사용자 그룹을 사용하면 서로 다른 제출 검토자 집합을 적응형 양식과 연결할 수 있습니다. 이 기능을 사용하면 권한이 없는 사용자로부터 제출 검토를 받을 수 없습니다.

다음 단계를 수행하기 전에 전제 조건을 [참조하십시오](../../forms/using/adding-reviewers-form.md#prerequisite).

그룹을 만들고 여기에 구성원을 추가하려면 도구 > 작업 > **보안** > **그룹** 으로 **** 이동합니다 ****.Groups로이동합니다.
자세한 내용은 사용자 관리 [및 서비스를 참조하십시오](/help/sites-administering/security.md).
기본 사용자 그룹의 구성원으로 만든 그룹을 추가해야 합니다. **양식 제출 검토자**. 이 사용자 그룹은 AEM Forms와 함께 제공되므로 사용자를 제출 검토자로 추가할 수 있습니다.

사용자 그룹을 적응형 양식과 연결하려면

1. 작성 모드에서 양식 > **양식** 및 **문서로 이동합니다**.
1. **Select **Select **옵션을 사용하여 적응형 양식을 선택하고 속성 **보기를 클릭합니다**.
1. 양식의 속성 창에서 편집을 클릭한 **다음**&#x200B;고급을 **클릭합니다**.
1. 제출 검토자 그룹 필드에 그룹을 입력하고 완료를 **클릭합니다**.

   전송 검토자 그룹 필드가 응용 양식의 편집된 메타데이터 스키마에 지정한 이름과 함께 나타납니다.

>[!NOTE]
>
>사용자 및 양식을 복제하여 AEM Forms의 원격 구현에서 사용자와 양식을 사용할 수 있도록 합니다.
>
>원격 구현에서 사용자 그룹의 구성원을 검토하도록 모든 사용자가 복제되었는지 확인합니다.

