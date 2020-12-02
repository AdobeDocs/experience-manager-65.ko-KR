---
title: 이메일 서비스 공급자에 이메일 게시
seo-title: 이메일 서비스 공급자에 이메일 게시
description: ExactTarget 및 Silverpop Engage와 같은 이메일 서비스에 뉴스레터를 게시할 수 있습니다.
seo-description: ExactTarget 및 Silverpop Engage와 같은 이메일 서비스에 뉴스레터를 게시할 수 있습니다.
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 75%

---


# 이메일 서비스 공급자에 이메일 게시{#publishing-an-email-to-email-service-providers}

ExactTarget 및 Silverpop Engage와 같은 이메일 서비스에 뉴스레터를 게시할 수 있습니다. 이 문서에서는 이러한 이메일 서비스에 뉴스레터를 게시하기 위해 AEM을 구성하는 방법에 대해 설명합니다.

>[!NOTE]
>
>이메일을 작성하고 게시하려면 먼저 서비스 공급자를 구성해야 합니다. 자세한 내용은 [Configuring ExactTarget](/help/sites-administering/exacttarget.md) 및 [Silverpop Engage 구성](/help/sites-administering/silverpop.md)을 참조하십시오.

이메일 서비스 공급자에게 이메일을 게시하려면 다음 절차를 수행해야 합니다.

1. 이메일을 작성합니다.
1. 이메일에 이메일 서비스 구성을 적용합니다.
1. 이메일을 게시합니다.

>[!NOTE]
>
>뉴스레터를 게시 인스턴스에 먼저 게시하지 않았거나 게시 인스턴스를 사용할 수 없는 경우에 이메일 공급자를 업데이트하거나, 플라이트 테스트를 수행하거나, 뉴스레터를 전송하는 경우 이러한 작업이 실패합니다. 뉴스레터를 게시하고 게시 인스턴스가 작동되어 실행 중인지 확인하십시오.

## 이메일 만들기 {#creating-an-email}

이메일 서비스에 게시하려는 이메일 또는 뉴스레터는 **Geometrixx 뉴스레터** 템플릿을 사용하여 캠페인 아래에 만들 수 있습니다. **Geometrixx Outdoors 이메일** 템플릿을 사용할 수도 있습니다. **Geometrixx Outdoors 이메일** 템플릿을 기반으로 하는 샘플 이메일/뉴스레터는 `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`에서 사용할 수 있습니다.

구성된 이메일 서비스에 게시된 새 이메일을 만들려면:

1. **웹 사이트**&#x200B;로 이동한 다음 **캠페인**&#x200B;으로 이동합니다. 캠페인 선택.
1. **새로 만들기**&#x200B;를 클릭하여 **페이지 만들기** 창을 엽니다.
1. 제목과 이름을 입력하고 사용 가능한 템플릿 목록에서 **Geometrixx 뉴스레터** 템플릿을 선택합니다.
1. **만들기**&#x200B;를 클릭합니다.
1. 만든 이메일을 엽니다.
1. 디자인 모드로 전환하여 사이드킥에 표시할 구성 요소를 선택합니다.
1. 편집 모드로 전환한 후 컨텐츠(텍스트, 이미지, [이메일 도구](#adding-exacttarget-email-tools-to-your-email), [개인화 변수](#adding-text-and-personalization-tool-to-your-e-mail) 등)를 이메일에 추가하기 시작합니다.

### 이메일에 ExactTarget 이메일 도구 추가 {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>이 섹션은 ExactTarget 서비스용입니다.

ExactTarget에 대한 **이메일 도구** 구성 요소를 이용하여 이메일/뉴스레터에 이메일 기능을 더 추가할 수 있습니다.

1. ExactTarget에 게시할 이메일을 엽니다.
1. 사이드 킥을 사용하여 페이지에 구성 요소 **ET - 이메일 도구**&#x200B;를 추가합니다. 구성 요소를 편집 모드에서 엽니다.

   ![chlimage_1](assets/chlimage_1.gif)

1. **옵션** 메뉴에서 옵션을 선택합니다.

<table>
 <tbody>
  <tr>
   <td>실제 우편 주소(필수)</td>
   <td>이 구성 요소는 조직의 실제 우편 주소를 이메일에 삽입합니다.</td>
  </tr>
  <tr>
   <td>프로필 센터(필수)</td>
   <td>이 프로필 센터는 사용자가 보유하고 있는 개인 정보를 가입자가 입력하고 유지 관리할 수 있는 웹 페이지입니다.</td>
  </tr>
  <tr>
   <td>이메일을 웹 페이지로 보기</td>
   <td>이 구성 요소를 사용하면 이메일을 웹 페이지로 볼 수 있습니다..</td>
  </tr>
  <tr>
   <td>개인정보 보호정책</td>
   <td>이 구성 요소는 이메일에 개인정보 보호 정책에 대한 링크를 삽입합니다.<br /> </td>
  </tr>
  <tr>
   <td>가입 해지 센터</td>
   <td>메일링 목록에서 가입을 취소하는 옵션을 제공합니다..</td>
  </tr>
  <tr>
   <td>가입 센터</td>
   <td>가입 센터는 조직에서 받는 메시지를 가입자가 제어할 수 있는 웹 페이지입니다.</td>
  </tr>
  <tr>
   <td>이메일 열기 횟수 추적</td>
   <td>ExactTarget 추적 기능을 사용할 수 있도록 해주는 숨겨진 구성 요소입니다.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**옵션** 드롭다운 메뉴는 ExactTarget 구성이 이메일에 적용되는 경우에만 채워집니다. 자세한 내용은 [이메일 설정에 이메일 서비스 구성 적용](#applying-e-mail-service-configuration-to-e-mail-settings)을 참조하십시오.

1. ExactTarget에 이메일을 게시합니다.

   이메일 도구가 있는 이메일은 구성된 ExactTarget 계정에서 사용할 수 있습니다.

>[!NOTE]
>
>* 전자 메일 도구 내의 URL은 **단순 전송** 또는 **안내 전송**&#x200B;을 사용하여 전자 메일을 보낼 때만 실제 값으로 대체되며 **테스트 전송**&#x200B;은 사용할 수 없습니다.
   >
   >
* 두 가지 이메일 도구, **실제 우편 주소(필수)**&#x200B;와 **프로필 센터(필수)**&#x200B;는 필수입니다. 이메일이 ExactTarget에 게시되면 이러한 두 개의 이메일 도구가 기본적으로 모든 메일 하단에 추가됩니다.

>



### 이메일에 텍스트 및 개인화 도구 추가  {#adding-text-and-personalization-tool-to-your-e-mail}

페이지에 **텍스트 및 개인화** 구성 요소를 추가하여 이메일에서 개인화된 필드를 추가할 수 있습니다.

1. 이메일 서비스에 게시할 이메일을 엽니다.
1. 이메일 서비스에서 개인화 필드를 사용할 수 있도록 설정하려면 이메일 서비스를 구성하는 동안 프레임워크 구성을 추가하십시오. 자세한 내용은 [Silverpop Engage](/help/sites-administering/silverpop.md) 및 [Exact Target](/help/sites-administering/exacttarget.md) 구성을 참조하십시오.
1. 사이드 킥에서 구성 요소 **텍스트 및 개인화**&#x200B;를 추가합니다. 이 구성 요소는 뉴스레터 그룹의 일부입니다. 이 구성 요소를 편집 모드에서 여십시오.

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 드롭다운 메뉴에서 필드를 선택하고 **삽입**&#x200B;을 클릭하여 필요한 개인화된 필드를 텍스트에 추가합니다.
1. **확인**&#x200B;을 클릭하여 마칩니다.

## 이메일 설정에 이메일 서비스 구성 적용 {#applying-e-mail-service-configuration-to-e-mail-settings}

뉴스레터에 이메일 서비스 구성을 적용하려면 다음을 수행하십시오.

1. 이메일 서비스 구성을 만듭니다.
1. 이메일/뉴스레터를 엽니다.
1. **설정**&#x200B;을 클릭하거나 사이드 킥에서 **페이지 속성을 클릭하여 이메일/뉴스레터 설정을 엽니다.**
1. **클라우드 서비스** 탭에서 **서비스 추가**&#x200B;를 클릭합니다. 서비스 목록이 표시됩니다. 목록에서 필요한 구성(**ExactTarget** 또는 **Silverpop**)을 선택하십시오.

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. **확인**&#x200B;을 클릭합니다.

## 이메일 서비스에 이메일 게시 {#publishing-emails-to-email-service}

다음 절차에 따라 이메일/뉴스레터를 이메일 서비스에 게시할 수 있습니다.

1. 이메일을 엽니다.
1. 이메일을 게시하기 전에 이메일에 올바른 구성을 적용했는지 확인하십시오.
1. **게시**&#x200B;를 클릭합니다. **이메일 서비스 공급자에 뉴스레터 게시** 창이 열립니다.
1. **뉴스레터 이름** 필드에 이름을 입력합니다. 이메일/뉴스레터가 이 이름으로 이메일 서비스 공급자에 게시됩니다. 이메일 이름을 제공하지 않으면 AEM의 뉴스레터 페이지 이름을 사용하여 이메일이 게시됩니다.
1. **게시**&#x200B;를 클릭합니다. 

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   성공적으로 작업이 수행되면 AEM은 ExactTarget이나 Silverpop Engage에서 해당 이메일을 볼 수 있다는 것을 확인합니다.

   ExactTarget의 경우 게시된 이메일은 **게시된 이메일 보기**&#x200B;를 클릭하여 볼 수 있습니다. 이렇게 하면 ExactTarget([https://members.exacttarget.com/](https://members.exacttarget.com/))에 게시된 뉴스레터가 바로 표시됩니다.

>[!NOTE]
>
>이메일/뉴스레터가 이미 게시된 이메일/뉴스레터와 같은 이름으로 게시되더라도 이전 이메일/뉴스레터가 교체되지는 않습니다. 대신 새 이메일/뉴스레터가 같은 이름으로 만들어집니다(그렇지만 두 뉴스레터의 ID는 다름).
>
>이메일/뉴스레터를 이메일 서비스 공급자에게 게시해도 이메일/뉴스레터가 AEM 게시 인스턴스에 게시됩니다.


### 게시된 이메일 업데이트 {#updating-a-published-e-mail}

게시 대화 상자의 **업데이트** 단추를 사용하면 이미 이메일 서비스 공급자에 게시된 뉴스레터를 업데이트할 수 있습니다. 뉴스레터가 아직 게시되지 않았고 **업데이트** 단추를 클릭한 경우에는 **뉴스레터가 게시되지 않음** 메시지가 표시됩니다.

게시된 이메일을 업데이트하려면:

1. 이전에 이메일 서비스 공급자에게 게시했었는데 변경하여 다시 게시할 이메일/뉴스레터를 열어 변경합니다.
1. **게시**&#x200B;를 클릭합니다. **이메일 서비스 공급자에 뉴스레터 게시** 창이 표시됩니다. **업데이트**&#x200B;를 클릭합니다.

   이메일/뉴스레터가 ExactTarget에서 업데이트되었는지 확인하려면 **게시된 이메일 보기**&#x200B;를 클릭합니다. 게시된 이메일이 ExactTarget에 표시됩니다.

   이메일/뉴스레터가 Silverpop 이메일 서비스에서 업데이트되었는지 확인하려면 Silverpop Engage 사이트를 방문해 보십시오.

