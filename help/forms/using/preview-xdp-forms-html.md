---
title: XDP 양식의 HTML5 미리 보기 생성
description: HTML 디자이너의 미리 보기 LiveCycle 탭을 사용하여 브라우저에 나타나는 양식을 미리 볼 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: HTML5 Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# XDP 양식의 HTML5 미리 보기 생성{#generate-html-preview-of-an-xdp-form}

AEM Forms Designer에서 양식을 디자인하는 동안 양식의 PDF 렌디션을 미리 보는 것 외에도 해당 양식의 HTML5 렌디션을 미리 볼 수도 있습니다. 다음을 사용할 수 있습니다. **미리 보기 HTML** 탭에서 양식을 미리 볼 수 있습니다.

## 디자이너에서 XDP 양식에 대한 HTML 미리 보기 활성화 {#html-preview-of-forms-in-forms-designer}

디자이너가 XDP 양식의 HTML 미리 보기를 생성할 수 있도록 하려면 다음 구성을 수행하십시오.

* Apache Sling 인증 서비스 구성
* 보호 모드 비활성화
* AEM Forms 서버에 대한 세부 정보 제공

### Apache Sling 인증 서비스 구성 {#configure-apache-sling-authentication-service}

1. 다음으로 이동 `https://'[server]:[port]'/system/console/configMgr` OSGi에서 실행 중인 AEM Forms 또는
   `https://'[server]:[port]'/lc/system/console/configMgr` jee에서 실행 중인 AEM Forms에서.
1. 를 찾아 클릭합니다. **Apache Sling 인증 서비스** 구성 : 편집 모드에서 엽니다.

1. OSGi에서 AEM Forms을 실행하는지 또는 JEE에서 실행하는지에 따라 **인증 요구 사항** 필드:

   * JEE의 AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs

   * OSGi의 AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >값의 특수 문자가 손상될 수 있으므로 인증 요구 사항 필드에 지정된 값을 복사하여 붙여넣지 마십시오. 대신 필드에 지정된 값을 입력합니다.

1. 에서 사용자 이름 및 암호 지정 **[!UICONTROL 익명 사용자 이름]** 및 **[!UICONTROL 익명 사용자 암호]** 각각 필드입니다. 지정된 자격 증명은 익명 인증을 처리하고 익명 사용자에 대한 액세스를 허용하는 데 사용됩니다.
1. 클릭 **저장** 구성을 저장합니다.

### 보호 모드 비활성화 {#disable-protected-mode}

다음 [보호 모드](../../forms/using/get-xdp-pdf-documents-aem.md) 은(는) 기본적으로 설정되어 있습니다. 프로덕션 환경에 대해 활성화 상태를 유지합니다. 개발 환경에서 비활성화하여 desinger에서 HTML5 Forms을 미리 볼 수 있습니다. 비활성화하려면 다음 단계를 수행하십시오.

1. 관리자로 AEM 웹 콘솔에 로그인합니다.

   * OSGi의 AEM Forms URL `https://'[server]:[port]'/system/console/configMgr`
   * JEE의 AEM Forms URL은 `https://'[server]:[port]'/lc/system/console/configMgr`

1. 열기 **[!UICONTROL 모바일 Forms 구성]** 편집할 수 있습니다.
1. 선택 취소 **[!UICONTROL 보호 모드]** 옵션 및 클릭 **[!UICONTROL 저장]**.

### AEM Forms 서버에 대한 세부 정보 제공 {#provide-details-of-aem-forms-server}

1. 디자이너에서 **도구** > **옵션**.
1. 옵션 창에서 다음을 선택합니다. **서버 옵션** 페이지를 열고 다음 세부 정보를 입력한 다음 **확인**.

   * **서버 URL**: AEM Forms 서버 URL.

   * **HTTP 포트 번호**: AEM 서버 포트. 기본값은 4502입니다.
   * **HTML 미리 보기 컨텍스트:** XFA 양식을 렌더링하기 위한 프로필의 경로입니다. 다음 기본 프로필은 Designer에서 양식을 미리 보는 데 사용됩니다. 하지만 사용자 지정 프로필의 경로를 지정할 수도 있습니다.

      * `/content/xfaforms/profiles/default.html` (OSGi의 AEM Forms)

      * `/lc/content/xfaforms/profiles/default.html` (JEE의 AEM Forms)

   * **Forms Manager 컨텍스트:** Forms Manager UI가 배포되는 컨텍스트 경로. 기본값은 다음과 같습니다.

      * `/aem/forms` (OSGi의 AEM Forms)
      * `/lc/forms` (JEE의 AEM Forms)

   >[!NOTE]
   >
   >AEM Forms 서버가 실행 중인지 확인합니다. HTML 미리보기는 CRX 서버에 연결하여에 *생성* 미리보기.

   ![AEM Forms Designer 옵션 ](assets/server_options.png)

   AEM Forms Designer 옵션

1. HTML에서 양식을 미리 보려면 **미리 보기 HTML** 탭.

   >[!NOTE]
   >
   >
   >
   >
   >    * HTML 미리 보기 탭이 닫혀 있으면 F4 키를 눌러 미리 보기 HTML 탭을 엽니다. 보기 메뉴에서 HTML 미리보기 를 선택하여 HTML 미리보기 탭을 열 수도 있습니다.
   >    * HTML 미리 보기는 PDF 문서를 지원하지 않습니다. HTML 미리 보기는 XDP 문서에 대해서만 수행됩니다.
   >
   >

   >[!CAUTION]
   >
   >실제 최종 사용자 경험을 테스트하려면 외부 브라우저(Google Chrome, Microsoft Edge, Mozilla Firefox 등)에서도 양식을 미리 봅니다. 모든 브라우저는 별도의 엔진을 사용하여 HTML을 렌더링하므로 디자이너 및 외부 브라우저에서 양식 미리 보기 방식에 약간의 차이가 있을 수 있습니다.

## 샘플 데이터를 사용하여 양식 미리 보기 {#to-preview-a-form-using-sample-data}

디자이너를 사용하면 샘플 XML 데이터를 사용하여 양식을 미리 보고 테스트할 수 있습니다. 샘플 데이터로 양식을 자주 테스트하여 양식이 올바르게 렌더링되는지 확인하는 것이 좋습니다.

샘플 데이터가 없는 경우 디자이너가 만들거나 직접 만들 수 있습니다. (참조: [양식을 미리 볼 샘플 데이터를 자동으로 생성하려면 다음을 수행합니다](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) 및 [샘플 데이터를 만들어 양식 미리 보기](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

샘플 데이터 소스를 사용하여 양식을 테스트하면 데이터와 필드가 매핑되고 반복되는 하위 양식이 예상대로 반복됩니다. 병합된 데이터를 표시할 각 개체에 적절한 공간을 제공하는 균형 잡힌 양식 레이아웃을 만들 수 있습니다.

1. 선택 **파일 > 양식 속성**.

1. 다음을 클릭합니다. **미리 보기** 을 탭하고 데이터 파일 상자에 테스트 데이터 파일의 전체 경로를 입력합니다. 찾아보기 단추를 사용하여 파일을 탐색할 수도 있습니다.

1. 클릭 **확인**. 다음번에 다음에서 양식을 미리 볼 때 **미리 보기 HTML** 탭에서는 샘플 XML 파일의 데이터 값이 각 객체에 나타납니다.

## 저장소에서 양식 미리 보기 {#html-preview-of-forms-in-forms-manager}

AEM Forms에서는 저장소의 양식 및 문서를 미리 볼 수 있습니다. 미리 보기를 통해 양식의 모양과 동작을 최종 사용자가 정확하게 파악할 수 있습니다.
