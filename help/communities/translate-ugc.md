---
title: 사용자 생성 컨텐츠 번역
seo-title: 사용자 생성 컨텐츠 번역
description: 변환 기능의 작동 방식
seo-description: 변환 기능의 작동 방식
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---


# 사용자 생성 컨텐츠 번역 {#translating-user-generated-content}

AEM Communities의 번역 기능은 SCF( [소셜 구성 요소 프레임워크) 구성 요소를 사용하여 커뮤니티 사이트에 게시된 사용자 생성 컨텐츠](../../help/sites-administering/translation.md) (UGC)로 페이지 컨텐츠를 [변환하는 개념을 확장합니다](scf.md).

UGC의 번역을 통해 사이트 방문자와 회원은 언어 장벽을 제거하여 글로벌 커뮤니티를 경험할 수 있습니다.

예를 들어 다음과 같이 가정합니다.

* 프랑스 출신 한 회원이 다국적 요리 웹사이트에서 프랑스어로 된 요리법을 커뮤니티 포럼에 게시했다.
* 또 다른 일본 멤버는 번역기능을 사용해 프랑스어를 일본어로 번역하기도 한다.
* 일본어로 된 요리법을 읽은 후, 일본의 한 멤버는 일본어로 댓글을 올렸다.
* 이 말을 프랑스어로 번역하는 데 프랑스 출신 A씨.
* 글로벌 커뮤니케이션

## 개요 {#overview}

설명서의 이 섹션에서는 번역 서비스가 UGC와 작동하는 방식에 대해 자세히 설명하며 AEM을 [번역 서비스 제공업체에](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) 연결하고 [번역 통합 프레임워크를 구성하여 해당 서비스를 웹 사이트에 통합하는 방법에 대해 설명합니다](../../help/sites-administering/tc-tic.md).

번역 서비스 공급자가 사이트와 연결되어 있으면 사이트의 각 언어 사본은 주석과 같은 SCF 구성 요소를 통해 게시된 자체 UGC 스레드를 유지합니다.

번역 서비스 제공업체 외에 번역 통합 프레임워크가 구성되면 사이트의 각 언어 복사본에서 UGC의 단일 스레드를 공유할 수 있으므로 언어 사본 간에 글로벌 커뮤니케이션을 제공할 수 있습니다. 언어별로 분리된 토론 스레드 대신 구성된 [전역 공유 저장소를](#global-translation-of-ugc) 사용하면 표시되는 언어 복사와 상관없이 전체 스레드를 볼 수 있습니다. 또한 지역별 등 글로벌 참가자의 논리적 그룹화를 위해 서로 다른 글로벌 공유 스토어를 지정하여 여러 번역 통합 구성을 구성할 수 있습니다.

## 기본 번역 서비스 {#the-default-translation-service}

AEM Communities은 여러 언어로 [기본 번역 서비스를](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) [](../../help/sites-administering/tc-msconf.md) 제공하는 시험버전 라이선스와 함께 제공됩니다.

커뮤니티 사이트 [를](sites-console.md)만들 때 TRANSLATION `Allow Machine Translation` 하위 패널에서 [선택하면 기본 번역 서비스가](sites-console.md#translation) 활성화됩니다.

>[!CAUTION]
>
>기본 번역 서비스는 데모용입니다.
>
>프로덕션 시스템의 경우 라이선스 번역 서비스가 필요합니다. 라이센스가 없는 경우 기본 번역 서비스를 [해제해야 합니다](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## UGC의 전역 번역 {#global-translation-of-ugc}

웹 사이트에 여러 [언어 복사본이](../../help/sites-administering/tc-prep.md)있는 경우, 기본 번역 서비스는 UGC가 같은 구성 요소(구성 요소를 포함하는 페이지의 언어 사본)에 의해 생성된 경우처럼 한 사이트에 입력된 UGC가 다른 사이트에 입력된 UGC와 관련이 있을 수 있다는 것을 인식하지 못합니다.

한 대기업 집단의 모든 사람들이 한 대화에 참여하는 것에 비하면, 이 주제에 대해 토론하는 사람들은 자신이 아닌 다른 그룹으로 만들어진 논평들을 알지 못하는 것과 비슷하다.

&quot;하나의 그룹 대화&quot;를 원하는 경우 여러 언어 복사본이 있는 웹 사이트에서 전체 번역 기능을 활성화할 수 있습니다. 이렇게 하면 표시되는 언어 복사본과 상관없이 전체 스레드가 표시됩니다.

예를 들어 기본 사이트, 언어 사본 작성 및 글로벌 번역 기능이 활성화된 포럼이 설정된 경우 하나의 언어 사본으로 게시된 항목이 모든 언어 사본에 나타납니다. 답글이 입력된 언어 복사본에 상관없이 모든 답글에 대해서도 마찬가지입니다. 그 결과, 주제가 표시되는 언어 복사본에 관계없이 주제와 전체 답글이 표시됩니다.

>[!CAUTION]
>
>전역 번역 이전에 존재했던 UGC는 더 이상 표시되지 않습니다.
>
>UGC는 여전히 [공용 저장소에](working-with-srp.md)있지만, 언어 전용 UGC 위치에 있고 글로벌 번역이 구성된 후 추가된 새 컨텐츠는 글로벌 공유 스토어 위치에서 검색되고 있습니다.
>
>언어별 콘텐츠를 글로벌 공유 스토어로 이동 또는 병합하기 위한 마이그레이션 도구는 없습니다.

### 번역 통합 구성 {#translation-integration-configuration}

번역 서비스 커넥터를 작성 인스턴스의 웹 사이트와 통합하는 새로운 번역 통합을 만들려면 다음을 수행하십시오.

* 관리자로 로그인
* 주 [메뉴에서](http://localhost:4502/)
* 도구 **[!UICONTROL 선택]**
* 작업 **[!UICONTROL 선택]**
* 클라우드 **[!UICONTROL 선택]**
* Cloud Services **[!UICONTROL 선택]**
* 아래로 스크롤하여 **[!UICONTROL 번역 통합]**

   ![번역 통합](assets/translation-integration.png)

* 구성 **[!UICONTROL 표시 선택]**

   ![show-configuration](assets/translation-integration1.png)

* 사용 가능한 구성 옆에 `[+]` 있는 **** 아이콘을 선택하여 새 구성을 만듭니다.

#### 구성 만들기 대화 상자 {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL 상위 구성]**

   (필수) 일반적으로 기본값으로 둡니다. 기본값은 `/etc/cloudservices/translation`입니다.

* **[!UICONTROL 제목]**

   (필수) 선택한 표시 제목을 입력합니다. 기본값이 없습니다.

* **[!UICONTROL 이름]**

   (선택 사항) 구성 이름을 입력합니다. 기본값은 제목을 기반으로 하는 노드 이름입니다.

* **[!UICONTROL 만들기]**&#x200B;를 선택합니다

#### 변환 구성 대화 상자 {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

자세한 지침은 번역 [통합 구성 만들기를 참조하십시오.](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL 사이트]** 탭:기본값으로 둘 수 있습니다.

* **[!UICONTROL 커뮤니티]** 탭:
   * **[!UICONTROL 번역 공급자]**&#x200B;드롭다운 목록에서 번역 공급자를 선택합니다. 기본값은 
`microsoft`로 설정되어 있는지 확인하십시오.

   * **[!UICONTROL 컨텐츠 카테고리]**&#x200B;번역되는 컨텐츠를 설명하는 카테고리를 선택합니다. 기본값은 
`General.`

   * **[!UICONTROL 로케일 선택..]**(선택 사항) UGC를 저장할 로케일을 선택하면 모든 언어 사본의 게시물이 하나의 글로벌 대화로 표시됩니다. 규칙으로 웹 사이트의 [기본 언어](sites-console.md#translation) 로케일을 선택합니다. 선택 `No Common Store` 을 선택하면 글로벌 번역이 비활성화됩니다. 기본적으로 전역 번역은 비활성화됩니다.

* **[!UICONTROL 자산]** 탭:기본값으로 둘 수 있습니다.
* 확인 **[!UICONTROL 선택]**

#### 활성화 {#activation}

게시 환경에 대해 새로운 번역 통합 클라우드 서비스를 활성화해야 합니다. 웹 사이트와 연결된 경우 아직 활성화되지 않으면 연결된 페이지가 게시될 때 활성화 워크플로우에서 이 클라우드 서비스 구성을 게시하라는 메시지가 표시됩니다.

## 번역 설정 관리 {#managing-translation-settings}

>[!NOTE]
>
>**기본 언어**
>
>게시물이 기본 언어와 다른 언어로 되어 있는지 여부를 탐지하기 위해 사이트 방문자의 기본 언어를 설정해야 합니다.
>
>기본 언어는 사이트 방문자가 로그인하고 언어 기본 설정을 지정한 경우 사용자 프로필에 설정된 언어 기본 설정입니다.
>
>사이트 방문자가 익명이거나 프로필에 언어 기본 설정을 지정하지 않은 경우 기본 언어는 페이지 템플릿의 기본 언어입니다.

### 사용자 환경 설정 {#user-preference}

#### 사용자 프로필 {#user-profile}

모든 커뮤니티 사이트에서는 로그인한 구성원이 편집할 수 있는 사용자 프로필을 제공하여 커뮤니티를 식별하고 해당 사이트의 환경 설정을 설정할 수 있습니다.

이러한 설정 중 하나는 기본 언어로 커뮤니티 콘텐츠를 항상 표시할지 여부입니다. 기본적으로 설정은 설정되지 않으며 기본적으로 시스템 설정으로 설정됩니다. 사용자는 설정을 켜거나 꺼짐으로 변경하여 시스템 설정을 재정의할 수 있습니다.

페이지가 사용자가 선호하는 언어로 자동 번역되는 경우에도 원본 텍스트를 표시하고 번역을 향상시키는 UI를 계속 사용할 수 있습니다.

![사용자 프로필](assets/translation-integration4.png)

### 커뮤니티 사이트 설정 {#community-site-setting}

커뮤니티 사이트를 만들 때 번역 옵션을 활성화하고 구성할 수 있습니다. 번역 설정은 익명의 사이트 방문자가 볼 수 있는 컨텐츠에 대해 적용되지만 사용자의 프로필 설정에 의해 무시됩니다.
