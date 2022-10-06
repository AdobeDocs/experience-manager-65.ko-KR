---
title: 태그 관리
seo-title: Administering Tags
description: AEM에서 태그를 관리하는 방법을 알아봅니다.
seo-description: Learn how to administer Tags in AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
exl-id: ff041ef0-e566-4373-818e-76680ff668d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 6%

---

# 태그 관리 {#administering-tags}

태그는 웹 사이트에 포함된 콘텐츠를 빠르고 손쉽게 분류할 수 있는 방법입니다. 이러한 태그는 검색 결과로 컨텐츠를 더 빨리 찾을 수 있도록 해주는 키워드 또는 레이블(메타데이터)으로 생각할 수 있습니다.

Adobe Experience Manager(AEM)에서 태그는

* 페이지의 컨텐츠 노드(참조) [태그 사용](/help/sites-authoring/tags.md))

* 자산에 대한 메타데이터 노드(참조) [디지털 자산에 대한 메타데이터 관리](/help/assets/metadata.md))

태그는 페이지 및 자산 외에도 AEM Communities 기능에 사용됩니다

* 사용자가 생성한 컨텐츠(참조) [UGC 태깅)](/help/communities/tag-ugc.md)

* 사용 리소스(참조) [태깅 지원 리소스](/help/communities/functions.md#catalog-function))

## 태그 기능 {#tag-features}

AEM 내의 태그 기능 중 일부는 다음과 같습니다.

* 태그는 다양한 네임스페이스로 그룹화할 수 있습니다. 이러한 계층 구조를 통해 분류 체계를 만들 수 있습니다. 이러한 분류법은 AEM 전체에서 전역적입니다.
* 새로 만든 태그의 주요 제한 사항은 특정 네임스페이스 내에서 고유해야 한다는 것입니다.
* 태그의 제목에 태그 경로 분리 문자가 포함되지 않아야 합니다(가 있는 경우 표시되지 않음)

   * 콜론 `:` - 네임스페이스 태그를 구분합니다
   * 슬래시 `/` - 하위 태그를 구분합니다

* 태그는 작성자와 사이트 방문자가 적용할 수 있습니다. 작성자가 누구인지에 관계없이 페이지에 지정할 때나 검색 시에 모든 형태의 태그를 선택할 수 있습니다.
* 태그를 작성하고 &quot;tag-administrators&quot; 그룹 및 다음에 대한 수정 권한이 있는 구성원이 분류를 수정할 수 있습니다 `/content/cq:tags`.

   * 하위 태그를 포함하는 태그를 컨테이너 태그라고 합니다
   * 컨테이너 태그가 아닌 태그는 리프 태그라고 합니다
   * 태그 네임스페이스는 리프 태그 또는 컨테이너 태그입니다

* 태그는 [검색 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) 컨텐츠 찾기를 용이하게 합니다.
* 태그는 [티저 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html): 사용자의 태그 클라우드를 모니터링하여 타깃팅된 컨텐츠를 제공합니다.
* 태깅이 컨텐츠의 중요한 측면인 경우

   * 태그를 사용하는 페이지로 태그를 패키징해야 합니다
   * 확인 [태그 권한](#setting-tag-permissions) 읽기 액세스 활성화

## 태깅 콘솔 {#tagging-console}

태깅 콘솔은 태그와 해당 분류법을 만들고 관리하는 데 사용됩니다. 한 가지 목표는 기본적으로 동일한 것과 관련된 유사한 태그가 많이 없도록 하는 것입니다. 예를 들어, 페이지 및 페이지나 신발 또는 신발을 예로 들 수 있습니다.

태그는 네임스페이스로 그룹화하고, 기존 태그를 사용하여 새로운 태그를 만들기 전에 검토하고, 현재 참조된 컨텐츠에서 태그를 끊지 않고 재구성하여 관리합니다.

태깅 콘솔에 액세스하려면:

* 작성자
* 관리 권한으로 로그인
* 전역 탐색에서

   * 선택 **`Tools`**
   * 선택 **`General`**
   * 선택 **`Tagging`**

![managing_tags_usingthentagationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### 네임스페이스 만들기 {#creating-a-namespace}

새 네임스페이스를 만들려면 **`Create Namespace`** 아이콘.

네임스페이스 자체는 태그이며 하위 태그를 포함할 필요가 없습니다. 그러나 분류 체계를 계속 만들려면 [하위 태그 만들기](#creating-tags): 리프 태그 또는 컨테이너 태그일 수 있습니다.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespace](assets/creating_tags_andnamespacesa.png)

* **제목**

   *(필수)* 네임스페이스의 표시 제목입니다.

* **이름**
   *(선택 사항)* 네임스페이스의 이름입니다. 지정하지 않으면 제목에서 유효한 노드 이름이 만들어집니다. 자세한 내용은 [TagID](/help/sites-developing/framework.md#tagid).

* **설명**

   *(선택 사항)* 네임스페이스에 대한 설명입니다.

필요한 정보를 입력하면

* 선택 **만들기**

### 태그 작업 {#operations-on-tags}

네임스페이스 또는 다른 태그를 선택하면 다음 작업을 사용할 수 있습니다.

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

브라우저 창이 충분히 크지 않아 모든 아이콘을 표시할 수 없을 때, 가장 오른쪽에 있는 아이콘은 **`... More`** 아이콘 - 선택 시 숨겨진 작업 아이콘의 드롭다운 목록을 표시합니다.

![chlimage_1-185](assets/chlimage_1-185.png)

### 네임스페이스 태그 선택 {#selecting-a-namespace-tag}

처음 선택하면 네임스페이스에 태그가 없으면 속성이 오른쪽에 표시되고 그렇지 않으면 하위 태그가 표시됩니다. 선택한 각 태그에는 포함된 태그나 하위 태그가 없는 경우 해당 속성이 표시됩니다.

작업에 대한 태그를 선택하고 다중 선택하려면 제목 옆에 있는 아이콘만 선택합니다. 제목을 선택하면 속성만 표시하거나 태그를 열어 컨텐츠를 표시합니다.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### 태그 속성 보기 {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

네임스페이스 또는 다른 태그를 선택한 경우 **`View Properties`** 아이콘에 대한 정보가 표시됩니다. `name`, 마지막 편집 시간 및 참조 수. 게시된 경우 마지막으로 게시한 시간과 게시자의 ID가 표시됩니다. 이 정보는 태그 열 왼쪽에 있는 열에 나타납니다.

![chlimage_1-189](assets/chlimage_1-189.png)

### 태그 참조 표시 {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

네임스페이스 또는 다른 태그를 선택한 경우 **참조** 아이콘은 태그가 적용된 콘텐츠를 식별합니다.

초기 디스플레이는 적용된 태그 수입니다.

![chlimage_1-191](assets/chlimage_1-191.png)

카운트 오른쪽에 있는 화살표를 선택하면 참조 이름이 나열됩니다.

참조 위로 마우스를 가져가면 참조 경로가 도구 팁으로 표시됩니다.

![chlimage_1-192](assets/chlimage_1-192.png)

### 태그 만들기 {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

네임스페이스 또는 다른 태그를 선택한 경우(제목 옆에 있는 아이콘을 선택하여) **`Create Tag`** 아이콘.

![chlimage_1-194](assets/chlimage_1-194.png)

* **제목**
*(필수) *태그의 표시 제목입니다.

* **이름**
*(선택 사항) *태그의 이름입니다. 지정하지 않으면 제목에서 유효한 노드 이름이 만들어집니다. 자세한 내용은 [TagID](/help/sites-developing/framework.md#tagid).

* **설명**
*(선택 사항) *태그에 대한 설명입니다.

필요한 정보를 입력하면

* 선택 **만들기**

### 태그 편집 {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

네임스페이스 또는 다른 태그를 선택하면 제목, 설명을 변경하고, 다음을 선택하여 제목의 현지화를 제공할 수 **`Edit`**icon.

편집한 후 을 선택합니다 **저장**.

언어 번역 추가에 대한 자세한 내용은 [다른 언어로 태그 관리](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### 태그 이동 {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

네임스페이스 또는 다른 태그를 선택한 경우 **`Move`** 아이콘을 사용하면 태그 관리자 및 개발자가 태그를 새 위치로 이동하거나 이름을 변경하여 분류법을 정리할 수 있습니다. 선택한 태그가 컨테이너 태그이면 태그를 이동하면 모든 하위 태그도 이동합니다.

>[!NOTE]
>
>작성자는 [편집](#editing-tags) 태그 `title`를 눌러 태그를 이동하거나 이름을 변경하지 마십시오.

![chlimage_1-198](assets/chlimage_1-198.png)

* **경로**

   *(읽기 전용)* 선택한 태그의 현재 경로입니다.

* **이동 위치**
태그를 이동할 새 경로를 찾습니다.

* **이름 바꾸기**
처음에는 현재 
`name`섹션에 있는 마지막 항목이 될 필요가 없습니다. 새로운 `name`을 입력해야 합니다.

* 선택 **저장**

### 태그 병합 {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

분류 체계에 중복이 있을 경우 태그 병합을 사용할 수 있습니다. 태그 A를 태그 B로 병합하면 태그 A가 지정된 모든 페이지에 태그 B가 적용되고 작성자는 태그 A를 더 이상 사용할 수 없습니다.

네임스페이스 또는 다른 태그를 선택한 경우 **병합** 아이콘을 클릭하면 병합할 경로를 선택할 수 있는 패널이 열립니다.

![chlimage_1-200](assets/chlimage_1-200.png)

* **경로**

   *(읽기 전용)* 다른 태그에 병합되도록 선택한 태그의 경로입니다.

* **에 병합**
로 이동하여 병합할 태그의 경로를 선택합니다.

>[!NOTE]
>
>병합 후 **경로** 원래 선택된 (사실상) 더 이상 존재하지 않습니다.
>
>참조된 태그를 이동하거나 병합하면 태그가 물리적으로 삭제되지 않으므로 참조를 유지할 수 있습니다.

### 태그 게시 {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

네임스페이스 또는 다른 태그를 선택한 경우 **게시** 아이콘을 사용하여 게시 환경에서 태그를 활성화합니다. 페이지 컨텐츠와 유사하게, 컨테이너 태그인지 여부에 관계없이 선택한 태그만 게시됩니다.

분류 체계(네임스페이스 및 하위 태그)를 게시하기 위해 가장 좋은 방법은 [패키지](/help/sites-administering/package-manager.md) 네임스페이스( [분류 루트 노드](/help/sites-developing/framework.md#taxonomy-root-node)). 반드시 다음을 수행하십시오 [권한 적용](#setting-tag-permissions) 패키지를 만들기 전에 네임스페이스로 이동합니다.

### 태그 게시 취소 {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

네임스페이스 또는 다른 태그를 선택한 경우 **게시 취소** 아이콘이 작성 환경에서 태그를 비활성화하고 게시 환경에서 제거합니다. 와 비슷합니다 `Delete`작업: 선택한 태그가 컨테이너 태그인 경우 모든 하위 태그가 작성 환경에서 비활성화되고 게시 환경에서 제거됩니다.

### 태그 삭제 {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

네임스페이스 또는 다른 태그를 선택한 경우 **삭제** 아이콘이 작성 환경에서 태그를 영구적으로 제거합니다. 태그가 게시되면 게시 환경에서도 제거됩니다. 선택한 태그가 컨테이너 태그인 경우 해당 하위 태그도 모두 제거됩니다.

## 태그 권한 설정 {#setting-tag-permissions}

태그 권한은 다음과 같습니다 [&#39;secure(기본적으로)&#39;](/help/sites-administering/production-ready.md); 태그에 읽기 권한을 명시적으로 허용해야 하는 게시 환경에 대한 우수 사례입니다. 기본적으로, 이 작업은 작성자에 대한 권한이 설정된 후 태그 네임스페이스의 패키지를 만들고 모든 게시 인스턴스에 패키지를 설치하면 수행됩니다.

* 작성자 인스턴스

   * 관리 권한으로 로그인
   * 액세스 [보안 콘솔](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * 예를 들어 http://localhost:4502/useradmin으로 이동합니다.
   * 왼쪽 창에서 [권한 읽기](/help/sites-administering/security.md#permissions) 부여됨
   * 오른쪽 창에서 태그 네임스페이스에 대한 **Path **를 찾습니다

      * 예, `/content/cq:tags/mycommunity`
   * 선택 `checkbox`에서 **읽기** 열
   * 선택 **저장**



![chlimage_1-204](assets/chlimage_1-204.png)

* 모든 게시 인스턴스가 동일한 권한을 가지는지 확인합니다

   * 하나의 접근 방식 [패키지 만들기](/help/sites-administering/package-manager.md#package-manager) 작성자에 대한 네임스페이스

      * on `Advanced` 탭, 대상 `AC Handling` 선택 `Overwrite`
   * 패키지 복제

      * 선택 `Replicate` 패키지 관리자에서


## 여러 언어로 태그 관리 {#managing-tags-in-different-languages}

다음 `title`태그의 속성은 여러 언어로 번역될 수 있습니다. 번역되면 적절한 태그가 표시됩니다 `title`사용자 언어 또는 페이지 언어에 따라 표시될 수 있습니다.

### 여러 언어로 태그 제목 정의 {#defining-tag-titles-in-multiple-languages}

다음은 를 번역하는 방법에 대해 설명합니다 `title`태그 **동물** 영어, 독일어, 프랑스어.

먼저 **스톡 사진** 네임스페이스 및 ** 선택`Edit`** 아이콘(참조: [태그 편집](#editing-tags) 섹션).

태그 편집 패널에서는 태그 제목을 현지화할 언어를 선택하는 기능을 제공합니다.

각 언어를 선택하면 번역된 제목을 입력할 수 있는 텍스트 입력 상자가 나타납니다.

모든 번역이 입력되면 다음을 선택합니다 **저장** 편집 모드를 종료하려면 다음을 수행하십시오.

![chlimage_1-205](assets/chlimage_1-205.png)

일반적으로 태그에 대해 선택한 언어는 사용 가능한 경우 페이지 언어로 이동됩니다. 이 [ `tag` 위젯](/help/sites-developing/building.md#tagging-on-the-client-side) 가 다른 경우에 사용됩니다(양식 또는 대화 상자 등에서). 태그 언어는 컨텍스트에 따라 다릅니다.

페이지 언어 설정을 사용하는 대신 Tagging 콘솔에서는 사용자 언어 설정을 사용합니다. Tagging 콘솔의 &#39;Animals&#39; 태그의 사용자 속성에서 언어를 프랑스어로 설정한 사용자에 대해 &#39;Animaux&#39;가 표시됩니다.

대화 상자에 새 언어를 추가하려면 [태그 편집 대화 상자에 새 언어 추가](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>표준 페이지 구성 요소의 태그 클라우드 및 메타 키워드는 현지화된 태그를 사용합니다 `titles`가능한 경우 페이지 언어를 기반으로 합니다.

## 리소스 {#resources}

* [개발자를 위한 태깅](/help/sites-developing/tags.md)

   사용자 지정 애플리케이션에서 태그를 확장 및 포함하는 태깅 프레임워크에 대한 정보입니다.

* [클래식 UI 태깅 콘솔](/help/sites-administering/classic-console.md)
