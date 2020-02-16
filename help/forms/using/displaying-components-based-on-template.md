---
title: 사용된 템플릿을 기반으로 구성 요소 표시
seo-title: 사용된 템플릿을 기반으로 구성 요소 표시
description: 양식을 만들 때 선택한 템플릿을 기반으로 세로 막대에서 구성 요소를 활성화하는 방법을 알아봅니다.
seo-description: 양식을 만들 때 선택한 템플릿을 기반으로 세로 막대에서 구성 요소를 활성화하는 방법을 알아봅니다.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# 사용된 템플릿을 기반으로 구성 요소 표시{#displaying-components-based-on-the-template-used}

양식 작성자가 [템플릿을](../../forms/using/template-editor.md)사용하여 적응형 양식을 만들면 양식 작성자는 템플릿 정책을 기반으로 특정 구성 요소를 보고 사용할 수 있습니다. 양식 작성 시 양식 작성자가 보는 구성 요소 그룹을 선택할 수 있도록 템플릿 컨텐츠 정책을 지정할 수 있습니다.

## 템플릿의 콘텐츠 정책 변경 {#changing-the-content-policy-of-a-template}

템플릿을 만들면 컨텐츠 저장소 아래에 `/conf` 생성됩니다. 디렉토리에서 만든 폴더에 따라 템플릿 경로는 다음과 같습니다. `/conf``/conf/<your-folder>/settings/wcm/templates/<your-template>`Adobe

템플릿의 컨텐츠 정책을 기반으로 세로 막대에 구성 요소를 표시하려면 다음 단계를 수행하십시오.

1. CRXDE lite를 엽니다.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. CRXDE 파섹

   예를 들어,`/conf/<your-folder>/`

1. CRXDE 파섹 `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   구성 요소 그룹을 선택하려면 새 컨텐츠 정책이 필요합니다. 새 정책을 만들려면 기본 정책을 복사하여 붙여넣고 이름을 변경합니다.

   기본 컨텐츠 정책 경로: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   폴더에서 기본 정책을 복사하여 붙여 넣고 이름을 변경합니다. `gridFluidLayout` 예, `myPolicy`.

   ![기본 정책 복사](assets/crx-default1.png)

1. 새로 만든 정책을 선택하고 형식이 **있는 오른쪽 패널에서 구성 요소** `string[]`속성을 선택합니다.

   구성 요소 속성을 선택하고 열면 구성 요소 편집 대화 상자가 표시됩니다. 구성 요소 편집 대화 상자를 사용하면 **+** 및 **단추를 사용하여 구성 요소 그룹을 추가하거나 제거할 수 있습니다** . 작성자가 사용할 구성 요소를 포함하는 구성 요소 그룹을 추가할 수 있습니다.

   ![정책에서 구성 요소 추가 또는 제거](assets/add-components-list1.png)

   구성 요소 그룹을 추가한 후 확인을 클릭하여 **목록을** 업데이트한 다음 CRXDE 주소 **모음 위에 모두** 저장을 클릭하고 새로 고칩니다.

1. 템플릿에서 컨텐츠 정책을 기본적으로 새로 만든 정책으로 변경합니다. ( `myPolicy` 이 예에서 )

   정책을 변경하려면 CRXDE에서 로 `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`이동합니다.

   속성에서 새 `cq:policy` 정책 `default` `myPolicy`이름()으로 변경합니다.

   ![업데이트된 템플릿 컨텐츠 정책](assets/updated-policy.png)

   템플릿을 사용하여 만든 양식을 작성하면 사이드바에 추가된 구성 요소를 볼 수 있습니다.

