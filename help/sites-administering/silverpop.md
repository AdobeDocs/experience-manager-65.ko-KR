---
title: Silverpop Engage와 통합
seo-title: Integrating with Silverpop Engage
description: AEM을 Silverpop Engage와 통합하는 방법을 알아봅니다
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# Silverpop Engage와 통합{#integrating-with-silverpop-engage}

>[!NOTE]
>
>Silverpop 통합은 **not** 즉시 사용 가능합니다. 를 다운로드해야 합니다. [Silverpop 통합 패키지](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) 패키지 공유에서 인스턴스에 설치합니다. 패키지를 설치한 후 이 문서에 설명된 대로 구성할 수 있습니다.

AEM과 Silverpop Engage를 통합하면 Silverpop을 통해 AEM에서 만든 이메일을 관리하고 보낼 수 있습니다. 또한 AEM 페이지에서 AEM Forms를 통해 Silverpop의 리드 관리 기능을 사용할 수 있습니다.

통합은 다음과 같은 기능을 제공합니다.

* AEM에서 이메일을 만들고 배포용으로 Silverpop에 게시하는 기능.
* Silverpop 가입자를 만들기 위해 AEM 양식의 작업을 설정하는 기능.

Silverpop Engage가 구성된 후 Silverpop Engage에 뉴스레터 또는 이메일을 게시할 수 있습니다.

## Silverpop 구성 만들기 {#creating-a-silverpop-configuration}

를 통해 Silverpop 구성을 추가할 수 있습니다 **Cloudservices**, **도구**, 또는 **API 종료 지점**. 모든 방법은 이 섹션에 설명되어 있습니다.

### Cloudservices를 통해 Silverpop 구성 {#configuring-silverpop-via-cloudservices}

Cloud Services에서 Silverpop 구성을 만들려면 다음을 수행하십시오.

1. AEM에서 을 탭하거나 클릭합니다 **도구** > **배포** > **Cloud Services**. (또는 `https://<hostname>:<port>/etc/cloudservices.html`)
1. 타사 서비스에서 **Silverop Engage** 그리고 **구성**. Silverpop 구성 창이 열립니다.

   >[!NOTE]
   >
   >패키지 공유에서 패키지를 다운로드하지 않는 한 타사 서비스에서는 Silverpop Engage를 옵션으로 사용할 수 없습니다.

1. 제목과 원하는 이름을 입력하고 **만들기**. ** Silverpop 설정** 구성 창이 열립니다.
1. 사용자 이름, 암호를 입력하고 드롭다운 목록에서 API 엔드포인트를 선택합니다.
1. 클릭 **Silverpop에 연결합니다.** 연결되면 성공 대화 상자가 표시됩니다. 클릭 **확인** 을 눌러 창을 종료합니다. 을 클릭하여 Silverpop으로 이동할 수 있습니다 **Silverpop Engage로 이동**.
1. Silverpop이 구성되었습니다. 을 클릭하여 구성을 편집할 수 있습니다 **편집**.
1. 또한 제목과 이름을 제공하여 개인화된 작업에 대해 Silverpop Engage 프레임워크를 구성할 수 있습니다(선택 사항). 만들기 를 클릭하면 이미 구성된 Silverpop 연결에 대한 프레임워크가 성공적으로 만들어집니다.

   가져온 데이터 확장 열은 나중에 AEM 구성 요소를 통해 사용할 수 있습니다. **텍스트 및 개인화**.

### 도구를 통해 Silverpop 구성 {#configuring-silverpop-via-tools}

도구에서 Silverpop 구성을 만들려면:

1. AEM에서 을 탭하거나 클릭합니다 **도구** > **배포** > **Cloud Services**. 또는 다음 위치로 이동하여 직접 탐색합니다. `https://<hostname>:<port>/misadmin#/etc`.
1. 선택 **도구**, 그런 다음 **Cloud Services 구성,** 그런 다음 **Silverpop Engage**.
1. **새로 만들기**&#x200B;를 클릭하여 **페이지 만들기** 창을 엽니다.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 을(를) 입력합니다. **제목** 원할 경우 **이름**&#x200B;를 클릭하고 **만들기**.
1. 이전 절차의 4단계에서 설명한 대로 구성 정보를 입력합니다. 해당 절차에 따라 Silverpop 구성을 완료합니다.

### 여러 구성 추가 {#adding-multiple-configurations}

여러 구성을 추가하려면 다음을 수행합니다.

1. 시작 페이지에서 **Cloud Services** 을(를) 클릭합니다. **Silverpop Engage**. 클릭 **구성 표시** 하나 이상의 Silverpop 구성을 사용할 수 있는 경우 표시되는 단추입니다. 사용 가능한 모든 구성이 나열됩니다.
1. 을(를) 클릭합니다. **+** 사용 가능한 구성 옆에 서명합니다. 이렇게 하면 **구성 만들기** 창을 엽니다. 이전 구성 절차에 따라 새 구성을 만듭니다.

### Silverpop에 연결하기 위한 API 종료 지점 구성 {#configuring-api-end-points-for-connecting-to-silverpop}

현재 AEM에는 6개의 비보안 종료 포인트가 있습니다(참여 1~6). 이제 Silverpop은 기존 끝점과 연결 끝점이 변경된 두 개의 새 끝점을 제공합니다.

API 종료 지점을 구성하려면:

1. 이동 `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` on `https://<hostname>:<port>/crxde.`
1. 마우스 오른쪽 단추를 클릭하고 을 선택합니다 **만들기**, 그런 다음 **노드 만들기**.
1. 을(를) 입력합니다. **이름** 로서의 `sp-e0` 및 **유형** 로서의 `cq:Widget`.
1. 새로 추가된 노드에 다음 두 속성을 추가합니다.

   1. **이름**: `text`, **유형**: `String`, **값**: `Engage 0`
   1. **이름**: `value`, **유형**: `String`, **값**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   모두 저장 단추를 클릭합니다.

1. 노드 하나 더 만들기 **이름** 로서의 `sp-e7` 및 **유형** 로서의 `cq:Widget`.

   새로 추가된 노드에 다음 두 속성을 추가합니다.

   1. **이름**: `text`, **유형**: `String`, **값**: `Pilot`
   1. **이름**: `value`, **유형**: `String`, **값**: `https://apipilot.silverpop.com/XMLAPI`

1. 기존 API 종료 지점을 변경하려면(참여 1~6) 각각 하나씩 클릭하고 다음과 같이 값을 바꾸십시오.

   | **노드 이름** | **기존 끝점 값** | **새 끝점 값** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. 클릭 **모두 저장**. 이제 AEM에서 보안 끝점 위에 Silverpop에 연결할 준비가 되었습니다.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
