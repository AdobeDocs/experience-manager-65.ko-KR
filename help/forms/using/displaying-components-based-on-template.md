---
title: 사용된 템플릿을 기반으로 구성 요소 표시
seo-title: 사용된 템플릿을 기반으로 구성 요소 표시
description: 양식을 만들 때, 선택한 템플릿을 기준으로 사이드바에서 구성 요소를 활성화할 수 있는 방법을 알아봅니다.
seo-description: 양식을 만들 때, 선택한 템플릿을 기준으로 사이드바에서 구성 요소를 활성화할 수 있는 방법을 알아봅니다.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 1%

---

# 사용된 템플릿{#displaying-components-based-on-the-template-used}에 따라 구성 요소 표시

양식 작성자가 [템플릿](../../forms/using/template-editor.md)을 사용하여 적응형 양식을 작성하면 양식 작성자는 템플릿 정책을 기반으로 특정 구성 요소를 보고 사용할 수 있습니다. 양식 작성 시 양식 작성자에게 표시되는 구성 요소 그룹을 선택할 수 있는 템플릿 컨텐츠 정책을 지정할 수 있습니다.

## 템플릿 {#changing-the-content-policy-of-a-template} 의 컨텐츠 정책 변경

템플릿을 만들면 컨텐츠 저장소의 `/conf` 아래에 만들어집니다. `/conf` 디렉토리에서 만든 폴더에 따라 템플릿의 경로는 다음과 같습니다.`/conf/<your-folder>/settings/wcm/templates/<your-template>`.

템플릿의 컨텐츠 정책에 따라 사이드바에 구성 요소를 표시하려면 다음 단계를 수행하십시오.

1. CRXDE Lite를 엽니다.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. CRXDE에서 템플릿을 만들 폴더로 이동합니다.

   예를 들어,`/conf/<your-folder>/`

1. CRXDE에서 다음 위치로 이동합니다.`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   구성 요소 그룹을 선택하려면 새 컨텐츠 정책이 필요합니다. 새 정책을 만들려면 기본 정책을 복사하여 붙여넣은 다음 이름을 바꿉니다.

   기본 컨텐츠 정책의 경로는 다음과 같습니다.`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   `gridFluidLayout` 폴더에서 기본 정책을 복사하여 붙여넣고 이름을 바꿉니다. 예, `myPolicy`.

   ![기본 정책 복사](assets/crx-default1.png)

1. 새로 만든 정책을 선택하고 `string[]` 유형의 오른쪽 패널에서 **구성 요소** 속성을 선택합니다.

   구성 요소 속성을 선택하고 열면 구성 요소 편집 대화 상자가 표시됩니다. 구성 요소 편집 대화 상자에서는 **+** 및 **-** 단추를 사용하여 구성 요소 그룹을 추가하거나 제거할 수 있습니다. 작성자가 사용할 구성 요소를 포함하는 구성 요소 그룹을 추가할 수 있습니다.

   ![정책에서 구성 요소 추가 또는 제거](assets/add-components-list1.png)

   구성 요소 그룹을 추가한 후 **확인**&#x200B;을 클릭하여 목록을 업데이트한 다음 CRXDE 주소 표시줄 위에 **모두 저장**&#x200B;을 클릭하고 새로 고칩니다.

1. 템플릿에서 컨텐츠 정책을 기본값에서 만든 새 정책으로 변경합니다. ( 이 예에서 `myPolicy`)

   정책을 변경하려면 CRXDE에서 `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`으로 이동합니다.

   `cq:policy` 속성에서 `default`을 새 정책 이름( `myPolicy`)으로 변경합니다.

   ![템플릿 콘텐츠 정책이 업데이트되었습니다.](assets/updated-policy.png)

   템플릿을 사용하여 양식을 작성할 때 사이드바에서 추가된 구성 요소를 볼 수 있습니다.
