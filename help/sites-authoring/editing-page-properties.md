---
title: 콘텐츠 페이지 속성 편집
description: Adobe Experience Manager에서 페이지에 필요한 속성을 정의합니다.
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 42%

---

# 페이지 속성 편집{#editing-page-properties}

페이지에 필요한 속성을 정의할 수 있습니다. 이러한 속성은 페이지의 특성에 따라 다를 수 있습니다. 예를 들어 일부 페이지는 라이브 카피에 연결되어 있을 수 있지만 다른 페이지는 연결되지 않고 라이브 카피 정보를 적절하게 사용할 수 있게 됩니다.

## 페이지 속성 {#page-properties}

속성은 여러 탭에 분산되어 있습니다.

### 기본 {#basic}

* **제목**

  페이지 제목은 여러 위치에 표시됩니다. 예를 들어 **웹 사이트** 탭 목록 및 **사이트** 카드/목록 보기가 있습니다.

  필수 필드입니다.

* **태그**

  선택 상자의 목록을 업데이트하여 페이지에서 태그를 추가하거나 제거할 수 있습니다.

   * 태그를 선택하면 선택 상자 아래에 태그가 나열됩니다. 이 목록에서 x를 사용하여 태그를 제거할 수 있습니다.
   * 빈 선택 상자에 이름을 입력하여 새 태그를 입력할 수 있습니다.

      * Enter 키를 누르면 새 태그가 만들어집니다.
      * 새 태그 오른쪽에 새 태그임을 나타내는 작은 별표가 표시됩니다.

   * 드롭다운 기능을 사용하여 기존 태그에서 선택할 수 있습니다.
   * 선택 상자에서 태그 항목을 마우스로 가리키면 x가 표시됩니다. 이를 통해 이 페이지에서 해당 태그를 제거할 수 있습니다.

  태그에 대한 자세한 내용은 [태그 사용](/help/sites-authoring/tags.md)을 참조하십시오.

* **탐색에서 숨기기**

  결과 사이트의 페이지 탐색에 페이지가 표시되거나 숨겨지는지 여부를 나타냅니다.

* **브랜딩**

  각 페이지 제목에 브랜드 슬러그를 추가하여 페이지 전체에서 일관된 브랜드 정체성을 적용합니다. 이 기능을 사용하려면 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko-KR)의 릴리스 2.14.0 이상에서 페이지 구성 요소를 사용해야 합니다.

   * **재정의** - 이 페이지의 브랜드 슬러그를 정의하려면 선택합니다.
      * 하위 페이지에 **재정의** 값이 설정되지 않은 경우 이 값이 모든 하위 페이지에 상속됩니다.
   * **재정의 값** - 페이지 제목에 추가될 브랜드 슬러그의 텍스트입니다.
      * 이 값은 페이지에서 파이프 문자 뒤에 추가됩니다(예: “Cycling Tuscany | Always ready for the WKND”)
* **페이지 제목**

  페이지에서 사용할 제목입니다. 일반적으로 제목 구성 요소별로 사용됩니다. 비어 있는 경우, **제목**&#x200B;이 사용됩니다.

* **탐색 제목**

  탐색에서 사용할 별도의 제목을 지정할 수 있습니다(예: 간결하게 나타내고자 하는 경우). 비어 있는 경우, **제목**&#x200B;이 사용됩니다.

* **자막**

  페이지에서 사용할 부제입니다.

* **설명**

  페이지, 페이지 용도 또는 추가하고자 하는 기타 세부 정보에 대한 설명입니다.

* **정시**

  게시된 페이지가 활성화되는 날짜 및 시간입니다. 이 페이지는 게시되면 지정된 시간까지 휴면 상태로 유지됩니다.

  즉시 게시하려는 페이지의 경우 이러한 필드를 비워 두십시오(일반적인 시나리오).

* **해제 시간**

  게시된 페이지가 비활성화되는 시간.

  즉각적인 조치를 취할 수 있도록 이 필드를 비워 두십시오.

* **별칭 URL**

  이 페이지의 단축 URL을 입력하여 더 짧고/짧거나 표현식 URL을 가질 수 있습니다.

  예를 들어 웹 사이트 `http://example.com,`에 대해 경로 `/v1.0/startpage`로 식별되는 페이지에 대한 별칭 URL을 `welcome`(으)로 설정하면 `http://example.com/welcome`이(가) `http://example.com/content/v1.0/startpage`의 별칭 URL이 됩니다

  >[!CAUTION]
  >
  >별칭 URL:
  >
  >* 고유해야 합니다. 값이 다른 페이지에서 이미 사용되고 있지 않은지 확인하십시오.
  >* 정규 표현식 패턴을 지원하지 않습니다.
  >* 기존 페이지로 설정하면 안 됩니다.
  >

  vanity URL에 액세스할 수 있도록 Dispatcher을 구성합니다. 자세한 내용은 [가상 URL에 대한 액세스 활성화](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls)를 참조하십시오.

* **가상 URL 리디렉션**

  페이지에서 별칭 URL을 사용할지를 지정합니다.

### 고급 {#advanced}

* **언어**

  페이지 언어입니다.

* **언어 루트**

  페이지가 언어 사본의 루트인 경우 선택해야 합니다.

* **리디렉션**

  이 페이지를 자동으로 리디렉션할 페이지를 지정합니다.

* **디자인**

  이 페이지에 사용할 [디자인](/help/sites-developing/designer.md)을(를) 지정하십시오.

* **별칭**

  이 페이지에서 사용할 별칭을 지정합니다.

   * 예를 들어 페이지 `/content/wknd/us/en/magazine/members-only`에 대한 `private`의 별칭을 정의하면 `/content/wknd/us/en/magazine/private`을 통해서도 이 페이지에 액세스할 수 있습니다.
   * 별칭을 만들면 페이지 노드의 `sling:alias` 속성이 설정되며, 이는 저장소 경로가 아닌 리소스에만 영향을 미칩니다.
   * 편집기의 별칭을 통해 액세스하는 페이지는 게시할 수 없습니다. 편집기의 [게시 옵션](/help/sites-authoring/publishing-pages.md)은 실제 경로를 통해 액세스하는 페이지에 대해서만 사용할 수 있습니다.
   * 자세한 내용은 [SEO 및 URL 관리 모범 사례 아래의 지역화된 페이지 이름](/help/managing/seo-and-url-management.md#localized-page-names)을 참조하십시오.

* **&lt;*경로*>**&#x200B;에서 상속

  페이지가 상속되는지 여부를 나타냅니다. 및 출처:

* **클라우드 구성**

  구성의 경로입니다.

* **허용된 템플릿**

  [사용할 수 있는 템플릿 목록을 정의](/help/sites-authoring/templates.md#allowingatemplate)합니다.

* **사용**(인증 요구 사항)

  페이지에 액세스할 수 있도록 인증 사용을 활성화(또는 비활성화)합니다.

  >[!NOTE]
  >
  >페이지의 닫힌 사용자 그룹은 **[권한](/help/sites-authoring/editing-page-properties.md#permissions)** 탭에 정의됩니다.

  >[!CAUTION]
  >
  >**[권한](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** 탭에서는 `granite:AuthenticationRequired` mixin의 존재 여부에 따라 CUG 구성을 편집할 수 있습니다. `cq:cugEnabled` 속성의 존재에 따라 더 이상 사용되지 않는 CUG 구성을 사용하여 페이지 권한을 구성한 경우 **인증 요구 사항**&#x200B;에 경고 메시지가 표시되며 옵션을 편집할 수 없으며 [권한](/help/sites-authoring/editing-page-properties.md#permissions)도 편집할 수 없습니다.
  >
  >
  >이 경우 CUG 권한은 [클래식 UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)에서 편집해야 합니다.

* **로그인 페이지**

  로그인에 사용할 페이지입니다.

* **구성 내보내기**

  내보내기 구성을 지정합니다.

### 썸네일 {#thumbnail}

페이지 썸네일 이미지를 표시합니다. 다음을 작업을 수행할 수 있습니다.

* **미리 보기 생성**

  썸네일로 사용할 페이지의 미리보기를 생성합니다.

* **이미지 업로드**

  썸네일로 사용할 이미지를 업로드합니다.

* **이미지 선택**

  썸네일로 사용할 기존 에셋을 선택합니다.

* **되돌리기**

  이 옵션은 썸네일을 변경한 후에 사용할 수 있습니다. 변경 사항을 유지하지 않으려면 저장하기 전에 해당 변경 사항을 되돌릴 수 있습니다.

### 소셜 미디어 {#social-media}

* **소셜 미디어 공유**

  페이지에서 사용할 수 있는 공유 옵션을 정의합니다. [핵심 구성 요소 공유](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/sharing.html)에 사용할 수 있는 옵션을 표시합니다.

   * **Facebook에 대해 사용자 공유 사용**
   * **Pinterest에 대해 사용자 공유 사용**
   * **선호하는 XF 변형**
페이지의 메타데이터 생성에 사용되는 경험 조각 변형을 정의합니다.

### 클라우드 서비스 {#cloud-services}

* **클라우드 서비스**

  [클라우드 서비스](/help/sites-developing/extending-cloud-config.md)에 대한 속성을 정의합니다.

### 개인화 {#personalization}

* **ContextHub 구성**

  [ContextHub 구성](/help/sites-developing/ch-configuring.md) 및 [세그먼트 경로](/help/sites-administering/segmentation.md)를 선택하십시오.

* **타겟팅 구성**

  [타깃팅할 범위를 지정하려면 브랜드](/help/sites-authoring/target-adobe-campaign.md)를 선택합니다.

  >[!NOTE]
  >이 옵션을 사용하려면 사용자 계정이 `Target Adminstrators`그룹에 있어야 합니다.

### 권한 {#permissions}

* **권한**

  이 탭에서는 다음 작업을 수행할 수 있습니다.

   * [권한 추가](/help/sites-administering/user-group-ac-admin.md)
   * [폐쇄된 사용자 그룹 편집](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * [유효 권한](/help/sites-administering/user-group-ac-admin.md) 보기

  >[!CAUTION]
  >
  >**권한** 탭에서 `granite:AuthenticationRequired` mixin의 존재 여부에 따라 CUG 구성을 편집할 수 있습니다. `cq:cugEnabled` 속성의 존재 여부에 따라 더 이상 사용되지 않는 CUG 구성을 사용하여 페이지 권한을 구성한 경우 경고 메시지가 표시되고 CUG 권한을 편집할 수 없으며 [고급](/help/sites-authoring/editing-page-properties.md#advanced) 탭의 인증 요구 사항도 편집할 수 없습니다.
  >
  >
  >이 경우 CUG 권한은 [클래식 UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)에서 편집해야 합니다.

  >[!NOTE]
  >
  >권한 탭에서는 빈 CUG 그룹을 만들 수 없으며, 이는 모든 사용자의 액세스를 거부하는 간단한 방법으로 유용할 수 있습니다. 이렇게 하려면 CRX Explorer를 사용해야 합니다. 자세한 내용은 [사용자, 그룹 및 액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md) 문서를 참조하십시오.

### 블루프린트 {#blueprint}

* **블루프린트**

  [다중 사이트 관리](/help/sites-administering/msm.md) 내에서 블루프린트 페이지에 대한 속성을 정의합니다. 수정 사항이 라이브 카피에 전파되는 상황을 제어합니다.

### Live Copy {#live-copy}

* **Livecopy**

  [다중 사이트 관리](/help/sites-administering/msm.md) 내에서 Live Copy 페이지에 대한 속성을 정의합니다. 블루프린트에서 수정 사항이 반영되는 상황을 제어합니다.

### 사이트 구조 {#site-structure}

* **등록 페이지**, **오프라인 페이지** 등 사이트 전체 기능을 제공하는 페이지에 대한 링크를 제공합니다.

## 페이지 속성 편집 {#editing-page-properties-1}

페이지 속성을 정의할 수 있습니다.

* **Sites** 콘솔에서:

   * [페이지 만들기](/help/sites-authoring/managing-pages.md#creating-a-new-page)(속성의 하위 집합)

   * **속성** 클릭 또는 탭

      * 단일 페이지의 경우
      * 여러 페이지의 경우 (속성의 하위 집합만 편집 가능)

* 페이지 편집기에서

   * **페이지 정보**&#x200B;를 사용하여 **속성 열기**

### Sites 콘솔에서 - 단일 페이지 {#from-the-sites-console-single-page}

**속성**&#x200B;을 클릭하거나 탭하여 페이지 속성을 정의하십시오.

1. **사이트** 콘솔에서 속성을 보고 편집할 페이지의 위치로 이동합니다.

1. 다음 중 하나를 사용하여 필요한 페이지에 대한 **속성** 옵션을 선택합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#selectionmode)

   페이지 속성이 해당 탭을 사용하여 표시됩니다.

1. 필요에 따라 속성을 보거나 편집합니다.

1. **저장**&#x200B;을 사용하여 업데이트를 저장한 다음 **닫기**&#x200B;를 클릭하여 콘솔로 돌아갈 수 있습니다.

### 페이지 편집 시 {#when-editing-a-page}

페이지를 편집할 때 **페이지 정보**&#x200B;를 사용하여 페이지 속성을 정의할 수 있습니다.

1. 속성을 편집할 페이지를 엽니다.

1. **페이지 정보** 아이콘을 선택하여 다음과 같은 선택 메뉴를 엽니다.

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. **속성 열기**&#x200B;를 선택하면 해당 탭별로 정렬된 속성을 편집할 수 있는 대화 상자가 열립니다. 다음 버튼은 도구 모음 오른쪽에서도 사용할 수 있습니다.

   * **취소**
   * **저장 및 닫기**

1. **저장 및 닫기** 버튼을 사용하여 변경 사항을 저장합니다.

### Sites 콘솔에서 - 다중 페이지 {#from-the-sites-console-multiple-pages}

**사이트** 콘솔에서 여러 페이지를 선택한 다음 **속성 보기**&#x200B;를 사용하여 페이지 속성을 보거나 편집할 수 있습니다. 이를 페이지 속성의 일괄 편집이라고 합니다.

>[!NOTE]
>
>속성의 일괄 편집은 자산에 대해서도 사용할 수 있습니다. 비슷하지만 몇 가지 점에서 차이가 있습니다. 자세한 내용은 [여러 Assets의 속성 편집](/help/assets/metadata.md)을 참조하십시오.
>
>[대량 편집기](/help/sites-administering/bulk-editor.md)도 있습니다. 이 편집기를 사용하면 GQL(Google 쿼리 언어)을 사용하여 여러 페이지에서 컨텐츠를 검색한 다음 변경 사항을 원래 페이지에 저장하기 전에 벌크 편집기를 사용하여 직접 컨텐츠를 편집할 수 있습니다.

다음을 비롯하여 다양한 방법으로 일괄 편집할 여러 페이지를 선택할 수 있습니다.

* **Sites** 콘솔을 찾아볼 때
* **검색**&#x200B;을 사용하여 일련의 페이지를 찾은 후

![epp-01](assets/epp-01.png)

페이지를 선택한 다음 **속성 옵션**&#x200B;을 클릭하거나 탭하면 일괄 속성이 표시됩니다.

![epp-02](assets/epp-02.png)

다음과 같은 페이지에 대해서만 일괄 편집을 수행할 수 있습니다.

* 동일한 리소스 유형 공유
* Live Copy의 일부가 아님

   * 페이지가 Live Copy에 있을 경우, 속성을 열면 메시지가 표시됩니다.

벌크 편집을 시작하면 다음을 수행할 수 있습니다.

* **보기**

  여러 페이지에 대한 페이지 속성을 볼 때 다음을 볼 수 있습니다.

   * 영향 받는 페이지 목록

      * 필요한 경우 선택/선택 해제할 수 있습니다.

   * 탭

      * 단일 페이지의 속성을 볼 때처럼 탭 아래에 속성이 정렬됩니다.

   * 속성 하위 집합

      * 선택한 모든 페이지에서 사용할 수 있고 일괄 편집에서 사용할 수 있다고 명시적으로 정의된 속성이 표시됩니다.
      * 페이지 선택을 한 페이지로 제한하면 모든 속성이 보입니다.

   * 공통 값을 갖는 공통 속성

      * 공통 값을 갖는 속성만 보기 모드에 표시됩니다.
      * 필드가 다중 값이면(예: 태그) *모두*&#x200B;가 일반적인 경우에만 값이 표시됩니다. 일부만 일반적인 경우 편집할 때만 표시됩니다.

  공통 값이 있는 속성이 없으면 메시지가 표시됩니다.

* **편집**

  여러 페이지에 대한 페이지 속성을 편집할 때:

   * 사용 가능한 필드의 값을 업데이트할 수 있습니다.

      * **완료**&#x200B;를 선택하면 선택한 모든 페이지에 새 값이 적용됩니다.
      * 필드가 다중 값이면(예: 태그) 새 값을 추가하거나 공통 값을 제거할 수 있습니다.

   * 공통되지만 여러 페이지에서 값이 다른 필드는 텍스트 `<Mixed Entries>`과(와) 같은 특수 값으로 표시됩니다.

>[!NOTE]
>
>벌크 편집에 사용할 수 있는 필드를 지정하도록 페이지 구성 요소를 구성할 수 있습니다. [페이지 속성의 벌크 편집을 위한 페이지 구성](/help/sites-developing/bulk-editing.md)을 참조하십시오.
