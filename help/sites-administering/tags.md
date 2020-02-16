---
title: 태그 관리
seo-title: 태그 관리
description: AEM 파섹
seo-description: AEM 파섹
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 태그 관리 {#administering-tags}

태그는 웹 사이트에 포함된 컨텐츠를 빠르고 손쉽게 분류할 수 있는 방법입니다. 검색 결과로 보다 신속하게 컨텐츠를 찾을 수 있도록 키워드 또는 레이블(메타데이터)으로 간주할 수 있습니다.

Adobe Experience Manager(AEM)에서 태그는

* 페이지의 컨텐츠 노드(태그 [사용 참조](/help/sites-authoring/tags.md))

* 자산에 대한 메타데이터 노드(디지털 자산에 [대한 메타데이터 관리 참조](/help/assets/metadata.md))

페이지 및 자산 외에도 태그는 AEM Communities 기능에 사용됩니다

* 사용자가 생성한 컨텐츠(UGC [태그 지정 참조)](/help/communities/tag-ugc.md)

* 지원 리소스(Tagging [Enablement 리소스 참조](/help/communities/functions.md#catalog-function))

## 태그 기능 {#tag-features}

AEM 내의 태그 기능 중 일부는 다음과 같습니다.

* 태그를 다양한 네임스페이스로 그룹화할 수 있습니다. 이러한 계층 구조를 통해 분류 체계를 만들 수 있습니다. 이러한 분류는 AEM 전체에서 글로벌합니다.
* 새로 만든 태그의 주요 제한 사항은 특정 네임스페이스 내에서 고유해야 한다는 것입니다.
* 태그 제목에는 태그 경로 분리를 포함할 수 없으며, 태그 경로 분리가 있는 경우 표시되지 않습니다.

   * 콜론 `:` - 네임스페이스 태그 구분
   * 슬래시 `/` - 하위 태그 구분

* 태그는 작성자 및 사이트 방문자가 적용할 수 있습니다. 작성자가 누구인지에 관계없이 페이지에 지정할 때나 검색 시에 모든 형태의 태그를 선택할 수 있습니다.
* 태그를 만들고 &quot;태그 관리자&quot; 그룹의 구성원 및 수정 권한이 있는 구성원이 해당 분류법을 수정할 수 `/content/cq:tags`있습니다.

   * 하위 태그를 포함하는 태그를 컨테이너 태그라고 합니다
   * 컨테이너 태그가 아닌 태그는 리프 태그라고 합니다
   * 태그 네임스페이스는 리프 태그 또는 컨테이너 태그입니다.

* 태그는 검색 구성 요소에서 [](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) 컨텐츠 찾기를 용이하게 하기 위해 사용됩니다.
* Tags are used by the [Teaser component](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html), which monitors a user&#39;s tag cloud to provide targeted content.
* 태깅이 컨텐츠의 중요한 측면인 경우

   * 태그를 사용하는 페이지와 함께 패키징해야 합니다.
   * 태그 사용 권한을 [](#setting-tag-permissions) 읽기 권한으로 설정했는지 확인

## 태깅 콘솔 {#tagging-console}

태깅 콘솔은 태그 및 해당 택소노미를 만들고 관리하는 데 사용됩니다. 한 가지 목표는 기본적으로 동일한 것과 관련된 비슷한 태그가 많이 발생하지 않도록 하는 것입니다.예를 들어, 페이지 및 페이지 또는 신발 및 신발 등을 들 수 있습니다.

태그는 네임스페이스로 그룹화하고, 새 태그를 만들기 전에 기존 태그의 사용을 검토하고, 현재 참조된 컨텐츠에서 태그를 끊지 않고 다시 구성함으로써 관리됩니다.

Tagging 콘솔에 액세스하려면:

* 작성자
* 관리자 권한으로 로그인
* 전역 탐색

   * select **`Tools`**
   * select **`General`**
   * select **`Tagging`**

![managing_tags_usingthentagationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### 네임스페이스 만들기 {#creating-a-namespace}

새 네임스페이스를 만들려면 **`Create Namespace`** 아이콘을 선택합니다.

네임스페이스 자체는 태그이며 하위 태그를 포함할 필요가 없습니다. 그러나 분류 체계를 계속 만들려면 하위 태그를 [](#creating-tags)만듭니다. 이 하위 태그는 리프 태그 또는 컨테이너 태그일 수 있습니다.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_and namespaces](assets/creating_tags_andnamespacesa.png)

* **제목**
   *(필수)* 네임스페이스의 표시 제목입니다.

* **이름**
   *(선택 사항)* 네임스페이스의 이름입니다. 지정하지 않으면 제목에서 유효한 노드 이름이 생성됩니다. TagID [를 참조하십시오](/help/sites-developing/framework.md#tagid).

* **설명**
   *(선택 사항)* 네임스페이스에 대한 설명입니다.

필요한 정보를 입력하면

* select **Create**

### 태그에 대한 작업 {#operations-on-tags}

네임스페이스 또는 기타 태그를 선택하면 다음 작업을 사용할 수 있습니다.

* [속성 보기](#viewing-tag-properties)
* [참조](#showing-tag-references)
* [태그 만들기](#creating-tags)
* [편집](#editing-tags)
* [이동](#moving-tags)
* [병합](#merging-tags)
* [게시](#publishing-tags)
* [게시 취소](#unpublishing-tags)
* [삭제](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

브라우저 창의 너비가 부족하여 모든 아이콘을 표시할 수 없을 때, 맨 오른쪽 아이콘은 **`... More`** 아이콘 아래에 함께 그룹화되며, 이 아이콘을 선택하면 숨겨진 작업 아이콘의 드롭다운 목록이 표시됩니다.

![chlimage_1-185](assets/chlimage_1-185.png)

### 네임스페이스 태그 선택 {#selecting-a-namespace-tag}

처음 선택하면 네임스페이스에 태그가 없으면 속성이 오른쪽에 표시되고 그렇지 않으면 하위 태그가 표시됩니다. 선택한 각 태그는 포함된 태그나 하위 태그가 없는 경우 해당 속성을 표시합니다.

작업에 사용할 태그를 선택하고 다중 선택하려면 제목 옆에 있는 아이콘만 선택합니다. 제목을 선택하면 속성만 표시하거나 태그를 열어 컨텐츠를 표시합니다.

![chlimage_1-186](assets/chlimage_1-186.png)![chlimage_1-187](assets/chlimage_1-187.png)

### 태그 속성 보기 {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

네임스페이스 또는 다른 태그를 선택하면 **`View Properties`** 아이콘을 선택하면 해당 `name`아이콘을 선택하면 마지막 편집 시간 및 참조 수에 대한 정보가 표시됩니다. 게시되면 마지막으로 게시된 시간과 게시자의 ID가 표시됩니다. 이 정보는 태그 열 왼쪽에 있는 열에 나타납니다.

![chlimage_1-189](assets/chlimage_1-189.png)

### 태그 참조 표시 {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

네임스페이스 또는 다른 태그를 선택하면 **참조** 아이콘을 선택하면 태그가 적용된 컨텐츠를 식별합니다.

초기 표시는 적용된 태그 수입니다.

![chlimage_1-191](assets/chlimage_1-191.png)

카운트 오른쪽에 있는 화살표를 선택하면 참조 이름이 나열됩니다.

참조 위로 마우스를 가져가면 참조 경로가 도구 팁으로 표시됩니다.

![chlimage_1-192](assets/chlimage_1-192.png)

### 태그 만들기 {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

네임스페이스 또는 다른 태그를 선택한 경우(제목 옆에 있는 아이콘을 선택하여) **`Create Tag`** 아이콘을 선택하여 현재 태그에 대해 하위 태그를 만들 수 있습니다.

![chlimage_1-194](assets/chlimage_1-194.png)

* **제목***(필수) *태그의 표시 제목입니다.

* **이름***(선택 사항) *태그의 이름입니다. 지정하지 않으면 제목에서 유효한 노드 이름이 생성됩니다. TagID [를 참조하십시오](/help/sites-developing/framework.md#tagid).

* **설명***(선택 사항) *태그에 대한 설명입니다.

필요한 정보를 입력하면

* select **Create**

### 태그 편집 {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

네임스페이스 또는 기타 태그를 선택하면 제목, 설명을 변경하고 **`Edit`**아이콘을 선택하여 제목의 현지화를 제공할 수 있습니다.

편집 후 저장을 **선택합니다**.

언어 번역 추가에 대한 자세한 내용은 다른 언어로 태그 [관리 섹션을 참조하십시오](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### 태그 이동 {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

네임스페이스 또는 다른 태그를 선택하면 태그 관리자 및 개발자는 **`Move`** 아이콘을 선택하여 태그를 새 위치로 이동하거나 이름을 변경하여 분류법을 정리할 수 있습니다. 선택한 태그가 컨테이너 태그이면 태그를 이동하면 모든 하위 태그도 이동합니다.

>[!NOTE]
>
>작성자는 태그를 이동하거나 이름을 변경하지 않고 태그의 [편집만](#editing-tags) 할 `title`수 있는 것이 좋습니다.

![chlimage_1-198](assets/chlimage_1-198.png)

* **경로**
   *(readonly)* 선택한 태그의 현재 경로입니다.

* **이동**: 태그를 이동할 새 경로로 이동합니다.

* **다음으로**&#x200B;이름 바꾸기처음에 태그의 현재 `name`위치를 표시합니다. 새 항목을 입력할 `name`수 있습니다.

* select **Save**

### 태그 병합 {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

분류 체계에 중복이 있을 경우 태그 병합을 사용할 수 있습니다. 태그 A가 태그 B로 병합되면 태그 A가 태그 지정된 모든 페이지에 태그 B가 적용되고 작성자는 태그 A를 더 이상 사용할 수 없습니다.

네임스페이스 또는 다른 태그를 선택하면 **병합** 아이콘을 선택하면 병합할 경로를 선택할 수 있는 패널이 열립니다.

![chlimage_1-200](assets/chlimage_1-200.png)

* **경로**
   *(readonly)* 다른 태그에 병합하기 위해 선택한 태그의 경로입니다.

* **검색에**&#x200B;병합을 클릭하여 병합할 태그의 경로를 선택합니다.

>[!NOTE]
>
>병합 후에는 원래 **선택한** 경로가 더 이상 존재하지 않습니다.
>
>참조된 태그가 이동 또는 병합되면 참조를 유지할 수 있도록 태그가 물리적으로 삭제되지 않습니다.

### 태그 게시 {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

네임스페이스 또는 다른 태그를 선택한 경우 게시 **아이콘을 선택하여** 게시 환경에서 태그를 활성화합니다. 페이지 컨텐츠와 유사하게 선택한 태그만 컨테이너 태그인지 여부에 관계없이 게시됩니다.

분류(네임스페이스 및 하위 태그)를 게시하려면 네임스페이스의 [패키지를](/help/sites-administering/package-manager.md) 만드는 것이 좋습니다(분류 루트 노드 [참조](/help/sites-developing/framework.md#taxonomy-root-node)). 패키지를 생성하기 전에 네임스페이스에 권한을 [](#setting-tag-permissions) 적용해야 합니다.

### 태그 게시 취소 {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

네임스페이스 또는 다른 태그를 선택하면 게시 **취소** 아이콘을 선택하면 작성 환경에서 태그가 비활성화되고 게시 환경에서 제거됩니다. 이 `Delete`작업과 유사하게, 선택한 태그가 컨테이너 태그이면 모든 하위 태그가 작성 환경에서 비활성화되고 게시 환경에서 제거됩니다.

### 태그 삭제 {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

네임스페이스 또는 다른 태그를 선택하면 삭제 **아이콘을** 선택하면 태그가 작성 환경에서 영구적으로 제거됩니다. 태그가 게시되면 게시 환경에서도 제거됩니다. 선택한 태그가 컨테이너 태그이면 모든 하위 태그도 제거됩니다.

## 태그 권한 설정 {#setting-tag-permissions}

태그 권한은 [&#39;보안&#39;(기본적으로)](/help/sites-administering/production-ready.md);태그에 대한 읽기 권한이 명시적으로 허용되어야 하는 게시 환경에 대한 우수 사례입니다. 기본적으로, 이 작업은 작성자에 대한 권한이 설정된 후에 태그 네임스페이스의 패키지를 만들고 모든 게시 인스턴스에 패키지를 설치하면 수행됩니다.

* 작성자 인스턴스

   * 관리자 권한으로 로그인
   * 보안 [콘솔](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)액세스,

      * 예를 들어 http://localhost:4502/useradmin로 이동합니다.
   * 왼쪽 창에서 [읽기 권한을](/help/sites-administering/security.md#permissions) 부여할 그룹(또는 사용자)을 선택합니다.
   * 오른쪽 창에서 태그 네임스페이스에 대한 **Path **를 찾습니다.

      * for example, `/content/cq:tags/mycommunity`
   * 읽기 `checkbox`열에서 **선택합니다** .
   * select **Save**



![chlimage_1-204](assets/chlimage_1-204.png)

* 모든 게시 인스턴스에 동일한 권한이 있는지 확인

   * 한 가지 방법은 작성자에 네임스페이스의 패키지를 [](/help/sites-administering/package-manager.md#package-manager) 만드는 것입니다.

      * 탭에서 `Advanced` `AC Handling``Overwrite`
   * 패키지 복제

      * 패키지 `Replicate` 관리자에서 선택


## 여러 언어로 태그 관리 {#managing-tags-in-different-languages}

태그의 `title`속성은 여러 언어로 번역될 수 있습니다. 번역된 태그는 사용자 언어 또는 페이지 언어에 따라 표시될 `title`수 있습니다.

### 여러 언어로 태그 제목 정의 {#defining-tag-titles-in-multiple-languages}

다음은 Animals 태그의 `title`내용을 **영어로** 독일어 및 프랑스어로 변환하는 방법에 대해 설명합니다.

먼저 Stock Photography 네임스페이스 아래에서 태그를 **선택하고** **`Edit`** [아이콘을 선택합니다(태그](#editing-tags) 편집 섹션 참조).

태그 편집 패널에서는 태그 제목을 현지화할 언어를 선택할 수 있습니다.

각 언어를 선택하면 번역된 제목을 입력할 수 있는 텍스트 입력 상자가 나타납니다.

모든 번역이 입력되면 저장을 선택하여 **편집** 모드를 종료합니다.

![chlimage_1-205](assets/chlimage_1-205.png)

일반적으로, 태그에 대해 선택한 언어는 페이지 언어에서 가져옵니다(사용 가능한 경우). When the [ `tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) is used in other cases (for example in forms or in dialogs), the tag language depends on the context.

태그 지정 콘솔에서는 페이지 언어 설정을 사용하는 대신 사용자 언어 설정을 사용합니다. Tagging 콘솔의 &#39;Animals&#39; 태그에서는 사용자 속성에서 언어를 프랑스어로 설정하는 사용자에 대해 &#39;Animaux&#39;가 표시됩니다.

대화 상자에 새 언어를 추가하려면 태그 편집 대화 [상자에 새 언어 추가를 참조하십시오](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>The tag cloud and the meta keywords in the standard page component use the localized tag `titles`based on the page language, if available.

## 리소스 {#resources}

* [개발자를 위한 태그 지정](/help/sites-developing/tags.md)

   태그 지정 프레임워크와 사용자 정의 애플리케이션의 태그를 확장 및 포함하는 방법에 대한 정보입니다.

* [클래식 UI 태깅 콘솔](/help/sites-administering/classic-console.md)

