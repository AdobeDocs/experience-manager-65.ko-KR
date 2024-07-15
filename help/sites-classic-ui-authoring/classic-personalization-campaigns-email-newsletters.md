---
title: 이메일 서비스 공급자에 이메일 게시
description: ExactTarget 및 Silverpop Engage와 같은 이메일 서비스에 뉴스레터를 게시할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 3%

---

# 이메일 서비스 공급자에 이메일 게시{#publishing-an-email-to-email-service-providers}

ExactTarget 및 Silverpop Engage와 같은 이메일 서비스에 뉴스레터를 게시할 수 있습니다. 이 문서에서는 이러한 이메일 서비스에 뉴스레터를 게시하도록 AEM을 구성하는 방법에 대해 설명합니다.

>[!NOTE]
>
>이메일을 만들고 게시하려면 먼저 서비스 공급자를 구성해야 합니다. 자세한 내용은 [ExactTarget 구성](/help/sites-administering/exacttarget.md) 및 [Silverpop Engage 구성](/help/sites-administering/silverpop.md)을 참조하십시오.

이메일을 이메일 서비스 공급자에 게시하려면 다음 단계를 수행해야 합니다.

1. 이메일을 만듭니다.
1. 이메일에 이메일 서비스 구성을 적용합니다.
1. 이메일을 Publish 합니다.

>[!NOTE]
>
>이메일 공급자를 업데이트하거나 플라이트 테스트를 수행하거나 뉴스레터를 전송하는 경우 뉴스레터가 먼저 Publish 인스턴스에 게시되지 않았거나 Publish 인스턴스를 사용할 수 없는 경우 이러한 작업이 실패합니다. 뉴스레터를 게시하고 Publish 인스턴스가 실행 중인지 확인하십시오.

## 이메일 만들기 {#creating-an-email}

전자 메일 서비스에 게시할 전자 메일 또는 뉴스레터는 **Geometrixx 뉴스레터** 템플릿을 사용하는 캠페인에서 만들 수 있습니다. **Geometrixx Outdoors 전자 메일** 템플릿을 사용할 수도 있습니다. **Geometrixx Outdoors 이메일** 템플릿을 기반으로 하는 샘플 이메일/뉴스레터는 `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`에서 사용할 수 있습니다.

구성된 이메일 서비스에 게시되는 이메일을 만들려면 다음 작업을 수행하십시오.

1. **웹 사이트**(으)로 이동한 다음 **캠페인**(으)로 이동합니다. 캠페인을 선택합니다.
1. **새로 만들기**&#x200B;를 클릭하여 **페이지 만들기** 창을 엽니다.
1. 제목, 이름을 입력하고 사용 가능한 템플릿 목록에서 **Geometrixx 뉴스레터** 템플릿을 선택합니다.
1. **만들기**&#x200B;를 클릭합니다.
1. 생성된 이메일을 엽니다.
1. 디자인 모드로 전환하여 사이드 킥에 표시할 구성 요소를 선택합니다.
1. 편집 모드로 전환하고 전자 메일에 콘텐츠(텍스트, 이미지, [전자 메일 도구](#adding-exacttarget-email-tools-to-your-email), [개인화 변수](#adding-text-and-personalization-tool-to-your-e-mail) 등)를 추가하기 시작합니다.

### 이메일에 ExactTarget 이메일 도구 추가 {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>이 섹션은 ExactTarget 서비스에만 해당됩니다.

ExactTarget용 **이메일 도구** 구성 요소는 이메일/뉴스레터에 더 많은 이메일 기능을 추가할 수 있습니다.

1. ExactTarget에 게시할 이메일을 엽니다.
1. 사이드 킥을 사용하여 구성 요소 **ET - 이메일 도구**&#x200B;를 페이지에 추가합니다. 편집 모드에서 구성 요소를 엽니다.

   ![chlimage_1](assets/chlimage_1.gif)

1. **옵션** 메뉴에서 옵션을 선택하십시오.

<table>
 <tbody>
  <tr>
   <td>실제 우편 주소(필수)</td>
   <td>이 구성 요소는 이메일에 조직의 실제 우편 주소를 삽입합니다.</td>
  </tr>
  <tr>
   <td>프로필 센터(필수)</td>
   <td>프로필센터는 구독자가 본인에 대해 보유하고 있는 개인정보를 입력하고 유지할 수 있는 웹페이지다.</td>
  </tr>
  <tr>
   <td>이메일을 웹 페이지로 보기</td>
   <td>사용자는 이 구성 요소를 통해 이메일을 웹 페이지로 볼 수 있습니다.</td>
  </tr>
  <tr>
   <td>개인정보 처리방침</td>
   <td>이 구성 요소는 전자 메일에 개인정보 처리방침에 대한 링크를 삽입합니다.<br /> </td>
  </tr>
  <tr>
   <td>가입 해제 센터</td>
   <td>사용자에게 메일링 목록에서 구독을 취소할 수 있는 옵션을 제공합니다.</td>
  </tr>
  <tr>
   <td>가입 센터</td>
   <td>구독 센터는 구독자가 조직에서 받는 메시지를 제어할 수 있는 웹 페이지입니다.</td>
  </tr>
  <tr>
   <td>이메일 열기 횟수 추적</td>
   <td>ExactTarget 추적 기능을 사용할 수 있는 숨겨진 구성 요소입니다.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**옵션** 드롭다운 메뉴는 ExactTarget 구성이 전자 메일에 적용된 경우에만 채워집니다. 자세한 내용은 [전자 메일 설정에 전자 메일 서비스 구성 적용](#applying-e-mail-service-configuration-to-e-mail-settings)을 참조하십시오.

1. ExactTarget으로 이메일을 Publish 합니다.

   이메일 도구가 포함된 이메일은 구성된 ExactTarget 계정에서 사용할 수 있습니다.

>[!NOTE]
>
>* 전자 메일 도구 내의 URL은 **단순 보내기** 또는 **안내 보내기**&#x200B;를 사용하여 전자 메일을 보냈지만 **테스트 보내기**&#x200B;를 사용할 수 없는 경우에만 받은 전자 메일의 실제 값으로 바뀝니다.
>
>* 전자 메일 도구 중 두 개가 필요합니다. **실제 메일 주소(필수)** 및 **프로필 센터(필수)**. 이메일이 ExactTarget에 게시되면 기본적으로 이 두 개의 이메일 도구가 모든 메일의 맨 아래에 추가됩니다.
>

### 이메일에 텍스트 및 Personalization 도구 추가 {#adding-text-and-personalization-tool-to-your-e-mail}

**텍스트 및 Personalization** 구성 요소를 페이지에 추가하여 전자 메일에 개인화된 필드를 추가할 수 있습니다.

1. 전자 메일 서비스에 게시할 전자 메일을 엽니다.
1. 이메일 서비스의 개인화 필드를 활성화하려면 이메일 서비스를 구성하는 동안 프레임워크 구성을 추가하십시오. 자세한 내용은 [Silverpop Engage 구성](/help/sites-administering/silverpop.md) 및 [정확한 타겟 구성](/help/sites-administering/exacttarget.md)을 참조하십시오.
1. 사이드 킥에서 구성 요소 **Text &amp; Personalization**&#x200B;을(를) 추가합니다. 이 구성 요소는 뉴스레터 그룹에 속합니다. 편집 모드에서 이 구성 요소를 엽니다.

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 드롭다운 메뉴에서 필드를 선택하고 **삽입**&#x200B;을(를) 클릭하여 개인화된 필수 필드를 텍스트에 추가하십시오.
1. **확인**&#x200B;을 클릭하여 완료하십시오.

## 이메일 설정에 이메일 서비스 구성 적용 {#applying-e-mail-service-configuration-to-e-mail-settings}

뉴스레터에 이메일 서비스 구성을 적용하려면:

1. 전자 메일 서비스 구성을 만듭니다.
1. 이메일/뉴스레터를 엽니다.
1. **설정**&#x200B;을 클릭하거나 사이드 킥에서 **페이지 속성**&#x200B;을 클릭하여 전자 메일/뉴스레터 설정을 엽니다.
1. **Cloud Service** 탭에서 **서비스 추가**&#x200B;를 클릭합니다. 서비스 목록이 표시됩니다. 드롭다운 목록에서 필요한 구성(**ExactTarget** 또는 **Silverpop**)을 선택하십시오.

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. **확인**&#x200B;을 클릭합니다.

## 이메일 서비스에 이메일 게시 {#publishing-emails-to-email-service}

다음 단계를 수행하여 이메일/뉴스레터를 이메일 서비스에 게시할 수 있습니다.

1. 이메일을 엽니다.
1. 이메일을 게시하기 전에 이메일에 올바른 구성을 적용했는지 확인하십시오.
1. **게시**&#x200B;를 클릭합니다. **전자 메일 서비스 공급자에 대한 Publish 뉴스레터** 창이 열립니다.
1. **뉴스레터 이름** 필드에 내용을 입력하십시오. 이메일/뉴스레터는 이 이름으로 이메일 서비스 공급자에 게시됩니다. 이메일 이름이 제공되지 않는 경우 이메일은 AEM에 있는 뉴스레터의 페이지 이름을 사용하여 게시됩니다.
1. **게시**&#x200B;를 클릭합니다.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   성공하면 AEM에서 ExactTarget 또는 Silverpop Engage에서 이메일을 볼 수 있음을 확인합니다.

   ExactTarget이 있는 경우 **게시된 전자 메일 보기**&#x200B;를 클릭하여 게시된 전자 메일을 볼 수 있습니다. 이렇게 하면 ExactTarget([https://members.exacttarget.com/](https://members.exacttarget.com/))에 게시된 뉴스레터로 바로 이동합니다.

>[!NOTE]
>
>이메일/뉴스레터가 이미 게시된 이메일/뉴스레터와 동일한 이름으로 게시된 경우, 이전 이메일/뉴스레터는 교체되지 않습니다. 대신 동일한 이름으로 새 이메일/뉴스레터가 만들어집니다(하지만 두 뉴스레터의 ID는 다름).
>
>이메일/뉴스레터를 이메일 서비스 공급자에 게시하면 이메일/뉴스레터도 AEM 게시 인스턴스에 게시됩니다.
>

### 게시된 이메일 업데이트 {#updating-a-published-e-mail}

Publish 대화 상자의 **업데이트** 단추를 사용하면 전자 메일 서비스 공급자에 이미 게시된 뉴스레터를 업데이트할 수 있습니다. 뉴스레터가 아직 게시되지 않았으며 **업데이트** 단추를 클릭하면 **뉴스레터가 게시되지 않음** 메시지가 표시됩니다.

게시된 이메일을 업데이트하려면:

1. 이메일/뉴스레터를 변경한 후 다시 게시하려는 이메일 서비스 공급자에게 이전에 게시된 이메일/뉴스레터를 엽니다.
1. **게시**&#x200B;를 클릭합니다. **Publish Newsletter to Email Service Provider** 창이 표시됩니다. **업데이트**&#x200B;를 클릭합니다.

   ExactTarget에 이메일/뉴스레터가 업데이트되었는지 확인하려면 **게시된 이메일 보기**&#x200B;를 클릭하세요. 이렇게 하면 ExactTarget에 게시된 이메일로 이동합니다.

   Silverpop 이메일 서비스에 대한 이메일/뉴스레터의 업데이트 여부를 확인하려면 Silverpop Engage 사이트를 방문하십시오.
