---
title: 규칙 세트를 사용하여 URL 변환
description: 'Dynamic Media에서 규칙 세트를 배포하여 URL을 변환할 수 있습니다. 규칙 세트는 XML 데이터를 평가하고 특정 조건을 충족하는 경우 특정 작업을 수행하는 스크립팅 언어(예: JavaScript)로 작성된 지침 세트입니다.'
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: Business Practitioner, Administrator,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: 구성,규칙 세트
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---

# 규칙 세트를 사용하여 URL {#using-rulesets-to-transform-urls} 변환

Dynamic Media에서 규칙 세트를 배포하여 URL을 변환할 수 있습니다. 규칙 세트는 XML 데이터를 평가하고 특정 조건을 충족하는 경우 특정 작업을 수행하는 스크립팅 언어(예: JavaScript)로 작성된 지침 세트입니다. 각 규칙은 하나 이상의 조건과 하나 이상의 작업으로 구성됩니다. 규칙은 조건에 대해 XML 데이터를 평가하고 조건이 충족되면 적절한 작업을 수행합니다. 규칙 세트의 예는 다음과 같습니다.

* MIME 유형 접미사를 추가하는 중입니다. 대부분의 서비스 및 웹 사이트에는 URL에 `.jpg` 추가 등의 이미지 접미사가 필요합니다.
* SEO(검색 엔진 최적화) 목적의 URL에 대한 폴더 경로 만들기

   [Adobe Dynamic Media Classic이 SEO를 지원하는 방법](/help/assets/assets/s7_seo.pdf)을 참조하십시오.

* SEO(검색 엔진 최적화) 목적으로 URL에 메타데이터 추가.

   [Adobe Dynamic Media Classic이 SEO를 지원하는 방법](/help/assets/assets/s7_seo.pdf)을 참조하십시오.

* 다운로드를 트리거하도록 컨텐츠 처리를 설정합니다.
* 개인화를 위해 이미지 제공 템플릿 URL을 단순화합니다. 예를 들어 `rgb{XX,YY,ZZ}`을 RTF 지원 `\redXX\greenYY\blueZZ`으로 전환합니다.

* `$`, `{`, `}` 등과 같이 인코딩할 특정 문자와 ImageServer로 디코딩할 특정 문자를 요청합니다. 예를 들어 Facebook은 특수 문자가 포함된 URL에서 잘 작동하지 않습니다.

   [URL에서 특수 문자 제거](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)를 참조하십시오.

Dynamic Media 컨텍스트에서 XML 기반 시스템을 사용하여 자산 정보를 관리하는 웹 사이트는 XML 파일을 Dynamic Media에 업로드할 수 있습니다. 이러한 파일 중 하나를 Dynamic Media 자산을 제공할 사전 처리 규칙 세트 파일로 지정할 수 있습니다. 이 파일은 Dynamic Media과 통합되는 시스템의 비즈니스 로직을 충족하도록 표준 URL 프로토콜 형식을 재구성합니다. 규칙 세트 정의 파일 경로로 사용할 XML 파일을 지정합니다.

>[!CAUTION]
>
>규칙 세트를 사용할 때는 주의하십시오.웹 사이트에 Dynamic Media 컨텐츠가 표시되지 않도록 할 수 있습니다.

고유한 규칙 세트를 만드는 데 도움이 되는 샘플 규칙 세트를 사용할 수 있습니다.
[규칙 세트 참조](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html)를 참조하십시오.

모든 규칙 세트 생성과 마찬가지로 xmlvalid와 같은 XML 유효성 검사기 프로그램을 사용하여 업로드하기 전에 XML 파일이 유효한지 확인하십시오.
[문제 해결 규칙 세트](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)도 참조하십시오.

또한 라이브 프로덕션 환경에 영향을 주지 않는 스테이징 환경에서 규칙 세트를 먼저 테스트해야 합니다.
프로덕션 환경 및 스테이징 환경에서는 일반적으로 다른 로그인이 필요합니다.

로그인 정보](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app)에 대해서는 [Adobe Dynamic Media Classic 데스크탑 응용 프로그램을 참조하십시오.

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

규칙 세트](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)에서 &#39;is&#39; 이미지 대신 &#39;asset&#39;를 사용하기를 참조하십시오.[

**XML 규칙 세트를 배포하려면**

1. [Dynamic Media Classic 데스크탑 응용 프로그램에 로그인](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   자격 증명 및 로그인 세부 정보는 프로비저닝 시 Adobe이 제공했습니다. 이 정보가 없는 경우 기술 지원 센터에 문의하십시오.

1. 다음을 수행하여 규칙 세트 파일을 업로드합니다.

   * 전역 탐색 모음에서 **[!UICONTROL 업로드]**&#x200B;를 클릭합니다.
   * 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 업로드]** 페이지에서 **[!UICONTROL 찾아보기]**&#x200B;를 클릭합니다.
   * **[!UICONTROL 열기]** 대화 상자에서 규칙 세트 파일(XML)로 이동합니다.
   * 파일을 선택한 다음 **[!UICONTROL 열기]**&#x200B;를 클릭합니다.
   * **[!UICONTROL 업로드]** 페이지의 오른쪽에서 규칙 세트 파일의 대상 폴더를 선택합니다.
   * 페이지 하단 근처에 있는 **[!UICONTROL 업로드 후 게시]**&#x200B;가 선택되어 있는지 확인합니다.
   * 페이지의 오른쪽 아래 모서리에서 **[!UICONTROL 업로드 제출]**&#x200B;을 클릭합니다.
   * 전역 탐색 막대에서 **[!UICONTROL 작업]**&#x200B;을 클릭하여 업로드 작업의 상태를 확인합니다. **[!UICONTROL 작업]** 페이지의 **[!UICONTROL 상태]** 열에 업로드 완료 가 표시되면 다음 단계를 계속 진행합니다.

1. 페이지 상단 근처에 있는 탐색 모음에서 **[!UICONTROL 설정 > Application Setup > Publish Setup > Image Server]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 이미지 서버 게시]** 페이지의 **[!UICONTROL 카탈로그 관리]** 그룹에서 **[!UICONTROL 규칙 세트 정의 파일 경로]**&#x200B;를 찾은 다음 **[!UICONTROL 선택]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 규칙 세트 정의 파일(XML) 선택]** 페이지에서 규칙 세트 파일로 이동한 다음 페이지의 오른쪽 아래에서 **[!UICONTROL 선택]**&#x200B;을 클릭합니다.
1. 설정 페이지의 오른쪽 아래 모서리에서 **[!UICONTROL 닫기]**&#x200B;를 클릭합니다.
1. 이미지 서버 게시 작업을 실행합니다.

   규칙 세트 조건은 라이브 Dynamic Media 이미지 서버에 대한 요청에 적용됩니다.

   규칙 세트 파일을 변경하면 다시 업로드하고 업데이트된 규칙 세트 파일을 다시 게시할 때 변경 사항이 즉시 적용됩니다.
