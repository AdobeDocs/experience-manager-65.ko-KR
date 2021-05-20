---
title: XDP 양식의 HTML5 미리 보기 생성
seo-title: XDP 양식의 HTML5 미리 보기 생성
description: LiveCycle 디자이너의 미리 보기 HTML 탭을 사용하여 브라우저에서 나타나는 양식을 미리 볼 수 있습니다.
seo-description: LiveCycle 디자이너의 미리 보기 HTML 탭을 사용하여 브라우저에서 나타나는 양식을 미리 볼 수 있습니다.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
feature: Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# XDP 양식의 HTML5 미리 보기 생성{#generate-html-preview-of-an-xdp-form}

AEM Forms Designer에서 양식을 디자인하는 동안 양식의 PDF 렌디션을 미리 보는 것 외에도 양식의 HTML5 렌디션을 미리 볼 수도 있습니다. **HTML** 미리 보기 탭을 사용하여 브라우저에 표시되는 대로 양식을 미리 볼 수 있습니다.

## 디자이너에서 XDP 양식에 대한 HTML 미리 보기 활성화 {#html-preview-of-forms-in-forms-designer}

디자이너가 XDP 양식의 HTML 미리 보기를 생성할 수 있도록 하려면 다음 구성을 수행하십시오.

* Apache Sling 인증 서비스 구성
* 보호 모드 비활성화
* AEM Forms 서버에 대한 세부 정보 제공

### Apache Sling 인증 서비스 {#configure-apache-sling-authentication-service} 구성

1. OSGi 또는`https://'[server]:[port]'/system/console/configMgr`
   `https://'[server]:[port]'/lc/system/console/configMgr` JEE에서 실행 중인 AEM Forms에서.
1. **Apache Sling 인증 서비스** 구성을 찾아 클릭하여 편집 모드에서 엽니다.

1. OSGi 또는 JEE에서 AEM Forms을 실행 중인지 여부에 따라 **인증 요구 사항** 필드에 다음을 추가하십시오.

   * JEE의 AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs
   * OSGi의 AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >지정한 값을 Authentication Requirements 필드에 복사하여 붙여넣으면 값의 특수 문자가 손상될 수 있습니다. 대신 필드에 지정된 값을 입력합니다.

1. **[!UICONTROL 익명 사용자 이름]** 및 **[!UICONTROL 익명 사용자 암호]** 필드에 각각 사용자 이름과 암호를 지정하십시오. 지정한 자격 증명은 익명 인증을 처리하고 익명 사용자에 대한 액세스를 허용하는 데 사용됩니다.
1. **저장**&#x200B;을 클릭하여 구성을 저장합니다.

### 보호 모드 {#disable-protected-mode} 사용 안 함

[보호 모드](../../forms/using/get-xdp-pdf-documents-aem.md)가 기본적으로 켜져 있습니다. 프로덕션 환경에 대해 사용하도록 설정합니다. 개발 환경에서 비활성화하여 Designer에서 HTML5 Forms을 미리 볼 수 있습니다. 비활성화하려면 다음 단계를 수행하십시오.

1. 관리자로 AEM 웹 콘솔에 로그인합니다.

   * OSGi에서 AEM Forms의 URL은 `https://'[server]:[port]'/system/console/configMgr`입니다.
   * JEE의 AEM Forms용 URL은 `https://'[server]:[port]'/lc/system/console/configMgr`입니다.

1. 편집할 **[!UICONTROL 모바일 Forms 구성]**&#x200B;을 엽니다.
1. **[!UICONTROL 보호 모드]** 옵션을 선택 취소하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

### AEM Forms 서버 {#provide-details-of-aem-forms-server}에 대한 세부 정보를 제공합니다.

1. 디자이너에서 **도구** > **옵션**&#x200B;으로 이동합니다.
1. 옵션 창에서 **서버 옵션** 페이지를 선택하고 다음 세부 정보를 제공한 다음 **확인**&#x200B;을 클릭합니다.

   * **서버 URL**:AEM Forms 서버 URL입니다.

   * **HTTP 포트 번호**:AEM 서버 포트입니다. 기본값은 4502입니다.
   * **HTML 미리 보기 컨텍스트:** XFA 양식을 렌더링하기 위한 프로필의 경로입니다. 디자이너의 양식을 미리 보는 데 사용되는 기본 프로필은 다음과 같습니다. 그러나 사용자 지정 프로필에 대한 경로를 지정할 수도 있습니다.

      * `/content/xfaforms/profiles/default.html` (OSGi의 AEM Forms)

      * `/lc/content/xfaforms/profiles/default.html` (JEE의 AEM Forms)
   * **Forms Manager 컨텍스트:**  Forms Manager UI가 배포되는 컨텍스트 경로입니다. 기본값은 다음과 같습니다.

      * `/aem/forms` (OSGi의 AEM Forms)
      * `/lc/forms` (JEE의 AEM Forms)

   >[!NOTE]
   >
   >AEM Forms 서버가 작동 중인지 확인합니다. HTML 미리 보기는 CRX 서버에 연결하여 *생성* 미리 보기에 연결합니다.

   ![AEM Forms 디자이너 옵션  ](assets/server_options.png)

   AEM Forms 디자이너 옵션

1. HTML로 양식을 미리 보려면 **HTML 미리 보기** 탭을 클릭하십시오.

   >[!NOTE]
   >
   >
   >
   >
   >    * HTML 미리 보기 탭이 닫혀 있는 경우 F4 키를 눌러 HTML 미리 보기 탭을 엽니다. 보기 메뉴에서 HTML 미리 보기 를 선택하여 HTML 미리 보기 탭을 열 수도 있습니다.
   >    * HTML 미리 보기는 PDF 문서를 지원하지 않으며 HTML 미리 보기는 XDP 문서에만 해당됩니다.


   >[!CAUTION]
   >
   >실제 최종 사용자 경험을 테스트하려면 외부 브라우저(Google Chrome, Microsoft Edge, Mozilla Firefox 등)에서도 양식을 미리 봅니다. 모든 브라우저는 별도의 엔진을 사용하여 HTML을 렌더링하므로 디자이너와 외부 브라우저에서 양식을 미리 보는 방식에 몇 가지 차이가 있을 수 있습니다.

## 샘플 데이터를 사용하여 양식을 미리 보려면 {#to-preview-a-form-using-sample-data}

디자이너를 사용하면 샘플 XML 데이터를 사용하여 양식을 미리 보고 테스트할 수 있습니다. 양식이 올바르게 렌더링되도록 하려면 샘플 데이터로 양식을 자주 테스트하는 것이 좋습니다.

샘플 데이터가 없는 경우 Designer에서 만들거나 직접 만들 수 있습니다. (](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) 및 [양식을 미리 보기 위해 샘플 데이터를 자동으로 생성하려면 [양식](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2)을(를) 참조하십시오.)

샘플 데이터 소스를 사용하여 양식을 테스트하면 데이터 및 필드가 매핑되고 반복 하위 양식이 예상대로 반복됩니다. 병합된 데이터를 표시할 각 개체에 적절한 공간을 제공하는 균형 잡힌 양식 레이아웃을 만들 수 있습니다.

1. **파일 > 양식 속성**&#x200B;을 선택합니다.

1. **미리 보기** 탭을 클릭하고 데이터 파일 상자에서 테스트 데이터 파일의 전체 경로를 입력합니다. 찾아보기 단추를 사용하여 파일로 이동할 수도 있습니다.

1. **확인**&#x200B;을 클릭합니다. 다음에 **미리 보기 HTML** 탭에서 양식을 미리 볼 때 샘플 XML 파일의 데이터 값이 각 개체에 나타납니다.

## 저장소에 있는 양식 미리 보기 {#html-preview-of-forms-in-forms-manager}

AEM Forms에서 리포지토리에서 양식과 문서를 미리 볼 수 있습니다. 미리 보기는 최종 사용자가 사용할 양식의 모양과 동작 방식을 정확하게 파악하는 데 도움이 됩니다.
