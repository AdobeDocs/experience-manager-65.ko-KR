---
title: '[!DNL Adobe Experience Manager] 6.5 이전 서비스 팩 릴리스 노트'
description: ' [!DNL Adobe Experience Manager] 6.5 서비스 팩의 릴리스 노트'
contentOwner: AK
mini-toc-levels: 2
exl-id: aeed49a0-c7c2-44da-b0b8-ba9f6b6f7101
source-git-commit: 97d0b0d85276c733b487a8f3c5095bc4feb7e08d
workflow-type: tm+mt
source-wordcount: '23168'
ht-degree: 50%

---

# 이전 서비스 팩에 포함된 핫픽스 및 기능 팩 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.9.0 {#experience-manager-6590}

[!DNL Adobe Experience Manager] 6.5.9.0에는 2019년 4월 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. 서비스 팩이 [!DNL Adobe Experience Manager] 6.5에 설치됩니다.

[!DNL Adobe Experience Manager] 6.5.9.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* [!DNL Experience Manager Sites] 이제 Dynamic Media Foundation 구성 요소를 사용하여 응답형 이미지 사전 설정 또는 스마트 자르기를 사용할 때 고해상도 장치에 대한 최적화를 켜거나 끌 수 있습니다.

* 성능을 향상시키기 위해 `hidden=false` 조건이 JCR 쿼리에서 [!UICONTROL QueryBuilder] 평가기로 이동됩니다. 변경 후 숨겨진 설명이 작동하는지 확인하려면 [!DNL Experience Manager] 은 숨겨진 폴더가 표시되지 않는지 확인합니다.

* [!DNL Experience Manager Sites] 페이지에서 삭제된 페이지 및 트리를 복원하는 기능.

* 메일 시스템 구성 서비스에 대한 새로 고침 토큰을 사용하여 액세스 토큰을 새로 고침하도록 새 사용자가 지원합니다.

* [메일 구성 서비스에 대한 SMTP XOAUTH2 ](/help/sites-administering/notification.md#setting-up-oauth)  메커니즘을 지원합니다.

* [!DNL MongoDB] 버전 4.2 및 4.4를 지원합니다.

* 홍콩, 마카오 및 대만과 관련된 이름의 발생 횟수는 중국 로케일 및 지역에 대한 새 이름 지정 규칙에 따라 업데이트됩니다.

* [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590) 및 [[!DNL Dynamic Media]](#accessibility-dm-6590)의 액세스 가능성이 개선되었습니다.

* 스마트 이미징 DPR(장치 픽셀 비율) 및 네트워크 대역폭 최적화를 통해 최상의 품질 이미지를 효율적으로 제공할 수 있습니다. 고해상도의 디스플레이와 제한된 네트워크 대역폭을 가진 디바이스 자세한 내용 및 타임라인은 [스마트 이미징 FAQ](/help/assets/imaging-faq.md)를 참조하십시오.

* [!DNL Dynamic Media] 배달(`fmt` URL 수정자)은 차세대 이미지 형식 AVIF(AV1 이미지 형식)를 지원합니다. 자세한 내용 및 타임라인은 [이미지 제공 및 API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html)를 참조하십시오.

* [!UICONTROL 작업 할당] 워크플로우 단계를 사용하여 그룹에 알림 이메일을 보낼 수 있습니다.

* 소스 Interactive Communication을 수정한 후 Interactive Communication 초안을 검색하는 기능.

* [!DNL Experience Manager Forms]에서 reCAPTCHA 서비스를 로드, 렌더링 및 유효성 검사하기 위한 사용자 지정 도메인 이름을 설정합니다.

* [!UICONTROL 양식 데이터 모델 서비스 호출] 워크플로우 단계에 대한 입력 데이터 개선 사항.

* [!DNL Experience Manager Forms]의 레코드 문서 템플릿에서 여러 마스터 페이지를 사용할 수 있습니다.

* [!DNL Experience Manager Forms]의 레코드 문서에서 지원 페이지가 중단됩니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 1.22.7.

[!DNL Experience Manager] 6.5.9.0에 도입된 기능 및 개선 사항의 전체 목록은 [6.5 서비스 팩 9](new-features-latest-service-pack.md)의 새로운 기능 을 참조하십시오. [!DNL Adobe Experience Manager] 

>[!NOTE]
>
>서비스 팩 9부터 [!DNL Experience Manager] 고객은 Java™ SE와 표준을 준수하는 OpenJDK의 [!DNL Azul Zulu] 빌드가 배포되는 [!DNL Experience Manager] 애플리케이션을 개발하고 운영할 수 있습니다.
>[!DNL Azul Zulu] JDK에 대한 지원은 [!DNL Experience Manager] 고객에게도 Adobe이 제공합니다.
>[Adobe 소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 [!DNL Azul Zulu] JDK의 관련 버전을 다운로드할 수 있습니다.
>Adobe에 의해 배포되는 Oracle Java™ 기술에 대한 사용 권한은 2022년 12월 말까지 만료됩니다. [!DNL Experience Manager] 고객은 이 날짜까지 최신  [!DNL Azul Zulu] JDK에 대한 사용을 계획 및 구현하는 것이 좋습니다. [!DNL Oracle Java™] 기술 및 [!DNL Azul Zulu] 기술의 사용에 대한 자세한 내용은 관련 [FAQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf)를 참조하십시오.

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

* 사용자가 태그에 대한 임시 텍스트(시스템에 없는 태그)를 입력하고 Enter 키를 누르면 태그 필드가 필드 아래에 표시되지만 컨텐츠 조각을 저장하고 다시 열면 임시 태그가 사라집니다(NPR-36132).

* 받은 편지함에는 비동기 작업의 상태를 표시하는 옵션이 없습니다(NPR-36104).

* 상속을 복원한 후 중복 구성 요소가 만들어집니다(NPR-36000).

* `RemoteContentRenderingService`을(를) 사용할 때 `RemoteContentRendererRequestHandler.getRequest`에 대한 요청에는 항상 `ComponentExporter`에 대한 루트 페이지가 포함되지만, 순회 깊이 및 필터링 선택 사항을 기반으로 루트 모델에 포함되지 않은 경우에는 요청된 페이지를 포함하지 않습니다. SPA에 응답을 렌더링할 수 있는 정보가 충분하도록 요청에 항상 요청된 페이지가 포함되어야 합니다(NPR-35961).

* onTime/offTime 항목은 예상 onTime/offTime에서 활성화/비활성화되지 않습니다(NPR-35936).

* `cq:lastModified` 속성이 없는 경험 조각이 포함된 페이지를 게시하면 `NullPointerException` 이 발생합니다(NPR-35914).

* 컨테이너 내에서 구성 요소의 크기를 조정하려고 할 때는 원래 크기로 다시 크기를 조정할 수 없습니다. 구성 요소 컨테이너 크기를 줄이면 크기를 다시 원본으로 설정할 수 없습니다(NPR-35809).

* 편집기에서 트리거되거나 Live Copy 개요에서 트리거되는 롤아웃 대화 상자의 페이지 분리, 일시 중단 또는 작성되지 않은 페이지에 대한 상태 아이콘이 잘못되었습니다(NPR-35691).

* 마스터 롤아웃 페이지 및 하위 페이지 무시 확인란의 다중 사이트 관리자 롤아웃 페이지 내 속성 (NPR-35634).

* 클래식 UI에서 사용할 수 있는 복원 트리 기능이 Touch UI에서 누락되었습니다(CQ-4315352, CQ-4309415).

* [!DNL Experience Manager Sites] 페이지에서 상속을 되돌리고 페이지를 롤아웃하는 동안 문제가 발생했습니다(NPR-36033).

### [!DNL Assets] {#assets-6590}

[!DNL Assets]에서 다음과 같은 사용자 경험 개선 작업이 수행됩니다.

* [!UICONTROL 만들기], [!UICONTROL 수정] 또는 [!UICONTROL 이름] 매개 변수 중 하나를 기반으로 정렬되지 않은 자산을 보려면 [!DNL Adobe Experience Manager]에서 [!UICONTROL 없음] 옵션을 제공합니다. [!UICONTROL 정렬 기준] 옵션. [!UICONTROL 없음] 옵션은 자산 사용자 인터페이스(카드, 열 및 인사이트 보기)의 자산이 JCR 노드에 있는 자산과 동일한 순서로 유지되도록 합니다(NPR-36356).

* [!DNL Adobe Experience Manager]에서 ACP API 응답에서 이메일 ID를 소문자로 만들려면 선택적 설정이 도입됩니다. as a1/> 사용자가 ID에 모든 문자가 소문자로 포함되어 있지 않으면 자산을 체크 인할 수 없습니다. [!DNL Adobe Asset Link] [!DNL Adobe Asset Link] 패널에서는 [!DNL Adobe Experience Manager]의 ACP API 응답을 사용합니다(CQ-4317704).

다음 액세스 가능성 향상은 서비스 팩 9의 일부로 [!DNL Assets]에서 사용할 수 있습니다.

다음 텍스트와 아이콘의 대비(배경 포함)가 개선되어 시력이 제한된 사용자와 색상을 인식하는 데 도움이 됩니다.

* [!UICONTROL 속성] 페이지의 자산 제목(NPR-35967).
* 다양한 위치의 [!UICONTROL 등급] 섹션에 별 등급 아이콘이 표시됩니다(NPR-36009).
* 자산 및 폴더 카드 보기의 텍스트(NPR-35966).
* [!UICONTROL 타임라인] 보기의 자리 표시자 텍스트(NPR-35965).
* 자산 검색 결과의 자산 이름(NPR-35964).
* [!UICONTROL 링크 공유] 대화 상자의 자리 표시자 텍스트(NPR-35963).
* [!UICONTROL 보기 설정 대화 상자]의  [!UICONTROL 목록 옵션]에 있는 메타데이터  , 상태      및 기타 텍스트(NPR-35910).
*  전역 검색 [!UICONTROL 에서 ] 검색 자리 표시자 텍스트를 표시하는 위치 및 유형입니다(NPR-35909).
* [!UICONTROL 컨텐츠 트리] 아래에서 아이콘을 확장 및 축소합니다(NPR-35908).
* 자산 폴더가 표시되는 페이지의 [!UICONTROL Assets] 텍스트(NPR-35905).
* 자산 세부 사항 페이지의 [!UICONTROL 개요] 옵션 내의 [!UICONTROL 자산 메타데이터], [!UICONTROL 사용 통계]의 텍스트(NPR-35904).
* 자산 세부 사항 페이지의 [!UICONTROL 속성] 및 [!UICONTROL 편집] 옵션에 대한 바로 가기 키에 대한 텍스트입니다(NPR-35904).

다음 버그 수정 사항은 서비스 팩 9의 일부로 [!DNL Assets]에서 사용할 수 있습니다.

* [!UICONTROL 폴더 메타데이터 스키마] 양식의 태그 선택 요소 내에서 생성된 태그는 저장되지 않습니다(NPR-36119).

* 작은 타원을 사용하여 자산에 주석을 지정하면 타원이 인쇄 버전의 주석 수와 겹칩니다(NPR-36114).

* 때로는 열 보기에서 중복 자산이 업로드될 때 [!DNL Experience Manager]이 중복 자산 충돌을 묻지 않습니다(NPR-36048).

* 링크 공유 대화 상자가 열려 있고 변경 사항이 없는 경우 닫기 단추를 클릭하여 닫히지 않습니다(NPR-36030).

* 속성을 업데이트하기 위해 여러 자산을 선택하면 오류가 발생하거나 선택되지 않은 자산의 속성이 업데이트되는 경우가 있습니다(NPR-36002).

* 자산 업로드 시 공백이 자산 파일 이름의 시작 또는 끝에 추가되고, 나머지 문자가 리포지토리의 기존 자산 이름과 동일한 경우, 로깅 없이 기존 자산이 바뀝니다(NPR-36001).

* 자산 세부 사항 페이지에서 비디오가 재생되면 재생 및 일시 중지 옵션이 작동하지 않습니다(NPR-35999).

* 자산을 벌크로 게시 취소할 때 Brand Portal에서 요청 URI가 너무 길음을 제안하는 오류를 생성합니다(NPR-35954).

* 긴 주석 텍스트가 있는 자산을 인쇄하면 공간이 있더라도 주석 텍스트를 트림합니다(NPR-35948).

* 카탈로그 만들기 페이지의 템플릿 보기 선택에서 페이지를 선택할 때 다음 페이지로 이동하는 옵션이 비활성화됩니다(CQ-4315462).

* 비디오 자산에서 자산 업데이트 워크플로우가 시작되면 페이지가 반복적으로 새로 고쳐집니다(CQ-4313375).

* DAM 폴더를 삭제하거나 이동할 수 없으며 예외가 기록됩니다(NPR-35942).

### [!DNL Dynamic Media] {#dynamic-media-6590}

[!DNL Adobe Experience Manager] 6.5.9.0에서는 [!DNL Dynamic Media]에서 다음과 같은 액세스 가능성이 개선되었습니다.

* 대화 상자를 열어 [!UICONTROL 이미지 세트] 편집기에서 키보드 키를 사용하여 자산을 추가하는 경우:
   * 화면 판독기는 대화 상자가 열려 있음을 알려줍니다.
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

Adobe Experience Manager 6.5.9.0 Assets는 [!DNL Dynamic Media]에서 다음 문제를 수정합니다.

* [!DNL Dynamic Media]이 [기본](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html#troubleshoot-dm-config)에 의해 선택적으로 활성화되고 비활성화될 때 사용자 지정 뷰어 사전 설정 및 CSS가 [!DNL Dynamic Media]에 복제되지 않습니다(NPR-36232).

* 자산 세부 사항 페이지에서 비디오 표현물을 미리 보려 하면 비디오가 느리게 로드됩니다(CQ-4320122).

* 중복 자산 탐지기가 활성화된 상태에서 200개 이상의 자산을 업로드할 때 브라우저 페이지가 응답하지 않고 속도가 느려집니다(CQ-4319633).

* 페이지의 파노라마 미디어 구성 요소에 파노라마 이미지 자산을 추가하면 발견되지 않은 참조 오류가 기록됩니다(CQ-4317666).

* 경험 조각을 사용하여 대화형 미디어 뷰어가 구현되면 경험 조각이 게시자에서 열리지 않고 오류가 기록됩니다(CQ-4317655).

* [!UICONTROL Dynamic Media에 ] 게시 옵션은 속성 페이지의  [!UICONTROL 빠른 ] 게시 옵션  에서 사용할 수 없습니다(CQ-4317199).

* 읽기 전용 권한이 있는 사이트 작성자는 자산에 스마트 자르기 기능을 사용하고 스마트 자르기 렌디션을 편집할 수 있습니다(CQ-4316450).

* [!DNL Experience Manager] 인스턴스가 [!DNL Dynamic Media] 모드에서 설정되어 있어도 [!DNL Dynamic Media] 구성이 활성화되지 않은 폴더 경로에는 비디오 주석이 작동하지 않습니다(CQ-4314950).

* 자산 제목에 2바이트, 멀티바이트, 높은 ASCII, 키릴 자모, 서로게이트 쌍, 히브리어, 아랍어 및 GB18030 문자가 있는 경우, Dynamic Media에 게시할 때 자산 제목에 물음표(?)가 표시됩니다. (CQ-4311872).

>Experience Manager 6.5.9.0의 Dynamic Media *에 있는 알려진 비디오 재생 문제는*&#x200B;입니다.
>
>* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.
>* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.


### 플랫폼 {#platform-6590}

* 블루프린트에 대한 축소판을 생성하고 Live Copy 변경 사항을 롤아웃하면 일부 필드에 대한 상속이 작동하지 않습니다(CQ-4319517).

* 폴더를 만들 때 정렬 가능한 속성을 선택하고 폴더에 20개 이상의 자산을 추가하고 폴더의 모든 자산을 선택하면 잘못된 개수가 표시됩니다(CQ-4316243).

* 페이지를 새로 고칠 때 폴더 또는 자산을 정렬해도 적절한 결과가 표시되지 않습니다(CQ-4316200).

* Handlebars JavaScript 라이브러리가 v4.7.7로 업그레이드되었습니다(NPR-36375).

* 패키지 관리자를 사용하여 새 코드 패키지를 설치할 때 사용자 지정 번들이 업데이트되지 않습니다(NPR-35949).

* `resourceresolver` Sling 번들로 인해 `Sling:alias` 쿼리가 실패합니다(NPR-35335).

* Experience Manager에서 SSL을 설정할 때 컨텍스트 경로가 제거됩니다(NPR-35294).

* 긴 실행 세션 후 `SegmentNotFound` 예외가 반환됩니다(NPR-36405).

### 통합 {#integrations-6590}

* Cloud Services 경험 조각에 대해 상속이 활성화된 페이지 속성을 저장할 수 없습니다(NPR-36107).

* IMS 사용자 인터페이스 페이지 매김 및 지연 로드는 적절한 결과를 표시하지 않습니다(NPR-36046).

* A4T Target 구성을 만들고 보고 소스를 [!DNL Adobe Analytics](으)로 선택하면 드롭다운 목록에서 사용할 수 있는 Adobe Target 지원 보고서 세트가 없습니다(NPR-36006).

### 프로젝트 {#projects-6590}

* 프로젝트 경로에 추가된 슬래시(`/`)가 추가되어 프로젝트의 JCR 경로가 확인되지 않으므로 프로젝트의 속성을 저장할 수 없습니다(NPR-36191).

### 스크린 {#screens-6590}

* [!DNL Experience Manager Screens] 사용자 지정 2단계 인증 핸들러가 사용되는 경우 플레이어를 인증할 수 없습니다(NPR-35854).

### 상거래 {#commerce-6590}

* [!UICONTROL 상거래 카탈로그] 마법사가 열 보기에서 40개 이상의 항목을 로드하지 못했습니다(CQ-4318379).

### 번역 프로젝트 {#translation-6590}

* `es` 페이지를 `es_es` 페이지로 다시 번역하는 동안 업데이트 또는 덮어쓰기 옵션이 표시되지 않습니다(NPR-36170).

* 인간 변환이 있는 프로젝트에 대해 자동 승인 옵션을 선택하면 작업 상태가 `Unknown`으로 표시됩니다(NPR-35981).

* 페이지를 번역하는 경우 [!DNL Experience Fragments]의 참조 경로가 대상 [!DNL Experience Fragment] 참조 경로로 업데이트되지 않습니다(NPR-35911).

* 상위 및 하위 페이지를 변경하고 상위 페이지를 번역용으로 보내면 하위 페이지도 잘못 변환됩니다(NPR-35896).

* 선택한 페이지에 대해 여러 개의 동시 번역 프로젝트가 있는 경우, [!UICONTROL 프로젝트로 이동] 옵션이 최신 번역 프로젝트에 연결되지 않습니다(NPR-35454).

* 자산을 [!DNL Dynamic Media]에 게시하면 게시 취소된 태그에 대한 잘못된 메시지가 [!DNL Experience Manager]에 표시됩니다(CQ-4315914, CQ-4315913).

* 삭제된 작업을 열면 [!DNL Experience Manager]에 잘못된 메시지가 표시됩니다(CQ-4315910).

### 워크플로우 {#workflow-6590}

* 받은 편지함에서 사용할 수 있는 항목에 대해 완료, 위임 또는 열기 작업을 클릭하면 이러한 작업이 완료되는 시각적 단서가 없습니다(NPR-36317).

### [!DNL Communities] {#communities-6590}

* 스팸 필터링에서 시스템은 Java™ 힙의 100%를 소비하여 Experience Manager 서버가 응답하지 않습니다(NPR-36316, NPR-36493).
* 포럼에서 `SearchCommentSocialComponentListProvider`에서 시작된 JCR 세션 데이터가 누출됩니다(NPR-36235).
* 특정 받은 편지함 메시지를 열면 잘못된 페이지 매김 및 기타 문제가 있는 모든 메시지가 반영됩니다(NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* [!DNL Brand Portal](으)로 [!DNL Experience Manager Assets] 구성 시 자산 소싱 기능 플래그가 자동으로 활성화됩니다(NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 는 예정된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜로부터 1주일 후에 추가 기능 패키지를 출시합니다.


**적응형 양식**

* 여러 번역 사전을 생성하는 동안 [!DNL Experience Manager Forms] 6.5.7.0에서 언어 초기화 문제가 발생합니다(NPR-36439).
* 적응형 양식 조각에 첨부 파일을 추가하고 양식을 제출하면 [!DNL Experience Manager Forms]에 다음 오류 메시지가 표시됩니다(NPR-36195).

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* 인간 변환을 사용하여 사전을 업데이트한 다음 적응형 양식을 미리 보면 수정 사항이 표시되지 않습니다(NPR-36035).

**대화형 통신**

* 대화형 통신 인쇄 채널을 사용하여 이미지를 업로드하고 편집하면 이미지가 더 이상 표시되지 않습니다(NPR-36518).

* 텍스트 자산을 편집하고 자리 표시자를 채우면 탐색 창에서 모든 대화형 요소가 제거됩니다(NPR-35991).

**워크플로우**

* JBoss®에서 [!DNL Experience Manager Forms] 서비스의 REST 엔드포인트를 호출하면 [!DNL Experience Manager]에 다음 오류 메시지가 표시됩니다(NPR-36305).

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**백엔드 통합**

* 읽기 서비스 인수를 대시가 포함된 리터럴 값에 바인딩하는 동안 양식 데이터 모델을 저장할 수 없습니다(NPR-36366).

**문서 보안**

* GlobalSign용 인증 및 HSM을 설정하면 LTV에 타임스탬프를 추가하는 동안 [!DNL Experience Manager Forms]에 `Unsuported Algorithm` 및 `Invalid TSA Certificate` 오류 메시지가 표시됩니다(NPR-36026, NPR-36025).

**문서 서비스**

* [!DNL Experience Manager Forms]과의 통합을 위해 [!DNL Gibson] 라이브러리에 대한 업데이트(NPR-36211).

**Foundation JEE**

* AdminUI에서 끝점 관리 를 선택하면 [!DNL Experience Manager Forms]에 `endpoint registry failure` 오류 메시지가 표시됩니다(CQ-4320249).

보안 업데이트에 대한 자세한 내용은 [[!DNL Experience Manager] 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

### Experience Manager 6.5.9.0의 알려진 문제 {#known-issues-6590}

* [!DNL Experience Manager] 인스턴스를 6.5에서 6.5.10.0 버전으로 업그레이드하는 경우 `error.log` 파일에서 `RRD4JReporter` 예외를 볼 수 있습니다. 문제를 해결하려면 인스턴스를 다시 시작합니다.

* [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 서비스 팩을 [!DNL Experience Manager] 6.5에 설치하는 경우 자산 사용자 지정 워크플로우 모델(`/var/workflow/models/dam`에서 만들어짐)의 런타임 복사본이 삭제됩니다.
런타임 복사본을 검색하려면 Adobe에서 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사와 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* 사용자는 [!DNL Assets]에서 계층 구조의 폴더의 이름을 변경하고 중첩된 폴더를 [!DNL Brand Portal]에 게시할 수 있습니다. 그러나 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* 6.5.x.x Experience Manager 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target Standard API(IMS 인증)를 사용하여 Experience Manager에 Adobe Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경으로 등록 취소를 완료할 때까지 기다리는 중 시간이 초과되었습니다.

## [!DNL Adobe Experience Manager] 6.5.8.0 {#experience-manager-6580}

[!DNL Adobe Experience Manager] 6.5.8.0에는 2019년 4월 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. 서비스 팩이 [!DNL Adobe Experience Manager] 6.5에 설치됩니다.

[!DNL Adobe Experience Manager] 6.5.8.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* 이제 [연결된 자산 기능](/help/assets/use-assets-across-connected-assets-instances.md)을 사용할 때 자산을 사용하는 모든 [!DNL Sites] 페이지의 목록을 볼 수 있습니다. 자산에 대한 이러한 참조는 자산의 [!UICONTROL 속성] 페이지에서 사용할 수 있습니다. 이를 통해 관리자, 마케터 및 라이브러리에서는 자산 사용을 완전히 볼 수 있으므로 추적, 관리 및 브랜드 일관성을 향상시킬 수 있습니다.

* 웹 페이지에서 참조되는 자산을 삭제할 때 [!DNL Experience Manager] [에 경고](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references)가 표시됩니다. 참조된 자산을 강제로 삭제하거나 자산의 [!DNL Properties] 페이지에 표시되는 참조를 확인하고 수정할 수 있습니다. 참조를 클릭하면 로컬 및 원격 [!DNL Sites] 페이지가 열립니다.

* [!UICONTROL 이름], [!UICONTROL 마지막 수정 날짜,] 및 [!UICONTROL 마지막 롤아웃 날짜] 속성을 사용하여 롤아웃에 사용할 수 있는 Live Copy 페이지를 정렬합니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 1.22.6. <!-- TBD: Mention the version -->

[!DNL Experience Manager] 6.5.8.0에 도입된 기능 및 개선 사항의 전체 목록은 [6.5 서비스 팩 8](new-features-latest-service-pack.md)의 새로운 기능 을 참조하십시오. [!DNL Adobe Experience Manager] 

다음은 [!DNL Experience Manager] 6.5.8.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6580}

* 페이지를 블루프린트로 이동하면 링크의 대상이 업데이트되지 않습니다(NPR-35724).
* 타이젠 기반 플레이어가 특정 브라우저에서 인증되지 않습니다. 이 문제는 samesite=none 속성을 지원하지 않는 브라우저에서 발생합니다(NPR-35589).
* 잠금 해제된 응답형 컨테이너는 허용된 구성 요소를 표시하지 않습니다(NPR-35565).
* 새로 추가된 페이지의 Live Copy를 만들 때 언어 마스터는 각 도메인에 대해 두 개의 복사본을 만듭니다(NPR-35545).
* `org.apache.felix.scr.impl.ComponentRegistry` 타이머로 인해 많은 스레드가 차단되는 경우 SCR 구성 요소 레지스트리에서 교착 상태가 발생합니다. 그 결과, [!DNL Experience Manager]이(가) 무기한 응답하지 않습니다(GRANITE-33125,FELIX-6252).
* 사이드 레일에서 특정 자산을 검색할 때 결과에 검색되지 않은 자산이 포함됩니다(NPR-35524).
* Experience Manager 인스턴스에 대해 SSL을 사용하도록 설정하면 컨텍스트 경로가 제거됩니다(NPR-35477).
* 목록을 만들고, 일부 텍스트를 첫 번째 요소로 추가하고, 테이블을 두 번째 요소로 추가하고, 표 내에 목록을 추가하면 상위 목록이 왜곡됩니다(NPR-35465).
* 연속된 목록 항목에서 다른 플러그인을 사용하는 경우 추가 <br> 태그가 목록 항목에 추가됩니다(NPR-35464).
* 두 단락 사이에 목록을 배치하면 목록에 테이블을 추가할 수 없습니다(NPR-35356).
* AEM 인스턴스 업그레이드를 AEM 6.3에서 AEM 6.5로 시작하면 업그레이드 인스턴스를 시작하는 데 시간이 오래 걸립니다(NPR-35323).
* 브라켓()을 포함하는 AEM 자산을 복제할 때. 이름에서 복제가 실패합니다(GRANITE-27004, NPR-35315).
* 리치 텍스트 편집기에 제목을 추가하면 단락 단추가 비활성화됩니다(NPR-35256).
* 기존 목록에 항목을 추가하면 후속 축소 또는 전환 목록이 삭제됩니다(NPR-35206).
* 페이지 롤아웃 옵션을 선택하면 사용 가능한 모든 Live Copy가 있는 대화 상자가 나타나고 자동 롤아웃이 수행됩니다. 페이지의 Live Copy는 사용자 작업 없이 모든 지리적 위치에 롤아웃됩니다(NPR-35138).
* 하위 포함 옵션을 사용하는 경우 게시 관리 옵션에 모든 페이지가 나열되지는 않습니다. 22페이지만 나열됩니다(NPR-35086).
* 정책을 편집해도 텍스트 구성 요소는 정책 변경 사항을 유지하지 않습니다(NPR-35070).
* 번호가 매겨진 목록의 일부 항목을 들여쓸 때, 들여쓰기가 동일한 항목의 경우 번호 매기기를 1부터 시작해야 하지만 모든 항목은 동일한 번호를 유지합니다(CQ-4313011).
* 축소가 활성화되면 페이지나 구성 요소를 편집할 수 없습니다. AEM 6.5 서비스 팩 7을 설치한 후 문제가 시작되었습니다(CQ-4311133).
* 옴니 검색 및 자산 필터가 관련이 없거나 결과를 반환하지 않습니다(CQ-4312322, NPR-35793).
* 여러 페이지가 동시에 클라이언트 라이브러리에 액세스하면 HTML 라이브러리 관리자가 클라이언트 라이브러리를 로드하지 못합니다. 이로 인해 페이지가 잘못 렌더링됩니다(NPR-35538).
* [!DNL Experience Manager]에서 SSL을 설정할 때 컨텍스트 경로가 자동으로 제거됩니다(NPR-35294).
* 패키지 관리자는 로그아웃 옵션을 클릭한 후 사용자를 로그아웃하지 않습니다(NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0에서는  [!DNL Assets] 다음 문제를 수정하고 다음 개선 사항을 제공합니다.

* 이전 버전의 자산을 복원하면 OSGi 콘솔에서 DamEvent.Type RESTORED 이벤트가 트리거되지 않습니다(NPR-35789).
* `IndexWriter.merge` 스마트  `OutOfMemoryError` 태깅 기능이 큰  `/oak:index/lucene` 및  `/oak:index/ntBaseLucene` 인덱스를 만들므로 오류가 발생합니다(NPR-35651).
* 이름에 멀티바이트 문자가 있는 [!UICONTROL 자산 기여도] 유형 폴더를 저장하려고 하면 오류 메시지가 표시됩니다(NPR-35605).
* 계단식 메타데이터 하위 유형 필드를 사용하면 잘못된 &#39;이 필드 채우십시오&#39; 오류가 발생합니다(NPR-35643).
* 기존 자산을 [!DNL Assets] 사용자 인터페이스에서 드래그하고 새 버전을 만들면 메타데이터의 변경 사항이 지속되지 않습니다(NPR-34940).
* 계단식 메뉴에 대한 메타데이터 스키마 편집기에서 규칙을 만들 때 [!UICONTROL 종속 설정] 옵션이 동일한 이름을 반복합니다(NPR-35596).
* [!UICONTROL Assets 관리 검색 레일]을 편집한 후에는 유사성 검색이 작동하지 않습니다(NPR-35588).
* 폴더 내에서 [!UICONTROL 필터]를 클릭하여 왼쪽 레일에서 자산 검색을 여는 경우, [!UICONTROL 상태] > [!UICONTROL 체크아웃] > [!UICONTROL 체크아웃]이 작동하지 않습니다(NPR-35530).
* 자산의 모든 스마트 태그를 삭제하고 변경 사항을 저장하려고 하면 태그가 제거되지 않습니다. 하지만 사용자 인터페이스는 변경 사항이 저장되었음을 나타냅니다(NPR-35519).
* 사용자는 정렬 가능한 폴더에서 목록 보기에서 자산을 다시 배열하거나 정렬할 수 없습니다(NPR-35516).
* 기본 메타데이터 스키마를 편집하는 경우, 자산의 [!UICONTROL 속성] 페이지의 태그 필드가 텍스트 필드로 변경됩니다. 변경 사항을 통해 모르는 사용자가 온디맨드 태그를 추가할 수 있고 태그는 리포지토리에 문자열로 저장됩니다(NPR-35478).
* 자산을 다운로드할 때 유효한 이메일 주소가 없는 이름을 제공하는 경우 다운로드 옵션을 사용할 수 없습니다. 하지만 다운로드 대화 상자에서 다른 옵션을 선택하면 버튼이 활성화되지만 이메일이 전송되지 않습니다(NPR-35365).
* 사용자가 [!DNL Adobe InDesign]에서 자산을 편집한 후 자산을 체크 인할 수 없으며 권한 부족에 대한 오류가 표시됩니다(NPR-35341).
* Handlebars JavaScript 라이브러리가 v4.7.6로 업그레이드되었습니다(NPR-35333).
* 단일 항목을 선택할 때까지 벌크 메타데이터 편집에서 시작하고 항목을 선택 취소하여 메타데이터 편집기 인터페이스가 예상대로 작동하지 않습니다(NPR-35144).
* `assets.html` 페이지 내에서 클릭할 때 전역 탐색에서 올바른 콘솔이 열리지 않습니다(CQ-4312311).
* [!DNL Assets] RGB 표현물이 있는 자산에 대한 RGB 표현물을 표시하지 않습니다(CQ-4310190).
* 메뉴의 [!UICONTROL 관계] 옵션이 [!UICONTROL 속성] 페이지에 제대로 표시되지 않습니다(CQ-4310188).
* 문서에 대한 파일 유형 필터를 사용하여 자산을 검색하고 Smart Collection을 만드는 경우 컬렉션에 액세스할 때 필터가 적용되지 않습니다. 대신, 모든 유형의 자산이 검색에 표시됩니다(NPR-35759).
* [!DNL Assets] 사용자 인터페이스에서 Lightbox에 자산을 끌어다 추가할 수 없습니다(NPR-35901).
* 이름 지정 충돌을 해결한 후 기존 자산의 새 버전을 만들면 원래 자산의 메타데이터를 덮어씁니다(CQ-4313594).
* 검색 필터나 조건자를 사용하여 자산 검색을 필터링하고, 자산을 열어 보거나 편집한 다음 검색 결과 페이지로 돌아가면 필터가 작동하지 않습니다. 검색된 모든 자산이 필터링되지 않은 상태로 나열됩니다(NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* RESS 이미지 사전 설정에 대한 URL 옵션은 자산 세부 사항 페이지에서 활성화됩니다. 이제 다이내믹 표현물 섹션에서 RESS 이미지 사전 설정을 선택하면 자산 세부 사항 페이지에서 URL과 RESS 옵션을 모두 사용할 수 있습니다. (CQ-4311241)
* 대화형 미디어 구성 요소 - 사용자에게 선택적 게시 구성이 있는 [!DNL Experience Manager]이 있는 경우 대화형 비디오가 작동하지 않습니다(CQ-4311054).
* 폴더 간에 자산을 이동하는 경우 API를 통해 [!DNL Experience Manager] 과 [!DNL Dynamic Media–Scene7] 간의 동기화가 매우 느립니다(CQ-4310001).
* Omnisearch를 사용할 때 로그 크기가 크게 증가합니다(CQ-4309153).
* 선택적 동기화가 활성화되고 자산이 동기화 폴더로 복사(이동되지 않음)되면 이 동기화는 예상대로 동기화되지 않습니다(CQ-4307122).
* DM에 자동으로 게시되는 업로드된 자산의 경우 상태는 AEM에 게시됨 을 표시하지 않습니다. 또한 Dynamic Media 게시 상태 열에 올바른 게시된 상태가 표시되지 않습니다(CQ-4306415).
* 자산이 [!DNL Experience Manager]에 게시되고 활성화 시 [!DNL Dynamic Media]에 게시하도록 설정된 경우 `scene7FileStatus` 메타데이터 값이 예상대로 업데이트되지 않습니다(CQ-4308269).
* 비디오 프로필을 편집할 때 [!DNL Experience Manager]에 비디오 사전 설정에 설정된 높이 및 비트율 값이 표시되지 않습니다. 필드가 공백으로 표시됩니다(CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* 상거래의 모든 제품에 대한 사용자 지정 태그를 만들 수 없습니다(CQ-4310682).

* 제품 자산 참조 업데이트로 인해 ProductAssetListener 스레드가 JCR에 대한 커밋을 완료할 때까지 복제 스레드가 대기 상태에 있게 됩니다(NPR-35269).

### 플랫폼 {#platform-6580}

* 탭 없이 Coral Tab 보기 구성 요소를 사용한 다음 Foundation 유효성 검사기를 트리거하면 다음 오류가 발생합니다(NPR-35636).

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 이름에 쉼표가 포함된 노드의 삭제 이벤트에 대해 SCD 전달 복제가 실패합니다(NPR-35191).

* AEM 6.5.7로 업그레이드하면 빌드가 실패합니다. 이유는 이전 버전이나 jackson-core가 uber-jar에 포함되지 않기 때문입니다(GRANITE-33006).

### 사용자 인터페이스 {#ui-6580}

* 자산 콘솔의 폴더에 있는 문서에 대해 카드 보기에서 목록 보기로 전환하는 경우 정렬이 제대로 작동하지 않습니다(NPR-35842).

* 텍스트 구성 요소에 텍스트를 하이퍼링크를 만들면 검색 기능에 적절한 결과가 표시되지 않습니다(NPR-35849).

* 필수로 표시된 숨김 필드에 값을 제공하지 않으면 구성 요소를 저장할 수 없습니다(NPR-35219).

### 통합 {#integrations-6580}

* IMS 테넌트 ID 및 Target 클라이언트 코드에 대해 다른 값을 사용하는 경우 [!DNL Experience Manager]이 [!DNL Adobe Target]과 통합되지 않습니다(NPR-35342).

### 번역 프로젝트 {#translation-6580}

* [!DNL Experience Manager]에서 번역 작업을 내보내거나 가져올 때 문제가 발생합니다(NPR-35259).

### 캠페인 {#campaign-6580}

* Touch UI에서 기본 제공 템플릿을 사용하여 캠페인 페이지를 만들고 페이지 속성 대화 상자에서 이메일 탭을 열면 제목 및 본문 필드에 대한 개인화 변수가 비활성화됩니다(CQ-4312388).

### [!DNL Communities] {#communities-6580}

* 커뮤니티 그룹에 페이지 구조를 추가하면 탐색 표시의 [!UICONTROL 그룹] 제목이 첫 번째 [!UICONTROL 페이지]의 제목으로 변경됩니다(NPR-35803).
* 중재자와 달리, 표준 커뮤니티 구성원은 초안 게시물에 액세스하고 편집할 수 없습니다(NPR-35339).
* 색인화가 완료될 때까지 커뮤니티 사이트를 다운시키는 `DSRPReindexServlet`을(를) 사용하여 액세스 제어 및 서비스 거부가 중단되었습니다(NPR-35591).
* [!UICONTROL 관리자] 필드에서 [!UICONTROL 모든 사용자를 제거해도 실제로 백 엔드에서 제거되지 않습니다(NPR-35592, NPR-35611).]
* 입력한 텍스트가 부분 일치할 때 [!UICONTROL Compose Message] 구성 요소가 결과를 반환하지 않습니다(NPR-35666).

* **[!UICONTROL 태그 추가]**&#x200B;를 선택하여 새 블로그에 태그를 추가하려고 하면 성능이 저하되고 속도가 느려질 수 있습니다. 성능을 향상하려면 [cqTagLucene-0.0.1.zip 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip)를 설치하십시오.

### [!DNL Brand Portal] {#brandportal-6580}

* [!UICONTROL 자산 기여도] 유형 폴더에 구성원을 추가하면 Brand Portal 활성 사용자만 지원되고 그룹이 아니지만 사용자 인터페이스에 [!UICONTROL 사용자 추가 또는 그룹] 캡션이 표시됩니다(NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 는 예정된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜로부터 1주일 후에 추가 기능 패키지를 출시합니다.

**적응형 양식**

* 적응형 양식에 인스턴스가 여러 개 있는 반복 가능한 패널에 반복 가능한 행이 있는 테이블을 삽입하면 테이블이 항상 패널의 첫 번째 인스턴스에 추가됩니다(NPR-35635).

* 적응형 양식에서 한 번 탭 포커스가 CAPTCHA 구성 요소를 확인하면 [!DNL Experience Manager Forms]에 `Provide Captcha phrase to proceed` 오류 메시지가 표시됩니다(NPR-35539).

**대화형 통신**

* 번역된 양식을 제출하면 제출 메시지가 영어로 표시되고 적절한 언어로 번역되지 않습니다(NPR-35808).

* 첨부된 XDP 또는 문서 조각에 숨기기 조건을 포함하는 경우 대화형 커뮤니케이션이 로드되지 않습니다(NPR-35745).

**서신 관리**

* 편지를 편집할 때 조건이 있는 모듈을 로드하는 데 시간이 오래 걸립니다(NPR-35325).

* 편지에 포함되지 않은 왼쪽 탐색 창에서 자산을 선택한 다음 다음 자산을 선택하면 이전에 선택한 자산에서 파란색 강조 표시가 제거되지 않습니다(NPR-35851).

* 편지에서 텍스트 필드를 편집할 때 [!DNL Experience Manager Forms]에 `Text Edit Failed` 오류 메시지가 표시됩니다(CQ-4313770).

**워크플로우**

* iOS용 [!DNL Experience Manager Forms] 모바일 애플리케이션에서 적응형 양식을 열려고 하면 애플리케이션이 중지되어 응답합니다(CQ-4314825).

* HTML 작업 영역의 [!UICONTROL To-do] 탭에 HTML 문자가 표시됩니다(NPR-35298).

**XMLFM**

* 출력 서비스를 사용하여 XML 문서를 생성하는 경우 일부 XML 파일에 대해 `OutputServiceException` 오류가 발생합니다(CQ-4311341, CQ-4313893).

* 글머리 기호의 첫 번째 문자에 위 첨자 속성을 적용하면 글머리 기호 크기가 작아집니다(CQ-4306476).

* 출력 서비스를 사용하여 생성된 PDF forms에 테두리가 포함되지 않습니다(CQ-4312564).

**디자이너**

* [!DNL Experience Manager Forms] Designer에서 XDP 파일을 열면 XDP 파일과 동일한 폴더에 designer.log 파일이 생성됩니다(CQ-4309427, CQ-4310865).

**HTML5 양식**

* [!DNL iOS 14.1 or 14.2] 웹 브라우저의 [!DNL Safari] 웹 브라우저에서 적응형 양식에 확인란을 선택하면 추가 필드가 표시되지 않습니다(NPR-35652).

**Forms 관리**

* XDP 파일을 CRX 저장소에 성공적으로 업로드했음을 나타내는 확인 메시지가 없습니다(NPR-35546).

**문서 보안**

* AdminUI의 [!UICONTROL 정책 편집] 옵션에 대해 여러 문제가 보고되었습니다(NPR-35747).

### Experience Manager 6.5.8.0의 알려진 문제 {#known-issues-6580}

* [!DNL Experience Manager] 인스턴스를 6.5에서 6.5.8.0 버전으로 업그레이드하는 경우 `error.log` 파일에서 `RRD4JReporter` 예외를 볼 수 있습니다. 인스턴스를 다시 시작하여 문제를 해결합니다.

* [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 서비스 팩을 [!DNL Experience Manager] 6.5에 설치하는 경우 자산 사용자 지정 워크플로우 모델(`/var/workflow/models/dam`에서 만들어짐)의 런타임 복사본이 삭제됩니다.
런타임 복사본을 검색하려면 Adobe에서 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사와 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* [!UICONTROL 규칙 정의] 대화 상자를 사용하여 [!UICONTROL 폴더 메타데이터 스키마 Forms 편집기] 및 [!UICONTROL 메타데이터 스키마 Forms 편집기]에서 계단식 규칙을 편집하고 만들 때 문제가 발생하면 Adobe 고객 지원 센터에 문의하십시오. 이미 만들고 저장된 규칙이 예상대로 작동합니다.

* 계층 구조의 한 폴더의 이름이 [!DNL Experience Manager Assets]에서 변경되고 자산이 있는 중첩된 폴더가 [!DNL Brand Portal]에 게시되는 경우 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* [!UICONTROL 연결된 자산 구성] 마법사가 설치 후 404 오류 메시지를 반환하는 경우 패키지 관리자를 사용하여 `cq-remotedam-client-ui-content` 및 `cq-remotedam-client-ui-components` 패키지를 수동으로 다시 설치합니다.

* 6.5.x.x Experience Manager 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target Standard API(IMS 인증)를 사용하여 Experience Manager에 Adobe Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경으로 등록 취소를 완료할 때까지 기다리는 중 시간이 초과되었습니다.

## [!DNL Adobe Experience Manager] 6.5.7.0 {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0은 2019년 4월 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. 서비스 팩은 [!DNL Adobe Experience Manager] 6.5에 설치됩니다.

[!DNL Adobe Experience Manager] 6.5.7.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* 페이지 이동 및 MSM 롤아웃을 비동기 작업으로 수행하면 런타임 성능에 대한 영향을 줄일 수 있습니다.

* 사용자는 카드 및 열 보기에서 디지털 자산을 정렬할 수 있습니다.

* [!DNL Assets] 과  [!DNL Dynamic Media] 에서는 다양한 액세스 가능성이 개선되었습니다. 향상된 기능은 키보드 탐색, 화면 판독기 사용 및 유사한 AT(보조 기술)를 사용할 수 있도록 하는 것과 관련이 있습니다. [[!DNL Assets] 개선 사항](#assets-6570) 및 [[!DNL Dynamic Media] 개선 사항](#dynamic-media-6570)을 참조하십시오.

* [양식 데이터 모델 HTTP 클라이언트 ](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) 구성: 성능을 최적화합니다.

* [레이아웃 모드에서 각 구성 ](../../help/forms/using/resize-using-layout-mode.md#resize-components) 요소에 대한 재설정 옵션 가용성

* [!DNL Experience Manager] 6.5 서비스 팩 7 Forms은 다음 제품의 성능을 향상시킵니다.

   * 적응형 양식을 제출할 때 서버의 필드 값을 확인하는 중입니다.

   * [!DNL Automated Forms Conversion service] 을 사용하여 PDF 양식을 적응형 양식으로 변환

* [!DNL Experience Manager Forms]에서 [!DNL Microsoft SQL Server] 2019를 지원합니다.

* OSGi 배포를 위한 고가용성을 위한 [!DNL Microsoft] SQL Server 2016 Always On 가용성 그룹 지원

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.5으로 업데이트되었습니다.

[!DNL Experience Manager] 6.5.7.0에 도입된 기능 및 개선 사항의 전체 목록은 [6.5 서비스 팩 7](new-features-latest-service-pack.md)의 새로운 기능 을 참조하십시오. [!DNL Adobe Experience Manager] 

다음은 [!DNL Experience Manager] 6.5.7.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6570}

* 페이지에 대한 [!UICONTROL 타임랩] 옵션을 열고 타임라인 측 레일 옵션을 연 채로 [!UICONTROL 사이트] 콘솔로 이동하면 `Failed to Load` 오류가 발생합니다(NPR-34951).

* [!UICONTROL 타임랩] 옵션은 선택한 날짜 및 시간 범위에 대한 이미지를 표시하지 않습니다(NPR-34951).

* 필터가 컨텐츠 조각이 포함된 페이지에서 `getHeader()`을 호출하면 `java.lang.AbstractMethodError` 오류가 발생합니다(NPR-34942).

* 페이지의 경로에 여러 컨텐츠 부분 문자열이 포함되어 있으면 미리 보기가 렌더링되지 않고 버전 비교 기능도 실패합니다(NPR-34740).

* 구성 요소의 `String` 유형 레이블 속성에 대해 숫자 값을 설정하면 구성 요소를 삭제하고 삭제 작업을 취소할 수 있습니다. 그러나 삭제를 취소하면 레이블 속성이 `String`에서 `Long`(NPR-34739)으로 변경됩니다.

* 잠긴 레이아웃이 있는 템플릿을 페이지에 기반으로 경험 조각을 추가할 때 다음 예외가 발생합니다(NPR-34632).

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* 폴더를 이동하면 순회 문제가 발생하고 다음 오류가 발생합니다(NPR-34554).

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 새 자산을 만들고, 게시하고, 새 위치로 이동하면 `Request to complete move operation` 워크플로우가 만들어지고 결과가 중단됨 상태가 됩니다. 새 자산을 업로드하고 `move` 작업을 실행하면 보류 중인 상태로 `Request to complete move operation` 워크플로우가 만들어집니다(NPR-34543).

* [!DNL Experience Manager] 6.5.2 환경에서 [!DNL Target] Standard로 경험 조각을 내보내면 작업 공간 속성을 [!DNL Target] Standard에 사용할 수 없으므로 API 호출이 실패합니다(NPR-34557).

* [!UICONTROL 게시] 옵션이 사라지므로 사용자는 [!UICONTROL 게시 관리] 옵션을 통해 페이지를 게시할 수 없습니다(NPR-34542).

* 텍스트에 일부 스타일을 추가하면 `<div>` 태그가 텍스트에 추가되고 더 이상 텍스트에 스타일을 적용할 수 없습니다(NPR-34531).

* 팝업 메뉴에서 항목을 선택하고 필수 파일을 업데이트하면 다른 메뉴에 빈 필수 필드가 있으므로 대화 상자 값을 저장할 수 없습니다(NPR-34529).

* 사용자 지정 템플릿에서 페이지를 만들고 블루프린트 계층 내에서 이동하면 페이지에서 이전에 삭제된 구성 요소가 Live Copy 계층 내의 페이지에 표시됩니다(NPR-34527).

* 아티클 스타일이 콘텐츠에 적용되면 제거할 수 없습니다(NPR-34486).

* 경험 조각의 모든 라이브 카피 및 사본은 동일한 [!DNL Adobe Target] 오퍼 ID를 가리킵니다(NPR-34469).

* 글머리 기호 목록 항목이 번호 목록 외에 표시됩니다(NPR-34455).

* 소스에 비교 선택 사항이 소스 페이지와 페이지의 편집된 버전 간의 차이를 표시하지 않습니다(NPR-34285).

* 페이지를 삭제하면 버전 관리 세부 사항을 구성할 수 없습니다(NPR-34159).

* 사용자가 [!UICONTROL 선택 항목 열기] 대화 상자 옵션을 선택하면 키보드 포커스가 페이지에 있는 숨겨진 컨트롤로 이동합니다(CQ-4307779, CQ-4293601).

* 작성자에서 게시된 폴더를 이동하면 게시 인스턴스에서 폴더 경로가 그에 따라 업데이트되지 않습니다(CQ-4305144).

* 사용자가 [!UICONTROL 모두 선택] 옵션에서 `Enter` 키를 선택하면 키보드 포커스가 [!UICONTROL 컨트롤 만들기] 옵션으로 이동되지 않습니다(CQ-4293599).

* `Esc` 키를 선택하면 포커스가 상위 컨트롤로 복원되지 않습니다(CQ-4293593, CQ-4293590).

* [!DNL Sites] UI 및 핵심 구성 요소에 대한 WCAG 준수가 개선되었습니다(CQ-4293448).

*  페이지에 대해   확대/축소 및  [!DNL Sites Editor] 확장 기능이 비활성화됩니다(CQ-4282353).

* [오른쪽으로 회전] 옵션을 사용하면 화면 판독기에서 현재 회전 또는 뒤집기 상태에 대해 내레이션이 중지됩니다(CQ-4282128).

* 완료 및 구성 취소 대화 상자 단추에는 많은 탭-스톱(CQ-4274601)이 있습니다.

* 동일한 수준에서 이름이 비슷한 페이지를 이동할 수 없습니다(NPR-35041).

* 지우기 (x) 옵션을 선택한 후 키보드 포커스가 [!UICONTROL 필터] 필드로 이동하지 않습니다(CQ-4293581).

* [!DNL Experience Manager] 6.5.6.0으로 업그레이드하면 상속된 단락 시스템의 동작이 변경되고 제대로 작동하지 않습니다(NPR-35117).

* 키보드 사용자는 [!DNL AEM Sites] 페이지에서 [!UICONTROL Action] 섹션을 선택한 후 탭 포커스를 적절한 순서로 이동할 수 없습니다(CQ-4307786).

* 컨텐츠 조각을 편집할 때 RTE 도구 모음의 링크 대상 메뉴 목록에서 옵션을 선택하면 컨텐츠 조각 작성자 대화 상자가 깜박거리기 시작합니다(CQ-4305532).

* 키보드 사용자는 아래쪽 화살표 키를 사용하여 [!UICONTROL 구성 요소 추가] 드롭다운 목록에서 옵션을 선택할 수 없습니다(CQ-4295097).

* [!DNL Sites] 페이지의 [!UICONTROL Assets] 탭에 있는 달력 메뉴에서 날짜를 선택할 때 탭 포커스가 적절한 순서로 이동하지 않습니다(CQ-4293600).

* 사이트 페이지를 편집할 때 사용할 수 있는 링크 또는 텍스트 옵션을 삭제한 후 탭 포커스가 키보드 사용자의 다음 또는 이전 옵션으로 이동하지 않습니다(CQ-4293597).

* 키보드 사용자는 사용 가능한 옵션을 보고 `Esc` 키를 누른 후 [!UICONTROL 작업] 섹션의 추가 옵션으로 탭 포커스를 다시 이동할 수 없습니다(CQ-4293592).

* [!UICONTROL 편집] 모드에서 이미지에 대해 [!UICONTROL 회전] 옵션을 활성화하면 회전 시간이 남은 대신 탭 포커스가 키보드 사용자에 대한 [!UICONTROL 다시 실행] 옵션으로 이동합니다(CQ-4293587).

* [!UICONTROL 링크 및 작업] 탭에 있는 사용 가능한 [!UICONTROL 선택 항목 열기] 대화 상자에서 탭 포커스가 [!UICONTROL 취소] 옵션 다음에 페이지에 있는 숨겨진 요소로 이동합니다(CQ-4293579).

* 키보드 사용자가 이미지를 편집할 때 [!UICONTROL 완료] 옵션으로 이동한 다음 Enter 키를 누르면 화면 판독기에서 완료 내용이 표시되지 않습니다(CQ-4282351).

* 화면 판독기와 키보드 사용자는 [!UICONTROL 링크 및 작업] 대화 상자에서 사용할 수 있는 위로 이동 및 아래로 이동 옵션을 사용할 수 없습니다(CQ-4281120).

* 키보드 사용자는 [!UICONTROL 속성] 페이지의 닫기(X) 옵션으로 이동한 후 탭 포커스를 복원할 수 없습니다(CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0에서는 다음  [!DNL Assets] 문제를 수정하고 다음 개선 사항을 제공합니다.

* 이 릴리스의 [!DNL Experience Manager Assets]에 있는 액세스 가능성에 대해 다음 개선 사항이 수행됩니다. 자세한 내용은 [!DNL Assets]](/help/assets/accessibility.md)의 [액세서빌러티 기능 을 참조하십시오.

   * 키보드를 사용하여 타임라인을 탐색할 때 `Esc` 키는 포커스를 잃지 않고 [!UICONTROL 모두 표시] 옵션을 축소할 수 있습니다(CQ-4293598).
   * 키보드 탭 키를 사용하여 탐색할 때 추가한 태그에서 마지막 태그를 제거한 후 태그 필드에 포커스가 유지됩니다(NPR-35109).
   * [!DNL Experience Manager] 이제 구성 요소에 화면 판독기에서 사용할 이름, 역할 및 값에 대한 적절한 정보가 포함되어 있습니다(NPR-34255).
   * 유형/크기 콤보 상자, 링크 콤보 상자, 언어 콤보 상자, 텍스트 편집 상자를 삭제하면 키보드 포커스가 다음 또는 이전 사용자 인터페이스 요소나 보다 적절한 사용자 인터페이스 요소로 돌아갑니다(CQ-4293585).
   * 포인터를 옵션 위로 가져가면 선택 및 다운로드와 같은 팁이 나타납니다. 화면 돋보기를 사용하는 사용자는 이러한 팁으로 인해 파일 미리 보기를 볼 수 없습니다. 이제 `Escape` 키를 사용하여 옵션을 제거한 후 포커스를 유지할 수 있습니다. (CQ-4293554).
   * 페이지에 있는 그리드에서 그리드 셀을 선택하면 포커스가 화면에 나타나는 작업 막대로 이동합니다(CQ-4282127).
   * [!DNL Experience Manager] 홈 페이지의 모든 솔루션에 대한 링크에 대한 시각적 단서(밑줄 및 V자 아이콘)가 표시되므로 시각적 사용자는 일반 텍스트와 링크를 구별할 수 있습니다(CQ-4282072).

* [!DNL Assets]에서 다음과 같은 사용자 경험 개선 작업이 수행됩니다.

   * 카드 보기 및 열 보기에서 자산을 정렬할 수 있습니다(NPR-35097).

* 6.5로 업그레이드 후 Assets HTTP API를 사용하여 JSON 파일이 생성되면 파일에 사용된 인코딩에 문제가 발생합니다(NPR-35129).

* 컬렉션을 만들 수 있는 권한이 제공되지 않은 그룹 사용자(컬렉션 만들기 옵션을 사용할 수 없음)는 URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections`에 직접 액세스하여 컬렉션을 만들 수 있습니다(NPR-35115).

* 이름별로 정렬하면 검색된 자산이 대/소문자를 구분하는 방식으로 정렬됩니다. 이렇게 하면 검색 결과에 정렬된 방식으로 표시되는 케이싱을 기반으로 별도의 정렬된 두 개의 목록이 만들어집니다(NPR-35068).

* 편집기에서 컨텐츠 조각을 열면 경고 메시지(`Invalid value specified for a metadata property`)가 오류 로그에 기록됩니다(NPR-35012).

* 관리자 권한이 없는 사용자는 [Experience Manager] 데스크탑 앱을 사용하여 만료된 자산을 편집할 수 있습니다. (NPR-34993).

* 동일한 자산을 자산 사용자 인터페이스에서 드래그하고 새 버전을 만들면 메타데이터의 변경 사항이 지속되지 않습니다(NPR-34940).

* 컬렉션을 편집할 때 사용자는 컬렉션의 제목을 삭제하고 변경 사항을 성공적으로 저장할 수 있습니다(NPR-34889).

* 중복 이미지를 업로드할 때 삭제 옵션이 표시됩니다. 삭제를 선택하면 이미지를 업로드할 수 있습니다. DAM 자산 업데이트 워크플로우가 트리거됩니다(NPR-34744).

* [!DNL Adobe InDesign]과 함께 [!DNL Adobe Asset Link]을 사용하는 경우 검색 결과에 폴더와 컬렉션이 포함되지 않고 자산만 포함됩니다(NPR-34699, CQ-4303666).

* 카드 보기에서 포인터를 가져가면 카드의 빠른 작업에 (자동) 초점이 맞춰져 화면 스크롤이 됩니다(NPR-34514).

* 여러 자산의 속성을 일괄적으로 편집할 때 [!UICONTROL 저장] 옵션을 선택하면 벌크 편집기 보기가 닫히고 기본 [!DNL Assets] 페이지로 리디렉션됩니다. 이 동작은 [!UICONTROL 저장 및 닫기] 옵션의 동작과 동일하며 예상되지 않습니다(NPR-34546).

* 저장 후 스마트 컬렉션에 올바른 사용자 인터페이스 설정이 없습니다. 쿼리가 제대로 저장되지만 인터페이스에 항상 마지막으로 추가된 옵션 설명이 표시됩니다(NPR-34539).

* 자산을 [!DNL Experience Manager]에 추가할 때 네임스페이스가 없는 메타데이터를 가져오지 않습니다(NPR-34530).

* 폴더에서 자산을 드래그하여 이동할 때 사용자 인터페이스에는 [!UICONTROL Lightbox] 및 [!UICONTROL Drop in Collection]에도 옵션이 표시됩니다. 이동 작업이 취소되더라도 사용자 인터페이스에 나머지 두 옵션이 계속 표시됩니다(NPR-34526).

* `%>` 기호가 컬렉션 페이지에 표시됩니다(NPR-34499).

* 열 보기에서 모든 자산이 표시되기 전에 위쪽 및 아래쪽으로 스크롤할 때 [!DNL Assets]에 중복 폴더 및 자산 이름이 표시됩니다(NPR-34464).

* 공개 폴더를 만든 후 즉시 비공개 폴더를 만들면 공용 폴더는 비공개 폴더 설정을 사용합니다(NPR-34415).

* 카드 보기에서 카드는 알파벳순으로 나열되지 않으며 카드를 알파벳순으로 정렬할 수 없습니다(NPR-34234).

* 계단식 규칙을 다시 열면 사용자 인터페이스에서 선택 사항이 유지되지 않습니다(CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* [!DNL Dynamic Media]의 액세스 가능성에 대해 다음 개선 사항이 수행됩니다(CQ-4290306). 자세한 내용은 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)의 [접근성 기능을 참조하십시오.

   * 화면 판독기(JAWS, 내레이터)는 포함 크기 메뉴 옵션에서 메뉴 항목의 이름, 역할 및 상태에 대해 나레이트합니다(CQ-4290927).
   * 사용자는 `Tab` 키를 사용하여 이메일 링크 대화 상자를 탐색할 수 있습니다(CQ-4290926).
   * 비디오 인코딩 프로필을 만드는 워크플로우는 화면 판독기의 향상된 기능을 통해 사용자에게 더 친숙합니다(CQ-4290623, CQ-4290622).
   * `Tab` 키를 사용하여 탐색할 때 포커스가 워크플로우의 적절한 사용자 인터페이스 요소로 이동하여 대화형 비디오를 만듭니다(CQ-4290621, CQ-4290620, CQ-4290619).
   * 웹 표준을 준수하도록 게시 페이지, 자산 편집 페이지, 스마트 자르기 편집 페이지 및 이미지 세트 편집기 페이지가 개선되었습니다. 이제 AT(Assistive Technology) 사용자가 이러한 페이지를 쉽게 탐색하고 이미지 자르기와 같은 작업을 수행할 수 있습니다(CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-4290610, CQ-4290614).
   * 사용자가 키보드를 사용하여 탐색할 수 있도록 뷰어가 개선되었습니다(CQ-4290615).
   * 키보드 및 화면 판독기 사용자는 자르기 기능을 사용할 수 있습니다(CQ-4290609).
   * 키보드 사용자는 핫스팟을 보다 효율적으로 관리할 수 있습니다(CQ-4290604, CQ-4290603).

* 회사 이름과 폴더 이름이 동일한 경우 [!DNL Experience Manager]에서 원격 이미지 세트를 편집할 수 없습니다(NPR-31340).

* 핫스팟을 [!DNL Dynamic Media] 이미지에 추가한 후 또는 이미지를 사용하여 [!DNL Dynamic Media] 비디오 또는 [!DNL Experience Fragment]를 편집한 후 출력을 미리 보기하려고 하면 z-색인 순서가 올바르지 않습니다(CQ-4307267).

* [!DNL Dynamic Media] 혼합 미디어 세트를 다시 처리할 때 동기화가 실패합니다(CQ-4307184).

* 자산이 [!DNL Dynamic Media]에 대한 자동 동기화가 구성된 폴더로 이동되면 자산이 동기화되지 않습니다(CQ-4307122).

* [!DNL Dynamic Media] 비디오가 기본 HTML5 비디오 컨트롤을 사용하여 iOS 장치에서 재생되지 않습니다(CQ-4306977, CQ-4306727).

* SmartCrop이 적용된 이미지를 다운로드할 수 없습니다(CQ-4304558).

* 폴더를 Dynamic Media에 선택적으로 게시할 수 없습니다(CQ-4304526).

* [!DNL Experience Manager]에서 비디오 파일의 게시를 취소해도 구성된 Scene7 배포에서 응용 비디오 세트의 게시를 취소하지 않습니다(CQ-4304405).

* 파노라마 미디어 구성 요소에 파노라마 이미지 자산을 추가하고 페이지를 새로 고치면 `Uncaught ReferenceError: $ is not defined` 오류가 발생합니다(CQ-4302810).

* [!UICONTROL 뷰어 사전 설정 편집기]에서 [!UICONTROL PanasonicImage/PanoricImage_VR] 사전 설정을 편집할 때 `PanoramicView` 구성 요소에서 `PANORAMICVIEW_AUTOROTATE` 수정자 레이블을 사용할 수 없습니다(CQ-4302443).

* 비디오가 MixedMediaSet에서 첫 번째 비디오가 아닌 경우 비디오 캡션이 표시되지 않습니다(CQ-4298161).

* iPhone 모바일 장치의 HTML5 eCatalog 뷰어에서 페이지를 전환하거나 페이지를 전환할 수 없습니다(CQ-4296611).

* 모바일 장치에서 색상 견본을 스크롤할 때 색상 견본은 몇 초 동안 볼 수 있는 영역에서 오른쪽으로 스크롤하여 보기로 다시 스크롤합니다(CQ-4296439).

* 뷰어 사전 설정 기본 레코드가 만들어지면 CSS 및 아트웍이 게시되지 않고 뷰어 사전 설정만 게시됩니다(CQ-4262205).

* 지정된 핫스팟에 대한 경험 조각을 [!UICONTROL 대화형 비디오/이미지] 구성 요소에서 연결하려고 하면 선택한 경험 조각 경로가 표시되지 않습니다. 대신 경로 필드에서 빈 값을 반환합니다(NPR-35146, CQ-4298136).

* IVV 편집기에서 경험 조각을 미리 볼 수 없습니다(CQ-4308560).

* 이미지에 핫스팟을 추가하고 경험 조각을 선택할 때는 경험 조각의 하위 폴더와 변형을 선택할 수 없습니다(CQ-4307455).

* 이미지가 아닌 자산이 업로드 후 게시됨으로 표시되지 않습니다(CQ-4306415).

#### [!DNL Experience Manager] 3D 자산 {#three-d-assets-6570}

* `DAM CQ MIME Type` 서비스에서 잘못된 MIME 유형을 3D 자산에 적용하여 잘못된 렌더링을 만듭니다(NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* Commerce 제품 컬렉션 사용자 인터페이스는 컬렉션 내에 15개 이상의 제품을 나열하지 않습니다(NPR-34502).

### 플랫폼 {#platform-6570}

* HTTPS를 통한 HTTP 세션이 무효화되지 않습니다(NPR-35083).
* 사용자 인터페이스에서 일별 또는 주별 유지 관리 작업을 시작할 때 `NullPointerException`이 반환됩니다(NPR-34953).
* W3C 유효성 검사기는 호환 클라이언트 라이브러리 JavaScript 파일에 대한 경고를 보고합니다(NPR-34898).
* `AudienceOmniSearchHandler` 함수는 더 이상 사용되지 않는 인덱스를 사용합니다(NPR-34870).
* Experience Manager에서 로그아웃해도 쿠키가 지워지지 않습니다(NPR-34743).
* 태그 이름에 특수 문자가 포함된 경우 `TagManager` API의 `findByTitle` 함수가 작동하지 않습니다(NPR-34357).
* 사용자 동기화 패키지를 가져오는 프로세스가 실패합니다(NPR-34399).
* `ariaLabel` 및 `ariaLabelledby` 속성에 대한 지원을 `Coral.Masonry` 구성 요소에 추가했습니다(GRANITE-29962).
* 최신 핵심 구성 요소 패키지를 설치한 후 컨텐츠 조각이 있는 페이지에 대한 Dispatcher 캐시가 새로 고쳐지지 않습니다(CQ-4306788).
* 큰따옴표(`"`)가 있는 현지화된 태그 이름이 사용자 인터페이스에 제대로 표시되지 않습니다(CQ-4305439).

### 사용자 인터페이스 {#ui-6570}

* 구성 요소 속성의 [!UICONTROL 링크] 필드에 지정된 문자열과 일치하지 않는 자동 완성 제안이 표시됩니다(NPR-34865).

* 2일 간에 배포되는 일별 유지 관리 기간을 예약할 때 AEM에 다음 오류 메시지가 표시됩니다(NPR-35280).

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 통합 {#integrations-6570}

* 기존 [!DNL Adobe Launch] 구성을 편집하지 못했습니다(NPR-35045).
* IMS 구성 및 [!DNL Adobe Target Standard] 환경을 사용하는 경우 [!DNL Experience Fragments]을 [!DNL Adobe Target](으)로 내보낼 수 없습니다(NPR-34555).
* [!UICONTROL 만들기] 옵션이 폴더에서 [!UICONTROL 대상] 페이지로 이동할 때 [!UICONTROL 대상] 페이지에 표시됩니다(NPR-35151).

### 슬링 {#sling-6570}

* 기본 로그인 상태 확인은 존재하지 않는 사용자의 자격 증명을 확인합니다(NPR-34686).

### 번역 프로젝트 {#translation-6570}

* [!DNL Experience Manager]에서 번역 프로젝트를 취소하면 취소 요청이 번역 공급자에게 전송되지 않습니다(NPR-34433).

### [!DNL Communities] {#communities-6570}

* 제품의 불공정한 용어 인스턴스는 모두 수락된 동산으로 대체됩니다(NPR-34311).
* [!DNL Google+] 이 소셜 공유 옵션 목록에서 제거됩니다(NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* 사용자 인터페이스가 [!UICONTROL 목록 보기]에서 자산을 선택할 때 응답하지 않습니다(NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 는 예정된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜로부터 1주일 후에 추가 기능 패키지를 출시합니다.

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

**적응형 양식**

* [!DNL Experience Manager] 서비스 팩 6을 적용한 후 클래식 UI를 사용하여 적응형 양식을 편집할 수 없습니다(NPR-35126).

* PDF를 적응형 양식으로 변환할 때 탭 레이아웃의 양식 데이터 모델을 사용하여 중첩된 패널에 대한 값을 설정할 수 없습니다. 또한 코드 편집기를 사용하여 정적 배열에서 라디오 단추 그룹에 대한 값을 동적으로 설정할 때 문제가 발생합니다(NPR-35062).

* 적응형 양식의 텍스트 필드 구성 요소에 일본어 문자를 입력하면 최대 35자 제한보다 많은 문자를 지정할 수 있습니다(NPR-35039).

* 적응형 양식에 양식을 제출한 후 표시되는 **[!UICONTROL 감사]** 페이지에 `owner` 및 `status`과 같이 원하지 않는 매개 변수가 표시됩니다(NPR-34989).

* [!UICONTROL 첨부 파일] 구성 요소에 대한 [!UICONTROL 파일 선택] 대화 상자에 지원되지 않는 파일 형식뿐만 아니라 선택 항목으로 인해 적응형 양식 제출 중에 오류가 발생합니다(NPR-34970).

* 양식 앞에 텍스트가 포함된 [!DNL Experience Manager Sites] 페이지에 적응형 양식을 삽입하면 커서 포커스가 양식 앞에 있는 텍스트 대신 양식으로 직접 이동합니다(NPR-34947).

*  6.2 데이터 XML  [!DNL Experience Manager] 파일을 사용하여 적응형 양식을 미리 채우기 위한 데이터 옵션을 사용하여 미리 보기가 제대로 작동하지 않습니다(NPR-35087).

* 적응형 양식에 대한 데이터 사전을 업데이트할 때 양식이 번역되지 않습니다. 적응형 양식이 캐시된 값을 반환합니다(NPR-34845).

* 캐시 무효화로 인해 조각을 로드하는 데 시간이 오래 걸립니다(NPR-34567).

* 적응형 양식의 화면 판독기에 탭 탐색 기능이 제대로 작동하지 않습니다(NPR-34544).

**서신 관리**

* 부동 유형이 포함된 숫자 데이터를 사용하여 XML 태그의 값을 초안으로 저장할 수 없습니다(NPR-35050).

* ES3에서 자산을 마이그레이션할 때 자산에는 편집할 수 없는 두 가지 기본 조건이 포함됩니다(NPR-34972).

* 편지에서 데이터 사전을 편집하면 [!UICONTROL 빌려준 콘텐츠] 섹션에 유용한 정보 대신 방사 직사각형이 표시됩니다(NPR-34853).

**대화형 통신**

* [!DNL Forms] 추가 기능 패키지를 설치한 후 사용할 수 있는 대화형 커뮤니케이션에 대한 롤아웃 구성 이름은 표준 롤아웃 구성 이름을 복제합니다(NPR-34976).

**문서 보안**

* 새 문서 보안 정책을 저장하면 Forms Experience Manager에 `Relative validity period is required` 오류 메시지가 표시됩니다(NPR-34679).

* 문서 보안에서 PDF 2.0 문서를 보호할 수 없습니다(CQ-4305851).

보안 업데이트에 대한 자세한 내용은 [Experience Manager 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

## [!DNL Adobe Experience Manager] 6.5.6.0 {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 맨 위에 설치할 수 있습니다.

Adobe Experience Manager 6.5.6.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* [!UICONTROL 빠른 게시] 또는 [!UICONTROL 게시 관리] 마법사를 사용하여 [!DNL Experience Manager] 또는 [!DNL Dynamic Media]에 자산을 선택적으로 게시하거나 게시 취소합니다.

* [!DNL Dynamic Media] 사용자 인터페이스를 사용하여 CDN(Content Delivery Network) 캐시 콘텐츠를 무효화합니다.

* 이제 프록시 서버를 통해 Brand Portal에서 Experience Manager 자산에 자산 기여 폴더를 게시하는 것이 지원됩니다.

* 이제 자동 생성된 개인 폴더 그룹이 [!DNL Experience Manager Assets]에서 개인 폴더를 삭제할 때 정리됩니다.

* 비디오 [!UICONTROL 뷰어] 사전 설정 편집기의 수정자에 대한 설명이 [!DNL Dynamic Media]에 업데이트되었습니다.

* [!DNL Dynamic Media] 커넥터의 상태를 반영하도록 새 회사 설정이 제공됩니다.

* `test` 및 `aiprocess`에 대한 기본 옵션은 사용자가 축소판만 만들고 페이지 추출 및 키워드 추출을 건너뛸 수 있도록 이전에 Dynamic Media의 `Rasterize`에서 `Thumbnail`로 업데이트되었습니다.

* [클라이언트에서 적응형 양식 미리 채우기](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [양방향 SSL 구현을 통해 서버의 RESTful API와 양식 데이터 모델 통합](../../help/forms/using/configure-data-sources.md).

* [번역된 적응형 양식 페이지에 대한 캐싱 기능이 개선되었습니다](../../help/forms/using/configure-adaptive-forms-cache.md).

* automated forms conversion 서비스에서 [Adobe Sign 텍스트 태그를 지원합니다](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* [색상 양식을 [!DNL Automated Forms Conversion service]을 사용하여 적응형 양식으로 전환](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)

* SMB 2 및 SMB 3 프로토콜 지원

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.4으로 업데이트되었습니다.

Experience Manager 6.5.6.0에 도입된 기능 및 개선 사항의 전체 목록은 [Adobe Experience Manager 6.5 서비스 팩 6의 새로운 기능](new-features-latest-service-pack.md)을 참조하십시오.

다음은 [!DNL Experience Manager] 6.5.6.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6560}

* [!DNL Sites] 또는 [!DNL Screens]에서 프로젝트를 선택하고 [!UICONTROL 게시물 관리]를 클릭합니다. 사용자 인터페이스 오류로 인해 [!UICONTROL 게시 관리] 마법사를 진행할 수 없습니다. 특히 [!UICONTROL 게시] 옵션이 작동하지 않습니다(NPR-34099).
* [!UICONTROL 상속 취소] 또는 [!UICONTROL 상속 비활성화] 옵션을 선택 취소한 후 iParsys(상속된 단락 시스템)의 위치가 원래 기본 위치로 복귀되지 않습니다(NPR-34097).
* `RolloutConfigManagerFactoryImpl`에서 롤아웃 구성을 로드할 수 없는 경우 누락된 구성을 로드하지 않습니다. 캐시된 구성을 반환합니다(NPR-34092).
* 텍스트 코어 구성 요소에서 소스 HTML 편집 옵션을 사용한 후 `em` 태그의 클래스가 제거됩니다(NPR-34081).
* Experience Manager 6.3.3에서 Experience Manager 6.5.3으로 업그레이드한 후 롤아웃 프로세스가 훨씬 길어지고 시간 초과 오류로 롤아웃이 실패합니다(NPR-34049).
* `htmlwriter`은 속성 값을 인코딩하지 않습니다. XF 마크업에 있는 마크업은 디코딩된 속성 값(즉, `&#34` 대신 `"`)으로 내보내집니다. 내보낸 XF를 사용하는 시각적 경험 작성기의 Target 측에 문제가 발생합니다(NPR-34048).
* [!DNL Experience Manager Sites]에서 페이지를 이동할 때 이유가 있는 버전 생성 오류를 캡처하도록 로깅을 향상시킵니다(NPR-34014).
* [!DNL Rich Text Editor]에서 모든 텍스트가 제거되면 단락 태그도 제거됩니다(NPR-33976).
* `siteadmin` 페이지(클래식 UI의)를 열거나 새로 고치면 `New` 메뉴의 옵션이 비활성화됩니다(NPR-33949).

   ![클래식 UI에서 메뉴가 누락되었다는 문제를 보여주는 스크린샷입니다](assets/33949_missing_menu.png)

* [!DNL Content Fragment] 은 `ContentFragmentUsePojo`에서 실패하므로 `TemplatedResource` 로 사용할 수 없습니다(NPR-33911).
* 동기 및 비동기 이동 작업으로 인해 동시 전송으로 인해 오류가 발생할 수 있습니다. 페이지 이동 작업은 비동기 이동으로만 제한됩니다. 페이지를 동시에 이동할 수 없습니다(NPR-33875).
* [!UICONTROL 작성자] 에서 게시 인스턴스로 컨텐츠를 복제하기 위한 게시 관리 작업이 실패하고 JavaScript 오류가 생성됩니다(NPR-33872).
* 버전을 만들기 위해 여러 페이지 또는 자산을 선택하면 마지막으로 선택한 페이지 또는 자산에 대해서만 새 버전이 만들어집니다(NPR-33866).
* Live Copy가 있는 블루프린트 페이지를 다른 폴더로 이동합니다. 원래 폴더로 이동할 때 오류 없이 이동 작업이 실패합니다(NPR-33864).
* 이동 작업을 사용하여 [!DNL Sites] 콘솔에서 웹 페이지의 이름을 변경하면 마법사의 마지막 단계에서 겹치는 대화 상자가 두 개 표시됩니다(NPR-33831).

   ![이동 대화 상자가 겹치는 NPR-33831 문제를 설명하는 스크린샷입니다](assets/33831_rename_dialog.png)

* 복사에서 [!DNL Adobe Campaign]에 대한 `cq:acLinks` 및 `cq:acUUID` 속성은 복사 및 붙여넣기 작업 중에 제거됩니다(NPR-33794).
* 분리된 상위 Live Copy의 하위 페이지에서 롤아웃을 시도할 때 [!DNL Experience Manager]은(는) null 포인터 예외를 생성합니다(NPR-33676).
* 레이아웃 컨테이너를 복사하여 페이지에 다시 붙여넣으면 레이아웃 컨테이너의 [!DNL RTE] 구성 요소가 표시되지 않습니다. [!DNL RTE] 구성 요소는 편집할 수 없지만 페이지 새로 고침 시 표시됩니다(NPR-33662).
* 서로 다른 중단점(보통 및 큰)에 대한 레이아웃 구성 요소의 크기를 조정할 때 레이아웃이 예상대로 작동하지 않습니다(NPR-33608).
* [!DNL RTE]의 인라인 편집 모드에서 텍스트 구성 요소에 대해 이미지를 드래그하면 작동하지 않습니다(NPR-33602).
* 페이지 이름과 동일한 이름으로 블루프린트 페이지에서 구성 요소를 만들 수 있습니다. 롤아웃 중에 구성 요소의 이름을 바꾸도록 `_msm_moved`이 붙습니다. 구성 요소가 [!UICONTROL 단락 시스템]의 끝으로 이동됩니다(NPR-33535).
* offTime 또는 onTime이 많은 페이지 또는 자산에 설정되면 리소스가 많이 소비되며 시작 및 종료 중에 시스템이 느려집니다(NPR-33482).
* `/content/experience-fragment`에 CRUD 권한이 있는 사용자가 폴더를 삭제할 수 없습니다(NPR-33436).
* [!DNL Experience Fragments] 섹션의 상위 폴더에서 [!UICONTROL Adobe Target 내보내기 형식]에 대한 옵션으로 [!UICONTROL HTML &amp; JSON]을 선택할 수 있습니다. 동일한 속성이 이 상위 폴더의 하위 폴더에 대해 터치 사용 UI에 표시됩니다. 그러나 CRXDE에서는 `cq:adobeTargetExportFormat`에 대해 `html,json` 표시가 아닌 HTML만 표시됩니다(NPR-33423).
* 페이지 별칭에서 게시 또는 게시 취소는 지원되지 않습니다. 그렇지 않은 경우 클레임이 표시되는 옵션을 제거합니다(NPR-33415).
* 특정 태그는 [!DNL Experience Manager]에서 한 위치에서 다른 위치로 이동할 수 있습니다. 또한 이동 전후에 다른 페이지에 적용할 수도 있습니다. 페이지의 속성을 편집할 때 태그가 동일한 경우에도 태그가 편집용으로 표시되지 않습니다(NPR-33353).
* 여러 레이아웃 컨테이너를 포함하는 템플릿에서 레이아웃 컨테이너를 삭제하면 페이지 템플릿이 제대로 렌더링되지 않습니다(NPR-33347).
* 템플릿 편집기에서 `/content/` 아래에 있는 100000 이상 페이지에서 사용하는 템플릿을 삭제하려고 합니다. 오류 메시지 없이 오류가 표시됩니다(NPR-33312).
* `PageRedirectServlets` 은 URL 조각 또는 앵커 뒤에 쿼리 문자열을 하므로 앵커를 사용하는 [!DNL Experience Manager] 페이지로 리디렉션하지 작성자 인스턴스에서 작동하지 않습니다(NPR-34288).
* `/content/campaign` 아래에 브랜드를 만들면 캠페인을 만들 수 없는 구조가 됩니다. [!UICONTROL 브랜드 ] 만들기 옵션은 만들기 옵션이 없으므로  [!UICONTROL 오퍼 및 활동] 을 만들 수 없는 새로 만든 브랜드를   그대로 둡니다(NPR-34113).
* 페이지의 [!DNL Live Copy]을 일시 중단할 수 있으며 상속이 편집기 모드에서 보듯이 중단됩니다. 페이지 속성에서 상속을 나타내는 아이콘이 상속이 존재하며 끊기지 않음을 잘못 나타냅니다(NPR-34017).
* 참조가 많은 페이지를 비동기식으로 이동할 수 없으며 이동 작업이 실패하는 경우가 있습니다(CQ-4297969).
* 작성하는 동안 URL에 `/` 문자가 있는 웹 페이지가 응답하지 않습니다. 작성하는 동안 구성 요소를 추가하면 CPU 사용량이 증가하고 브라우저가 응답을 중지합니다(CQ-4295749).
* 검색 모드에서 NVDA는 유형/크기 메뉴 옵션에서 선택한 값에 내레이션이 적용되지 않습니다. 시각적 포커스가 선택한 요소에 없습니다. 화면 판독기를 사용하는 사용자는 찾아보기 모드를 사용할 수 없습니다(CQ-4294993).
* 웹 페이지를 만들 때 사용자는 [!UICONTROL 컨텐츠 페이지] 템플릿을 선택할 수 있습니다. [!UICONTROL 소셜 미디어] 탭에서 사용자가 [!UICONTROL 기본 XF 변형]을 선택합니다. NVDA 찾아보기 모드에서 경험 조각을 선택하려면 키보드 키를 사용할 수 없습니다(CQ-4292669).
* handlebars 라이브러리를 더 안전한 v4.7.3으로 업데이트했습니다(NPR-34484).
* [!DNL Experience Manager Sites] 구성 요소의 여러 교차 사이트 스크립팅 인스턴스(NPR-33925).
* 새 폴더를 만들 때 폴더 이름 필드는 저장된 교차 사이트 스크립팅에 취약합니다(GRANITE-30094).
* [!UICONTROL  시작] 페이지 및 경로 완료 템플릿의 검색 결과는 교차 사이트 스크립팅에 취약합니다(NPR-33719, NPR-33718).
* 구조화되지 않은 노드에 이진 속성을 만들면 이진 속성 대화 상자에서 교차 사이트 스크립팅이 발생합니다(NPR-33717).
* CRX DE 인터페이스에서 [!UICONTROL 액세스 제어 테스트] 옵션을 사용할 때 크로스 사이트 스크립팅이 수행됩니다(NPR-33716).
* 클라이언트에게 정보를 전송할 때 다양한 구성 요소에 대해 사용자 입력이 적절히 인코딩되지 않습니다(NPR-33695).
* Experience Manager 받은 편지함의 달력 보기에서 교차 사이트 스크립팅(NPR-33545).
* `childrenlist.html` 로 끝나는 URL은 404 응답 대신 HTML 페이지를 표시합니다. 이러한 URL은 교차 사이트 스크립팅에 취약합니다(NPR-33441).


### [!DNL Assets] {#assets-6560}

**Experience Manager Assets의 액세스 가능성이 개선되었습니다**

* 이제 사용자는 키보드 키를 사용하여 [!UICONTROL 참조] 자산 목록의 대화형 사용자 인터페이스 옵션에 액세스하고 해당 옵션에 집중할 수 있습니다(NPR-34115).

* 이제 화면 판독기에서 검색 페이지에서 설명 동작이 의도된 것임을 알려줍니다(NPR-34104).

* 이제 검색 페이지 및 검색 결과 페이지에 화면 판독기 사용자를 더 잘 이해할 수 있도록 더 유용한 제목이 있습니다(NPR-34093).

* 이제 화면 판독기에 자산 [!UICONTROL 속성] 페이지의 [!UICONTROL 기본] 탭에서 선택한 태그를 삭제하는 옵션이 표시됩니다(NPR-33972).

* 이제 목록 보기의 각 행에 있는 요소가 화면 판독기에서 동일한 행의 요소로 표시됩니다(NPR-33932).

* 이제 `Tab` 키를 사용하여 탐색할 때 사용자 포커스가 버전 미리 보기의 닫기 옵션으로 이동합니다(NPR-33863).

* 이제 Omnisearch가 닫힌 후 사용자 포커스가 검색 아이콘으로 이동합니다(NPR-33705).

* 이제 실행 가능한 사용자 인터페이스 옵션에는 키보드 키를 사용하여 탐색할 때 향상된 대비 기능이 있어 시각적 포커스가 더 잘 보입니다. 키보드 사용자는 집중 영역을 식별할 수 있습니다(NPR-33542).

* 이제 키보드를 사용한 드래그 기능이 화면 판독기의 검색 모드에서 [!UICONTROL 메타데이터 스키마 편집기]에서 작동합니다(CQ-4296326).

* 링크 공유 대화 상자의 검색 모드에서 탐색할 때 화면 판독기에서

   * 대화 상자가 로드되는 즉시 테이블 정보에 내레이션이 적용되지 않습니다.

   * 나열된 모든 자동 제안 항목으로 이동할 수 있습니다.

   * [!UICONTROL 이메일 주소 추가/검색]에 대해 표시된 자동 제안에 대해 내레이션이 적용됩니다(CQ-4294232).

* 카드 보기에서 빠른 작업 아이콘을 제거하기 위해 `Esc` 키를 사용하면 마지막 포커스가 있는 항목에서 키보드 포커스를 더 이상 제거할 수 없습니다(CQ-4293554).

* 이제 사용자 인터페이스의 대화형 옵션의 경우 화면 판독기는 아이콘의 리터럴 이름이 아닌 해당 용도를 알려줍니다(CQ-4272943).

* 이제 키보드 포커스가 [!UICONTROL Flyout], [!UICONTROL InlineZoom], [!UICONTROL Shoppable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL ZoomVertical_dark] 및 [!UICONTROL ZoomVertical_light] 및 &lt;a13/options114> 키에서 자산을 탐색할 때 &lt;Tab/> 키 탭으로 성공적으로 이동합니다. [!DNL Dynamic Media]의 ] 뷰어(CQ-4290605).[!UICONTROL 

* [!UICONTROL 이제 ] 키보드 키  를 사용하여 자산 속성 페이지의 저장 및 닫기 옵션에 액세스할 수 있습니다(NPR-34107).

* 이제 로그인 페이지에서 잘못된 사용자 이름 및 암호 조합으로 인한 오류 메시지가 오류가 발생할 때마다 화면 판독기에 표시됩니다(NPR-33722).

* [!DNL Experience Manager] 헤더 섹션에서 검색 모드로 탐색할 때 화면 판독기가 이제

   * [!UICONTROL Omnisearch에서 ]을 검색할 제안을 자동으로 편집했습니다.

   * [!UICONTROL 솔루션], [!UICONTROL 도움말], [!UICONTROL 받은 편지함] 및 [!UICONTROL 사용자] 옵션에 대해 확장되거나 축소된 상태입니다.

   * 사용자가 [!UICONTROL 도움말] 옵션 아래의 [!UICONTROL 도움말] 필드에 검색 문자열을 입력할 때 표시되는 [!UICONTROL 도움말] 상태 메시지를 검색합니다.

   ![헤더의 도움말 메뉴](assets/Help_aem_header.png)

   *그림:  [!UICONTROL 도움말 ] 메뉴를   검색합니다.*

   * [!UICONTROL 사용자] 옵션 아래의 [!UICONTROL 가장 대상] 필드에 잘못된 값을 입력한 경우 오류 메시지가 표시되고 포커스가 텍스트 필드로 올바르게 이동합니다(NPR-33804).

   ![헤더의 사용자 메뉴](assets/User_aem_header.png)

   *그림:  [!UICONTROL 헤더] 의 사용자   메뉴의 asfield 가장*

* 이제 사용자는 내의 키보드를 사용하여 포커스를 변경할 수 있습니다.

   * [!UICONTROL 링크 공유 대화 ] 상자에서 이메일 주소  [!UICONTROL 필드 검색/] 추가.

   * [!UICONTROL 폴더 ] 속성의 권한 탭 [!UICONTROL 의 ] 닫힌 사용자   그룹 아래의 사용자 또는  [!UICONTROL 그룹 ] 필드를 추가합니다(NPR-34452).

**Experience Manager Assets에서 해결된 문제**

[!DNL Adobe Experience Manager] 6.5.6.0에서는  [!DNL Assets] 다음 문제에 대한 수정 사항을 제공합니다.

* 자산의 타임라인에서 주석을 선택하면 강조 표시되지 않습니다(CQ-4302422).

* [!DNL Adobe InDesign] 템플릿을 사용하여 만든 마케팅 자료 자산(예: 브로셔, 플라이어 및 비즈니스 카드)의 미리 보기에는 라인 중단과 단락 나누기가 표시되지 않습니다(NPR-34268).

* 텍스트 추출 및 업로드된 PDF 파일에 대한 전체 텍스트 검색이 작동하지 않습니다(NPR-34164). 이 문제를 해결하려면 서비스 팩 6을 설치한 후 [!DNL sAdobe Experience Manager] 배포를 다시 시작합니다.

* 다중 페이지 자산의 타임라인에는 특정 하위 자산에 대한 주석을 표시하는 대신 타임라인 보기에서 자산을 탐색할 때 모든 하위 자산에 적용된 주석이 표시됩니다(NPR-34100).

* 폴더에 JavaScript, CSS 또는 JSON 파일 형식의 리소스가 포함되어 있는 경우 자산 폴더가 [!UICONTROL 게시 관리] 옵션을 사용하여 게시되지 않습니다(NPR-34090).

* Omnisearch에서 적용된 태그 또는 필터를 선택 취소하거나 제거하여 검색 쿼리를 여러 번 실행함으로써 검색 시간이 늘어납니다(NPR-34078).

* 워크플로우(폴더의 자산)가 진행 중이거나 보류 중일 때 카드 보기에서 워크플로우가 완료되거나 종료될 때까지 페이지가 다시 로드됩니다. 따라서 작성자는 아래로 스크롤해야 하는 폴더에서 해당 자산에서 작업할 수 없습니다(NPR-33986).

* 사용자가 게시된 자산을 새 위치로 이동하는 경우 [!UICONTROL 다시 게시] 옵션이 선택 취소되었더라도 자산이 다시 게시됩니다. 이로 인해 게시 인스턴스에 고립된 많은 자산이 배치됩니다. 그러나 기본 동작은 게시된 자산의 이동 작업이 자동으로 게시 취소됩니다. 이 자산은 작성자가 자산을 이동할 때 [!UICONTROL 다시 게시] 옵션을 선택하면 다시 게시됩니다(NPR-33934).

* 컬렉션의 에셋에 대한 [!UICONTROL 자산 이동] 페이지가 [!UICONTROL 조정/ 다시 게시] 옵션과 같은 모든 HTML 콘텐츠를 로드하지 않습니다. 따라서 사용자가 이동 작업을 완료할 수 없습니다(NPR-33860).

* 자산을 이동하고 이동한 자산의 이름 및 제목에 특수 문자를 추가하면 자산의 새 위치에 동일한 이름의 추가 폴더가 만들어집니다(NPR-33826).

*  다운로드 대화 상자에서 이메일 옵션  을 선택하면 자산에 대한 다운로드   단추가 비활성화됩니다(NPR-33730).

* 벌크 메타데이터 편집과 같은 자산에 대한 벌크 작업을 수행할 때 &#39;Request-URI too long&#39; 오류가 관찰되었습니다(NPR-33723).

* JavaScript 오류가 관찰되었으며, 업로드된 JSON 파일에 값에 공간 또는 특수 문자가 있는 경우 사용자가 [!UICONTROL 폴더 메타데이터 스키마 양식 편집기]에서 [!UICONTROL 드롭다운] 필드에 JSON 경로] 기능을 통해 추가 기능을 사용하여 생성된 선택 사항을 선택하거나 삭제할 수 없습니다(NPR-33712).[!UICONTROL 

* 자산의 정적 표현물은 [!DNL desktop app] 또는 [!DNL Adobe Asset Link]에서 [!UICONTROL 열기] 옵션을 사용하여 자산이 업데이트되고 [!DNL Adobe Experience Manager]에 다시 동기화될 때 업데이트되지 않습니다(CQ-4296279).

* 열 보기에서 자산 집합에 대한 이동 작업도 [!UICONTROL 필터] 옵션을 사용하기 전에 선택한 자산도 이동합니다. [!UICONTROL 필터] 옵션을 사용하면 이전 선택 사항이 선택 취소됩니다(NPR-34018).

* 이름에 특수 문자가 있는 자산의 검색 제안에 특수 문자 앞에 백슬래시가 추가됩니다(NPR-33834).

* [!UICONTROL 폴더 메타데이터 스키마 양식]에 드롭다운에 대한 규칙을 만들 때 사용자는 [!UICONTROL 필드 선택 사항] 열에서 값을 선택할 수 없습니다(CQ-4297530).

* [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 버전을 [!DNL Experience Manager] 6.5에 설치하면 자산 사용자 지정 워크플로우 모델(`/var/workflow/models/dam`에서 만들어짐)의 런타임 복사본이 삭제됩니다(NPR-34532). 런타임 복사본을 검색하려면 HTTP API를 사용하여 워크플로우 모델의 디자인 타임 사본을 런타임 복사본과 동기화합니다.
   `<designModelPath>/jcr:content.generate.json`.

**Dynamic Media에서 해결된 문제**

* 사용자가 비디오 프로필을 만든 후 편집 시 인코딩 설정을 정의하면 비디오 프로필에서 스마트 자르기 설정이 제거됩니다(CQ-4299177).

* 사용자가 자산 세부 사항 페이지에서 사이드 레일 옵션(예: [!UICONTROL 개요], [!UICONTROL 타임라인], [!UICONTROL 뷰어]) 간을 전환할 때 페이지 로드 시 자산 깜박임이 발생합니다(NPR-34235).

* 재처리 작업에서 다음과 같은 문제가 관찰됩니다.

   * 재처리 작업에서 반환된 작업 핸들에 작업 ID가 없습니다.

   * 비디오 로그 파일 이름만 재처리하며 전체 경로가 아닙니다.

   * 재처리 작업에는 자산 유형을 정적으로 설정하는 옵션이 없습니다.

   * `ExcludeFromAVS` 옵션이 제공되지 않습니다(CQ-4298401).

* 이미지 프로필이 여러 종횡비를 갖는 폴더(예: 11)에 추가되는 경우 오류가 발생하여 스마트 자르기 기능이 실패합니다(NPR-34082).

* DAM 자산 업데이트 워크플로우는 사용자가 Dynamic Media Scene7으로 구성된 [!UICONTROL 도구]에서 [!UICONTROL 워크플로우] 탭의 [!UICONTROL 워크플로우 아카이브] 페이지로 스크롤할 때 트리거됩니다(CQ-4299727).[!DNL Adobe Experience Manager]

* [!UICONTROL 뷰어 사전 설정 편집기]의 [!UICONTROL 동작] 탭에 있는 심볼이 현지화되지 않습니다(CQ-4299026).

* 뷰어가 응답형 모드인 경우 기본 보기에는 뷰어에 맞지 않는 잘못된 레이아웃으로 이미지가 표시됩니다(CQ-4298293).

* [!UICONTROL Adobe Experience Manager]에서 이미지 사전 설정에 대한 변경 사항이 Scene7 Publishing System과 동기화되지 않습니다(CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* 자산을 이동할 때 제품의 자산에 대한 링크는 리팩터링되지 않습니다(NPR-34098).

### 플랫폼 {#platform-6560}

* 업그레이드된 Experience Manager 인스턴스에서 진단 도구를 사용하여 로그를 다운로드할 수 없습니다(NPR-34336).
* `cq-wcm-api` foundation 패키지의 특정 버전에 대한 종속성으로 인해 오류가 발생하여 업그레이드가 실패합니다(CQ-4300520).
* 기본 에이전트(게시) 구성에 대한 **[!UICONTROL 연결 시간 초과]** 및 **[!UICONTROL 소켓 시간 초과]** 설정에 대한 기본값이 지정되지 않았습니다(NPR-33707).
* `/etc/map.publish` 아래의 매핑 구성에 대한 업데이트가 사이트 페이지에 반영되지 않습니다(NPR-34015).
* [API 참조 ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) 설명서에는 패키지 설명서가  `com.day.cq.tagging` 포함되지 않습니다(CQ-4295864).

### 사용자 인터페이스 {#ui-6560}

* 오프로딩 브라우저 인터페이스에 모든 작업 항목이 표시되지 않습니다(NPR-34308).
* [구성 브라우저](/help/sites-administering/configurations.md) 인터페이스에 모든 구성이 표시되지 않습니다(NPR-33644).
* 가장할 사용자를 검색할 때 `Esc` 키를 누르면 사용자 목록 대신 **[!UICONTROL User]** 대화 상자가 닫힙니다(NPR-34084).

### 통합 {#integrations-6560}

* 이름이 긴 활동은 [!DNL Adobe Target]과 동기화되지 않습니다(NPR-34254).

* 새 Adobe Launch 구성을 만드는 동안 속성을 선택하면 다음 오류 메시지가 표시됩니다(NPR-33947).

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### 번역 프로젝트 {#translation-6560}

* 사용자의 `authorizableID`에 특수 문자가 포함된 경우 번역 프로젝트가 생성되지 않습니다(NPR-33828).

### 슬링 {#sling-6560}

* 상태 확인 및 패턴 탐지기 기능이 겹칩니다. 결과적으로 히스 검사가 제품에서 제거됩니다(NPR-33928).

### WCM {#wcm-6560}

* 기초 구성 요소 - 페이지에 기초 이미지 구성 요소를 추가하고 이미지를 참조하면 `Undo` 작업이 작동하지 않습니다(NPR-34516).

* 페이지 이동 작업을 사용할 수 없습니다(CQ-4303028).

### [!DNL Communities] {#communities-6560}

* 소셜 미디어에서 게시물을 공유하는 경우 Google+에 더 이상 사용되지 않는 옵션이 표시됩니다(NPR-33877).

* 커뮤니티 구성원이 그룹 템플릿 또는 기타 그룹 기능 설정을 수정할 수 없습니다(NPR-33530).

* 이미지의 하이퍼링크 태그가 포럼 게시물에서 제대로 생성되지 않습니다(NPR-33464).

* 액세스 가능성 오류가 커뮤니티 할당 기능에서 식별됩니다(NPR-33442).

* Admin Console을 통해 추가된 커뮤니티 그룹의 기존 사용자는 커뮤니티 그룹 콘솔에서 수정된 내용에 대한 사용자 목록에서 제거됩니다(NPR-34315).

* `TagFilterServlet`은 잠재적으로 민감한 데이터를 노출합니다(NPR-33868).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

[!DNL Experience Manager Forms] 6.5.6.0 추가 기능 패키지를 설치한 후:

* [!DNL Experience Manager Forms] 인스턴스를 중지합니다.

* `crx-repository\launchpad\ext` 디렉토리에서 `bcpkix-1.51`, `bcmail-1.51` 및 `bcprov-1.51` JAR 파일을 삭제합니다.

* `sling.properties` 파일에서` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` 속성을 삭제합니다.

* [!DNL Experience Manager Forms] 인스턴스를 다시 시작합니다.

**적응형 양식**

* 누락된 적응형 양식 조각이 있는 경우 적응형 양식이 렌더링되지 않습니다(NPR-34302).

* 적응형 양식 필드에 대한 도움말 컨텐츠 설명에 단락 HTML 태그가 표시됩니다(NPR-34116).

* 서버&#x200B;]**속성에서**[!UICONTROL &#x200B;재유효성 검사 속성을 선택하면 적응형 양식이 제출되지 않습니다(NPR-33876).

* **[!UICONTROL REST 엔드포인트에 제출]** 제출 작업이 적응형 양식에 대해 작동하지 않습니다(CQ-4299044).

* 액세스 가능성: 필수 필드에 대한 첨부 파일을 업로드하지 않고 적응형 양식을 제출하려고 하면 포커스가 첨부 파일 필드로 자동 이동하지 않습니다(CQ-4298065).

* 적응형 양식의 테이블에 행을 추가할 때 **[!UICONTROL 맨 위에 추가]** 및 **[!UICONTROL 맨 아래에 추가]** 옵션이 적절한 결과를 표시하지 않습니다(CQ-4297511).

* [!UICONTROL 값 커밋] 스크립트가 잘못 트리거되어 적응형 양식으로 데이터가 손실됩니다(CQ-4296874).

* 현지화된 적응형 양식에 대해 날짜 선택기가 제대로 작동하지 않습니다(NPR-34333).

* 파일 이름에 밑줄 또는 공백이 있으면 파일을 적응형 양식에 첨부할 수 없습니다(CQ-4301001).

* 중첩된 반복 가능한 패널에 상위 패널보다 더 많은 항목이 있으면 중첩된 반복 가능한 패널이 모두 미리 채우지 못합니다(NPR-33666).

* 적응형 양식에는 열려 있는 리소스 확인기가 있습니다. 이로 인해 제출 실패가 발생합니다. 문제가 간헐적으로 발생합니다(CQ-4299407).

* 처음 필드 구성을 열면 속성 아이콘이 표시되지 않습니다(CQ-4296284).

* 사용자는 적응형 양식을 제출할 때 `afPath`, `afSubmissionTime` 및 `signers` 등의 제출 메타데이터를 편집할 수 있습니다. 이 문제를 해결하려면 메타데이터 값이 클라이언트 측의 양식 제출 데이터에서 제거됩니다. 사용자는 `FormSubmitInfo` 개체를 사용하여 서버에서 이러한 값을 검색할 수 있습니다(NPR-33654).

* 사용자 입력은 클라이언트에 정보를 보낼 때 [!DNL Forms] 구성 요소에 대해 적절히 인코딩되지 않습니다(NPR-33611).

**워크플로우**

* 워크플로우 승인자가 첨부 파일을 업로드하면 첨부 파일의 이름이 `undefined`으로 변경됩니다(NPR-33699).

* [!DNL Experience Manager] 워크플로우 삭제 작업이 실패하고 다음 오류 메시지가 표시됩니다(NPR-33575).

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] 양식  [!DNL Windows] 제출 후 용 앱이 응답하지 않습니다(NPR-34409).

* AEM 서비스 팩을 설치하면 항목 **완료** 목록이 링크로 표시되지 않습니다. **To Do** 항목의 텍스트에 HTML 태그가 포함됩니다(NPR-34317).

**대화형 통신**

* 중첩된 반복 가능한 구성 요소가 있는 텍스트 문서 조각을 포함하는 경우 대화형 커뮤니케이션이 저장되지 않습니다(NPR-34095).

**서신 관리**

* 데이터 사전 값을 포함하는 텍스트 문서 조각을 수정하면 에이전트 UI가 응답하지 않습니다(NPR-33930).

* [!DNL Microsoft Word] 문서의 컨텐츠를 편지에서 텍스트 문서 조각에 복사하여 붙여넣으면 형식 문제가 발생합니다(NPR-33536).

**문서 서비스**

* 출력 및 Forms 서비스를 사용하여 XDP 파일에서 PDF 파일을 생성하면 텍스트가 누락되고 텍스트가 중첩됩니다(NPR-34237, CQ-4299331).

* HTML 파일을 PDF로 변환할 때 `MaxReuseCount` 속성을 구성할 수 없습니다(NPR-33470).

* Reader 확장 대화형 기능이 포함된 PDF 파일을 다운로드할 때 [!DNL Adobe Reader] 을 사용하여 PDF 파일에 첨부 파일을 추가할 수 없습니다(NPR-33729).

**문서 보안**

* [!DNL Experience Manager] 서비스 팩을 설치한 후 PDF 파일에 HSM 기반 인증서로 서명 작업을 실행할 수 없습니다(NPR-34310).

**디자이너**

* Designer 버전 6.5.x에서 XForms를 열 수 없습니다(CQ-4295322).

* 디자이너를 열면 시작 화면에 잘못된 연도(CQ-4295289)이 표시됩니다.

* 서버에 [!DNL Acrobat DC]을 설치하면 **[!UICONTROL 양식 배포]** 옵션이 비활성화됩니다(CQ-4296304).

보안 업데이트에 대한 자세한 내용은 [Experience Manager 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 맨 위에 설치할 수 있습니다.

[!DNL Adobe Experience Manager] 6.5.5.0에 도입된 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* CRXDE Lite에 대한 익명 액세스가 허용되지 않습니다. 대신 사용자에게 로그인 화면이 표시됩니다. [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)을 사용하여 개발 을 참조하십시오.

* [!DNL Adobe Experience Manager] 받은 편지함에 표시되는 열 이름을 사용자 지정합니다.

* 페이지 편집기, 코어 구성 요소, RTE 및 관리자 인터페이스와 같은 Experience Manager WCM(웹 컨텐츠 관리)의 다양한 영역에서 액세스 가능성이 개선되었습니다.

* 초안을 [!DNL Interactive Communication](으)로 저장합니다.

* JEE에서 Experience Manager Forms용 [!DNL Oracle WebLogic 12] 지원.

* [!DNL Adobe Experience Manager Assets] 사용자 인터페이스 흐름의 예외 처리가 개선되었습니다.

* Dynamic Media Scene7에 대한 게시 URL을 가져오려면 새로운 방법 `getRemoteAssetPublishURL`이 `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` 인터페이스에 추가됩니다.

* WCAG(Web Content Accessibility Guidelines)를 준수하여 [ ](#assets-6550)액세스 가능성 개선[!DNL Adobe Experience Manager Assets].

* Adobe Experience Manager와 패키지 공유 통합이 제거되었습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.3으로 업데이트되었습니다.

Experience Manager 6.5 서비스 팩 5에 소개된 전체 기능, 주요 특징 및 주요 기능 목록에 대해서는 [Adobe Experience Manager 6.5 서비스 팩 5의 새로운 기능](new-features-latest-service-pack.md) 을 참조하십시오.

다음은 [!DNL Experience Manager] 6.5.5.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites는 해당 별칭에서 페이지를 게시 또는 게시 취소하는 옵션을 제공합니다. 이 옵션이 작동하지 않습니다(NPR-33415).
* 여러 템플릿이 들어 있는 템플릿에서 레이아웃 컨테이너를 삭제하면 템플릿이 올바르게 렌더링되지 않습니다(NPR-33347).
* Experience Manager Sites 페이지가 여러 Live Copy가 있는 큰 컨텐츠 세트의 일부인 경우 페이지 버전 기록 미리 보기가 로드되지 않습니다(NPR-33311).
* 이동 명령을 사용하여 Experience Manager Sites 페이지의 이름을 변경하면 페이지 제목이 업데이트되지 않습니다(NPR-33264).
* 열 보기를 통해 페이지를 이동하면 열이 사라집니다(NPR-33216).
* 언어 복사본에 있는 로컬 구성 요소의 이름이 블루프린트에서 구성 요소의 이름과 동일하고, 구성 요소가 블루프린트에서 롤아웃되면 `_msm_moved` 용어가 로컬 구성 요소의 이름에 추가되지 않습니다(NPR-33208).
* 페이지 리디렉션 서블릿은 ResourceType이 `cq:Page`가 아닌 Sites URL에 .html을 추가합니다(NPR-33176).
* 하위 트리를 붙여넣을 때 해당 하위 페이지를 붙여넣을 것인지 여부를 결정하는 옵션이 없습니다(NPR-33149).
* 구성 요소의 라이브 사용량 결과 수는 49로 제한됩니다(NPR-33058).
* 스키마에 컨텐츠 조각을 기반으로 하고 필수 텍스트 영역 또는 경로 필드를 포함하는 경우 컨텐츠 조각이 저장되지 않습니다(NPR-33007).
* 기본 경험 구성요소 구성 요소를 사용하여 사용자 지정 구성 요소를 만들고 Experience Manager Sites 페이지에서 사용하면 Experience Manager에 사용자 지정 구성 요소에 대한 참조(사용량)를 표시하지 않습니다(NPR-32852).
* 참조 수가 많은 폴더의 이름을 바꾸면 해당 폴더에 대한 많은 참조가 업데이트되지 않습니다(NPR-32765).
* 소스 편집 옵션을 활성화하면 인라인 전체 화면 옵션에는 사용할 수 있지만 리치 텍스트 편집기의 편집 대화 상자와 전체 화면 옵션에는 누락된 상태로 남게 됩니다(NPR-32763).
* 다중 필드가 있고 블루프린트의 페이지 속성에 필수 필드(예: 드롭다운 또는 경로 필드)가 포함되어 있는 경우 이러한 다중 필드가 포함된 페이지가 롤아웃되면 Live Copy의 페이지 속성이 저장되지 않습니다(NPR-32751).
* 화면 판독기에서 제목 구조를 사용하여 페이지를 탐색할 수 없습니다. 또한 구성 요소 탭에 잘못된 레이블이 있습니다(NPR-32648).
* 페이지 매김이 시작되면 경험 조각 선택기가 일부 항목을 로드하지 않습니다(NPR-32605).
* Live Copy를 읽고, 수정하고, 만들고, 삭제할 수 있는 작성자 권한이 취소됩니다. 각 작성자는 블루프린트 내에서 페이지를 이동하기 위해 읽기 및 수정 권한을 명시적으로 제공해야 했습니다(NPR-32550).
* 컨텐츠 작성자가 Adobe Analytics와 통합된 페이지에 대해 시작을 만들지 못했습니다(NPR-32548).
* 사용자가 동기화와 함께 상속을 다시 시작하면 상위 페이지의 Live Copy는 블루프린트와 동기화되지 않고 잘못된 상태를 표시합니다(NPR-32500).
* Experience Manager Sites 편집기 페이지는 로드하는 데 15초 이상 걸립니다(NPR-32413).
* 특정 필드에는 상속 취소 옵션이 표시되지 않습니다(NPR-32362).
* 경험 조각 구성 요소의 경로를 선택하고 선택 대화 상자 열기 확인란을 선택하면 경로 브라우저에서 선택한 경로로 이동되지 않습니다(NPR-32308).
* Experience Manager 6.2에서 Experience Manager 6.5로 업그레이드하는 경우 정적 템플릿의 Parsys 구성 요소가 올바르게 표시되지 않습니다. Parsys 구성 요소의 높이가 0으로 설정되고 이 구성 요소 내에 있는 구성 요소가 표시되지 않습니다(NPR-33663).
* 사용자가 동일한 페이지에서 레이아웃 컨테이너를 복사하고 붙여넣으면 레이아웃 컨테이너의 구성 요소가 표시되지 않습니다(NPR-33648).
* Dispatcher 상태 확인은 로그 파일에 `Invalid cookie header` 경고 메시지를 표시합니다(NPR-33629).
* PreferencesServlet에 XSS가 반영되었습니다(NPR-33438).
* 익명 사용자는 CRXDE Lite 기능에 액세스할 수 있습니다(GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>[!DNL Experience Manager desktop app]의 Windows 사용자는 [데스크탑 앱 버전 2.0.3.2](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html#what-is-new)로 업그레이드하여 [!DNL Adobe Experience Manager 6.5.5.0] 인스턴스의 DAM 저장소에 액세스하는 것이 좋습니다. 데스크탑 앱 버전 2.0.2를 사용하여 [!DNL Adobe Experience Manager] 6.5.5.0 인스턴스에서 DAM 저장소에 액세스할 때 문제가 발생할 수 있습니다.

**Experience Manager Assets의 액세스 가능성이 개선되었습니다**

* 이제 자산의 [!UICONTROL 타임라인] 패널에서 [!UICONTROL 새 버전 만들기]에 있는 버전 설명 [!UICONTROL 만들기]에 대한 클릭 가능한 옵션과 [!UICONTROL 댓글] 목록에 키보드 포커스를 둘 수 있습니다(NPR-33424).

* 이제 키보드 키를 사용하여 [!UICONTROL 보기 설정] 대화 상자에서 자산에 대한 [!UICONTROL 보기 설정] 옵션에 도달하고 설정을 변경할 수 있습니다(NPR-33420).

* 이제 콤보 상자의 목록 상자 팝업(다른 페이지의 여러 필드)에 항목이 화면 판독기에서 알릴 수 있는 옵션 목록으로 표시됩니다(NPR-33516).

* 이제 정렬 가능한 머리글의 정렬 기능(목록 보기, [!UICONTROL 타임라인] 보기 및 [!UICONTROL 게시 관리] 페이지)을 화면 판독기에서 알려주고, 열 헤더의 정렬 컨트롤은 키보드를 사용하여 액세스할 수 있습니다(NPR-32979).

* 이제 클릭 가능한 요소(예: 주석 카드, 버전 업데이트, 콤보 상자, 메뉴의 펼침 아이콘)는 키보드를 사용하여 포커스를 지정하고 작업을 수행할 수 있습니다(NPR-33514).

* 이제 [!UICONTROL 인사이트 보기]의 인사이트 아이콘(사용량, 노출 횟수 및 클릭 수) 기능(또는 작업 목적)을 화면 판독기에서 올바르게 알려줍니다(NPR-33513).

* 이제 키보드를 사용하여 읽기 전용 양식 필드(예: 자산 [!UICONTROL 속성]의 [!UICONTROL 기본] 탭에서 비활성화된 필드)에 포커스를 지정할 수 있습니다.

* 다양한 입력 필드의 레이블은 이제 텍스트 입력 시 사라졌던 자리 표시자 레이블일 뿐만 아니라 영구 레이블(따라서 액세스 가능함)입니다(NPR-33475).

* 이제 다른 제목 수준(예: 페이지 제목 및 섹션 제목)은 화면 판독기 사용자에게 서로 수준의 제목으로 인식됩니다(NPR-33471).

* 이제 키보드를 사용하여 링크 및 옵션(자산 페이지의 헤더 및 확대/축소 옵션, 폴더 탐색)과 같은 대화형 사용자 인터페이스 요소에 액세스할 수 있습니다(NPR-33468, CQ-4271412).

* 이제 [!UICONTROL 게시 관리] 페이지의 [!UICONTROL 옵션], [!UICONTROL 범위] 및 [!UICONTROL 워크플로우] 진행 상태 표시기를 화면 판독기에서 탭 대신 진행 상태 표시기로 올바르게 읽을 수 있습니다(NPR-33416).

* 별점 등급 아이콘 색상(자산 [!UICONTROL 속성] 또는 카드 보기의 [!UICONTROL 고급] 탭에 있는 [!UICONTROL 등급] 섹션처럼)이 적절하게 대비되어 변경되므로 시력이 제한된 사용자와 색상을 인식하지 못하는 사용자가 볼 수 있습니다(NPR-33414).

* 이제 키보드 키(NPR-3397)를 사용하여 자산 세부 정보 페이지의 [!UICONTROL 댓글] 필드 옆에 있는 펼침 위쪽 화살표에 액세스할 수 있습니다(NPR-33397).

* 자산 [!UICONTROL 속성]의 [!UICONTROL 태그] 대화 상자 및 왼쪽 레일 탐색(자산 사용자 인터페이스)의 확장 및 축소 상태가 화면 판독기에 올바르게 표시됩니다(NPR-33396).

* 이제 [!DNL Adobe Experience Manager] Assets에서 검색한 모든 페이지의 제목이 고유합니다(NPR-33343).

* 이제 트리 구조를 탐색할 때 트리 보기 컨트롤의 여러 요소가 화면 판독기에 올바르게 표시됩니다(NPR-33304).

* 이제 키보드 키를 사용하여 자산 세부 사항 페이지의 [!UICONTROL 타임라인] 보기에서 다른 자산 버전에 액세스할 수 있습니다(NPR-33283).

* 이제 검색 기능을 사용할 때 Omnisearch 콤보 상자에 표시되는 검색 제안 이름이 화면 판독기에 표시됩니다(NPR-33280).

* [!UICONTROL 참조 레일]에서 클릭 가능한 요소 및 [!UICONTROL 링크로 이동] 기능이 이제 클릭 가능한 요소로 화면 판독기에 표시됩니다(NPR-33278).

* [!UICONTROL 링크 공유] 대화 상자가 열리면 이 대화 상자의 테이블 구조 정보(예: 행 1, 셀 1, 테이블)가 더 이상 화면 판독기에 표시되지 않습니다(NPR-33268).

* 이제 다양한 콤보 상자 요소(예: 자산 속성의 기본 탭에서 선택 대화 상자를 여는 옵션 및 경로 필드)의 목적이 화면 판독기에 올바르게 표시됩니다(NPR-33235).

* 목록 보기 테이블의 행을 선택할 수 있다는 정보는 키보드 포커스가 화면 판독기 사용자에게 있는 경우 전달됩니다. 포인터가 행을 가리키면 화면 판독기가 정보를 알려줍니다(NPR-33234).

* 이제 [!UICONTROL 속성]의 [!UICONTROL 기본] 탭에 있는 [!UICONTROL 태그] 필드 아래에서 선택한 각 태그를 제거하는 옵션([!UICONTROL x] 있음)에서 화면 판독기에 액세스할 수 있습니다(NPR-33206).

* 이제 화면 판독기 사용자와 정상 시력을 가진 키보드 사용자가 키보드를 사용하여 날짜 선택기에 포커스를 설정하고 작업을 수행할 수 있습니다(NPR-33200).

* 이제 목록 보기와 카드 보기 간에 전환하는 토글이 화면 판독기(보기 조정)에 기능을 올바르게 표시합니다(NPR-33069).

* 이제 왼쪽 레일의 메뉴에 액세스할 수 있습니다. 메뉴를 확장하는 기능과 목적은 화면 판독기에 적절히 표시됩니다(NPR-33068).

* 이제 시각 장애가 있는 화면 판독기 사용자가 목록 상자 및 기타 여러 사용자 인터페이스 요소에 액세스할 수 있으며, 이러한 요소에 대한 다음 정보가 화면 판독기에 표시됩니다(NPR-33040).

   * 양식을 제출하기 전에 요소에 사용자 입력이 필요한지 여부.
   * 요소를 편집할 수 없는지 여부.
   * 위젯을 선택했는지 여부.

* 이제 키보드를 사용하여 필터 사이드바를 여는 옵션에 액세스할 수 있습니다(NPR-32842, CQ-4273018).

* 이제 목록 보기의 열 헤더에 있는 확인란 컨트롤에 액세스할 수 있고, 이 컨트롤을 사용하는 목적이 화면 판독기에 표시됩니다(NPR-32722, NPR-33005).

* 달력 날짜 선택기의 시간(HH) 및 분(mm) 필드에 대한 레이블은 이제 자리 표시자 레이블 대신 영구 레이블로, 사용자가 이러한 필드에 텍스트를 입력할 때 사라지지 않습니다(NPR-32720).

* 이제 벨 아이콘을 클릭하면 표시되는 알림의 링크 텍스트가 화면 판독기 사용자에게 표시되면, 화면 판독기 사용자는 탭을 사용하여 각 링크에 액세스할 수 있습니다(NPR-32645).

* 이제 키보드를 사용하여 [!UICONTROL 인사이트 보기]에서 자산 카드의 [!UICONTROL 선택], [!UICONTROL 다운로드], [!UICONTROL 속성] 및 [!UICONTROL 추가 작업] 옵션에 액세스할 수 있습니다(NPR-32609).

* 화면 판독기에서 키보드를 사용하여 액세스할 때 시각적으로 숨겨진 내용(예: 검색 결과의 헤더 메뉴 막대 컨텐츠 등)이 더 이상 표시되지 않습니다(NPR-32606).

* 이제 일정 날짜 선택기에서 다음 달 및 이전 달로 이동할 컨트롤에 대한 레이블의 용도가 화면 판독기에 표시됩니다(NPR-32604).

* 이제 별 등급 아이콘은 키보드 키를 사용하여 포커스를 설정하고 작업을 수행할 수 있습니다(NPR-32513).

* 이제 탭(볼륨 슬라이더에 포커스 지정) 및 키보드의 화살표 키(볼륨 조정)를 통해 동영상 볼륨을 제어하는 기능에 액세스할 수 있습니다(NPR-32065).

* 파일 크기 필터의 하한([!UICONTROL 부터]) 및 상한([!UICONTROL 끝]) 입력 필드의 용도가 이제 시각 장애가 있는 화면 판독기 사용자에게 표시됩니다(NPR-32064).

* 이제 [!UICONTROL 작성 및 번역] 양식의 [!UICONTROL 언어] 메뉴에서 검색 모드로 화면 판독기에 액세스할 수 있습니다(CQ-4293906).

* 이제 다음과 같은 향상된 기능을 통해 [!UICONTROL 참조] 패널에 액세스할 수 있습니다(NPR-33261, CQ-4293798).

   * 검색 모드에서 화면 판독기 포커스는 더 이상 [!UICONTROL 사이트 참조], [!UICONTROL 자산 참조], [!UICONTROL 사본] 및 [!UICONTROL 참조 양식] 섹션에 숨겨진 여러 줄 편집 필드로 이동하지 않습니다.

   * 이제 화면 판독기에 [!UICONTROL 사이트 참조] 및 [!UICONTROL 언어 복사]의 역할이 표시됩니다 .

   * 검색 모드에서 화면 판독기의 포커스는 의미 있는 시퀀스에서 여러 요소로 이동합니다.

* 이제 키보드를 사용하여 [!UICONTROL 메타데이터 스키마 편집기] 페이지와 해당 요소에 액세스할 수 있으며, 이러한 페이지는 화면 판독기에 친숙합니다(CQ-4290962, CQ-4272953).

* 선택한 태그를 제거하는 `X` 기호의 용도는 이제 선택한 태그의 수와 함께 화면 판독기에서 알려줍니다(CQ-4273017).

* 화면 판독기를 사용하는 시각 장애 사용자에 대한 혼동을 방지하기 위해 이제 화면 판독기에서 장식 아이콘 및 이미지를 무시합니다(CQ-4272944).

**Experience Manager Assets에서 해결된 문제**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets은 다음 문제에 대한 수정 사항을 제공합니다.

* 컬렉션의 에셋에 대한 [!UICONTROL 워크플로우 만들기] 대화 상자에서 [!UICONTROL 시작] 옵션이 비활성화되어 워크플로우가 트리거되지 않습니다(NPR-32471).

* 메타데이터 스키마에서 계단식 팝업을 사용할 때 동안 하위 드롭다운에서 아포스트로피가 포함된 드롭다운 옵션 선택 및 저장 시 선택한 아포스트로피 옵션은 자산 [!UICONTROL 속성]을 다시 열면 사라집니다(NPR-32649).

* [!UICONTROL 자산 통찰력 동기화 작업] 이 다음 항목으로 이동하는 대신 잘못된 항목(Analytics 쪽)이 나타나면 중지되고 실패합니다(NPR-32674).

* 파노라마 뷰어의 모바일 브라우저에서 기본적으로 모션 센서가 비활성화되어 있으므로 자이로스코프가 작동하지 않습니다(CQ-4272937).

* 6.5.1에 6.5.3을 설치를 할 때 [!UICONTROL 연결된 자산 구성] 마법사가 404 오류로 작동하지 않습니다(NPR-32730).

* XMP 원본에 쓰기 절차 중에 모든 사용자 지정 네임스페이스 메타데이터 속성은 구성된 네임스페이스 접두어와 반대로 사용자 지정 네임스페이스 접두어를 ns2로 변경합니다(NPR-32748).

* 지연 로드는 트리거되지 않으며 알림 받은 편지함에서 작업을 검토하도록 선택할 때 100개의 자산만 표시됩니다(NPR-32750).

* `NullPointerException`은 새로 생성된 사용자 프로필에서 노드 기본 설정이 누락되어 관찰되었습니다(SAML/SSO). 이 오류로 인해 새로 로그인한 사용자가 [!DNL Adobe Experience Manager Stock] 통합을 사용할 수 없습니다(NPR-32777).

* 10,000개 이상의 자산이 포함된 스마트 컬렉션을 열 때 순회 경고가 로그에 관찰됩니다(NPR-32980).

* Dynamic Media Scene 7 런타임 모드에서 작동 중인 [!DNL Adobe Experience Manager]에서 자산을 한 폴더에서 다른 폴더로 이동할 때 자산 이름이 소문자로 변경됩니다(NPR-32995).

* 검색 결과에서 해당 속성으로 이동한 다음 검색 결과로 돌아가 삭제한 후 검색된 자산을 삭제할 수 없습니다(NPR-32998).

* [!UICONTROL 다음] 옵션은 [!UICONTROL 자산 이동] 인터페이스에서 대상 폴더를 선택할 때 비활성화됩니다(NPR-33356).

* [!UICONTROL 다음] 옵션이 상위 노드(단일 하위 폴더가 표시되는 경우)를 선택한 다음 하위 폴더를 선택할 때 활성화되지 않습니다(NPR-33275).

* AAL(Adobe Asset Link)에서 체크인 및 체크아웃 권한은 삭제 권한이 있는 사용자에게 읽기, 만들기 또는 수정과 같은 다른 권한이 부여되더라도 비활성화됩니다(NPR-33272).

* 스마트 자르기 렌디션은 자산 다운로드 대화 상자에서 사용할 수 없습니다(NPR-33167).

* 스마트 자르기 프로필이 있는 폴더에서 PDF에 대한 렌디션 레일을 열 때 로그에 예외가 관찰됩니다(CQ-4294201).

* Experience Manager의 Dynamic Media Scene7 실행 모드에서 기본적으로 [!UICONTROL Dynamic Media 동기화 모드]가 비활성화된 경우 이미지 사전 설정이 게시되지 않습니다(CQ-4294200).

* 벌크 업로드 중 자산 처리가 중단되고 워크플로우 인스턴스에 DAM 업데이트 자산의 중단 인스턴스가 표시됩니다(CQ-4293916).

* Experience Manager에서 Dynamic Media 구성 만들기가 작동하지만 사용자 인터페이스에서 저장을 선택하면 아무 일도 발생하지 않습니다(CQ-4292442).

* Safari/Mac에서 F4V 비디오 자산 미리 보기가 점진적 재생에서 작동하지 않습니다(CQ-4289844).

* 이름에 점 `.` 문자가 있는 상위 폴더의 자산을 스마트 자르기하면 추가 폴더가 만들어집니다(CQ-4289337).

* 썸네일이 깨지고 비디오가 복사되면 비디오 처리 배너가 표시되지 않습니다(CQ-4284125).

* 빈 카메라 보기가 있는 일부 모델의 경우 Firefox에서 차원 뷰어에 빈 썸네일이 잘못 표시됩니다(CQ-4283447).

* 6.5.5.0에서 해결된 성능 문제는 다음과 같습니다(CQ-4279206).

   * 큰 바이너리를 Dynamic Media 이미지 처리 서버로 업로드하는 데 시간이 너무 오래 걸립니다.

   * Dynamic Media Scene7 아키텍처로 인해 Experience Manager에서 축소판 생성 시간이 늘어납니다.

* 자산 수가 많은 고객의 경우 Dynamic Media Scene7 마이그레이션 문제가 발생합니다(CQ-4279206).

* `setVideo`를 사용하는 경우 비디오 360 뷰어의 레이아웃이 끊어지고 `video= modifier` 사용 시 비디오가 아래로 이동합니다(CQ-4263201).

* Experience Manager SDL 패키지를 설치하는 동안 오류 메시지가 표시됩니다(NPR-33175).

* Experience Manager의 SSRF 취약성(NPR-33435).

### 플랫폼 {#platform-6550}

* `sling:match` 맵 항목이 `/etc/maps`에 작성되지 않으면 [!DNL Sling] 필터가 호출되지 않습니다(NPR-33362).
* [!DNL Apache Lucene]의 세그먼트 문제로 인해 Experience Manager에서 충돌이 발생합니다(NPR-32988).
* Experience Manager uberjar 파일에 [!DNL Jackson] 코어 패키지가 없습니다(NPR-32848).
* CRXDE Lite는 노드의 `jcr:primaryType` 속성에 대한 읽기 권한이 없는 사용자에 대한 컨텐츠를 로드하지 않습니다(NPR-32611).
* [!DNL Granite] 유지 관리 작업 스케줄러가 Experience Manager 배포 시 너무 자주 다시 초기화됩니다(CQ-4294627).
* SQL 쿼리가 오래 실행되면(예: 7시간) Experience Manager가 응답하지 않습니다(NPR-33044).

### 사용자 인터페이스 {#ui-6550}

* 라디오 단추 선택이 다중 필드에서 지속되지 않습니다(NPR-33309).
* 목록 보기에서 레이지 로딩 제한이 작동하지 않습니다(NPR-33124).
* 일치하는 항목이 없으면 Omnisearch 결과 페이지에 메시지가 표시되지 않습니다(NPR-32974).
* Omnisearch 필터는 선택한 위치를 무시하고 `/content` 노드 아래에 모든 일치 항목을 반환합니다(NPR-32849).

### 통합 {#integrations-6550}

* Adobe Target 구성 요소가 있는 페이지가 게시되면 내부 캐시가 지워집니다(NPR-33162).
* Adobe Target과의 통합이 [!DNL Windows Internet Explorer] 11에서 작동하지 않습니다(NPR-33111).
* Adobe Target을 구성할 때 [!UICONTROL 회사] 및 [!UICONTROL 보고서 세트] 필드가 보고 소스 선택 시 표시되지 않습니다(NPR-32502).
* [!DNL Adobe I/O]을 사용하여 [!DNL Experience Fragments]을 내보낼 때 소스 제품과 같은 메타 데이터가 Adobe Target으로 내보내지지 않습니다(NPR-32159).
* 로컬 Experience Manager 관리 그룹의 승인된 IMS 사용자는 IMS 구성을 만들거나 수정할 수 없습니다(NPR-33045).
* Adobe Launch 구성 페이지에 모든 레코드가 표시되지 않습니다(NPR-33011).
* 컨텐츠 작성자 그룹의 사용자는 JavaScript 오류로 인해 Adobe Target 구성 요소의 속성을 편집할 수 없습니다(NPR-32996).
* JSON에 대한 교차 사이트 스크립팅(NPR-32744).

### 번역 프로젝트 {#translation-6550}

* 번역된 태그는 타사 번역 서비스에서 Experience Manager로 가져올 수 없습니다(NPR-33154).
* 번역 구성 페이지에는 변환에 사용한 것과 다른 잘못된 번역 공급자가 표시됩니다(NPR-32971).
* 기존 번역 프로젝트에 경험 조각 폴더를 추가하면 새 프로젝트가 만들어집니다(NPR-32843).
* 번역 작업 실행 시 로그에 `NullPointerException` 오류가 표시됩니다(NPR-32628).

### WCM {#wcm-6550}

* 페이지 편집기 - [!DNL Sites] 페이지 편집기에서 키보드 전용 사용자가 헤더에서 사용할 수 있는 모든 옵션을 통해 탭 포커스를 이동하는 대신 기본 컨텐츠로 건너뛸 수 없습니다(CQ-4293883).
* 페이지 편집기 - 잘 구성 요소를 사용하고 저장된 데이터를 포함하는 패널은 [!DNL Chrome] 및 [!DNL Firefox] 버전 업데이트로 인해 표시되지 않습니다(CQ-4292995).
* MSM - 페이지에서 구성 요소를 삭제해도 페이지의 게시된 버전에서 구성 요소가 삭제되지 않습니다(CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* [!DNL Brand Portal]에서 게시된 메타데이터 스키마를 제거하면 오류가 발생합니다(CQ-4292063).
* 관리자가 Adobe 개발자 콘솔을 통해 Brand Portal로 [!DNL Experience Manager Assets] 6.5.4를 구성하는 경우 [!DNL Brand Portal] 사용자는 기여 폴더의 자산을 [!DNL Brand Portal]에서 [!DNL Experience Manager]에 게시할 수 없습니다(NPR-33046).
* 충돌을 일으키는 상위 폴더가 중복 복제됩니다(NPR-33001).

### [!DNL Communities] {#communities-6550}

* 빠른 편집 메뉴 옵션을 사용하여 중재 콘솔에서 카드를 삭제할 수 없습니다(NPR-33117).
* [!UICONTROL 활동 스트림] 페이지 액세스 시 오류가 발생합니다(NPR-33146).
* 작성자 인스턴스에서 삭제된 그룹은 일부 게시 인스턴스에서 제거되지 않습니다(NPR-33199).
* 작성자는 새 그룹을 만든 후 [!DNL Internet Explorer] 11의 [!UICONTROL 커뮤니티 그룹] 섹션으로 리디렉션되지 않습니다(NPR-33205).
* Experience Manager 받은 편지함의 메시지에 액세스해도 메시지의 상태가 읽음으로 변경되지 않습니다(NPR-32764).
* [!DNL Communities] 그룹을 편집하고 썸네일 이미지를 변경해도 그룹 썸네일 이미지가 업데이트되지 않습니다(NPR-32599). 
* 사용자가 커뮤니티의 다른 사용자에게 이메일을 보낼 수 없습니다(NPR-32598).
* 사용자가 페이지를 새로 고칠 때까지 제출된 블로그가 표시되지 않습니다(NPR-32391).
* UGC(사용자 생성 컨텐츠)의 알림 및 구독 버전을 만드는 동안 소스 페이지의 잘못된 ID가 저장됩니다(CQ-4279355, CQ-4289703).
* 크로스 사이트 스크립팅 문제(NPR-33203).

### 워크플로우 {#workflow-6550}

* 왼쪽 레일의 [!UICONTROL 타임라인] 옵션을 로드하는 데 예상보다 시간이 더 걸립니다(NPR-32851).
* Experience Manager 인스턴스를 다시 시작하면 컬렉션에 대한 검토 작업 이메일에 잘못된 페이로드 링크가 포함되어 있습니다(NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager 서비스 팩에는 [!DNL Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 AEM Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

* 통신 관리: 대상 영역의 자산 순서는 편지를 제출한 후 섞입니다(NPR-33359, NPR-33153).
* 적응형 양식: 사용자가 적응형 양식을 편집할 때 [!UICONTROL 페이지 정보] 메뉴에서 사용할 수 있는 [!UICONTROL 워크플로우 시작] 옵션이 작동하지 않습니다(NPR-33004).
* 적응형 양식: 사용자가 둘 이상의 첨부 파일이 있는 적응형 양식을 저장할 수 없습니다(NPR-32997).
* 적응형 양식: 적응형 양식의 패널 레이아웃을 변경하면 오류가 발생합니다(CQ-4293880).
* 적응형 양식: 적응형 양식 사전의 문자열에 새 줄이 있으면 사전에 `&#xa;` 문자가 추가됩니다(NPR-33266).
* 적응형 양식 액세스 가능성: 사용자가 적응형 양식을 HTML 양식으로 미리 볼 때 [!UICONTROL 스크리블 서명] 필드는 탭 포커스를 유지할 수 없습니다(NPR-33159).
* 적응형 양식 액세스 가능성: 적응형 양식 제출 시 표시되는 오류 메시지는 `aria-describedBy` 속성에 연결되지 않습니다(NPR-33071).
* 적응형 양식 액세스 가능성: 적응형 양식에 필수로 표시된 필드에는 ARIA 액세스 가능성 스키마의 필수 속성이 True로 설정되어 있지 않습니다(NPR-33070).
* PDFG 서비스: 사용자가 텍스트 파일을 PDF로 변환하면 일본어 문자가 올바르게 렌더링되지 않습니다(NPR-33238).
* PDFG 서비스: `CreatePDF` 작업에서 PDF 파일을 PDF OCR 형식으로 변환하지 못했습니다(NPR-32994).
* PDFG 서비스: [!DNL OpenOffice] 문서의 200번째 인스턴스에 대해 PDF를 변환할 수 없습니다(NPR-32766). 
* 백엔드 통합: 잘못된 비활성 상태로 인해 새로 고침 토큰이 만료되므로 양식 데이터 모델 요청이 실패합니다(NPR-33169).
* 디자이너: 화면 판독기는 XDP 파일에 정의된 사용자 지정 탭 순서 대신 기본 지리적 순서에 따라 탭 순서를 실행합니다(NPR-32160).
* 디자이너: 태그 지정 옵션이 활성화된 경우 생성된 PDF 출력에서 하위 양식 테두리가 사라집니다(NPR-32778).
* GuideSOMProviderServlet과 함께 저장된 XSS(NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 맨 위에 설치할 수 있습니다.

Adobe Experience Manager 6.5.4.0에서 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* 이제 Adobe Experience Manager Assets은 [!DNL Adobe I/O] 콘솔을 통해 Brand Portal으로 구성됩니다.

* 이제 Adobe Experience Manager Forms 워크플로우에서 새로운 [인쇄 가능한 출력 생성](../forms/using/aem-forms-workflow-step-reference.md) 단계를 사용할 수 있습니다.

* 적용형 양식 및 대화형 커뮤니케이션용 레이아웃 모드에 대한 [다중 열을 지원](../forms/using/resize-using-layout-mode.md)합니다.

* HTML5 양식의 [리치 텍스트](../forms/using/designing-form-template.md)를 지원합니다.

* Experience Manager Assets의 [액세스 가능성이 개선](new-features-latest-service-pack.md#accessibility-enhancements)되었습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.8으로 업데이트되었습니다.

* 이제 선택적 컨텐츠 하위 트리를 `content/dam`에서 사용하는 대신 *Dynamic Media - Scene7 모드*&#x200B;로 동기화할 수 있습니다.

* 이제 SOAP 웹 서비스와 양식 데이터 모델 통합을 통해 요소에 대한 선택 그룹 또는 속성을 지원합니다.

* 이제 SOAP 입력 또는 출력 및 복잡한 데이터 구조가 Dynamic Group 대체를 지원합니다.

최신 서비스 팩에 포함된 기능 및 주요 특징 의 전체 목록을 살펴보려면 [Adobe Experience Manager 6.5 서비스 팩의 새로운 기능](new-features-latest-service-pack.md)을 참조하십시오.

### 사이트 {#sites-fixes}

* Adobe Experience Manager 사이트 페이지의 URL에 콜론(`:`) 또는 백분율 기호(`%`)가 포함되어 있으면 브라우저가 응답을 중단하고 CPU 사용 스파이크(NPR-32369, NPR-31918)가 발생합니다.

* Experience Manager Sites 페이지를 열어 편집하고 구성 요소를 복사하면 일부 자리 표시자에 대해 붙여넣기 작업을 사용할 수 없습니다(NPR-32317).

* 게시 관리 마법사가 열리면 코어 구성 요소에 연결된 경험 구성 요소가 게시된 참조 목록에 표시되지 않습니다(NPR-32233).

* Touch UI의 Live Copy 개요는 클래식 UI보다 렌더링하는 데 훨씬 시간이 오래 걸립니다(NPR-32149).

* 서버 시간과 컴퓨터 시간이 다른 시간대에 있는 경우 예약된 게시 시간은 Touch UI에 서버 시간을 표시하지만 클래식 UI에서는 시스템 시간이 표시됩니다(NPR-32077).

* Experience Manager Sites에서 URL에 접미사가 붙은 페이지를 열지 못합니다(NPR-32072).

* 사용자가 컨텐츠 조각을 편집하면 삭제된 컨텐츠 조각의 변형이 복원됩니다(NPR-32062).

* 사용자는 필수 필드에 정보를 제공하지 않고 컨텐츠 조각을 저장할 수 있습니다(NPR-31988).

* kernel.js와 ui.j는 사전 컴파일되거나 캐시되지 않습니다. 이로 인해 페이지 렌더링 시간이 추가로 발생합니다(NPR-31891).

* PageEventAuditListener가 활성화되어 있으면 커밋 큐의 길이가 늘어납니다. 벌크 게시, 탐색, 벌크 자산 이동과 같은 많은 작업 성능에 영향을 줍니다(NPR-31890).

* 경험 구성 요소를 드래그할 때 응답 시간이 오래 걸립니다(NPR-31878).

* 응답형 격자의 자리 표시자에서 구성 요소를 여기로 드래그하십시오. 옵션을 선택하면 GET 요청이 전송되고 HTTP 403 오류가 발생합니다(NPR-31845).

* 동일한 폴더 내에서 컨텐츠를 이동할 때 페이지 이동 옵션이 비활성화됩니다(NPR-31840).

* 편집 가능한 템플릿 구조 모드에서 레이아웃 컨테이너의 허용된 구성 요소 목록에 잘못된 결과가 표시됩니다. 디자인 대화 상자의 구성 요소만 레이아웃 컨테이너에 표시됩니다(NPR-31816).

* 페이지에 사용자에 대한 읽기 전용 권한이 있으면 속성 열기 옵션이 sites.html에 표시되지만 editor.html에는 표시되지 않습니다(NPR-31770).

* 사용자가 만들기 버튼을 클릭하면 페이지 옵션을 사용할 수 없습니다(NPR-31756).

* Adobe Campaign에서 OOTB(기본 제공) 디자인 가져오기 구성 요소가 포함된 캠페인을 동기화할 수 없습니다(NPR-31728).

* 글머리 기호 목록을 번호 매기기 목록으로 변경하려고 하면 목록의 처음 두 항목만 변경됩니다(NPR-31636).

* 페이지가 작성되지 않은 경우 하위 노드를 선택하면 선택 대화 상자에 여전히 초기 노드가 표시됩니다. 페이지가 작성된 경우 사용자가 찾아보기를 클릭하면 페이지가 작성된 노드 대신 루트 노드로 리디렉션됩니다(NPR-31618).

* 받은 편지함 사용자 지정 워크플로에서 구성 보기 대화 상자가 제대로 작동하지 않습니다(NPR-32503 및 NPR-32492).

* 받은 편지함을 사용하여 워크플로우 정보를 보는 동안 오류 메시지가 표시됩니다(CQ-4282168).

### 자산 {#assets-6540-enhancements}

* 자산 수집 페이지에서 워크플로우를 트리거하는 버튼이 비활성화됩니다(NPR-32471).

* Dynamic Media Scene7 구성을 사용하여 Experience Manager에서 자산을 폴더 간에 이동하는 동안 이름이 없는 폴더가 SPS(Scene7 Publishing System)에 생성됩니다(NPR-32440).

* 게시된 자산이 들어 있는 폴더로 모든 자산을 이동시키는 작업이 오류로 실패합니다(NPR-32366).

* ${extension}에서 자산의 렌디션이 생성되지 않습니다(NPR-32294).

* 버전 기록 URL은 자산 속성 페이지의 참조자 필드 아래에 표시됩니다(NPR-31889).

* DAM에서 다운로드한 ZIP 파일은 WinZip을 사용하여 열 수 없습니다(NPR-32293).

* 폴더 설정을 열어 폴더 제목이나 축소판 이미지를 변경한 다음 저장하면 폴더의 원래 권한이 업데이트됩니다(NPR-32292).

* 활성화가 예약된 달력 아이콘이 이후 날짜 및 시간에 대해 예약된 자산의 상태 열(DAM 자산 목록의 클래식 UI에 있음)에 표시되지 않습니다(NPR-32291).

* 코드 조각 템플릿을 사용하여 코드 조각을 만들면 코드 조각 만들기 프로세스 중에 컬렉션 검색 시 오류가 발생합니다(NPR-32290).

* 검색 필터에서 여러 태그를 선택하면 여러 검색 쿼리가 실행됩니다(NPR-32143).

* 파일 이름이 50자를 초과하는 자산을 업로드하면 Experience Manager Assets UI에 잘린 파일 이름이 표시됩니다(NPR-32054).

* Adobe Stock에서 확인란 트리의 수준 2 확인란을 선택한 경우 첫 번째와 두 번째 확인란의 선택을 취소하면 필터 패널의 모든 확인란이 지워집니다(NPR-31919).

* Omnisearch 패싯을 사용한 파일 및 폴더를 검색하면 예외가 발생합니다(NPR-31872).

* 종속성 규칙이 해당 메타데이터 스키마 양식에 설정된 경우 필수 필드를 선택하면 메타데이터 편집기의 필수 필드 선택을 위한 필드 강조 표시가 제거되지 않습니다(NPR-31834).

* 태그 계층 구조에서 리프 수준 태그의 전체 이름이 자산 속성 페이지에 표시되지 않습니다(NPR-31820).

* Safari 브라우저의 자산 속성 페이지에서 뒤로 명령을 사용하면 오류가 발생합니다(NPR-31753).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 사용자의 스크롤 위치가 손실됩니다(NPR-31307).

* Dynamic Media Scene7 실행 모드에서 실행되는 Experience Manager의 대상 컬렉션 및 렌디션 추가 버튼 이외의 작업 버튼이 PDF 에셋의 에셋 세부 정보 페이지에 표시되지 않습니다(CQ-4286705).

* Scene7의 일괄 업로드 프로세스를 통해 자산을 처리하는 데 시간이 너무 오래 걸립니다(CQ-4286445).

* 사용자가 Dynamic Media 클라이언트의 설정 편집기에서 변경하지 않은 경우 저장 버튼이 원격 세트를 가져오지 않습니다(CQ-4285690).

* 지원되는 3D 모델을 Experience Manager로 수집할 때 3D 자산 축소판이 도움이 되지 않습니다(CQ-4283701).

* 스마트 자르기 비디오 뷰어 사전 설정이 처리되지 않은 상태로 사전 설정 이름과 함께 배너 텍스트에 두 번 표시됩니다(CQ-4283517).

* 3D Viewer에서 업로드된 3D 모델을 미리 보기했을 때 모델의 잘못된 컨테이너 높이가 자산 세부 정보 페이지에서 확인되었습니다(CQ-4283309).

* 캐러셀 편집기가 Experience Manager Dynamic Media 하이브리드 모드로 IE 11에서 열리지 않습니다(CQ-425590).

* Chrome 및 Safari 브라우저에서 다운로드 대화 상자에 있는 이메일 드롭다운에서 키보드 포커스가 멈춥니다(NPR-32067).

* Experience Manager에서 DM 클라우드 구성을 추가하는 동안 모든 컨텐츠 동기화 확인란이 기본적으로 활성화되지 않습니다(CQ -4288533).

### 기본 UI {#foundation-ui-6540}

* 필터 패널을 사용하여 자산을 검색하는 동안 마우스 컨트롤이 기존 필터 필드에 있지 않고 이전 필터 필드로 이동합니다(NPR-32538).

* 플랫폼 태그 지정: 태그 필드에 입력하여 태그를 검색하면 루트 경계 외부에 태그가 표시되고 태그 필드의 `rootPath` 속성이 유지되지 않습니다(NPR-31895).

* 플랫폼 UI: 텍스트 필드에 잘못된 경로가 추가되면 경로 브라우저가 멈춥니다(NPR-31884).

* 페이지 선택 시 알림이 고정 메뉴 뒤로 가려집니다(NPR-31628).

### 플랫폼 {#platform-sling-6540}

* (HTL) URL의 경로 섹션에서 밑줄이 콜론을 대체합니다(NPR-32231).

### 프로젝트 {#projects-6540}

* 사용자가 하위 폴더에 프로젝트를 만들 수 있는 권한이 있어도 만들기 버튼이 표시되지 않습니다(NPR-31832).

### 프로젝트 번역 {#projects-translation-6540}

* 번역 프로젝트를 만들 때 `Apache Sling JSP Script Handler`에서 지우기 공간 옵션이 활성화되어 있으면 UI가 중단됩니다(NPR-32154).

* 변환할 태그가 번역 프로젝트에 추가될 때 오류 로그에 UI 및 의 Null 포인트 예외 오류가 관찰됩니다(NPR-31896).

### 통합 {#integrations-6540}

* Launch 라이브러리 URL 생성은 Launch API의 `path` 및 `library_name` 값만 기반으로 하고 `library_path` 값을 기반으로 하지 않습니다(NPR-31550).

* LiveFyre 관련 항목을 처리하는 동안 오류 메시지가 표시됩니다(FYR-12420).

* ReportSuitesServlet이 SSRF에 취약합니다(NPR-32156).

### WCM 템플릿 편집기 {#wcm-template-editor-6540}

* 편집 가능한 템플릿 구조 모드에서 레이아웃 컨테이너의 허용된 구성 요소 목록에 링크 버튼 구성 요소가 표시되지 않습니다(CQ-4282099).

### WCM 페이지 편집기 {#wcm-page-editor-6540}

* 오버레이를 선택한 다음 응답형 격자 구성 요소를 여기로 드래그하십시오.를 선택하면 오류가 발생합니다(CQ-4283342).

### 캠페인 타깃팅 {#campaign-targeting-6540}

* Target 클라우드 구성이 실패하고 Mbox 가져오기 요청이 실패했다는 오류가 표시됩니다(CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Brand Portal 사용자는 Experience Manager 6.5.4에서 [!DNL Adobe I/O](으)로 업그레이드할 때 기여도 폴더 자산을 [!DNL Assets]에 게시할 수 없습니다(CQDOC-15655). Experience Manager 6.5.4를 즉시 수정하려면 [핫픽스를 다운로드](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041)하고 작성자 인스턴스에 설치하는 것이 좋습니다.

* 메타데이터 스키마 팝업 값은 자산 속성에 표시되지 않습니다(CQ-4283287).

* 자산 속성의 MIME 유형에 따라 메타데이터 하위 스키마에 탭이 표시되지 않습니다(CQ-4283288).

* 메타데이터 스키마 게시를 취소하면 백엔드에서 스키마가 제거되더라도 오류 메시지가 표시됩니다.

* 게시된 자산에 대한 미리 보기 이미지가 표시되지 않습니다(CQ-4285886).

* 사용자가 이름에 작은 따옴표가 포함된 자산을 게시하거나 게시를 취소할 수 없습니다(CQ-4272686).

* 여러 자산을 다운로드하는 동안 약관이 표시되지 않습니다(CQ-4281224).

* 사소한 보안 취약점이 해결되었습니다.

### 커뮤니티 {#communities-6540}

* 구성원 만들기 양식이 빈 페이지로 표시됩니다(NPR-31997).

* 사용자가 작성자 인스턴스에서 Analytics 보고서를 볼 수 없습니다(NPR-30913).

### Oak 색인 지정 및 쿼리 {#oak-indexing-6540}

* JPEG 이미지가 포함된 MS Word 및 MS Excel 문서를 Tika 구문 분석기로 구문 분석하면 구문 분석되지 않고 클래스를 찾을 수 없다는 오류가 표시됩니다(NPR-31952).

### 양식 {#forms-6540}

>[!NOTE]
>
>Experience Manager 서비스 팩에는 Experience Manager Forms에 대한 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 Adobe Experience Manager Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 추가 문자가 표시됩니다(NPR-32626).

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 드롭다운 자리 표시자가 텍스트 구성 요소로 표시됩니다(NPR-32539).

* 서신 관리: 편지 템플릿에 정의된 기본값이 미리 보기 모드에서 표시되지 않습니다(NPR-32511).

* 모바일 양식: HTML 버전에서 XDP 양식을 렌더링하는 동안 제출 버튼 크기가 확장되어 표시됩니다(NPR-32514).

* 문서 서비스: 서비스 팩 2를 적용한 후 편지 및 일부 기타 페이지의 URL에 액세스하는 데 문제가 발생합니다(NPR-32508, NPR-32509).

* 문서 서비스: 서버의 트랜잭션 수가 특정 제한을 초과하는 경우 HTML을 PDF로 변환할 수 없고 [!DNL Forms] 서버에서 파일 유형 설정이 제거됩니다(NPR-32204).

* 적용형 양식: WCAG2 레벨 AA 지침에 따라 브라우저 접근성 도구가 적용형 양식의 오류를 보고합니다(NPR-32312, NPR-32309, CQ-4285439).

* 적용형 양식: Chrome 브라우저 접근성 도구가 모범 사례 오류를 보고합니다(NPR-32310).

* 적용형 양식: Experience Manager Sites 페이지에 포함된 적용형 양식을 구성하는 동안 번역 문제가 발생했습니다(NPR-32168).

* Workbench: PDF 유틸리티 서비스에 PDF 속성 가져오기 작업을 사용하는 동안 오류 메시지가 표시됩니다(NPR-32150).

* 문서 보안: DisableGlobalOfflineSynchronizationData 옵션이 True로 설정되어 보호된 PDF 파일을 오프라인으로 열 수 없습니다(NPR-32078).

* 디자이너: 태그 지정 옵션이 활성화된 경우 생성된 PDF 출력에서 하위 양식 테두리가 사라집니다(NPR-32547, NPR-31983, NPR-31950).

* 디자이너: 표에 병합된 셀이 있는 경우 출력 서비스를 사용하여 XDP 양식에서 변환된 출력 PDF 파일에 접근성 테스트를 수행하면 오류가 발생합니다(CQ-4285372).

* Foundation JEE: 클러스터에서 Experience Manager Forms 서버 연결이 끊어진 경우 캐싱 문제가 발생하여 서버에 다시 연결되지 않습니다(NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager]6.5.3.0은 **2019년 4월**&#x200B;에 6.5 릴리스의 공식 출시 이후에 발표된 성능, 안정성, 보안 및 주요 고객 수정 사항과 개선 사항을 포함하는 중요한 릴리스입니다. [!DNL Adobe Experience Manager] 6.5의 맨 위에 설치할 수 있습니다.

이 서비스 팩 릴리스의 몇 가지 주요 사항은 다음과 같습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.6으로 업데이트되었습니다.

* 이제 [!DNL Experience Manager Assets]에서 Deflate64 알고리즘을 사용하여 만든 ZIP 아카이브를 지원합니다.

* 정렬 가능한 작성된 날짜에 대한 새 열이 DAM 목록 보기 및 자산 검색 결과의 목록 보기에 추가되었습니다.

* 이름 열을 기반으로 한 자산 정렬이 목록 보기에서 활성화되었습니다.

* 이제 [!DNL Dynamic Media]에서 스마트 자르기 비디오 자산을 지원합니다. 스마트 자르기는 장면의 초점을 따라 프레임을 이동하면서 비디오를 다시 자르는 머신 러닝 기반의 기능입니다.

* [!DNL Dynamic Media]에서 스마트 이미징을 지원합니다.

*  워크플로우에서 [부재 중](../forms/using/configure-out-of-office-settings.md) 환경 설정을 지정하는 기능.[!DNL Experience Manager]

*  워크플로우에서 다른 사용자와 [받은 편지함 또는 받은 편지함 항목을 공유](../forms/using/configure-shared-queues-osgi.md)하는 기능.[!DNL Experience Manager]

* [일괄 처리 모드에서 인터랙티브한 커뮤니케이션을 생성](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)하는 기능.

* ContextHub에 번들로 포함된 jQuery의 버전이 3.4.1로 업데이트되었습니다.

### 자산 {#assets-6530-enhancements}

**제품 개선 사항**

* 이제 [!DNL Experience Manager Assets]에서 Deflate64 알고리즘을 사용하여 만든 ZIP 아카이브를 지원합니다(NPR-27573).

* 정렬 가능한 새로 만든 날짜에 대한 열이 목록 보기의 DAM 목록 보기 및 자산 검색 결과에 추가되었습니다(NPR-31312).

* 목록 보기에서 [!UICONTROL 이름] 열을 사용하여 자산 목록을 정렬할 수 있습니다(NPR-31299).

* GLB, GLTF, OBJ 및 STL 자산 파일은 DAM의 [!UICONTROL 자산 세부 정보] 페이지에서 자산 미리 보기를 지원합니다(CQ-4282277).

* `ReplicationOnModifyListener` 이벤트가 [!DNL Dynamic Media]에서 청크 업로드 중 청크 노드에 대해 트리거됩니다(CQ-4281279).

* 이제 [!DNL Dynamic Media]에서 스마트 자르기 비디오 자산을 지원합니다. 스마트 자르기는 장면의 초점을 따라 프레임을 이동하면서 비디오를 다시 자르도록 하는 머신 러닝 기반의 기능입니다(CQ-4278995).

* [!DNL Dynamic Media]에서 스마트 이미징을 지원합니다(CQ-422249).

* 요청에서 쿼리 매개 변수가 전달되면 Foundation 선택기에서 검색 또는 찾아보기 보기가 기본 보기로 설정되었습니다(NPR-31601).

**수정 사항**

* 일부 PDF 문서의 메타데이터는 해당 제목을 수정할 때 업데이트되지 않고 PDF에 저장됩니다(NPR-31629).

* 파일 이름에 더하기 문자(`+`)가 있는 자산에 대해 자산 공유가 작동하지 않습니다(NPR-31547).

* 기본 검색 양식 자산 관리 검색 레일의 편집이 예상대로 작동하지 않습니다(NPR-31502).

* 자산 보기에서 Omnisearch를 사용하여 자산 검색할 때 제안이 표시되지 않습니다(NPR-31496).

* 다른 사용자가 동일한 자산을 다른 컬렉션에서 참조하는 경우 참조된 자산을 다른 위치로 이동할 때 컬렉션 내의 자산 참조는 업데이트되지 않습니다(NPR-31486).

* 중복된 IPTC 태그가 자산 메타데이터에 추가됩니다(NPR-31328).

* 필터 레일에서 검색이 트리거될 때 검색 결과 카운트가 정확하게 업데이트되지 않습니다(NPR-31316).

* 파일 유형 필터에서 두 번째 수준 확인란을 선택 취소하면 모든 확인란이 선택 취소되고 검색 막대의 텍스트가 선택한 또는 선택되지 않은 속성과 동기화되지 않습니다(NPR-31287).

* 모든 구성원(사용자/그룹)은 폴더의 멤버 섹션에서 제거할 수 없습니다. 모든 사용자를 제거하려고 하면 로그인한 사용자가 목록에 추가됩니다(NPR-31171).

* 파일 이름에 더하기 기호(`+`)가 있는 자산은 삭제할 수 없습니다(NPR-31162).

* 폴더 선택 시 상단 메뉴에 표시되는 만들기 드롭다운 메뉴는 만들기 옵션으로 &#39;폴더&#39;를 표시하지 않습니다(NPR-30877).

* 경로에 있는 Deny `jcr:removeChildNodes` 및 `jcr:removeNode`에 대한 ACL이 사용자에 대해 적용되면 폴더 선택 만들기 > 파일 업로드 작업 항목이 누락됩니다(NPR-30840).

* 특정 mp4 자산이 업로드되면 DAM 워크플로우가 부실 상태로 전환되어 나머지 모든 워크플로우가 부실 상태로 전환됩니다(NPR-30662).

* 대용량 PDF 파일(일부 GB 중)이 DAM에 업로드되고 하위 자산이 처리되는 경우 메모리 부족 오류가 발생합니다(NPR-30614).

* 자산의 벌크 이동이 실패하고 경고 메시지가 표시됩니다(NPR-30610).

* [!DNL Dynamic Media]–Scene7 모드에서 실행 중인 [!DNL Experience Manager]에서 자산을 폴더 간에 이동할 때 자산 이름이 소문자로 변경됩니다(NPR-31630).

* 원격 이미지 집합을 편집하는 동안 Scene7 회사 이름과 같은 폴더에 있는 이미지에 대한 오류가 발견되었습니다(NPR-31340).

* [!DNL Dynamic Media]참조가 포함된 자산이 게시되지 않습니다(NPR-31180).

* [!DNL Dynamic Media]7–Scene7 모드에서 [!DNL Dynamic Media Classic]으로 업로드를 완료하는 데 시간이 너무 오래 걸립니다(NPR-31048).

* 이미지 자산에 추가된 핫스팟은 자산 세부 사항 페이지의 인터랙티브 이미지 뷰어를 통해 표시되지 않습니다(NPR-30979).

* [!DNL Experience manager Assets]의 자산에 대해 수행된 작업이 Scene 7로 전달되면 대규모 슬링 작업이 생성되고 처리 중 배너가 다시 나타납니다(NPR-30947).

* 자산의 언어 사본을 만들 때 충돌이 발생하여 Scene 7로 업로드할 수 없습니다(NPR-30932).

* [!DNL Dynamic Media]–Hybrid 모드에서 실행되는 [!DNL Experience Manager]에서 다운로드한 동적 변환이 손상되었습니다(이미지 컨텐츠 유형 대신 &#39;이미지를 찾을 수 없음&#39; 컨텐츠가 있는 텍스트 유형)(NPR-30876).

* [!DNL Dynamic Media] 인코딩 비디오 워크플로우가 [!DNL Dynamic Media Classic]에서 Adobe Experience Manager의 [!DNL Dynamic Media]-Scene7 모드로 마이그레이션된 비디오의 축소판을 생성하지 못합니다(CQ-4282011).

* IpsApiException은 다른 Scene7 회사 ID를 사용하여 하나의 인스턴스에서 다른 인스턴스로 자산을 마이그레이션하는 동안 관찰되었습니다(CQ-4280548).

* 지원되는 3D 모델을 [!DNL Experience Manager]으로 수집할 때 3D 자산 축소판이 도움이 되지 않습니다(CQ-4283701).

* 3D 자산에 카메라 보기가 거의 없는 경우 스크롤 버튼이 뷰어에 표시됩니다(CQ-4283322).

* 자산 세부 사항 페이지의 DimensionalViewer에서 미리 본 업로드된 3D 모델의 컨테이너 높이가 잘못되었습니다(CQ-4283309).

* Internet Explorer 11 및 Safari에서 SmartCropVideoViewer로 비디오를 재생할 수 없습니다(CQ-4281422).

* [!DNL Dynamic Media]–Scene7 실행 모드에서 실행되는 [!DNL Experience Manager]에서 폴더 간에 여러 자산을 이동할 때 이동 단추를 사용할 수 없습니다(CQ-4280384).

* MIME 유형이 MP4 이외인 경우 자산 세부 사항에 왜곡된 비디오가 표시됩니다(CQ-4279704).

* 비디오 프로필이 있는 폴더에서 새로 수집된 비디오는 인코딩 비율이 100%로 완료된 후에도 처리 중 상태로 유지됩니다(CQ-4279389).

* 폴더에서 자산을 이동하면 이상적으로 필요한 것보다 훨씬 많은 슬링 작업(Scene 7 API 호출)이 생성됩니다(CQ-4278664).

* 이미지 집합(또는 미디어 집합)을 만들고 DAM에서 적절한 명명 규칙을 사용하여 이름을 지정하면 Scene 7에서 이미지 집합 이름이 소문자로 변경됩니다(CQ-428112).

* Scene 7 Migrator가 게시 상태를 잘못 설정합니다(CQ-4263492).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 콘텐츠 조각에서 사용자의 스크롤 위치를 잃게 됩니다(CQ-4282898).

* PDF 파일은 색인이 되어 있지 않고 내부 콘텐츠를 검색할 수 없습니다(CQ-4278916).

* 사용자 선택기로 나열되지 않은 그룹: false가 true와 같아야 함 오류가 다른 `principalName` 및 `authorizableId`를 포함하여 닫힌 사용자 그룹 추가 시 관찰됩니다(CQ-4278177).

* 자산 UI 열 보기가 특정 테넌트의 dam 루트 경로와 관계없이 모든 경로를 표시합니다(CQ-4278175).

* 자산 선택기의 검색이 예상대로 작동하지 않습니다(CQ-4275886).

* 렌디션 워크플로가 실패했습니다(CQ-4271928).

* DAM 이벤트 삭제 기능은 최신(`maxSavedActivities`) 이벤트 데이터를 삭제하고 이전에 만든 데이터를 저장합니다(NPR-31336).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 사용자의 스크롤 위치가 손실됩니다(NPR-31307).

* 모두 선택한 다음 터치 UI에서 일부 항목(폴더/개별 자산)을 선택 해제할 때 작업 표시줄 및 자산 수가 업데이트되지 않습니다(NPR-31118).

* 자산에 대한 작업 세부 사항을 폴링하는 동안 [!DNL Experience Manager]에 예외가 표시됩니다(CQ-4283569).

### 사이트

* LiveCopy 상속이 끊어지면 LiveCopy 페이지에 LiveCopy 링크 대신 언어 복사 링크가 표시됩니다(NPR-30980).
* 새 블루프린트의 경우 레코드 수가 40개를 초과하는 경우 처음 40개의 레코드만 표시됩니다. 블루프린트는 나머지 레코드에 대한 빈 라인을 표시합니다(NPR-31182).
* 사용자가 메뉴의 설명 속성에 일본어 또는 한국어 문자를 추가하면 메뉴에 일본어 및 한국어 텍스트의 왜곡된 문자가 표시됩니다(NPR-31331).
* 리치 텍스트 편집기(RTE)가 포함된 테이블을 목록 항목으로 삽입할 수 없습니다(NPR-30879).
* 기본 제공되는 스캐폴딩 RTE(리치 텍스트 편집기)가 예기치 않게 인라인 글꼴 크기를 요소에 적용합니다(NPR-31284).
* 사용자가 왼쪽 레일 필드에 초점을 맞추고 키보드 단축키를 사용하여 콘텐츠를 붙여넣으면 왼쪽 레일 필드에서 복사한 콘텐츠 대신 페이지 편집기 클립보드의 콘텐츠를 붙여넣습니다(NPR-31172).
* 사용자가 다중 필드에 파일 업로드 필드를 추가하면 이미지 경로가 다중 필드 노드 대신 구성 요소 노드에 저장됩니다(NPR-30882).
* `ResponsiveGridExporter` API는 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 인터페이스를 반환하지 않습니다. `com.day.cq.wcm.foundation.model.impl` 패키지는 비공개 패키지로 선언됩니다(NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 일부 Experience Fragments가 포함된 페이지를 편집기가 아닌 모드(`editor.html` 접두사가 없고 `wcmmode=disabled`된 작성자 및 또는 게시자에서)로 열리면 HTTP 상태 오류 코드 `500`에서 요청이 종료됩니다(NPR-30743).
* 사용자는 암호를 변경하고 프로필 페이지에 액세스할 수 없습니다(NPR-31161).

### 검색 및 사용자 인터페이스 {#ui-interface-and-search}

* 검색 결과 페이지의 카드 보기에서 목록 보기로 전환하는 경우 페이지를 스크롤하려면 지연이 있습니다(NPR-31286).

* [!DNL Sites] 사용자 인터페이스의 목록 보기에서 [!UICONTROL 모두 선택] 확인란이 숨겨집니다(NPR-31614).

* 검색 결과 페이지에서 [!UICONTROL 모두 선택] 카운트가 잘못되었습니다(NPR-31120).

* 메타데이터 편집기에 존재하지 않는 태그가 표시됩니다(NPR-31119).

### 번역 {#translation}

* 번역 작업에서 기한 옵션을 선택하면 두 개의 달력 팝업이 나타납니다(NPR-31270).

### 플랫폼

* 웹 콘솔의 Mime 유형 옵션이 작동하지 않습니다(NPR-31108).

* SSO(Single Sign-On)를 구성할 때 클라이언트 인증서가 허용되지 않습니다(NPR-31165).

* Jetty 기반 HTTP 서비스에 대한 버퍼 크기 구성의 업데이트가 저장되지 않습니다(NPR-30925).

* 이제 QueryBuilder는 xpath 쿼리에서 `fn:name()` orderby를 지원합니다(NPR-31322).

* [!DNL Experience Manager] 6.3에서 업그레이드 시 중복 활성화 트리가 만들어집니다(NPR-31513).

* 전달된 요청은 슬링 인증 동안 설정된 응답 헤더를 보존하지 않습니다(NPR-30013).

* 선택기 구성 요소 내에서 검색이 작동하지 않습니다(NPR-31692).

* 서로 다른 버전의 Apache POI 및 Apache Tika 번들로 인해 ZIP 파일을 [!DNL Experience Manager Communities] 게시물에 첨부할 때 오류가 표시됩니다(NPR-31018).

* 이 `org.apache.sling.distribution.api` 번들은 구성 관리자에 숨겨져 있으므로 사용자 지정 번들에는 사용할 수 없습니다(NPR-31720).

### 프로젝트

* 달력 보기를 전환할 수 없습니다(NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**제품 개선 사항**

* [!DNL Experience Manager Assets]의 자산 소싱 가져오기 워크플로우가 [!DNL Brand Portal]에서 새로 만든 자산만 [!DNL Experience Manager]으로 가져오도록 수정되었으며, 복제를 방지하기 위해 NEW 폴더에 이미 있는 자산을 건너뜁니다(CQ-4278527).

**수정 사항**

* 자산 소싱 기능에서 새 기여도 폴더를 만들 때 잘못된 아이콘이 표시됩니다(CQ-4282825).
* 새 기여도 폴더를 만들 때 기여도 폴더에 하위 폴더 하나 또는 둘 다(NEW 및 SHARED) 나타나지 않습니다(CQ-4282424).
* 사용자가 [!DNL Experience Manager] 끝의 기여도 폴더에서 새 자산을 받은 후 [!DNL Brand Portal]에서 [!DNL Brand Portal]로 기여도 폴더를 다시 게시하려고 하면 시스템에서 예외가 발생합니다(CQ-4279740).
* 기여도 폴더(중첩된 폴더) 내에 기여도 폴더를 만들 수 없으므로 복잡성을 방지할 수 있습니다(CQ-4278391).
* [!DNL Experience Manager] Admin Console.솔에서 가져온 [!DNL Brand Portal] 사용자 목록(.csv 파일)을 업로드할 때 시스템에 예외가 발생합니다. 다음 .csv 파일의 이메일, 이름 및 성 필드만 필수 필드입니다(CQ-4278390).

### 커뮤니티 {#communities-6530}

**수정 사항**

* 그룹 관리(그룹 열기/편집/게시/삭제)에 대한 빠른 링크는 커뮤니티 관리자(그룹 관리자/사이트 관리자)에 표시되지 않습니다(NPR-31627).
* 페이지를 수동으로 새로 고치거나 다시 로드하지 않는 한 제출된 블로그가 표시되지 않습니다(NPR-31599).
* 언급 기능에 사용되는 JCR 쿼리는 대/소문자를 구분하며 결과를 반환하는데 너무 오래 걸립니다(NPR-31475).
* [!DNL Experience Manager] 6.5 UberJar 파일에서 예외가 발생하고, 6.5 UberJar 파일에서 `cq-social-translation` 번들이 누락되었습니다(NPR-31186).[!DNL Experience Manager]
* Jackson Databind 라이브러리가 새로운 취약점을 해결하기 위해 버전 2.9.9.3으로 업데이트되었습니다(NPR-30967).
* 활동 및 알림 제목이 일치하지 않습니다(NPR-30941).
* 페이지 매김이 [!DNL Communities] 블로그에서 제대로 작동하지 않습니다(NPR-30914).
* Analytics 보고서가 [!DNL Experience Manager] 작성자 환경에서 채워지지 않으며 빈 페이지가 표시됩니다(NPR-30913).

### Oak {#oak}

* Lucene 인덱스 업데이트로 인해 작성자 서버가 느려집니다(NPR-31548).

### 양식 {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Experience Manager Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

#### Forms 추가 기능 패키지 {#forms-add-on-package-6530}

**적응형 양식**

* 적응형 양식을 현지화하는 동안 문자열에 사전 키가 포함됩니다(NPR-31110).

**대화형 통신**

* **MissingNode.toString()**&#x200B;은 Jackson 라이브러리를 2.10.0으로 업그레이드한 후 부정확한 결과를 반환합니다(NPR-31549).

* 텍스트 편집기가 Microsoft Word에서 복사한 텍스트에서 공백 문자를 임의로 제거합니다(NPR-31113).

**서신 관리**

* LiveCycle ES4SP1에서 [!DNL Experience Manager] 6.5로 문자를 마이그레이션하는 동안에는 캡션 및 도구 설명이 표시되지 않습니다(NPR-31615).

* **문자를 초안으로 저장하는 동안 텍스트 흐름 형식이 더 이상 지원되지** 않습니다(NPR-30463).

**워크플로우**

* 100% CPU 사용률로 인해 OSGi 워크플로우가 실패합니다(NPR-31233).

**HTML5 양식**

* XDP 양식의 HTML5 미리 보기를 생성하면 하위 양식의 인스턴스를 추가하는 동안 깜박임이 표시됩니다(NPR-30909).

#### JEE 설치 프로그램의 양식 {#forms-jee-installer-6530}

**양식 - 문서 서비스**

* 다음 .NET 프로젝트에서 MTOM을 사용하는 SOAP 웹 서비스에는 AssemblerServiceClient 호출 및 HtmlToPDF2 메서드에 대한 예외가 표시됩니다(NPR-4281771).

* AXIS 1.4 jar에서 보안 취약성 2012-5784 및 2014-3596을 찾았으며, [AXIS1.4.1 jar](https://helpx.adobe.com/kr/aem-forms/quick-fixes/6-5/jee-patch-0014.html)에서 제공된 수정(NPR-31015).

**Foundation JEE**

* 작업 구성은 양식 호출 워크플로우 제출 작업에 대한 프로세스 이름을 로드하지 않습니다.

### 기능 팩이 포함됨 {#feature-packs-included-6530}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 고객의 경우 [!DNL Experience Manager] 서비스 팩, 누적 수정 팩 또는 기능 팩을 설치한 후 [!DNL Experience Manager Forms] 추가 기능 패키지를 설치해야 합니다.

#### 양식 - 기초 JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager]Oracle 18c에 대해 Forms가 지원됩니다(NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager][!DNL Adobe Experience Manager] 6.5.2.0은 2019년 4월에&#x200B;**6.5의 공식 출시 이후에 발표된 성능, 안정성, 보안 및 주요 고객 수정 사항과 개선 사항을 포함하는 중요한 릴리스입니다**. [!DNL Experience Manager] 6.5의 맨 위에 설치할 수 있습니다.

이 서비스 팩 릴리스의 몇 가지 주요 사항은 다음과 같습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.3으로 업데이트되었습니다.
* 경험 구성요소를 [!DNL Adobe Target]의 사용자 지정 작업 공간으로 직접 내보낼 수 있는 구성 속성이 추가되었습니다.
* Assets 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. [!DNL Experience Manager]는 사용자가 선택한 이미지와 유사한 DAM 저장소에서 스마트 태그가 지정된 이미지를 표시합니다. [시각적 검색](../assets/search-assets.md#visualsearch)을 참조하십시오.

* 원격 DAM 배포에서 문서를 가져오도록 지원을 추가하는 연결된 자산 기능이 향상되었습니다. 이제 사이트 작성자가 콘텐츠 파인더에서 지원되는 문서 유형을 검색하고 필터링할 수 있습니다. 원격 문서를 웹 페이지의 다운로드 구성 요소에 추가할 수 있습니다. [연결된 자산 사용](../assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

* 여러 값을 갖는 옵션을 지원하기 위해 추가 MIME 유형을 사용하는 EnhanceDocument 유형 필터입니다.
* 다중 리소스 지원을 위해 외부 재처리 워크플로우가 도입되었습니다.
* 복제에 기본 자산 필터를 사용하여 [!DNL Dynamic Media] 성능이 최적화되었습니다.
* DMS7에 대한 자르기/회전 자산 편집 옵션이 복원되었습니다.
* VideoPlayer에 로드 시 비디오를 음소거하는 옵션이 구현되었습니다.
* 자산 UI 열 보기에 임차인 관련 콘텐츠만 표시되도록 수정합니다.
* 검색 결과에 스타일 아코디언 변경 사항이 반영되도록 수정합니다.

### 자산

**제품 개선 사항**

* 원격 DAM 배포에서 문서를 가져오도록 지원을 추가하는 연결된 자산 기능이 향상되었습니다. 이제 사이트 작성자가 콘텐츠 파인더에서 지원되는 문서 유형을 검색하고 필터링할 수 있습니다. 원격 문서를 웹 페이지의 다운로드 구성 요소에 추가할 수 있습니다. CQ-4270245용 핫픽스. [연결된 자산 사용](/help/assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

* [!DNL Experience Manager Assets] 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. [!DNL Experience Manager]는 사용자가 선택한 이미지와 유사한 DAM 저장소에서 스마트 태그가 지정된 이미지를 표시합니다. [시각적 검색](../assets/search-assets.md#visualsearch)을 참조하십시오.

**수정 사항**

* ACP API에서 생성된 URL 및 폴더 메타데이터의 자산 경로는 URL로 인코딩되지 않습니다. GRANITE-26198: CQ-4271814용 핫픽스
* 이름에 백분율 기호(%)가 있는 폴더로 아카이브 압축을 푼 경우 [!DNL Experience Manager Assets] 인터페이스를 사용하여 열 수 없습니다. NPR-29989: CQ-4270467용 핫픽스
* Touch UI: 게시 마법사를 관리하는 동안 post 요청 본문의 페이지 뒤에 참조가 추가되어 모든 자산이 페이지 뒤에 게시되며, 페이지가 렌더링될 때 게시 인스턴스의 일부 자산이 누락됩니다. NPR-29985: CQ-4270724용 핫픽스
* 자산 관계 해제 기능은 이름에 특수 문자(URI로 인코딩되는 문자)가 있는 관련 자산에 대해 작동하지 않습니다. NPR-30387: CQ-4274446용 핫픽스
* 콘텐츠 조각을 편집할 때 버전이 잘못된 사용자로 생성됩니다.
* 임차인 기반 시스템에서 컬렉션을 작성하는 중에 오류가 발생합니다. NPR-30114: CQ-4272948용 핫픽스
* Asset UI 열 보기는 현재 임차인의 dam 루트 경로를 준수하지 않지만 모든 임차인 dam 경로에 액세스합니다. NPR-30636: CQ-4275481용 핫픽스
* 제한된 파일 경고 창을 통해 삽입된 이미지로 가능한 XSS(교차 사이트 스크립팅) 공격을 볼 수 있습니다. NPR-30617: CQ-4270133용 핫픽스
* MultiTenant: 폴더 속성을 저장하는 임차인은 성공 메시지와 작업이 실패했음을 설명하는 오류 메시지, &quot;속성을 편집할 수 없습니다. 권한이 부족합니다.&quot;를 모두 관찰하면 혼동됩니다. NPR-30545: CQ-4275333용 핫픽스
* 자산 선택기 대화 상자에서는 자산을 선택할 수 없으므로 관련 소스 교체 기능을 사용하여 소스를 업데이트할 수 없습니다. NPR-30502: CQ-4275029용 핫픽스
* [!UICONTROL DAM 자산 업데이트] 워크플로우 - 크기가 큰 mp4 파일을 업로드할 때 사용되지 않는 상태입니다. NPR-30480: CQ-4271352용 핫픽스
* null 페이로드로 인해 모든 후속 리뷰 관련 작업이 실패하므로 리뷰 작업 만들기 기능이 작동하지 않습니다. NPR-30468: CQ-4274263용 핫픽스
* Datapower를 통한 Adobe 스마트 태그 연결 문제. NPR-30026: CQ-4269457용 핫픽스
* Assets UI 열 보기에서 레일 왼쪽에 있는 필터를 여는 동안 오류가 발생했습니다. NPR-30501: CQ-4273862용 핫픽스
* LDAP에서 동기화된 그룹을 자산 폴더의 CUG(폐쇄된 사용자 그룹) 속성에서 추가할 때 이 그룹이 저장 및 검색되지 않습니다. NPR-30615: CQ-4274689용 핫픽스
* 필터 검색 스타일 및 방향 필드는 자동 완성된 값을 검색 쿼리에 적용하지 않습니다. NPR-30620: CQ-4275724용 핫픽스
* 이름에 공백 및 &quot;&amp;&quot; 문자가 있는 폴더의 자산 공유 링크에는 일부 자산에 대해 빈 회색 카드가 표시됩니다. NPR-30557: CQ-4270187용 핫픽스
* 폴더 메타데이터 스키마 양식은 자동으로 데이터 유형을 감지하지 않으므로 양식 전송 시 관련된 TypeHint를 생성하지 않습니다. NPR-30599: CQ-4275227용 핫픽스
* 자산 자르기 및 회전 편집 옵션이 DMS7 작성 UI에서 비활성화됩니다. NPR-30118: CQ-4273221용 핫픽스
* DMS7 구성이 있는 [!DNL Experience Manager] 인스턴스에서 링크 공유 기능이 작동하지 않습니다. NPR-30080, NPR-30492: CQ-4273651용 핫픽스
* 페이지에 [!DNL Dynamic Media]–Scene7 구성 요소를 추가한 다음 페이지를 게시하면 dmscene7 구성이 매번 트리거되지 않습니다. NPR-30641: CQ-4275962용 핫픽스
* 처리 프로필당 하나의 IPS(침입 방지 시스템) 작업만 작성하도록 [!DNL Experience Manager]에 IPSJobJournal이 추가되었습니다. NPR-30490: CQ-4273614용 핫픽스
* [!DNL Dynamic Media]: 자산이 복제되지 않도록 하는 기본 필터가 게시 노드에 추가되었습니다. [!DNL Experience Manager] NPR-30538: CQ-4274678용 핫픽스
* 폴더를 페이로드로 허용하도록 여러 리소스 지원을 위한 외부 재처리 워크플로우가 도입되었습니다. 이 워크플로우는 2단계로 진행됩니다. 메타데이터 맵을 통해 다음 단계로 자산을 재처리하고, 자산 핸들이 없는 모든 자산을 단일 IPS 작업으로 S7에 다시 업로드합니다. 자세한 내용은 [!DNL Dynamic Media] Cloud Service 구성을 참조하십시오. NPR-30489: CQ-4272903용 핫픽스
* 올바른 CSV 다음에 잘못된 CSV를 업로드하면 올바른 CSV가 지워집니다. CQ-4277694, CQ-4277814용 핫픽스
* 제거할 기여도 폴더와 관련된 잘못된 아이콘입니다. CQ-4277580용 핫픽스
* 자산 기여 탭의 사용자 선택기에서 사용자 선택 시 사용자의 이름이 표에 표시되지 않고 속성 페이지의 사용자 삭제 대화 상자에 잘못된 텍스트가 표시됩니다. CQ-4277875용 핫픽스
* 사용자를 선택하고 추가를 클릭하여 사용자 선택기의 자산 기여 폴더에 기여자를 추가할 수 없습니다. CQ-4277824, CQ-4278087용 핫픽스
* 사용자 선택기에서는 소문자 사용자 이름으로 검색할 수 없습니다. CQ-4277958, CQ-4277930용 핫픽스
* 관리자가 아닌 사용자가 자산 기여 폴더의 새 폴더에 자산을 게시할 수 있습니다. CQ-4278200용 핫픽스
* DAM 사용자(관리자가 아닌 사용자)는 자산 기여 폴더에 기여자를 추가할 수 없습니다. CQ-4278192용 핫픽스
* &quot;만들기&quot; 버튼은 자산 기여 폴더에 표시됩니다. CQ-4277560용 핫픽스
* 관련성을 기준으로 검색 쿼리를 정렬하면 [!DNL InDesign] 템플릿과 함께 [!DNL InDesign] 문서가 반환됩니다. CQ-4273864용 핫픽스
* 대문자 이메일 ID가 있는 사용자는 이전에 체크아웃된 자산에 대해 체크인할 수 없습니다. CQ-4276575용 핫픽스
* 삭제 작업은 선택한 사전 설정에만 적용되며, 작업 후 화면의 목록이 자동으로 새로 고쳐지면 이미 새로 고친 다른 사전 설정이 표시됩니다. CQ-4261461용 핫픽스
* [!DNL Dynamic Media]–Hybrid 모드에서 [!DNL Dynamic Media] Cloud Services를 구성하면 [!DNL Analytics]에 빈 보고서 세트가 여러 개 생성되고, [!DNL Experience Manager]에 저장된 보고서 세트 ID가 없기 때문에 보고서 세트가 중복됩니다. CQ-4249780용 핫픽스
* [!DNL Experience Manager] Assets에서 중복된 이름으로 이름을 바꾸면 Scene7과 동기화되지 않았습니다. CQ-4276763용 핫픽스
* 사용자 생성 콘텐츠가 검색 필터 패널에 잘못 표시됩니다. CQ-4273875용 핫픽스
* TIFF 이미지에서 유사 항목 찾기 옵션을 사용할 수 없습니다. CQ-4278238용 핫픽스
* VideoPlayer에 로드 시 비디오를 음소거하는 옵션이 구현되었습니다. CQ-4266465용 핫픽스
* 뷰어 - 외부 비디오가 사용되는 경우 VideoViewer: poster=none이 제대로 작동하지 않습니다. CQ-4265536용 핫픽스
* IE11 및 MS Edge 브라우저에서 비디오 재생 중에 대기 아이콘이 표시됩니다. CQ-4251539용 핫픽스
* 3.8 SDK 및 5.13 뷰어 README 파일이 업데이트되지 않으며 이전 릴리스의 정보를 포함합니다. CQ-4273737용 핫픽스
* 콘텐츠 조각은 변경 사항을 저장하기 전에도 버전이 지정됩니다. NPR-30616: CQ-4273088용 핫픽스
* 썸네일 프로세스에서 Asset#getMetadata(String)를 Asset#getMetadataValueFromJcr(String)로 바꿉니다. NPR-30491: CQ-4273067용 핫픽스
* jpg를 업로드하면 메시지의 여러 인스턴스가 각 자산에 대해 &quot;ReplicateOnModifyWorker 복제가 업데이트&quot;되어 성능이 저하됩니다.
* 아카이브 추출 기능을 사용하여 zip 아카이브 압축을 풀면 이름에 해당 제목의 퍼센트(%)가 포함된 폴더에 문제가 발생합니다. NPR-29990: CQ-4270467용 핫픽스

### 사이트 {#sites-6520}

* LiveCopy 상속이 끊어지면 LiveCopy 페이지에 LiveCopy 링크 대신 언어 복사 링크가 표시됩니다(NPR-30980).
* 새 블루프린트의 경우 레코드 수가 40개를 초과하는 경우 처음 40개의 레코드만 표시됩니다. 블루프린트는 나머지 레코드에 대한 빈 라인을 표시합니다(NPR-31182).
* 텍스트 구성 요소의 리치 편집기(RTE) 플러그인은 일본어 및 한국어 텍스트의 왜곡된 문자를 표시합니다(NPR-31331).
* 리치 텍스트 편집기(RTE)가 포함된 테이블을 목록 항목으로 삽입할 수 없습니다(NPR-30879).
* 즉시 스캐폴딩할 수 있는 리치 텍스트 편집기(RTE)가 예기치 않게 인라인 글꼴 크기를 요소에 적용됩니다(NPR-31284).
* 사용자가 왼쪽 레일 필드에 초점을 맞추고 키보드 단축키를 사용하여 컨텐츠를 붙여넣으면 왼쪽 레일 필드에서 복사한 컨텐츠 대신 페이지 편집기 클립보드의 컨텐츠를 붙여넣습니다(NPR-31172).
* 사용자가 다중 필드에 파일 업로드 필드를 추가하면 이미지 경로가 다중 필드 노드 대신 구성 요소 노드에 저장됩니다(NPR-30882).
* `ResponsiveGridExporter` API는 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 인터페이스를 반환하지 않습니다. `com.day.cq.wcm.foundation.model.impl` 패키지는 비공개 패키지로 선언됩니다(NPR-31398).
* 일부 Experience Fragments가 포함된 페이지를 편집기가 아닌 모드(`editor.html` 접두사가 없고 `wcmmode=disabled`된 작성자 및 또는 게시자에서)로 열리면 HTTP 상태 오류 코드 500에서 요청이 종료됩니다(NPR-30743).

### WCM - 페이지 편집기 {#wcm-page-editor-6520}

**제품 개선 사항**

* `EnhanceDocument` 여러 값을 갖는 옵션을 지원하도록 추가 MIME 유형을 사용하는 필터를 입력합니다. CQ-4270694용 핫픽스

### 콘텐츠 조각 관리 {#content-fragment-management-6520}

* 콘텐츠 조각 모델 UI에 사용된 쿼리가 매우 느리므로 오류가 발생합니다. CQ-4270807용 핫픽스

### UI - 기초 {#ui-foundation}

* 사용자가 특정 사용자 인터페이스 내에서 &#39;m&#39;, &#39;p&#39;, &#39;e&#39;를 사용하지 못하도록 하는 단축키 트리거입니다. NPR-30355: GRANITE-26346용 핫픽스
* [!DNL Experience Manager Assets] 검색 UI를 닫으면 왼쪽 레일이 컨텐츠 선택 사항으로 재설정되지 않아 사용자가 이후에 필터 레일을 다시 열 수 없습니다. NPR-30509: CQ-4274716용 핫픽스
* 다중 임차인 환경: [!DNL Experience Manager Assets] UI 최상위 탐색을 사용할 수 없으며 JavaScript 오류가 발생합니다. NPR-30104: GRANITE-26344용 핫픽스

### 번역 {#translation-6520}

* 번역 문제 - 일부 구성 요소만 기계 번역을 사용하여 번역됩니다. NPR-30079: CQ-4273764용 핫픽스

### 플랫폼 {#platform-6520}

* [!DNL Experience Manager] 기본 메일 발송자가 TLS v1.2를 통해 원격 SMTP 서버로 메일을 전송할 수 없습니다. NPR-30476: GRANITE-26605용 핫픽스

### 프로젝트 {#projects-6520}

* dam:folderThumbnailPaths 값이 새로 고쳐지지 않으며, 폴더 내의 자산을 삭제한 후에도 이전 썸네일이 표시됩니다. NPR-30424: CQ-4273667용 핫픽스
* 이동 옵션을 완료할 때 자산의 제목과 이름은 변경되지 않은 상태로 유지됩니다. NPR-30647: CQ-4276265용 핫픽스

### 커뮤니티 {#communities-6520}

* 사용자 동기화 진단은 완전히 손상되어 작동하지 않습니다. NPR-30004, NPR-29943: CQ-4270287, CQ-4271348용 핫픽스

### 슬링 {#sling}

* 6.3.3.2에서 6.5로 인스턴스를 업그레이드하면 OSGi 구성이 중복됩니다. NPR-30130: CQ-4274016용 핫픽스

### 통합

* 사용자 지정 콘텐츠는 인스턴스를 다시 시작할 때까지 게시 인스턴스에 올바르게 표시되지 않습니다. NPR-30377: CQ-4273706용 핫픽스
* 웹 사이트에서 Launch를 구성할 때 라이브러리 주소에는 앞에 슬래시(/)가 추가되어 매번 수동으로 작업해야 합니다. NPR-30694: CQ-4275501용 핫픽스

### 양식 {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Experience Manager Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

[!DNL Experience Manager] 6.5.2.0 Forms의 주요 기능은 다음과 같습니다.

* `RenderAtClient` Forms OSGi용 API의 `PDFFormRenderOptions`에 &#39;자동&#39; 설정이 추가되었습니다. [!DNL Experience Manager]

#### Forms 추가 기능 패키지

**백엔드 통합**

* 호스팅된 AWS의 로드 균형 조정된 URL을 사용하여 양식 데이터 모델을 구성할 수 없습니다. NPR-30123: CQ-4273359용 핫픽스
* WSDL(웹 서비스 정의 언어)을 사용하여 FDM(양식 데이터 모델)을 만드는 동안 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` 오류 메시지가 반환됩니다. NPR-30477: CQ-4272921용 핫픽스

**서신 관리**

* 콘솔에서 다음 오류가 발생하여 간헐적으로 CCR UI(통신 UI) 렌디션 만들기가 실패합니다.
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**대화형 통신**

* 양식 데이터 모델에 필수로 표시된 필드가 CCR UI(Create Correspondence UI)에 필수로 표시됩니다. NPR-30623: CQ-4274902용 핫픽스

**양식 - 워크플로우**

* 감시 폴더의 매핑되지 않은 출력 변수로 인해 호출이 실패합니다. CQ-4264451용 핫픽스

**HTML5 양식**

* 사용자 지정 코드 또는 프로젝트가 두 번째로 배포되면 페이지가 렌더링되지 않고 다음 오류가 발생합니다. .

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: CQ-4272509용 핫픽스

* 검색 모드에서 비시각적 데스크탑 액세스를 사용하여 HTML5 양식을 읽을 때 Chrome 브라우저는 양식 디자인에서 각 SVG(규모 가변적인 벡터 그래픽) 앞에 있는 &quot;그래픽&quot;을 읽습니다. NPR-30449: CQ-4274732용 핫픽스

#### Forms JEE 설치 프로그램

**양식 - 문서 보안**

* 타임스탬프가 포함된 서명이 적용되지 않고 ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: 호출 오류가 발생합니다. NPR-30820: CQ-4275852용 핫픽스

**양식 - 문서 서비스**

* SubmitURL에 앰퍼샌드(&amp;)가 포함된 경우 `renderpdf` 서블릿에 대한 POST 요청이 수행될 때 로그에 구문 분석 오류가 표시됩니다. NPR-30865: CQ-4278232용 핫픽스

**양식 - 기초 JEE**

* HTMLtoPDF 서비스가 JMX 콘솔에 maxReuseCount를 표시하지 않습니다. NPR-30134, NPR-30304: CQ-4273763용 핫픽스
* [!DNL Experience Manager Forms] Workbench에서 웹 서비스를 호출하여 웹 서비스 연결을 추가하거나 편집하면 ClassNotFoundException org.apache.axis.message.SOAPBodyElement 오류가 발생합니다. NPR-30105: CQ-4273217용 핫픽스

### 기능 팩이 포함됨

>[!NOTE]
>
>[!DNL Experience Manager Forms] 고객의 경우 [!DNL Experience Manager] 서비스 팩, 누적 수정 팩 또는 기능 팩을 설치한 후 [!DNL Experience Manager Forms] 추가 기능 패키지를 설치해야 합니다.

#### 사이트 {#sites-feature-packs-included}

* 경험 구성요소를 [!DNL Adobe Target]의 사용자 지정 작업 공간으로 직접 내보낼 수 있는 구성 속성이 추가되었습니다. NPR-29189: CQ-4249782용 핫픽스

#### 양식 - 문서 서비스 {#forms-document-services-1}

* `RenderAtClient` OSGi용 API의 `PDFFormRenderOptions`에 &#39;자동&#39; 설정이 추가되었습니다. [!DNL Experience Manager Forms] NPR-30759: CQ-4278193용 핫픽스

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager][!DNL Adobe Experience Manager] 6.5.1.0은 2019년 4월에&#x200B;*6.5의 공식 출시 이후에 발표된 성능, 안정성, 보안 및 주요 고객 수정 사항과 개선 사항을 포함하는 중요한 릴리스입니다.*[!DNL Experience Manager] 6.5의 맨 위에 설치할 수 있습니다.

이 서비스 팩 릴리스의 몇 가지 주요 사항은 다음과 같습니다.

* 사용자 지정 속성으로 이벤트를 추적할 때 dynamic-UI-state 포함을 활성화했습니다.
* [!DNL Dynamic Media]–Scene7 모드에 360도 비디오 자산의 배송에 대한 지원이 포함되었습니다.
* 리치 텍스트 편집기의 스타일 플러그인을 통해 *일본어 자동 줄 바꿈* 기능이 활성화되었습니다. 자세한 내용은 [일본어 자동 줄바꿈 구성](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)을 참조하십시오.

### 자산

* S3 다중 부분 지원에 대한 DAM DMGateway 인터페이스가 업데이트되었습니다. NPR-29740: CQ-4226303용 핫픽스
* [!DNL Experience Manager] 6.5로 업그레이드한 후 변환 미리 보기를 수행하면 `Only empty tenantId is currently supported` 오류가 발생합니다. NPR-29986: CQ-4272353에 대한 핫픽스
* 작업을 삭제할 수 있는 삭제 대화 상자가 표시되지 않습니다. NPR-29720: CQ-4271074용 핫픽스
* 속성 페이지에서 자산 제목을 추가한 후 사용자가 페이지를 닫으려고 하면 [!DNL Experience Manager]에 속성 페이지가 다시 열립니다. NPR-29627: CQ-4264929용 핫픽스
* VersioningTimelineEventProvider는 nt: 버전 유형의 노드와 함께 루트 버전을 제공해야 합니다. GRANITE-26063용 핫픽스
* [!DNL Experience Manager] DM-Scene7 모드에서 360 구형 비디오를 업로드하고 재생하는 기능이 구현되었습니다. CQ-4265131용 핫픽스
* 소스가 편집되면 Live copy가 올바르지 않은 상태를 검색합니다. CQ-4265451용 핫픽스
* [!DNL Experience Manager Assets]에 대한 다중 사이트 관리자 지원이 활성화되었습니다. CQ-4271453, CQ-4268621, CQ-4257491용 핫픽스
* [!DNL Experience Manager] 인터페이스는 타임라인 내역에서 자산의 현재 버전에 대한 추가 항목을 표시하여 [!DNL Adobe Asset Link]의 최신 체크인 설명을 표시해야 합니다. CQ-4262864용 핫픽스
* 속성이 누락된 경우 콘텐츠 조각 타임라인에 오류 메시지가 표시됩니다. CQ-4272560용 핫픽스
* 전체 화면으로 확장하는 경우 Scene 7 비디오 플레이어에 문제가 발생합니다. CQ-4266700용 핫픽스
* ZoomVerticalViewer: 단일 이미지 자산을 사용하는 경우 이동 버튼이 표시되지 않습니다. CQ-4264795용 핫픽스
* Live Copy에서 하위 노드를 삭제하려면 liveRelationship을 분리해야 합니다. CQ-4270395용 핫픽스
* 메타데이터 스키마에는 글로벌 구성의 항목만 포함되어 있고 활성 임차인의 항목이 없습니다. formPath URL 값은 변경된 경우에도 기본값으로 되돌아 갑니다. NPR-29945: CQ-4262898용 핫픽스
* [!DNL Brand Portal]에 이미지 사전 설정 게시가 실패하고 500 오류 코드가 표시됩니다. NPR-29510: CQ-4268659용 핫픽스

### 사이트

* 빈 속성 및 여러 속성이 롤아웃 중에 블루프린트에서 전파되지 않습니다. Live Copy를 블루프린트로 재설정해도 구성 요소에 대해 작동하지 않습니다. NPR-29253: CQ-4264928, CQ-4264926, CQ-4267722용 핫픽스
* CoralUI가 `Multifield`에서 사용되는 경우 multifield 수준이 아닌 구성 요소 수준에서 `fileReferenceParameter`를 저장합니다. NPR-29537: CQ-4266129용 핫픽스
* 일본어 [!DNL Experience Manager] 텍스트 구성 요소 및 텍스트 편집기의 개선 사항입니다. NPR-29785: CQ-4265090용 핫픽스
* 타임워프를 사용하여 복원된 페이지는 버전 지정 시 올바른 그림을 참조해야 합니다. NPR-29431: CQ-4262638용 핫픽스
* 스타일 시스템 노드를 상위에서 하위로 상속하는 데 문제가 있습니다. NPR-29516: CQ-4270330용 핫픽스
* [!DNL Facebook] 인증에 소셜 게시를 설정하는 동안 오류 메시지가 표시됩니다. NPR-29211: CQ-4266630용 핫픽스
* 콘텐츠 조각의 렌더링된 썸네일에 날짜 및 시간 필드에 대한 내부 달력 표현이 표시됩니다. NPR-29531: CQ-4269362용 핫픽스
* Coral2 구현에서 권한 탭을 열면 버튼이 표시되지 않습니다. CQ-4269419용 핫픽스

### 상거래

* 전자 상거래를 위해 레이지 콘텐츠 마이그레이션을 실행할 때의 ConstraintViolationException입니다. NPR-29247: CQ-4264383용 핫픽스

### 콘텐츠 조각 관리

* 달러 `($)` 및 여는 중괄호 `({)` 문자가 있는 콘텐츠 조각을 열 때 구문 분석 오류가 발생합니다. CQ-4270266용 핫픽스

### 경험 구성요소

* [!DNL Experience Manager] 경험 구성 요소를 [!DNL Adobe Target]으로 내보냅니다. CQ-4265469용 핫픽스
* 스마트 이미지를 사용한 타겟으로 경험 구성요소 내보내기가 실패합니다. CQ-4269606용 핫픽스

* 사용자가 카드 보기에서 Omnisearch를 통해 환경 조각을 이동하려고 하면 막다른 상황에 놓이게 됩니다. CQ-4263848용 핫픽스

### WCM - 페이지 편집기

* 올바르지 않은 선택기를 사용할 때 XSS(교차 사이트 스크립팅)이 반영됩니다. CQ-4270397용 핫픽스

### 복제

* 사용자가 제공한 데이터는 `cq/replication/components/agent` 구성 요소에서 출력에 이스케이프되지 않으므로, 저장된 XSS(교차 사이트 스크립팅)에 취약성이 발생합니다. CQ-4266263용 핫픽스

### 워크플로우

* 대화 상자 참가자의 달력 선택기 필드가 손상되었습니다. NPR-29727: CQ-4270423용 핫픽스

### WCM - SPA 편집기

* 원격 끝점에서 사전 렌더링된 콘텐츠 가져오기를 사용하도록 설정되었습니다. CQ-4270238용 핫픽스
* 서버 측에 렌더링된 SPA 템플릿 페이지를 열 때 로그에 경고가 표시됩니다. CQ-4270238용 핫픽스

### WCM - MSM

* [!DNL Experience Manager] 6.4.3으로 업그레이드하면 다중 사이트 관리자가 롤아웃하는 데 시간이 오래 걸립니다. CQ-4271410용 핫픽스

### 통합

* BrightEdge 자격 증명이 실패하고 연결 오류가 발생합니다. NPR-29168: CQ-4265872용 핫픽스

* [!DNL Experience Manager] 실행 구성을 편집하고 저장하려고 하면 예외 메시지가 표시됩니다. NPR-29176: CQ-4265782/CQ-4266153용 핫픽스

### 사용자 인터페이스

* 기초 추적 API의 특정 이벤트를 추적하는 동안 dynamic-UI-states를 사용자 지정 특성으로 추적하는 지원이 추가되었습니다. GRANITE-26283용 핫픽스
* 제출 버튼에 추적 기능을 설정할 수 없습니다. GRANITE-26326용 핫픽스
* 마법사가 버튼에 추적 기능을 설정할 수 없습니다. NPR-29995, NPR-30025: CQ-4264289용 핫픽스

### 커뮤니티

* 구성원 프로필 페이지의 드롭다운에서 새 배지를 정렬할 수 없습니다. NPR-29381: CQ-4267987용 핫픽스
* 중정자 권한이 없는 방문자 및 구성원은 URL을 붙여넣어 승인되지 않은/보류 중인 게시물을 볼 수 있습니다. NPR-29724: CQ-4271124, CQ-4271441용 핫픽스
* 커뮤니티에 대한 사용자 로그인에서 최대 40~50초의 높은 응답 시간이 관찰됩니다. NPR-29677: CQ-4269444용 핫픽스

### 복제

* 복제 에이전트 구성 요소는 중요한 정보를 권한이 없는 사용자에게 공개하는 취약성이 있습니다. NPR-29611: GRANITE-25070용 핫픽스

* [!DNL Brand Portal]에 복제할 때마다 OAuth 중에 세션 누수가 발생합니다. NPR-30001: GRANITE-26196용 핫픽스

### 프로젝트

* [!DNL Experience Manager] Author /content/dam/mac 폴더에서 [!DNL Brand Portal]로 [!DNL Experience Manager Assets]이 게시되지 않습니다. NPR-29819: CQ-4271118용 핫픽스

### 플랫폼

* HtmlLibraryManager가 캐시 무효화에 대한 crx-quickstart의 모든 콘텐츠를 삭제합니다. NPR-29863: GRANITE-26197용 핫픽스

### Felix

* Java11을 사용할 때 메모리 사용량 세부 사항이 시스템 콘솔에 표시되지 않습니다\. NPR-29669

### 양식

[!DNL Experience Manager Forms] 6.5.1.0의 주요 기능은 다음과 같습니다.

* OSGi만 해당: 출력 및 양식 서비스에 새 속성 `PAGECOUNT`가 추가되었습니다.

* OSGI만 해당: 양식 서비스를 사용한 정적 PDF 작성을 지원하도록 설정되었습니다.
* 관리자 및 루트 사용자에 대해 XMLForm.exe에 대한 권한을 사용하도록 설정했습니다.
* Dynamics On-Premise 통합을 위해 ADFS v3.0을 지원하도록 설정했습니다.

#### Forms 추가 기능 패키지

**백엔드 통합**

* 보호된 WSDL(Web Service Definition Language)을 가져오지 못했습니다. NPR-29944: CQ-4270777용 핫픽스
* [!DNL Experience Manager Forms]가 IBM WebSphere에 설치된 경우 SOAP를 기반으로 한 양식 데이터 모델을 작성할 수 없습니다. CQ-4251134용 핫픽스
* Microsoft Dynamics On-Premise 통합을 위한 ADFS(Active Directory Federation Service) v3.0에 대한 지원이 활성화되었습니다. CQ-4270586용 핫픽스
* 데이터 소스의 제목이 변경되면 양식 데이터 모델에 업데이트된 제목이 표시되지 않습니다. CQ-4265599용 핫픽스
* 엔티티 또는 속성의 이름에 하이픈이나 공백을 사용하는 경우 표현식이 그러한 엔티티 및 속성을 평가하지 못합니다. CQ-4225129용 핫픽스

* 콜론이 기본 문자열 출력에 있으면 올바르지 않은 출력이 관찰됩니다. CQ-4260825용 핫픽스

* REST API 출력에서 콘텐츠가 예상되지 않더라도 양식 데이터 모델의 호출 작업으로 인해 오류가 발생합니다. CQ-4268828용 핫픽스

**적응형 양식**

* 레이지 로딩 중에 응용 양식 조각에 새 인스턴스를 추가할 수 없습니다. NPR-29818: CQ-4269875용 핫픽스
* 구성 요소가 레코드 템플릿 문서에 대한 오류를 기록하거나 표시하지 않는지 확인합니다. CQ-4272999용 핫픽스
* 응용 양식에 대한 레이아웃 편집기를 비활성화하는 지원이 추가되었습니다. CQ-4270810용 핫픽스
* [!DNL Experience Manager] 6.5에서 적용형 양식에 대한 확인 단계가 복원되었습니다. CQ-4269583용 핫픽스

* 적용형 양식 필드 유효성 검사 오류로 [!DNL Adobe Sign]이 중단되었습니다. CQ-4269463용 핫픽스
* [!DNL Experience Manager Forms] 인스턴스에 적용형 양식 조각이 20개 이상 있고 모든 양식 조각의 이름이 동일한 문자열로 시작하는 경우 검색 결과에 최근에 작성된 조각 20개만 반환되거나 아무것도 반환되지 않습니다. CQ-4264414, CQ-4264914용 핫픽스

* 응용 양식 앱이 큰 데이터 세트에서 사용되는 경우 성능 문제가 발생합니다. CQ-4235310용 핫픽스

* 게시 인스턴스에서 익명 계정을 통해 액세스한 경우 GuideRuntime 스크립트가 로드되지 않습니다. CQ-4268679용 핫픽스

**양식 - 대화형 통신**

* 대화형 통신 템플릿에 허용되는 구성 요소 목록의 머리글 및 바닥글 구성 요소가 나열되지 않습니다. CQ-4237895용 핫픽스
* 이미지 필드를 포함하는 대화형 통신 인쇄 템플릿을 작성하면 차트 제목이 공백으로 설정됩니다. CQ-4264772용 핫픽스
* 차트의 선 색상이 삭제되는 경우 정의되지 않음으로 설정됩니다. CQ-4264762용 핫픽스
* 문서 조각에서 수행한 레이아웃 레이어 변경 사항은 변경 사항을 계속 동기화할 경우 사라집니다. CQ-4266054용 핫픽스
* 텍스트 필드에 바인딩된 문서 조각 내의 양식 데이터 모델 요소는 상속 아이콘이 표시되지 않으며 바인딩을 허용합니다. CQ-4261089용 핫픽스
* 인쇄 채널 렌더링 API에 API의 매개 변수로 데이터를 전달하는 옵션이 없습니다. CQ-4263540용 핫픽스
* 문자열 필드/변수에 대한 바인딩 형식이 텍스트 조각에서 없음/데이터 모델 개체로 변경되면 에이전트가 편집 가능 확인란이 선택 취소되므로 에이전트 설정이 표시되지 않습니다. CQ-4261953용 핫픽스
* 에이전트 UI 제출 시 결과 웹 데이터 json 파일은 상속이 취소된 바인딩되지 않은 필드에 대한 정보를 저장합니다. CQ-4265621용 핫픽스

**양식 - 워크플로우**

* 응용 양식 앱의 보낼 편지함에서 양식을 다시 제출하면 데이터가 손실됩니다. NPR-28345: CQ-4260929용 핫픽스
* 변수가 아닌 사례에 대해 저장하는 동안 문서가 닫히지 않습니다. CQ-4269784용 핫픽스
* 응용 양식 앱에서 Microsoft Windows 8.1에 대한 지원이 삭제되었습니다. CQ-4265274용 핫픽스
* 2MB 이상의 이미지가 [!DNL Experience Manager Forms] 앱의 Android 버전에서 양식에 대한 필드 수준의 첨부 파일로 첨부된 경우 앱이 충돌합니다. CQ-4265578용 핫픽스

* 작업 지정에서 대화형 통신 인쇄 채널에 대한 미리 채우기 옵션이 활성화되었습니다. CQ-4265577용 핫픽스
* 사용자는 작업이 지정된 그룹의 구성원이 될 때까지 공유 작업을 볼 수 없습니다. CQ-4248733용 핫픽스
* 응용 양식 앱에서 JEE 애플리케이션 저장 또는 제출은 Windows에서 차단됩니다. CQ-4268704용 핫픽스
* 양식 데이터 모델 변수와 연관된 양식 데이터 모델이 표시되지 않습니다. CQ-4266554용 핫픽스
* 변수 지원을 사용한 문서 기호의 상태 변수를 지원하지 않습니다. CQ-4266312용 핫픽스
* 모음 문자로 인해 작업 영역에서 제출되지 않습니다. CQ-4263172용 핫픽스
* 업그레이드된 설정에서, 워크플로우가 편집을 위해 열려 있는 경우 감시 폴더 UI(사용자 인터페이스)의 워크플로우 이름 대신 오류가 표시됩니다. CQ-4238579용 핫픽스

**양식 - 관리**

* xsd 또는 schema.json이 아닌 확장이 업로드되면 업로드가 발생하지 않고 오류 메시지가 생성되지 않습니다. CQ-4266716용 핫픽스

**양식 - 서신 관리**

* [!DNL Experience Manager Forms] 6.5 CCR UI(Create Correspondence UI)에서 [!DNL Experience Manager Forms] 6.3으로 작성된 서신을 열지 못합니다. CQ-4266392에 대한 핫픽스
* DDE 데이터 유형이 숫자 유형인 경우 XDP의 Sum 함수가 작동하지 않습니다. CQ-4227403용 핫픽스
* 자산이 게시될 때 마지막 수정 시간이 업데이트되지 않으므로 메모리 내 캐시 무효화 로직의 문자가 업데이트됩니다. CQ-4250465용 핫픽스
* 문서 조각, DD 및 문자를 게시할 수 없습니다. CQ-4272893용 핫픽스

#### Forms JEE 설치 프로그램

**PDF 생성기**

* 64비트 JDK로 인해 CAD 파일이 PDF로 변환되지 않습니다. NPR-29924, NPR-29925: CQ-4272113용 핫픽스
* HTMLtoPDF 변환을 위해 PhantomJS 이름이 WebToPDF로 대체되었습니다. NPR-29933: CQ-4234545용 핫픽스
* zip 파일을 PDF로 변환하는 중에 오류가 발생했습니다. CQ-4268628용 핫픽스

**양식 - 디자이너**

* [!DNL Experience Manager Forms Designer]를 사용하여 작성된 정적 PDF에서 전체 액세스 가능성 검사를 수행하면 누락된 언어 속성으로 인해 기본 언어 검사가 실패합니다. CQ-4272923, CQ-4271002용 핫픽스

**양식 - 문서 보안**

* HSM(하드웨어 보안 모듈)을 사용한 디지털 서명이 Java 11 및 Java 8이 설치된 OSGi Linux에서 작동하지 않습니다\. NPR-29838: CQ-4270441용 핫픽스
* HSM(하드웨어 보안 모듈)을 사용한 디지털 서명이 JEE Linux 및 모든 지원 앱 서버(예: JBoss 및 Websphere)에서 작동하지 않습니다. NPR-29839: CQ-4266721용 핫픽스
* PAdES(PDF 고급 전자 서명)를 사용하여 PDF에서 서명을 확인하면 InvalidOperationException이 생성됩니다. NPR-29842: CQ-4244837용 핫픽스
* Office 2019에 대한 문서 보안 확장 지원이 추가되었습니다\. CQ-4254369, CQ-4259764용 핫픽스

**양식 - 문서 서비스**

* 양식 필드에 모양 사전이 없기 때문에 PDF가 PDF/A-1b로 변환되지 않습니다. NPR-29940: CQ-4269618용 핫픽스

* OSGi: 렌더링 중에 생성된 페이지 수를 확인할 수 없습니다. NPR-28922: CQ-4270870용 핫픽스
* [!DNL Experience Manager Forms OSGi]에서 양식 서비스를 사용하는 정적 PDF에 대한 지원을 사용하도록 설정되었습니다. NPR-28572: CQ-4270869용 핫픽스
* XMLForm.exe에 대한 권한을 변경할 수 없습니다. NPR-29828, NPR-29237: Q-4267080용 핫픽스
* [!DNL Experience Manager Forms] 서버의 출력 모듈에서 작성된 정적 PDF가 언어 속성/태그를 작성된 문서의 언어로 채우지 않습니다. NPR-27332: CQ-4271002용 핫픽스

**양식 - 기초 JEE**

* 최종 아티팩트에서 사용할 수 없는 pdfg_srt로 인해 설치 프로그램에 오류가 발생합니다. NPR-29854: CQ-4270137용 핫픽스
* LCBackupMode.sh가 작동하지 않습니다. NPR-29840: CQ-4269424용 핫픽스
* WebSphere의 UI(사용자 인터페이스)에서 UDP 포트 참조를 제거해야 합니다. CQ-4264782용 핫픽스

### 기능 팩이 포함됨

#### 자산 - 포함

* [!DNL Experience Manager Assets]에 대한 다중 사이트 관리자 지원이 활성화되었습니다. 자세한 내용은 [Experience Manager Assets에 MSM을 사용하여 자산 재사용](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/reuse-assets-using-msm.html)을 참조하십시오. NPR-29199: CQ-4259922용 핫픽스

#### 사이트 - 포함

* [!DNL Experience Manager] 경험 구성 요소를 [!DNL Adobe Target]으로 내보냅니다. 자세한 내용은 [경험 구성요소 링크 재작성기 공급자 - HTML](https://helpx.adobe.com/kr/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML)을 참조하십시오. CQ-4265469용 핫픽스

#### 양식 - 문서 서비스 - 포함

* OSGi만 해당: 출력 및 양식 서비스에 새 속성 PAGECOUNT가 추가되었습니다.. NPR-28922: CQ-4270870용 핫픽스
* OSGI만 해당: 양식 서비스를 사용한 정적 PDF 작성을 지원하도록 설정되었습니다. NPR-28572: CQ-4270869용 핫픽스
* 관리자 및 루트 사용자에 대해 XMLForm.exe에 대한 권한을 사용하도록 설정했습니다. NPR-29237: CQ-4267080용 핫픽스

### OSGi 번들 및 콘텐츠 패키지

다음 텍스트 문서에는 [!DNL Experience Manager] 6.5.1.0에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

[!DNL Experience Manager] 6.5.1.0에 포함된 OSGi 번들 목록

[파일 가져오기](assets/6_5-bundle-list.txt)

[!DNL Experience Manager] 6.5.1.0에 포함된 컨텐츠 패키지 목록

[파일 가져오기](assets/6_5-content-package-list.txt)
