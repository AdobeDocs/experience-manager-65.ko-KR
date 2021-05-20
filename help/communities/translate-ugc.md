---
title: 사용자가 생성한 컨텐츠 번역
seo-title: 사용자가 생성한 컨텐츠 번역
description: 번역 기능 작동 방식
seo-description: 번역 기능 작동 방식
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Administrator
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 1%

---

# 사용자가 생성한 컨텐츠 번역 {#translating-user-generated-content}

AEM Communities의 번역 기능은 [페이지 컨텐츠 번역](../../help/sites-administering/translation.md)의 개념을 [SCF(소셜 구성 요소 프레임워크) 구성 요소](scf.md)를 사용하여 커뮤니티 사이트에 게시된 UGC(사용자 생성 컨텐츠)로 확장합니다.

UGC의 번역을 통해 사이트 방문자와 구성원이 언어 장벽을 제거하여 글로벌 커뮤니티를 경험할 수 있습니다.

예를 들어, 다음과 같이 가정하십시오.

* 프랑스 출신의 한 회원이 다국적 요리 웹사이트 커뮤니티 포럼에 요리법을 게재했다.
* 또 다른 일본인은 이 요리법을 프랑스어에서 일본어로 번역하는 것을 트리거하기 위해 사용한다.
* 이 요리법을 일본어로 읽은 뒤, 일본의 한 멤버는 일본어로 댓글을 올렸다.
* 프랑스 출신 A씨는 번역기능을 이용해 일본어 표현을 프랑스어로 번역한다.
* 글로벌 커뮤니케이션.

## 개요 {#overview}

이 설명서의 섹션에서는 AEM을 [번역 서비스 공급자](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider)에 연결하고 [번역 통합 프레임워크](../../help/sites-administering/tc-tic.md)를 구성하여 웹 사이트에 해당 서비스를 통합하는 방법을 이해하면서 UGC에서 번역 서비스가 작동하는 방식을 자세히 설명합니다.

번역 서비스 공급자가 사이트와 연결되면 사이트의 각 언어 사본은 주석과 같은 SCF 구성 요소를 통해 게시된 UGC 자체 스레드를 유지합니다.

번역 서비스 제공자 외에 번역 통합 프레임워크를 구성할 경우, 사이트의 각 언어 사본이 UGC의 단일 스레드를 공유할 수 있어 언어 사본 간에 글로벌 통신을 제공할 수 있다. 언어별로 구분된 토론 스레드 대신 구성된 [글로벌 공유 저장소](#global-translation-of-ugc)를 사용하면 표시된 언어 복사본에 관계없이 전체 스레드를 볼 수 있습니다. 또한, 지역별 등 글로벌 참여자의 논리적 그룹화를 위해 서로 다른 글로벌 공유 스토어를 지정하여 여러 번역 통합 구성을 구성할 수 있습니다.

## 기본 번역 서비스 {#the-default-translation-service}

AEM Communities에는 여러 언어로 활성화된 [기본 번역 서비스](../../help/sites-administering/tc-msconf.md)에 대한 [평가판 라이선스](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license)이 포함되어 있습니다.

[커뮤니티 사이트](sites-console.md)를 만들면 [TRANSLATION](sites-console.md#translation) 하위 패널에서 `Allow Machine Translation`를 선택하면 기본 번역 서비스가 활성화됩니다.

>[!CAUTION]
>
>기본 번역 서비스는 데모용입니다.
>
>프로덕션 시스템의 경우 라이선스 번역 서비스가 필요합니다. 라이센스가 없는 경우 기본 번역 서비스는 [해제되어 있어야 합니다](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## UGC {#global-translation-of-ugc}의 전역 번역

웹 사이트에 [언어 사본](../../help/sites-administering/tc-prep.md)이 여러 개 있는 경우, 기본 번역 서비스는 UGC가 기본적으로 동일한 구성 요소(구성 요소가 포함된 페이지의 언어 사본)에 의해 생성된 경우처럼 한 사이트에 입력한 UGC가 다른 사이트에 입력된 UGC와 관련이 있을 수 있음을 인식하지 못합니다.

자신이 아닌 그룹에서 무슨 말을 하는지 모르는 주제에 대해 토론하는 집단과 비슷하다. 한 대화에 참여한 큰 그룹의 모든 사람과 비교된다.

&quot;하나의 그룹 대화&quot;가 필요한 경우, 여러 언어 사본이 있는 웹 사이트에서 전역 번역을 활성화할 수 있으므로, 보고 있는 언어 사본에 관계없이 전체 스레드가 표시됩니다.

예를 들어, 기본 사이트에 포럼을 설정하고, 언어 사본을 만들고, 글로벌 번역을 활성화한 경우, 한 언어 사본으로 된 포럼에 게시된 항목이 모든 언어 복사본에 나타납니다. 답글을 입력한 언어 사본과 관계없이 모든 답글에 대해서도 동일하게 적용됩니다. 그 결과, 항목을 보고 있는 언어 사본과 관계없이 주제와 전체 답글 스레드가 표시됩니다.

>[!CAUTION]
>
>글로벌 번역 이전에 존재했던 모든 UGC는 더 이상 표시되지 않습니다.
>
>UGC가 여전히 [공용 스토어](working-with-srp.md)에 있는 동안 언어별 UGC 위치 아래에 있고, 글로벌 번역이 구성된 후 추가된 새 콘텐츠는 글로벌 공유 저장소 위치에서 검색됩니다.
>
>언어 관련 컨텐츠를 글로벌 공유 저장소로 이동하거나 병합하는 마이그레이션 도구가 없습니다.

### 번역 통합 구성 {#translation-integration-configuration}

번역 서비스 커넥터를 작성자 인스턴스의 웹 사이트와 통합하는 새 번역 통합을 만들려면:

* 관리자로 로그인
* [주 메뉴에서](http://localhost:4502/)
* **[!UICONTROL 도구]** 선택
* **[!UICONTROL 작업]** 선택
* **[!UICONTROL Cloud]** 선택
* **[!UICONTROL Cloud Services]** 선택
* 아래로 스크롤하여 **[!UICONTROL 번역 통합]**

   ![번역 통합](assets/translation-integration.png)

* **[!UICONTROL 구성 표시]** 선택

   ![show-configuration](assets/translation-integration1.png)

* **[!UICONTROL 사용 가능한 구성]** 옆에 있는 `[+]` 아이콘을 선택하여 새 구성을 만듭니다

#### 구성 만들기 대화 상자 {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL 상위 구성]**

   (필수) 일반적으로 기본값으로 둡니다. 기본값은 `/etc/cloudservices/translation`입니다.

* **[!UICONTROL 제목]**

   (필수) 선택한 항목의 표시 제목을 입력합니다. 기본값이 없습니다.

* **[!UICONTROL 이름]**

   (선택 사항) 구성 이름을 입력합니다. 기본값은 제목을 기반으로 하는 노드 이름입니다.

* **[!UICONTROL 만들기]**&#x200B;를 선택합니다

#### 번역 구성 대화 상자 {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

자세한 지침은 [번역 통합 구성 만들기](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)를 참조하십시오.

* **** Sitestab:를 기본값으로 둘 수 있습니다.

* **** 커뮤니티 탭:
   * **[!UICONTROL 번역]**
공급자드롭다운 목록에서 번역 공급자를 선택합니다. 기본값은 입니다. 
`microsoft`: 평가판 서비스입니다.

   * **[!UICONTROL 컨텐츠]**
카테고리번역되는 컨텐츠를 설명하는 카테고리를 선택합니다. 기본값은 입니다. 
`General.`

   * **[!UICONTROL 로케일 선택...]**
(선택 사항) UGC를 저장할 로케일을 선택하면 모든 언어 사본의 게시물이 하나의 글로벌 대화에 나타납니다. 규칙에 따라 웹 사이트의 [기본 언어](sites-console.md#translation)에 대한 로케일을 선택합니다. `No Common Store`을 선택하면 전역 번역이 비활성화됩니다. 기본적으로 글로벌 번역은 비활성화됩니다.

* **** 자산 탭:를 기본값으로 둘 수 있습니다.
* **[!UICONTROL 확인]** 선택

#### 활성화 {#activation}

새 번역 통합 클라우드 서비스를 게시 환경에 활성화해야 합니다. 웹 사이트와 연결되어 있을 때 아직 활성화되지 않은 경우 연관된 페이지가 게시될 때 활성화 워크플로우에서 이 클라우드 서비스 구성을 게시하라는 메시지를 표시합니다.

## 번역 설정 관리 {#managing-translation-settings}

>[!NOTE]
>
>**기본 언어**
>
>게시물이 기본 언어와 다른 언어인지 여부를 탐지하기 위해 사이트 방문자의 기본 언어를 설정해야 합니다.
>
>기본 언어는 사이트 방문자가 로그인하고 언어 기본 설정을 지정한 경우 사용자 프로필에 설정된 언어 기본 설정입니다.
>
>사이트 방문자가 익명 상태이거나 프로필에 언어 환경 설정을 지정하지 않은 경우 기본 설정 언어는 페이지 템플릿의 기본 언어입니다.

### 사용자 환경 설정 {#user-preference}

#### 사용자 프로필 {#user-profile}

모든 Communities Sites는 로그인한 구성원이 편집할 수 있는 사용자 프로필을 제공하여 커뮤니티에 자신을 식별하고 해당 커뮤니티의 환경 설정을 지정합니다.

이러한 설정 중 하나는 커뮤니티 콘텐츠를 항상 기본 언어로 표시할지 여부입니다. 기본적으로 이 설정은 설정되지 않으며 기본적으로 시스템 설정으로 설정됩니다. 사용자는 설정을 켜거나 꺼짐으로 변경하여 시스템 설정을 재정의할 수 있습니다.

페이지가 사용자의 기본 언어로 자동으로 번역되는 경우 원래 텍스트를 표시하고 번역 개선을 위한 UI를 계속 사용할 수 있습니다.

![user-profile](assets/translation-integration4.png)

### 커뮤니티 사이트 설정 {#community-site-setting}

커뮤니티 사이트가 만들어지면 번역 옵션을 활성화하고 구성할 수 있습니다. 번역 설정은 콘텐츠 익명 사이트 방문자가 볼 수 있지만 사용자의 프로필 설정에 의해 재정의됩니다.
