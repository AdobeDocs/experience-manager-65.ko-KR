---
title: 사용자 생성 콘텐츠 번역
description: UGC 콘텐츠 번역을 통해 사이트 방문자와 구성원이 언어 장벽을 제거하여 글로벌 커뮤니티를 경험하는 방법에 대해 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# 사용자 생성 콘텐츠 번역 {#translating-user-generated-content}

Adobe Experience Manager(AEM) 커뮤니티의 번역 기능은 [페이지 콘텐츠 번역](../../help/sites-administering/translation.md) 개념을 [SCF(소셜 구성 요소 프레임워크) 구성 요소](scf.md)를 사용하여 커뮤니티 사이트에 게시된 사용자 생성 콘텐츠(UGC)로 확장합니다.

UGC의 번역을 통해 사이트 방문자와 구성원은 언어 장벽을 제거하여 글로벌 커뮤니티를 경험할 수 있습니다.

예를 들어 다음과 같이 가정합니다.

* 한 프랑스 회원이 다국적 요리 웹사이트의 커뮤니티 포럼에 프랑스어로 된 레시피를 올리고 있다.
* 일본의 다른 회원은 번역 기능을 사용하여 프랑스어에서 일본어로 레시피 번역을 트리거합니다.
* 일본어로 조리법을 읽은 후, 일본에서 온 회원이 일본어로 댓글을 달았다.
* 프랑스인 회원은 번역 기능을 사용하여 일본어 주석을 프랑스어로 번역합니다.
* 글로벌 커뮤니케이션.

## 개요 {#overview}

이 섹션에서는 특히 UGC에서 번역 서비스가 작동하는 방식에 대해 설명합니다. 또한 사용자가 AEM을 [번역 서비스 공급자](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider)에 연결하고 [번역 통합 프레임워크](../../help/sites-administering/tc-tic.md)를 구성하여 해당 서비스를 웹 사이트에 통합하는 방법을 이해하고 있다고 가정합니다.

번역 서비스 제공업체가 사이트와 연결되면 사이트의 각 언어 사본은 댓글과 같은 SCF 구성 요소를 통해 게시된 UGC의 자체 스레드를 유지합니다.

번역 서비스 공급업체 외에 번역 통합이 구성된 경우 사이트의 각 언어 사본이 UGC의 단일 스레드를 공유할 수 있으므로 언어 사본 전반에 걸쳐 글로벌 커뮤니케이션을 제공합니다. 언어로 분리된 토론 스레드 대신 구성된 [글로벌 공유 저장소](#global-translation-of-ugc)를 사용하면 보고 있는 언어 사본에 관계없이 전체 스레드를 볼 수 있습니다. 또한, 복수의 번역 통합 구성은 영역별과 같은 글로벌 참여자의 논리적 그룹화에 대해 상이한 글로벌 공유 스토어를 지정하도록 구성될 수 있다.

## 기본 번역 서비스 {#the-default-translation-service}

AEM Communities에는 여러 언어에 사용할 수 있는 [기본 번역 서비스](../../help/sites-administering/tc-msconf.md)에 대한 [평가판 라이선스](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license)가 포함되어 있습니다.

[커뮤니티 사이트를 만들](sites-console.md) 때 [번역](sites-console.md#translation) 하위 패널에서 `Allow Machine Translation`을(를) 선택하면 기본 번역 서비스가 활성화됩니다.

>[!CAUTION]
>
>기본 번역 서비스는 데모용입니다.
>
>프로덕션 시스템의 경우 라이선스가 있는 번역 서비스가 필요합니다. 라이선스를 받지 않은 경우 기본 번역 서비스는 [꺼짐](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors)이어야 합니다.

## UGC의 글로벌 번역 {#global-translation-of-ugc}

웹 사이트에 [언어 사본](../../help/sites-administering/tc-prep.md)이 여러 개 있는 경우 기본 번역 서비스는 한 사이트에 입력된 UGC가 다른 사이트에 입력된 UGC와 관련이 있을 수 있음을 인식하지 못합니다. 이는 UGC가 동일한 구성 요소(구성 요소가 포함된 페이지의 언어 사본)에 의해 생성될 때 마찬가지입니다.

그것은 한 주제에 대해 토론하는 사람들의 그룹과 비슷하다. 이들은 한 대화에 참여하는 대규모 집단의 모든 사람에 비해 자신의 글이 아닌 다른 집단에서 이루어지는 댓글에 대해 인지하지 못한다.

&quot;하나의 그룹 대화&quot;를 원하는 경우, 여러 언어 사본이 있는 웹 사이트 간에 전역 번역을 활성화하여 조회 중인 언어 사본에 관계없이 전체 스레드를 볼 수 있습니다.

예를 들어 기본 사이트에 포럼을 설정하고 언어 사본을 만들며 글로벌 번역을 활성화한 경우, 하나의 언어 사본으로 만든 포럼에 게시된 주제가 모든 언어 사본에 나타납니다. 답변이 입력된 언어 사본에 관계없이 모든 답글에 대해서도 마찬가지입니다. 그 결과 주제가 표시되는 언어 사본에 관계없이 주제와 전체 회신 스레드가 표시됩니다.

>[!CAUTION]
>
>전역 번역 전에 있었던 모든 UGC는 더 이상 표시되지 않습니다.
>
>UGC가 [일반 저장소](working-with-srp.md)에 있는 동안 언어별 UGC 위치 아래에 있으며 전역 번역을 구성한 후 추가된 새 콘텐츠는 전역 공유 저장소 위치에서 검색됩니다.
>
>언어별 콘텐츠를 글로벌 공유 스토어로 이동하거나 병합하는 마이그레이션 도구는 없습니다.

### 번역 통합 구성 {#translation-integration-configuration}

번역 서비스 커넥터를 작성자 인스턴스의 웹 사이트와 통합하는 번역 통합을 만들려면 다음 작업을 수행하십시오.

* 관리자로 로그인
* [기본 메뉴](http://localhost:4502/)에서
* **[!UICONTROL 도구]** 선택
* **[!UICONTROL 작업]** 선택
* **[!UICONTROL 클라우드]** 선택
* **[!UICONTROL Cloud Service]** 선택
* 아래로 스크롤하여 **[!UICONTROL 번역 통합]**

  ![번역 통합](assets/translation-integration.png)

* **[!UICONTROL 구성 표시]** 선택

  ![show-configuration](assets/translation-integration1.png)

* 구성을 만들 수 있도록 **[!UICONTROL 사용 가능한 구성]** 옆에 있는 `[+]` 아이콘을 선택하십시오.

#### 구성 만들기 대화 상자 {#create-configuration-dialog}

![구성 만들기](assets/translation-integration2.png)

* **[!UICONTROL 상위 구성]**

  (필수) 일반적으로 기본값으로 둡니다. 기본값은 `/etc/cloudservices/translation`입니다.

* **[!UICONTROL 제목]**

  (필수) 선택한 표시 제목을 입력합니다. 기본값이 없습니다.

* **[!UICONTROL 이름]**

  (선택 사항) 구성 이름을 입력합니다. 기본값은 제목 을 기반으로 하는 노드 이름입니다.

* **[!UICONTROL 만들기]** 선택

#### 번역 구성 대화 상자 {#translation-config-dialog}

![구성-대화 상자](assets/translation-integration3.png)

자세한 지침은 [번역 통합 구성 만들기](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)를 참조하십시오.

* **[!UICONTROL 사이트]** 탭: 기본값으로 둘 수 있습니다.

* **[!UICONTROL 커뮤니티]** 탭:
   * **[!UICONTROL 번역 공급자]**
드롭다운 목록에서 번역 공급업체를 선택합니다. 기본값은 평가판 서비스인 `microsoft`입니다.

   * **[!UICONTROL 콘텐츠 범주]**
번역할 콘텐츠를 설명하는 범주를 선택합니다. 기본값은 `General.`입니다.

   * **[!UICONTROL 로케일 선택...]**
(선택 사항) UGC를 저장할 로케일을 선택하면 모든 언어 사본의 게시물이 하나의 글로벌 대화에 표시됩니다. 규칙에 따라 웹 사이트의 [기본 언어](sites-console.md#translation)에 대한 로케일을 선택하십시오. `No Common Store`을(를) 선택하면 전역 변환이 비활성화됩니다. 기본적으로 글로벌 번역은 비활성화되어 있습니다.

* **[!UICONTROL Assets]** 탭: 기본값으로 둘 수 있습니다.
* **[!UICONTROL 확인]** 선택

#### 활성화 {#activation}

새로운 번역 통합 클라우드 서비스를 Publish 환경에서 활성화해야 합니다. 웹 사이트와 연결된 경우 아직 활성화되지 않은 경우 연결된 페이지가 게시되면 활성화 워크플로우는 이 클라우드 서비스 구성을 게시하라는 메시지를 표시합니다.

## 번역 설정 관리 {#managing-translation-settings}

>[!NOTE]
>
>**기본 언어**
>
>게시물이 기본 언어와 다른 언어로 되어 있는지 감지할 때 사이트 방문자의 기본 언어가 설정되어 있어야 합니다.
>
>기본 언어는 사이트 방문자가 로그인하고 언어 기본 설정을 지정한 경우 사용자 프로필에 설정된 언어 기본 설정입니다.
>
>사이트 방문자가 익명이거나 프로필에 언어 기본 설정을 지정하지 않은 경우 기본 언어는 페이지 템플릿의 기본 언어입니다.

### 사용자 환경 설정 {#user-preference}

#### 사용자 프로필 {#user-profile}

모든 커뮤니티 사이트는 로그인한 구성원이 커뮤니티에 대해 자신을 식별하고 환경 설정을 지정하기 위해 편집할 수 있는 사용자 프로필을 제공합니다.

이러한 설정 중 하나는 커뮤니티 콘텐츠를 항상 기본 언어로 표시할지 여부입니다. 기본적으로 이 설정은 설정되어 있지 않으며 기본적으로 시스템 설정으로 지정됩니다. 사용자는 설정을 On 또는 Off로 변경하여 시스템 설정을 재정의할 수 있습니다.

페이지가 사용자의 기본 언어로 자동 번역되면 원본 텍스트를 표시하고 번역을 개선하기 위한 UI를 계속 사용할 수 있습니다.

![사용자 프로필](assets/translation-integration4.png)

### 커뮤니티 사이트 설정 {#community-site-setting}

커뮤니티 사이트를 만들 때 번역 옵션을 활성화하고 구성할 수 있습니다. 번역 설정은 익명의 사이트 방문자가 볼 수 있는 콘텐츠에 적용되지만 사용자의 프로필 설정에 의해 재정의됩니다.
