---
title: Adobe I/O를 사용한 Adobe Target과 통합
seo-title: Adobe I/O를 사용한 Adobe Target과 통합
description: Adobe I/O를 사용하여 AEM과 Adobe Target 통합에 대한 자세한 내용
seo-description: Adobe I/O를 사용하여 AEM과 Adobe Target 통합에 대한 자세한 내용
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: f476091236018c826ae303b4b0fc32c691318f79

---


# Adobe I/O를 사용한 Adobe Target과 통합{#integration-with-adobe-target-using-adobe-i-o}

Target Standard API를 통해 AEM과 Adobe Target을 통합하려면 Adobe IMS(Identity Management System) 및 Adobe I/O 구성이 필요합니다.

>[!NOTE]
>
>Adobe Target Standard API에 대한 지원은 AEM 6.5에 새롭게 추가되었습니다.Target Standard API는 IMS 인증을 사용합니다.
>
>이전 버전과의 호환성을 위해 AEM에서 Adobe Target Classic API를 계속 사용할 수 있습니다. Target [Classic API는 사용자 자격 증명 인증을](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)사용합니다.
>
>API 선택은 AEM/Target 통합에 사용되는 인증 방법에 의해 결정됩니다.

## 전제 조건 {#prerequisites}

이 절차를 시작하기 전에 Adobe [지원](https://helpx.adobe.com/contact/enterprise-support.ec.html) 팀에서 다음 항목에 대한 계정을 프로비저닝해야 합니다.

* Adobe Console
* Adobe I/O
* Adobe Target 및
* Adobe IMS(Identity Management System)

## IMS 구성 구성 - 공개 키 생성 {#configuring-an-ims-configuration-generating-a-public-key}

구성의 첫 번째 단계는 AEM에서 IMS 구성을 만들고 공개 키를 생성하는 것입니다.

1. AEM에서 도구 **메뉴를 엽니다** .
1. 보안 **섹션에서** Adobe IMS **구성을 선택합니다**.
1. 만들기를 **선택하여** Adobe IMS 기술 **계정 구성을 엽니다**.
1. 클라우드 구성 아래의 드롭다운을 **사용하여** Adobe Target을 **선택합니다**.
1. 활성화 **새 인증서를** 만들고 새 별칭을 입력합니다.
1. 인증서 **만들기로**&#x200B;확인합니다.

   ![](assets/integrate-target-io-01.png)

1. AEM **과** Adobe Target **과의 통합을 위해 Adobe I/O를**&#x200B;구성할 때 사용할 수 있도록 파일을 로컬 드라이브에 다운로드하려면 [다운로드 [(또는 공개 키 다운로드](#configuring-adobe-i-o-for-adobe-target-integration-with-aem))를 선택합니다.

   >[!CAUTION]
   >
   >이 구성을 열어 두십시오. AEM에서 IMS [구성을 완료할 때 다시 필요합니다](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## AEM과 Adobe Target 통합을 위한 Adobe I/O 구성 {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

AEM 파섹

### 통합 만들기 {#creating-the-integration}

Adobe I/O 콘솔을 열어 AEM에서 사용할 Adobe Target과 I/O 통합을 만듭니다.

>[!NOTE]
>
>Adobe I/ [O 자습서를](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)참조하십시오.

1. 통합을 위해 Adobe I/O 콘솔을 엽니다.

   * [https://console.adobe.io/integrations](https://console.adobe.io/integrations)

1. 새 **통합을**&#x200B;선택합니다.

   >[!NOTE]
   >
   >기존 통합이 이미 있는 경우 이러한 통합이 나열되고 새 **통합** 단추가 오른쪽 위에 표시됩니다.

   ![](assets/integrate-target-io-03.png)

1. API **액세스** 후 계속을 **선택합니다**.

   ![](assets/integrate-target-io-04.png)

1. Adobe **Target**, **계속**:

   ![](assets/integrate-target-io-05.png)

1. 통합 구성에 필요한 세부 정보를 추가합니다.

   * **이름**

      이름을 입력합니다.

   * **설명**

      설명은 선택 사항입니다.

   * **공개 키 인증서**

      공개 키 파일 업로드;IMS 구성 [- 공개 키 생성에서 생성되었습니다](#configuring-an-ims-configuration-generating-a-public-key).

      인증서를 로드하면 인증서 아래에 **나열됩니다**.

   * **제품 프로필**

      제품 프로필은 AEM에서 컨텐츠 내보내기 및 오퍼 제작에 사용할 수 있는 Target의 작업 영역과 같습니다. 기본적으로 타겟 기본 작업 영역이 선택됩니다. AEM에서 내보내기 대상으로 노출되어야 하는 다른 프로필/작업 영역을 선택합니다.
   예:

   ![](assets/integrate-target-io-06.png)

1. 통합을 **만들어**&#x200B;확인합니다.
1. 작성이 확인되고 이제 통합 세부 **사항을**&#x200B;계속 진행할 수 있습니다.AEM에서 IMS [구성을 완료하는 데 필요합니다](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)

### 통합에 권한 할당 {#assigning-privileges-to-the-integration}

이제 필요한 권한을 통합에 할당해야 합니다.

1. Adobe Admin **Console을 엽니다**.

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 제품( **위쪽** 도구 모음) **으로 이동한 다음&#x200B;*Adobe Target - &lt;*your-tenant-id** >(왼쪽 패널)을 선택합니다.
1. 제품 **프로필을**&#x200B;선택한 다음 목록에 있는 필수 작업 영역을 선택합니다. 예: 기본 작업 영역.
1. 통합을 **선택한**&#x200B;다음 필요한 통합 구성을 선택합니다.
1. 편집기를 **제품** 역할로 **선택**;옵저버 대신 **사용하십시오**.

## Adobe I/O 통합을 위해 저장된 세부 사항 {#details-stored-for-the-adobe-i-o-integration}

Adobe I/O 통합 콘솔에서 모든 통합 목록을 볼 수 있습니다.

* [https://console.adobe.io/integrations](https://console.adobe.io/integrations)

특정 **통합** 항목의 오른쪽에 있는 보기를 선택하여 구성에 대한 세부 정보를 표시합니다. 이러한 쿠키에는 다음이 포함됩니다.

* 개요
* 인사이트
* 서비스
* 이벤트
* JWT(JSON 웹 토큰)

이러한 기능 중 일부는 AEM에서 Target용 Adobe I/O 통합을 완료해야 합니다.

1. **개요**:

   ![](assets/integrate-target-io-08.png)

1. **JWT**:

   ![](assets/integrate-target-io-09.png)

## AEM에서 IMS 구성 완료 {#completing-the-ims-configuration-in-aem}

AEM으로 돌아가면 Target용 Adobe I/O 통합에서 필요한 값을 추가하여 IMS 구성을 완료할 수 있습니다.

1. AEM에서 [열린 IMS 구성으로 돌아갑니다](#configuring-an-ims-configuration-generating-a-public-key).
1. **다음**&#x200B;을 선택합니다.

1. 여기에서 Adobe I/O의 [세부 정보를 사용할 수 있습니다](#details-stored-for-the-adobe-i-o-integration).

   * **제목**:텍스트.
   * **인증 서버**:아래의 페이로드 섹션 `"aud"` 행에서 복사/ **붙여넣기** (예: `"https://ims-na1.adobelogin.com"` 아래 예)
   * **API 키**:Target용 [Adobe I](#details-stored-for-the-adobe-i-o-integration) /O 통합의 개요 섹션에서 이 파일을 복사합니다
   * **클라이언트 암호**:Target용 [Adobe](#details-stored-for-the-adobe-i-o-integration) I/O 통합의 개요 섹션에서 이 파일을 생성하고
   * **페이로드**:Target용 [Adobe I](#details-stored-for-the-adobe-i-o-integration) /O 통합의 JWT 섹션에서 복사합니다.
   ![](assets/integrate-target-io-10.png)

1. 만들기로 **확인합니다**.

1. Adobe Target 구성이 AEM 콘솔에 표시됩니다.

   ![](assets/integrate-target-io-11.png)

## IMS 구성 확인 {#confirming-the-ims-configuration}

구성이 예상대로 작동하는지 확인하려면:

1. 열기:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`
   예:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 구성을 선택합니다.
1. 도구 **모음에서 상태** 확인을 선택한 후 확인을 **선택합니다**.

   ![](assets/integrate-target-io-12.png)

1. 성공하면 다음과 같은 메시지가 표시됩니다.

   ![](assets/integrate-target-io-13.png)

## Adobe Target Cloud 서비스 구성 {#configuring-the-adobe-target-cloud-service}

이제 클라우드 서비스가 Target Standard API를 사용하도록 구성을 참조할 수 있습니다.

1. 도구 **메뉴를 엽니다** . 그런 다음 클라우드 서비스 **섹션에서** 레거시 클라우드 **서비스를 선택합니다**.
1. 아래로 스크롤하여 **Adobe Target** 으로 이동하고 지금 **구성을 선택합니다**.

   The **Create Configuration** dialog will open.

1. 제목을 **입력하고** 원하는 경우 **이름을** 입력합니다(비워 두면 제목에서 생성됩니다).

   필요한 템플릿을 선택할 수도 있습니다(하나 이상의 템플릿을 사용할 수 있는 경우).

1. 만들기로 **확인합니다**.

   구성 **요소** 편집 대화 상자가 열립니다.

1. Adobe Target 설정 **탭에 세부 사항을** 입력합니다.

   * **클라이언트 코드**:adobe IMS 테넌트 ID

      >[!CAUTION]
      >
      >Adobe IMS 임차인 ID는 클라이언트 코드라는 필드에 입력해야 합니다.

   * **인증**:IMS.
   * **IMS 구성**:ims 구성의 이름을 선택합니다.
   * **API 유형**:REST
   * **A4T Analytics 클라우드 구성**:타겟 활동 목표 및 지표에 사용되는 Analytics 클라우드 구성을 선택합니다. 컨텐츠를 타깃팅할 때 Adobe Analytics를 보고 소스로 사용하는 경우 이 옵션이 필요합니다. 클라우드 구성이 표시되지 않으면 A4T Analytics 클라우드 [구성 구성을 참조하십시오](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
   * **정확한 타깃팅**&#x200B;사용:기본적으로 이 확인란이 선택되어 있습니다. 이 옵션을 선택하면 클라우드 서비스 구성이 컨텍스트를 로드한 후 콘텐츠를 로드합니다. 참고:
   * **Adobe Target에서 세그먼트 동기화**:AEM에서 사용할 Target에 정의된 세그먼트를 다운로드하려면 이 옵션을 선택합니다. 인라인 세그먼트는 지원되지 않으며 항상 Target의 세그먼트를 사용해야 하기 때문에 API 유형 속성이 REST인 경우 이 옵션을 선택해야 합니다. (&#39;segment&#39;의 AEM 용어는 Target &#39;audience&#39;와 같습니다.)
   * **클라이언트 라이브러리**:AT.js 클라이언트 라이브러리 또는 mbox.js(더 이상 사용되지 않음)를 원하는지 선택합니다.
   * **태그 관리 시스템을 사용하여 클라이언트 라이브러리를**&#x200B;제공합니다.DTM(더 이상 사용되지 않음), Adobe Launch 또는 기타 태그 관리 시스템을 사용합니다.
   * **사용자 지정 AT.js**:태그 관리 상자를 선택하거나 기본 AT.js를 사용하려면 비워 둡니다. 또는 사용자 지정 AT.js를 업로드합니다. AT.js를 선택한 경우에만 나타납니다.
   >[!NOTE]
   >
   >[Target Classic API를 사용하기 위한 클라우드 서비스의](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) 구성은 더 이상 사용되지 않습니다(Adobe Recommendations 설정 탭 사용).

   예:

   ![](assets/integrate-target-io-14.png)

1. Target **에 연결을** 클릭하여 Adobe Target과의 연결을 초기화합니다.

   연결이 성공하면 [연결 성공] **이라는 메시지가** 표시됩니다.

1. 메시지에서 **확인을** 선택한 다음 **대화** 상자에서 확인을선택하여 구성을 확인합니다.
1. 이제 타겟 프레임워크 추가를 [진행하여](/help/sites-administering/target-configuring.md#adding-a-target-framework) Target으로 전송할 ContextHub 또는 ClientContext 매개 변수를 구성할 수 있습니다. AEM 경험 조각을 Target으로 내보내는 데 필요하지 않을 수 있습니다.

