---
title: '[!DNL Experience Manager] 6.5 서비스 팩 릴리스 노트'
description: ' [!DNL Adobe Experience Manager] 6.5 서비스 팩 9에 관한 릴리스 노트'
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 68928e251203f67faef498dc22f6d57ea141e748
workflow-type: tm+mt
source-wordcount: '3389'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트  {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.9.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2021년 5월 27일 |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.9.0에 포함된 사항 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.9.0에는 2019년 4월 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. 서비스 팩이 [!DNL Adobe Experience Manager] 6.5에 설치됩니다.

[!DNL Adobe Experience Manager] 6.5.9.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* 이제 AEM Sites Dynamic Media Foundation 구성 요소에서 응답형 이미지 사전 설정 또는 스마트 자르기를 사용할 때 고해상도 장치에 대한 최적화를 켜거나 끌 수 있습니다.

* 성능을 향상시키기 위해 hidden=false 조건이 JCR 쿼리에서 QueryBuilder 평가기로 이동됩니다. 변경 후 숨겨진 설명이 작동하는지 확인하기 위해 Adobe Experience Manager에서는 숨겨진 폴더가 인터페이스에 표시되지 않는지 확인합니다.

* [!DNL Experience Manager Sites] 페이지에서 삭제된 페이지 및 트리를 복원하는 기능.

* 메일 시스템 구성 서비스에 대한 새로 고침 토큰을 사용하여 액세스 토큰을 새로 고침하도록 새 사용자가 지원합니다.

* 메일 시스템 구성 서비스에 대한 SMTP XOAUTH2 메커니즘을 지원합니다.

* 홍콩, 마카오 및 대만과 관련된 이름 발생 횟수는 중국 로케일 및 지역에 대한 새 이름 지정 규칙에 따라 업데이트됩니다.

* [!DNL Experience Manager] [Assets](#assets-accessibility-6590) 및 [Dynamic Media](#accessibility-dm-6590)의 액세스 가능성이 개선되었습니다.

* 스마트 이미징 DPR(장치 픽셀 비율) 및 네트워크 대역폭 최적화를 통해 최상의 품질 이미지를 효율적으로 전달할 수 있습니다.고해상도의 디스플레이와 제한된 네트워크 대역폭을 가진 디바이스 자세한 내용은 [스마트 이미징 FAQ](/help/assets/imaging-faq.md)를 참조하십시오.

   >[!NOTE]
   >
   >위의 스마트 이미징 개선 사항에 대한 릴리스 타임라인은 다음과 같습니다.
   >
   >* 2021년 5월 24일 NA,
      >
      >
   * 유럽, 중동 및 아프리카 2021년 6월 25일
      >
      >
   * 아시아 태평양 2021년 7월 19일


* Dynamic Media 게재에서 차세대 이미지 형식 AVIF에 대한 지원이 도입되었습니다(fmt URL 수정자). 자세한 내용은 [이미지 제공 및 api fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) 렌더링 을 참조하십시오.

   >[!NOTE]
   >
   >AVIF 지원을 위한 릴리스 타임라인은 다음과 같습니다.
   >
   >* 북미 2021년 5월 10일
      >
      >
   * 2021년 5월 24일 유럽, 중동, 아프리카
      >
      >
   * 아시아 태평양 2021년 6월 24일.


* 내장된 저장소(Apache Jackrabbit Oak)가 1.22.7.

[!DNL Experience Manager] 6.5.9.0에 도입된 기능 및 개선 사항의 전체 목록은 [6.5 서비스 팩 9](new-features-latest-service-pack.md)의 새로운 기능 을 참조하십시오. [!DNL Adobe Experience Manager] 

>[!NOTE]
>
>AEM 서비스 팩 9부터 [!DNL Experience Manager] 고객은 Java SE와 표준을 준수하는 OpenJDK의 [!DNL Azul Zulu] 빌드가 배포되는 [!DNL Experience Manager] 애플리케이션을 개발하고 운영할 수 있습니다.
>[!DNL Azul Zulu] JDK에 대한 지원은 [!DNL Experience Manager] 고객에게도 Adobe이 제공합니다.
>[Adobe 소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 [!DNL Azul Zulu JDKs] 관련 버전을 다운로드할 수 있습니다.
>Adobe에 의해 배포되는 Oracle Java 기술에 대한 사용 권한은 2022년 12월 말까지 만료됩니다. [!DNL Experience Manager] 고객은 이 날짜까지 최신  [!DNL Azul Zulu] JDK에 대한 사용을 계획 및 구현하는 것이 좋습니다. [!DNL Oracle Java] 기술 및 [!DNL Azul Zulu] 기술의 사용에 대한 자세한 내용은 관련 [FAQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en)를 참조하십시오.

다음은 [!DNL Experience Manager] 6.5.9.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6590}

* 인증 요구 사항 속성이 활성화된 게시된 페이지는 로그인 페이지로 리디렉션되지 않고 404 오류 메시지를 반환하지 않습니다(NPR-36354).

* 하이퍼링크를 만들 때 텍스트 구성 요소에서 링크를 검색하는 옵션이 작동하지 않습니다(NPR-35849).

* `com.day.cq.wcm.commons.ReferenceSearch` API를 사용할 때 순회 쿼리가 트리거됩니다. [!DNL Experience Manager] 서버의 성능에 영향을 줍니다(NPR-36407).

* 크기가 조정된 다른 레이아웃 컨테이너 내의 중첩된 레이아웃 컨테이너에 해당 하위 구성 요소에 대해 잘못된 열 수가 표시되어 이러한 구성 요소가 그리드에 정렬되지 않습니다(NPR-36359).

* 외부 링크 검사기에 유효한 외부 링크가 잘못된 링크로 표시됩니다(NPR-36289).

* 한동안 참조를 표시하면 참조 패널에 오류 메시지가 표시됩니다(NPR-36167).

* 구성 요소를 이동할 때 자동으로 생성된 parsys에 `sling:resourceType` 노드가 없습니다(NPR-36165).

* Live Copy를 동기화하려고 할 때(롤아웃 구성을 사용하는 동안 [!UICONTROL 블루프린트 활성화에서 활성화] 및 [!UICONTROL 블루프린트 활성화에서 활성화 취소]) 구성 요소가 Live Copy 마스터에서 삭제되면 동기화가 실패하고 `NullPointerException`가 기록됩니다(NPR-36127).

* 사용자가 태그(시스템에 없는 태그)에 대한 임시 텍스트를 입력하고 Enter 키를 누르면 태그 아래에 태그가 표시되지만 컨텐츠 조각을 저장하고 다시 열면 임시 태그가 사라집니다(NPR-36132).

* 받은 편지함에는 비동기 작업의 상태를 표시하는 옵션이 없습니다(NPR-36104).

* 상속을 복원한 후 중복 구성 요소가 만들어집니다(NPR-36000).

* `RemoteContentRenderingService`을(를) 사용할 때 `RemoteContentRendererRequestHandler.getRequest`에 대한 요청에는 항상 `ComponentExporter`에 대한 루트 페이지가 포함되지만, 순회 깊이 및 필터링 선택 사항을 기반으로 루트 모델에 포함되지 않은 경우에는 요청된 페이지를 포함하지 않습니다. SPA에 응답을 렌더링할 수 있는 정보가 충분하도록 요청에 항상 요청된 페이지가 포함되어야 합니다(NPR-35961).

* onTime/offTime 항목은 예상 onTime/offTime에서 활성화/비활성화되지 않습니다(NPR-35936).

* `cq:lastModified` 속성이 없는 경험 조각이 포함된 페이지를 게시하면 `NullPointerException` 이 발생합니다(NPR-35914).

* 컨테이너 내에서 구성 요소의 크기를 조정하려고 할 때는 원래 크기로 다시 크기를 조정할 수 없습니다. 구성 요소 컨테이너 크기를 줄이면 크기를 다시 원본으로 설정할 수 없습니다(NPR-35809).

* 편집기나 Live Copy 개요에서 트리거되는 롤아웃 대화 상자의 페이지 분리, 일시 중단 또는 작성되지 않은 페이지에 대한 상태 아이콘이 잘못되었습니다(NPR-35691).

* 마스터 롤아웃 페이지 및 하위 페이지 무시 확인란의 다중 사이트 관리자 롤아웃 페이지 내 속성 (NPR-35634).

* 클래식 UI에서 사용할 수 있는 복원 트리 기능이 Touch UI에서 누락되었습니다(CQ-4315352, CQ-4309415).

* [!DNL Experience Manager Sites] 페이지에서 상속을 되돌리고 페이지를 롤아웃하는 동안 문제가 발생했습니다(NPR-36033).

### [!DNL Assets] {#assets-6590}

[!DNL Adobe Experience Manager] 6.5.9.0에서는  [!DNL Assets] 다음 문제가 해결되었습니다.

* [!UICONTROL 폴더 메타데이터 스키마] 양식의 태그 선택 요소 내에서 생성된 태그는 저장되지 않습니다(NPR-36119).

* 작은 타원을 사용하여 자산에 주석을 지정하면 타원이 인쇄 버전의 주석 수와 겹칩니다(NPR-36114).

* 열 보기에서 중복된 자산이 업로드될 때 [!DNL Experience Manager]이 중복 자산 충돌을 묻는 메시지를 표시하지 않는 경우가 있습니다(NPR-36048).

* 링크 공유 대화 상자가 열려 있고 변경 사항이 없는 경우 닫기 단추를 클릭하여 닫히지 않습니다(NPR-36030).

* 속성을 업데이트하기 위해 여러 자산을 선택하면 오류가 발생하거나 선택되지 않은 자산의 속성이 업데이트되는 경우가 있습니다(NPR-36002).

* 자산 업로드 시 공백이 자산 파일 이름의 시작 또는 끝에 추가되고, 나머지 문자가 리포지토리의 기존 자산 이름과 동일한 경우, 로깅 없이 기존 자산이 바뀝니다(NPR-36001).

* 자산 세부 사항 페이지에서 비디오가 재생되면 재생 및 일시 중지 옵션이 작동하지 않습니다(NPR-35999).

* 자산을 벌크로 게시 취소할 때 Brand Portal에서 요청 URI가 너무 길음을 제안하는 오류를 생성합니다(NPR-35954).

* 긴 주석 텍스트가 있는 자산을 인쇄하면 공간이 있더라도 주석 텍스트를 트림합니다(NPR-35948).

* 카탈로그 만들기 페이지의 템플릿 보기 선택에서 페이지를 선택할 때 다음 페이지로 이동하는 옵션이 비활성화됩니다(CQ-4315462).

* 비디오 자산에서 자산 업데이트 워크플로우가 시작되면 페이지가 반복적으로 새로 고쳐집니다(CQ-4313375).

* DAM 폴더를 삭제하거나 이동할 수 없으며 예외가 기록됩니다(NPR-35942).

#### Assets {#assets-enhancements}의 개선 사항

* 카드, 열 및 인사이트 보기에서 [!UICONTROL 없음] 옵션을 도입하여 JCR 노드에 저장된 순서로 자산을 정렬합니다(NPR-36356).

* Adobe Experience Manager의 API 응답에서 이메일 ID를 소문자로 추가하는 옵션이 추가되었습니다(CQ-4317704).

#### Assets의 액세스 가능성 개선 {#assets-accessibility-6590}

[!DNL Adobe Experience Manager] 6.5.9.0에서는 다음과 같은 액세스 가능성이  [!DNL Assets] 개선되었습니다.

다음 텍스트와 아이콘의 대비(배경 포함)가 개선되어 시력이 제한된 사용자와 색상을 인식하는 데 도움이 됩니다.

* [!UICONTROL 속성] 페이지의 자산 제목(NPR-35967).
* 다양한 위치의 [!UICONTROL 등급] 섹션에 별 등급 아이콘이 표시됩니다(NPR-36009).
* 자산 및 폴더 카드 보기의 텍스트입니다(NPR-35966).
* [!UICONTROL 타임라인] 보기의 자리 표시자 텍스트(NPR-35965).
* 자산 검색 결과의 자산 이름(NPR-35964).
* [!UICONTROL 링크 공유] 대화 상자의 자리 표시자 텍스트(NPR-35963).
* [!UICONTROL 보기 설정 대화 상자]의  [!UICONTROL 목록 옵션]에 있는 메타데이터  , 상태      및 기타 텍스트(NPR-35910).
*  전역 검색 [!UICONTROL 에서 ] 검색 자리 표시자 텍스트를 표시하는 위치 및 유형입니다(NPR-35909).
* [!UICONTROL 컨텐츠 트리] 아래에서 아이콘을 확장 및 축소합니다(NPR-35908).
* 자산 폴더가 표시되는 페이지의 [!UICONTROL 자산] 텍스트(NPR-35905).
* [!UICONTROL 자산 메타데이터], [!UICONTROL 자산 세부 정보 페이지의 [!UICONTROL 개요] 옵션 내의 텍스트(NPR-35904)]
* 자산 세부 사항 페이지의 [!UICONTROL 속성] 및 [!UICONTROL 편집] 옵션에 대한 바로 가기 키에 대한 텍스트입니다(NPR-35904).

### [!DNL Dynamic Media] {#dynamic-media-6590}

Adobe Experience Manager 6.5.9.0 Assets는 [!DNL Dynamic Media]에서 다음 문제를 수정합니다.

* [!DNL Dynamic Media]이 [기본](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=en#troubleshoot-dm-config)에 의해 선택적으로 활성화되고 비활성화될 때 사용자 지정 뷰어 사전 설정 및 CSS가 [!DNL Dynamic Media]에 복제되지 않습니다(NPR-36232).

* 자산 세부 사항 페이지에서 비디오 표현물을 미리 보려 하면 비디오가 느리게 로드됩니다(CQ-4320122).

* 중복 자산 탐지기가 활성화된 상태에서 200개 이상의 자산을 업로드할 때 브라우저 페이지가 응답하지 않고 속도가 느려집니다(CQ-4319633).

* 페이지의 파노라마 미디어 구성 요소에 파노라마 이미지 자산을 추가하면 발견되지 않은 참조 오류가 기록됩니다(CQ-4317666).

* 경험 조각을 사용하여 대화형 미디어 뷰어가 구현되면 경험 조각이 게시자에서 열리지 않고 오류가 기록됩니다(CQ-4317655).

* Dynamic Media에 게시 옵션은 메타데이터 편집기 보기의 빠른 게시에서 사용할 수 없습니다(CQ-4317199).

* 읽기 전용 권한이 있는 사이트 작성자는 자산에 스마트 자르기 기능을 사용하고 스마트 잘려진 렌디션을 편집할 수 있습니다. 그러나 읽기 전용 권한이 있는 사용자는 사이트 개발 인스턴스에서 자산 속성을 편집할 수 없습니다(CQ-4316450).

* AEM 인스턴스가 Dynamic Media 모드를 설정한 경우에도 Dynamic Media 구성이 활성화되지 않은 폴더 경로에는 비디오 주석이 작동하지 않습니다(CQ-4314950).

* 자산 제목에 2바이트, 멀티바이트, 높은 ASCII, 키릴 자모, 서로게이트 쌍, 히브리어, 아랍어 및 GB18030 문자가 있는 경우, Dynamic Media에 게시할 때 자산 제목에 물음표(?)가 표시됩니다. (CQ-4311872).

#### Dynamic Media {#accessibility-dm-6590}의 액세스 가능성이 개선되었습니다

[!DNL Adobe Experience Manager] 6.5.9.0에서는  [!DNL Assets] 다음과 같은 액세스 가능성이 개선되었습니다 [!DNL Dynamic Media].

* 이미지 세트 편집기에서 키보드 키를 사용하여 자산을 추가하기 위해 대화 상자를 엽니다.
   * 화면 판독기에서 대화 상자가 열려 있다고 알려줍니다.
   * 키보드 포커스가 열리면 대화 상자로 이동합니다.
   * 대화 상자가 닫히면 키보드 포커스가 자산 추가 옵션으로 다시 이동합니다(CQ-4312134).

* 이제 핫스팟 편집기에서 키보드 키를 사용하여 자산에 핫스팟을 추가 및 편집할 수 있습니다(CQ-4305965).

* 이제 키보드 키를 사용하여 핫스팟 관리를 통해 핫스팟에 하이퍼링크를 배치할 수 있습니다. 이제 화면 판독기 포커스가 필드로 이동하여 URL 경로 및 선택 항목 열기 대화 상자로 이동합니다(CQ-4290735).

* 이미지 세트 편집기 페이지의 텍스트 및 컨트롤의 대비(배경 포함)가 개선되어 시력이 제한된 사용자와 색상을 인식하지 못하는 사용자가 이해할 수 있습니다(CQ-4290733).

* 이제 뷰어 사전 설정 편집기에서 자산 공유 옵션으로 이동하고 키보드 키를 사용하여 확장된 공유 옵션을 축소할 수 있습니다(CQ-4290724).

* 이제 키보드 키를 사용하여 비디오 인코딩 편집 페이지의 기본 및 고급 탭에 있는 정보 아이콘과 경고 아이콘에 대한 도구 팁을 탐색하고 볼 수 있습니다(CQ-4290722).

* 이제 화면 판독기에 뷰어 사전 설정 편집기의 모양 탭 및 동작 탭의 다양한 필드에 대한 지침이 내레이션됩니다(CQ-4290721).

* 양식 모드에서 이미지 사전 설정 편집 페이지를 탐색할 때 화면 판독기에 다양한 필드 및 컨트롤의 목적과 이름이 내레이션됩니다(CQ-4290717).

* 이제 자산 세부 사항 페이지를 탐색할 때 화면 판독기에서 뷰어 내의 다양한 옵션의 용도를 설명합니다(CQ-4290716).

* 자산 세부 사항 페이지의 자리 표시자 텍스트 모든 표현물 변환 옵션의 대비(배경 포함)가 개선되어 시력이 제한된 사용자와 색상을 인식하는 인식기가 제한된 사용자가 이해할 수 있습니다(CQ-4290713).

* 필수 필드를 나타내는 시각적 별표는 이제 이미지 세트 편집기의 자산 제목 필드에 제공되며 화면 판독기에서 필드에 대한 필수 정보를 알려줍니다(CQ-4290712).

* 이제 화면 판독기에서 자산 세부 사항 페이지의 뷰어 내에서 다양한 대화형 옵션의 용도에 액세스하고 나레이션할 수 있습니다(CQ-4290708).

### 플랫폼 {#platform-6590}

* 블루프린트에 대한 축소판을 생성하고 Live Copy 변경 사항을 롤아웃하면 일부 필드에 대한 상속이 작동하지 않습니다(CQ-4319517).

* 폴더를 만들 때 정렬 가능한 속성을 선택하고 폴더에 20개 이상의 자산을 추가하고 폴더의 모든 자산을 선택하면 잘못된 개수가 표시됩니다(CQ-4316243).

* 페이지를 새로 고칠 때 폴더 또는 자산을 정렬해도 적절한 결과가 표시되지 않습니다(CQ-4316200).

* Handlebars JavaScript 라이브러리가 v4.7.7로 업그레이드되었습니다(NPR-36375).

* 패키지 관리자를 사용하여 새 코드 패키지를 설치할 때 사용자 지정 번들이 업데이트되지 않습니다(NPR-35949).

* `resourceresolver` Sling 번들로 인해 `Sling:alias` 쿼리가 실패합니다(NPR-35335).

* AEM에서 SSL을 설정할 때 컨텍스트 경로가 제거됩니다(NPR-35294).

* 긴 실행 세션 후 `SegmentNotFound` 예외가 반환됩니다(NPR-36405).

### 통합 {#integrations-6590}

* Cloud Services 경험 조각에 대해 상속이 활성화된 페이지 속성을 저장할 수 없습니다(NPR-36107).

* IMS 사용자 인터페이스 페이지 매김 및 지연 로드는 적절한 결과를 표시하지 않습니다(NPR-36046).

* A4T Target 구성을 만들고 보고 소스를 [!DNL Adobe Analytics](으)로 선택하면 드롭다운 목록에서 사용할 수 있는 Adobe Target 지원 보고서 세트가 없습니다(NPR-36006).

### 프로젝트 {#projects-6590}

* 프로젝트 경로에 추가된 슬래시(/)가 추가되어 프로젝트의 JCR 경로가 확인되지 않으므로 프로젝트의 속성을 저장할 수 없습니다(NPR-36191).

### 스크린 {#screens-6590}

* [!DNL Experience Manager Screens] 사용자 지정 2FA 인증 핸들러가 사용되는 경우 플레이어를 인증할 수 없습니다(NPR-35854).

### 상거래 {#commerce-6590}

* [!UICONTROL 상거래 카탈로그] 마법사가 열 보기에서 40개 이상의 항목을 로드하지 못했습니다(CQ-4318379).

### 번역 프로젝트 {#translation-6590}

* `es` 페이지를 `es_es` 페이지로 다시 번역하는 동안 업데이트 또는 덮어쓰기 옵션이 표시되지 않습니다(NPR-36170).

* 인간 변환이 있는 프로젝트에 대해 자동 승인 옵션을 선택하면 작업 상태가 `Unknown`으로 표시됩니다(NPR-35981).

* 페이지를 번역하는 경우 경험 조각의 참조 경로가 대상 경험 조각 참조 경로로 업데이트되지 않습니다(NPR-35911).

* 상위 및 하위 페이지를 변경하고 상위 페이지를 번역용으로 보내면 하위 페이지도 잘못 변환됩니다(NPR-35896).

* 선택한 페이지에 대해 여러 개의 동시 번역 프로젝트가 있는 경우, [!UICONTROL 프로젝트로 이동] 옵션이 최신 번역 프로젝트에 연결되지 않습니다(NPR-35454).

* 자산을 [!DNL Dynamic Media]에 게시하면 게시 취소된 태그에 대한 잘못된 메시지가 [!DNL Experience Manager]에 표시됩니다(CQ-4315914, CQ-4315913).

* 삭제된 작업을 열면 [!DNL Experience Manager]에 잘못된 메시지가 표시됩니다(CQ-4315910).

### 워크플로 {#workflow-6590}

* 받은 편지함에서 사용할 수 있는 항목에 대해 완료, 위임 또는 열기 작업을 클릭하면 이러한 작업이 완료되었음을 나타내는 시각적 단서가 없습니다(NPR-36317).

### [!DNL Communities] {#communities-6590}

* 스팸 필터링에서 시스템은 AEM 서버를 다운시키는 JAVA 힙의 100%를 사용합니다(NPR-36316, NPR-36493).
* 포럼에서 SearchCommentSocialComponentListProvider에서 시작한 JCR 세션 데이터가 누출됩니다(NPR-36235).
* 특정 받은 편지함 메시지를 열면 잘못된 페이지 매김 및 기타 문제가 있는 모든 메시지가 반영됩니다(NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* [!DNL Brand Portal](으)로 [!DNL Experience Manager Assets] 구성 시 자산 소싱 기능 플래그가 자동으로 활성화됩니다(NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 는 예정된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜로부터 1주일 후에 추가 기능 패키지를 출시합니다.

보안 업데이트에 대한 자세한 내용은 [Experience Manager 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

## 6.5.9.0 설치 {#install}

**설치 요구 사항 및 추가 정보**

* Experience Manager 6.5.9.0을 사용하려면 Experience Manager 6.5가 필요합니다. 세부 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 Experience Manager 6.5.9.0을 설치합니다.

>[!NOTE]
>
>Adobe에서는 [!DNL Adobe Experience Manager] 6.5.9.0 패키지를 삭제하거나 제거하지 않는 것이 좋습니다.

### 서비스 팩 {#install-service-pack} 설치

[!DNL Adobe Experience Manager] 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. 인스턴스가 업데이트 모드 상태인 경우 설치 전에 인스턴스를 다시 시작합니다(이 경우 인스턴스가 이전 버전에서 업데이트된 경우). Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 [!DNL Experience Manager] 인스턴스의 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9.zip)에서 서비스 팩을 다운로드하십시오.

1. 패키지 관리자를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하십시오.

1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하십시오.

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이러한 작업은 [!DNL Safari]에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

작업 인스턴스에 Adobe Experience Manager 6.5.9.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.

B. [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0은 Bootstrap 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품] 아래에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.9.0)`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은 버전 1.22.3 이상에 있습니다(웹 콘솔 사용:`/system/console/bundles`)

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

<!--

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.9.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to AEM 6.5.9.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.
-->

### UberJar {#uber-jar}

Experience Manager 6.5.9.0용 UberJar는 [Maven Central 저장소](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9/)에서 사용할 수 있습니다.

Maven 프로젝트에서 UberJar를 사용하려면 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 가공물은 Adobe Public Maven 저장소(`repo.adobe.com`) 대신 Maven 중앙 저장소에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`로 변경되었습니다. 따라서 `dependency` 태그에 대해 `apis` 값이 있는 `classifier`이 없습니다.

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

다음은 [!DNL Experience Manager] 6.5.7.0에서 더 이상 사용되지 않는 것으로 표시된 기능 및 기능 목록입니다. 기능은 처음에 더 이상 사용되지 않으며 이후 릴리스에서 이후에 제거됩니다. 일반적으로 대체 옵션이 제공됩니다.

배포에서 기능 또는 기능을 사용하는지 검토합니다. 또한 대체 옵션을 사용하도록 구현을 변경할 계획입니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 더 이상 사용되지 않습니다. Adobe IMS 및 I/O를 통해 인증을 사용하는 Adobe Target Standard API를 지원하고 분석 및 개인화를 위해 Experience Manager 페이지를 계측하는 Adobe Launch의 늘어나는 역할을 지원하도록 Experience Manager 6.5에서 옵트인 통합이 업데이트되어 옵트인 마법사가 기능상 무관해졌습니다. | 해당 Experience Manager 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 [!DNL Adobe I/O] 통합을 구성합니다. |
| 커넥터 | Microsoft SharePoint 2010 및 Microsoft SharePoint 2013용 Adobe JCR 커넥터는 Experience Manager 6.5에서 더 이상 사용되지 않습니다. | N/A |

## 알려진 문제 {#known-issues}

* [!DNL Experience Manager] 인스턴스를 6.5에서 6.5.9.0 버전으로 업그레이드하는 경우 `error.log` 파일에서 `RRD4JReporter` 예외를 볼 수 있습니다. 인스턴스를 다시 시작하여 문제를 해결합니다.

* [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 서비스 팩을 [!DNL Experience Manager] 6.5에 설치하는 경우 자산 사용자 지정 워크플로우 모델(`/var/workflow/models/dam`에서 만들어짐)의 런타임 복사본이 삭제됩니다.
런타임 복사본을 검색하려면 Adobe에서 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사와 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* 계층 구조의 한 폴더의 이름이 [!DNL Experience Manager Assets]에서 변경되고 자산이 있는 중첩된 폴더가 [!DNL Brand Portal]에 게시되는 경우 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* 6.5.x.x Experience Manager 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target Standard API(IMS 인증)를 사용하여 Experience Manager에 Adobe Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :등록 변경으로 등록 취소를 완료할 때까지 기다리는 중 시간이 초과되었습니다.

## OSGi 번들 및 콘텐츠 패키지가 설치됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 [!DNL Experience Manager] 6.5.9.0에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

* [Experience Manager 6.5.9.0에 포함된 OSGi 번들 목록](assets/6590_bundles.txt)

* [Experience Manager 6.5.9.0에 포함된 컨텐츠 패키지 목록](assets/6590_packages.txt)

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터에 문의하는 방법](https://experienceleague.adobe.com/docs/customer-one/using/home.html)을 참조하십시오.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 릴리스 노트](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] 제품 페이지](https://www.adobe.com/kr/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/subscription/priority-product-update.html) 구독

