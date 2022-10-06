---
title: Client Context
seo-title: Client Context
description: AEM에서 Client Context를 사용하는 방법을 알아봅니다.
seo-description: Learn how to use the Client Context in AEM.
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---

# Client Context{#client-context}

>[!NOTE]
>
>Client Context가 ContextHub로 대체되었습니다. 자세한 내용은 관련 [구성]ch-configuring.md) 및 [개발자](/help/sites-developing/contexthub.md) 설명서입니다.

Client Context 는 현재 페이지 및 방문자에 대한 특정 정보를 제공하는 메커니즘입니다. 다음 아이콘을 사용하여 열 수 있습니다 **Ctrl-Alt-c** (windows) 또는 **control-option-c** (Mac):

![](assets/clientcontext_alisonparker.png)

두 가지 모두 [게시 및 작성 환경 이 정보를 표시합니다.](#propertiesavailableintheclientcontext) 정보:

* 방문자 특정 정보가 요청되거나 파생되는 인스턴스에 따라 다릅니다.
* 페이지 태그 및 현재 방문자가 이러한 태그에 액세스한 횟수(특정 태그 위로 마우스를 이동할 때 표시됨) .
* 페이지 정보.
* 기술 환경에 대한 정보 IP 주소, 브라우저 및 화면 해상도 등
* 현재 해결된 모든 세그먼트입니다.

아이콘(작성 환경에서만 사용 가능)을 사용하여 클라이언트 컨텍스트의 세부 사항을 구성할 수 있습니다.

![](do-not-localize/clientcontext_icons.png)

* **편집**
새 페이지가 열리고 다음 작업을 수행할 수 있습니다 [프로필 속성 편집, 추가 또는 제거](#editingprofiledetails).

* **로드**
다음을 수행할 수 있습니다 [프로필 목록에서 을(를) 선택하고 프로필을 로드합니다](#loading-a-new-user-profile) 테스트해 보십시오.

* **재설정**
다음을 수행할 수 있습니다 [프로필 재설정](#resetting-the-profile-to-the-current-user) 현재 사용자의 ID로 전송하는 것입니다.

## 사용 가능한 Client Context 구성 요소 {#available-client-context-components}

Client Context는 다음 속성을 표시할 수 있습니다([편집을 사용하여 선택한 내용에 따라](#adding-a-property-component)):

**서퍼 정보** 다음 클라이언트측 정보를 표시합니다.

* a **IP 주소**
* **키워드** 검색 엔진 참조에 사용됩니다.
* a **브라우저** 사용 중
* a **OS** 사용 중인 운영 체제
* 화면 **resolution**
* a **마우스 X** position
* a **마우스 Y** position

**활동 스트림** 다양한 플랫폼에서 사용자의 소셜 활동에 대한 정보를 제공합니다. 예를 들어 AEM 포럼, 블로그, 등급 등이 있습니다.

**캠페인** 작성자가 캠페인에 대한 특정 경험을 시뮬레이션할 수 있습니다. 이 구성 요소는 일반적인 캠페인 해상도 및 경험 선택을 무시하여 다양한 순열 테스트를 활성화합니다.

캠페인 해결은 일반적으로 캠페인의 우선 순위 속성을 기반으로 합니다. 경험은 일반적으로 세그먼테이션을 기반으로 선택됩니다.

**장바구니** 제품 항목(제목, 수량, 가격, 형식이 지정된 등), 해결된 프로모션(제목, 메시지 등)을 포함한 장바구니 정보를 표시합니다. 및 바우처(코드, 설명 등)는

또한 장바구니 세션 저장소는 ClientContextCartServlet을 사용하여 해결된 프로모션 변경 사항(세그먼테이션 변경 사항 기반)에 대해 서버에 알립니다.

**일반 저장소** 저장소의 컨텐츠를 표시하는 일반 구성 요소입니다. 일반 저장소 속성 구성 요소의 하위 버전입니다.

일반 저장소는 사용자 지정 방식으로 데이터를 표시할 JS 렌더러로 구성해야 합니다.

**일반 저장소 속성** 저장소의 컨텐츠를 표시하는 일반 구성 요소입니다. 일반 저장소 구성 요소의 상위 수준 버전입니다.

일반 저장소 속성 구성 요소에는 구성된 속성(축소판과 함께)을 나열하는 기본 렌더러가 포함되어 있습니다.

**지리적 위치** 클라이언트의 위도와 경도를 표시합니다. HTML5 지리적 위치 API를 사용하여 브라우저에 현재 위치를 쿼리합니다. 이렇게 하면 방문자에게 팝업이 표시됩니다. 이 팝업에서는 브라우저가 방문자에게 위치 공유에 동의하는지 여부를 묻습니다.

Context Cloud에 표시되면 구성 요소는 Google API를 사용하여 맵을 축소판으로 표시합니다. 구성 요소는 Google API를 따릅니다 [사용 제한](https://developers.google.com/maps/documentation/staticmaps/intro#Limits).

>[!NOTE]
>
>AEM 6.1에서 Geolocation 저장소는 더 이상 역 Geocoding 기능을 제공하지 않습니다. 따라서 지리적 위치 저장소는 더 이상 도시 이름이나 국가 코드와 같이 현재 위치에 대한 세부 사항을 검색하지 않습니다. 이 저장소 데이터를 사용하는 세그먼트는 제대로 작동하지 않습니다. 지리적 위치 저장소는 위치의 위도와 경도만 포함합니다.

**JSONP 스토어** 설치에 따라 달라지는 컨텐츠를 표시하는 구성 요소입니다.

JSONP 표준은 동일한 오리진 정책을 우회할 수 있도록 해주는 JSON을 보완합니다(따라서 웹 앱이 다른 도메인에 있는 서버와 통신할 수 없도록 함). 이 JSON은 JSON 개체를 함수 호출에 래핑하는 방식으로 로드될 수 있습니다. `<script>` 다른 도메인(동일한 원본 정책에 허용되는 예외)에서 가져옵니다.

JSONP 저장소는 다른 스토어처럼 표시되지만 현재 도메인에 대한 해당 정보에 대한 프록시를 보유할 필요 없이 다른 도메인에서 오는 정보를 로드합니다. 에서 예제를 참조하십시오. [JSONP를 통해 Client Context에 데이터 저장](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>JSONP 저장소는 쿠키에 정보를 캐시하지 않지만 각 페이지 로드 시 해당 데이터를 검색합니다.

**프로필 데이터** 사용자 프로필에 수집된 정보를 표시합니다. 예를 들어 성별, 연령, 이메일 주소 등이 있습니다.

**해결된 세그먼트** 현재 해결된 세그먼트를 표시합니다(종종 Client Context에 표시된 다른 정보에 따라 다름). 캠페인을 구성할 때 관심이 있습니다.

예를 들어, 마우스가 현재 창의 왼쪽 또는 오른쪽 부분 위에 있는지 여부를 나타냅니다. 이 세그먼트는 주로 변경 사항을 즉시 볼 수 있으므로 테스트에 사용됩니다.

**소셜 그래프** 사용자의 친구 및 팔로워에 대한 소셜 그래프를 표시합니다.

>[!NOTE]
>
>현재 이 기능은 데모 사용자의 프로필 노드에 사전 구성된 데이터 세트를 사용하는 데모 기능입니다. 예를 들어 다음을 참조하십시오.
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => friends 속성

**태그 클라우드** 현재 페이지에 설정된 태그와 사이트를 서핑하는 동안 수집된 태그를 표시합니다. 태그 위로 마우스를 이동하면 현재 사용자가 특정 태그를 포함하는 페이지에 액세스한 횟수가 표시됩니다.

>[!NOTE]
방문한 페이지에 표시되는 DAM 자산에 설정된 태그는 카운트되지 않습니다.

**테크노그래픽 저장소** 이 구성 요소는 설치에 따라 다릅니다.

**ViewedProducts** 쇼핑객이 본 제품을 추적합니다. 가장 최근에 본 제품 또는 장바구니에 아직 없는 가장 최근에 본 제품에 대해 질문할 수 있습니다.

이 세션 저장소에 기본 클라이언트 컨텍스트 구성 요소가 없습니다.

자세한 내용은 [Client Context 관련 세부 사항](/help/sites-developing/client-context.md).

>[!NOTE]
페이지 데이터가 더 이상 Client Context에 기본 구성 요소로 없습니다. 필요한 경우 Client Context를 편집하고, **일반 저장소 속성** 구성 요소를 구성한 다음 이를 구성하여 **스토어** 로서의 `pagedata`.

## Client Context 프로필 변경 {#changing-the-client-context-profile}

Client Context를 사용하면 대화식으로 세부 사항을 변경할 수 있습니다.

* Client Context에서 사용 중인 프로필을 변경하면 다양한 사용자가 현재 페이지에 대해 보게 될 다양한 경험을 볼 수 있습니다.
* 사용자 프로필을 변경할 뿐만 아니라 일부 프로필 세부 사항을 변경하여 페이지 경험이 다양한 조건에서 어떻게 다른지 확인할 수 있습니다.

### 새 사용자 프로필 로드 {#loading-a-new-user-profile}

다음 방법 중 하나로 프로필을 변경할 수 있습니다.

* [로드 아이콘 사용](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [선택 슬라이더 사용](#loadinganewvisitorprofilewiththeselectionslider)

완료되면 다음을 수행할 수 있습니다 [프로필 재설정](#resetting-the-profile-to-the-current-user).

#### 프로필 로드 아이콘을 사용하여 새 방문자 프로필 로드 {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. 프로필 로드 아이콘을 클릭합니다.

   ![](do-not-localize/clientcontext_loadprofile.png)

1. 그러면 대화 상자가 열리고, 여기에서 로드할 프로필을 선택할 수 있습니다.

   ![](assets/clientcontext_profileloader.png)

1. 클릭 **확인** 을 눌러 로드하십시오.

#### 선택 슬라이더를 사용하여 새 사용자 프로필 로드 {#loading-a-new-user-profile-with-the-selection-slider}

선택 슬라이더를 사용하여 프로파일을 선택할 수도 있습니다.

1. 현재 사용자를 나타내는 아이콘을 두 번 클릭합니다. 선택기가 열리고 화살표를 사용하여 사용 가능한 프로필을 탐색하고 확인합니다.

   ![](assets/clientcontext_profileselector.png)

1. 로드할 프로필을 클릭합니다. 세부 사항이 로드되면 선택기 바깥쪽을 클릭하여 닫습니다.

#### 현재 사용자에게 프로필 재설정 {#resetting-the-profile-to-the-current-user}

1. 재설정 아이콘을 사용하여 Client Context의 프로파일을 현재 사용자의 프로파일에 반환합니다.

   ![](do-not-localize/clientcontext_resetprofile.png)

### 브라우저 플랫폼 변경 {#changing-the-browser-platform}

1. 브라우저 플랫폼을 나타내는 아이콘을 두 번 클릭합니다. 선택기가 열리고, 화살표를 사용하여 사용 가능한 플랫폼/브라우저를 탐색하고 확인합니다.

   ![](assets/clientcontext_browserplatform.png)

1. 로드할 플랫폼 브라우저를 클릭합니다. 세부 사항이 로드되면 선택기 바깥쪽을 클릭하여 닫습니다.

### 지리적 위치 변경 {#changing-the-geolocation}

1. 지리적 위치 아이콘을 두 번 클릭합니다. 확장된 맵이 열립니다. 여기에서 마커를 새 위치로 드래그할 수 있습니다.

   ![](assets/clientcontext_geomocationrelocate.png)

1. 닫으려면 맵 바깥쪽을 클릭합니다.

### 태그 선택 변경 {#changing-the-tag-selection}

1. Client Context의 Tag Cloud 섹션을 두 번 클릭합니다. 태그를 선택할 수 있는 대화 상자가 열립니다.

   ![](assets/clientcontext_tagselection.png)

1. 확인을 눌러 Client Context에 로드합니다.

## Client Context 편집 {#editing-the-client-context}

클라이언트 컨텍스트를 편집하는 것은 특정 속성의 값을 설정(또는 재설정)하거나, 새 속성을 추가하거나, 더 이상 필요하지 않은 속성을 제거하는 데 사용할 수 있습니다.

### 속성 세부 사항 편집 {#editing-property-details}

클라이언트 컨텍스트를 편집하는 것은 특정 속성의 값을 설정(또는 재설정)하는 데 사용할 수 있습니다. 이렇게 하면 특정 시나리오를 테스트할 수 있습니다(특히 [세분화](/help/sites-administering/campaign-segmentation.md) 및 [캠페인](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)).

![](assets/clientcontext_alisonparker_edit.png)

### 속성 구성 요소 추가 {#adding-a-property-component}

를 연 후 **ClientContext 디자인 페이지**, 다음 작업도 수행할 수 있습니다 **추가** 사용 가능한 구성 요소(구성 요소는 사이드 킥이나 **새 구성 요소 삽입** 을 두 번 클릭하면 열리는 대화 상자 **구성 요소 또는 자산을 여기로 드래그하십시오** 상자):

![](assets/clientcontext_alisonparker_new.png)

### 속성 구성 요소 제거 {#removing-a-property-component}

를 연 후 **ClientContext 디자인 페이지**, 다음 작업도 수행할 수 있습니다 **제거** 더 이상 필요하지 않은 경우 속성입니다. 여기에는 기본적으로 제공되는 속성이 포함됩니다. **재설정** 제거되면 복원할 것입니다.

## JSONP를 통해 Client Context에 데이터 저장 {#storing-data-in-client-context-via-jsonp}

JSONP 저장소 컨텍스트 저장소 구성 요소를 사용하여 외부 데이터를 Client Context에 추가하려면 이 예제를 따르십시오. 그런 다음 해당 데이터의 정보를 기반으로 세그먼트를 만듭니다. 이 예에서는 WIPmania.com이 제공하는 JSONP 서비스를 사용합니다. 이 서비스는 웹 클라이언트의 IP 주소를 기반으로 지리적 위치 정보를 반환합니다.

이 예제에서는 Geometrixx Outdoors 샘플 웹 사이트를 사용하여 Client Context에 액세스하고 생성된 세그먼트를 테스트합니다. 페이지가 Client Context를 활성화한 경우 다른 웹 사이트를 사용할 수 있습니다. (자세한 내용은 [페이지에 Client Context 추가](/help/sites-developing/client-context.md#adding-client-context-to-a-page))

### JSONP 저장소 구성 요소 추가 {#add-the-jsonp-store-component}

JSONP 저장소 구성 요소를 Client Context에 추가하고 이 구성 요소를 사용하여 웹 클라이언트에 대한 지리적 위치 정보를 검색하고 저장합니다.

1. AEM 작성자 인스턴스에서 Geometrixx Outdoors 사이트의 영어 홈 페이지를 엽니다. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Client Context를 열려면 Ctrl-Alt-c(windows) 또는 Control-option-c(Mac)을 누릅니다.
1. Client Context 상단의 편집 아이콘을 클릭하여 Client Context Designer를 엽니다.

   ![](do-not-localize/chlimage_1.png)

1. JSONP 저장소 구성 요소를 Client Context로 드래그합니다.

   ![](assets/chlimage_1-4.jpeg)

1. 구성 요소를 두 번 클릭하여 편집 대화 상자를 엽니다.
1. JSONP 서비스 URL 상자에 다음 URL을 입력한 다음 저장소 가져오기를 클릭합니다.

   `https://api.wipmania.com/jsonp?callback=${callback}`

   구성 요소는 JSONP 서비스를 호출하고 반환된 데이터에 포함된 모든 속성을 나열합니다. 목록에 있는 속성은 Client Context에서 사용할 수 있는 속성입니다.

   ![](assets/chlimage_1-40.png)

1. 확인을 클릭합니다.
1. Geometrixx Outdoors 홈 페이지로 돌아가서 페이지를 새로 고칩니다. 이제 Client Context에 JSONP 저장소 구성 요소의 정보가 포함됩니다.

   ![](assets/chlimage_1-41.png)

### 세그먼트 만들기 {#create-the-segment}

JSONP 저장소 구성 요소를 사용하여 만든 세션 저장소의 데이터를 사용합니다. 이 세그먼트는 세션 저장소의 위도와 현재 날짜를 사용하여 클라이언트의 위치에서 겨울 시간인지 여부를 결정합니다.

1. 웹 브라우저에서 도구 콘솔을 엽니다(`https://localhost:4502/miscadmin#/etc`).
1. 폴더 트리에서 도구/세그먼테이션 폴더를 클릭한 다음 새로 만들기 > 새 폴더를 클릭합니다. 다음 속성 값을 지정한 다음 만들기를 클릭합니다.

   * 이름: 세그먼트
   * 제목: 내 세그먼트

1. 내 세그먼트 폴더를 선택하고 새로 만들기 > 새 페이지를 클릭합니다.

   1. 제목에 Winter를 입력합니다.
   1. 세그먼트 템플릿을 선택합니다.
   1. 만들기를 클릭합니다.

1. 겨울 세그먼트를 마우스 오른쪽 버튼으로 클릭하고 열기 를 클릭합니다.
1. 일반 저장소 속성을 기본 AND 컨테이너로 드래그합니다.

   ![](assets/chlimage_1-5.jpeg)

1. 구성 요소를 두 번 클릭하여 편집 대화 상자를 열고 다음 속성 값을 지정한 다음 확인을 클릭합니다.

   * 저장: 위광
   * 속성 이름: latitude
   * 연산자: 보다 큼
   * 속성 값: 30

1. 스크립트 구성 요소를 동일한 AND 컨테이너로 드래그하고 해당 편집 대화 상자를 엽니다. 다음 스크립트를 추가한 다음 확인을 클릭합니다.

   `3 < new Date().getMonth() < 12`
