---
title: 번역 통합 프레임워크 구성
seo-title: 번역 통합 프레임워크 구성
description: 번역 통합 프레임워크를 구성하는 방법을 알아봅니다.
seo-description: 번역 통합 프레임워크를 구성하는 방법을 알아봅니다.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
translation-type: tm+mt
source-git-commit: 98dd2d3e7445ceda6d96f0dd11b39d8361f1f402

---


# 번역 통합 프레임워크 구성{#configuring-the-translation-integration-framework}

번역 통합 프레임워크는 타사 번역 서비스와 통합되므로 AEM 컨텐츠 번역을 조정할 수 있습니다.

* 번역 서비스 공급자에 연결합니다.
* 번역 통합 프레임워크 구성을 만듭니다.
* 클라우드 구성을 페이지와 연결합니다.

AEM의 컨텐츠 번역 기능에 대한 개요는 다국어 [사이트에 대한 컨텐츠 번역을 참조하십시오](/help/sites-administering/translation.md).

## 번역 서비스 공급자에 연결 {#connecting-to-a-translation-service-provider}

AEM을 번역 서비스 공급자에 연결하는 클라우드 구성을 만듭니다. AEM에는 기본적으로 Microsoft Translator에 연결하는 기능이 포함되어 있습니다. 다른 번역 공급자의 경우 패키지 공유에서 커넥터 패키지를 [다운로드하십시오](/help/sites-administering/package-manager.md#package-share).
다음 번역 공급업체는 번역 프로젝트에 대한 새로운 API를 구현합니다. 통합 및 패키지 공유에서 다운로드하는 방법에 대한 자세한 내용을 살펴보려면 링크를 클릭하십시오.

* [Translation.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (Adobe Exchange Premier Partner)
* [Clay Tablet Technologies](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/clay-tablet-translation-connector-for-aem.html) (PackageShare에서 제외, 공급업체에 직접 문의)
* [Lionbridge](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lionbridge-for-adobe-experience-manager.html)
* [Cloudwords](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/cloudwords-for-adobe-translations-connector.html)
* [CrossLang NV](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/crosslang-xtm-for-adobe-experience-manager.html)
* [린고택](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lingotek-for-adobe-experience-manager.html)
* Microsoft(Microsoft Translator는 AEM에 사전 설치되어 있음)
* [스마트링](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/smartling-connector-for-adobe-experience-manager.html)
* [SDL WorldServer](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdlworldserver-connector.html)
* [SDL TMS](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdl-tms-translation-connector-for-adobe-experience-manager.html)
* [Systran](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/systran-for-adobe-experience-manager.html)
* [알틀랑](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/Altlang.html)

>[!NOTE]
>
>인간 및 기계 번역 공급자의 최신 목록을 살펴보려면 다음 페이지를 참조하십시오.
>
>
>* [AEM Human Translation](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM 기계 번역](https://www.adobe.com/go/aem-machine-translation-connectors)
>



커넥터 패키지를 설치한 후 커넥터에 대한 클라우드 구성을 만들 수 있습니다. 일반적으로 번역 서비스로 인증하기 위해 자격 증명을 제공해야 합니다. Microsoft Translator 커넥터에 대한 클라우드 구성 추가에 대한 자세한 내용은 Microsoft [Translator와 통합을 참조하십시오](/help/sites-administering/tc-msconf.md).

필요한 경우 동일한 커넥터에 여러 클라우드 구성을 만들 수 있습니다. 예를 들어, 동일한 공급업체와 함께 있는 각 계정 또는 프로젝트에 대해 하나의 구성을 만듭니다.

연결을 구성한 후 이를 사용하는 번역 통합 프레임워크 구성을 만들 수 있습니다.

## 번역 통합 구성 만들기 {#creating-a-translation-integration-configuration}

번역 통합 프레임워크 구성을 만들어 컨텐츠를 변환하는 방법을 지정합니다. 구성에는 다음 정보가 포함됩니다.

* 사용할 번역 서비스 공급자입니다.
* 인간 번역 또는 기계 번역 수행 여부.
* 페이지와 연결된 다른 컨텐츠 또는 태그 등의 자산을 번역할지 여부.

프레임워크 구성을 만든 후 클라우드 구성을 구성에 따라 번역할 페이지와 연결합니다. 번역 프로세스가 시작되면 번역 워크플로우는 관련 프레임워크 구성에 따라 진행됩니다.

웹 사이트의 각 섹션에 번역 요구 사항이 서로 다른 경우 그에 따라 여러 프레임워크 구성을 만듭니다. 예를 들어 다국어 웹 사이트에는 영어, 스페인어 및 일본어 복사본이 포함됩니다. 사이트 소유자는 스페인어와 일본어 번역본을 두 개의 서로 다른 번역 서비스 제공업체를 사용합니다. 따라서 프레임워크의 두 구성이 구성됩니다. 각 구성에서는 다른 번역 서비스 공급자를 사용합니다.

번역 통합 프레임워크를 구성한 후 이를 사용하는 페이지에 [](/help/sites-administering/tc-prep.md) 연결할 수 있습니다.

**참고:** AEM의 컨텐츠 번역 기능에 대한 개요는 다국어 [사이트에 대한 컨텐츠 번역을 참조하십시오](/help/sites-administering/translation.md).

프레임워크의 단일 구성은 페이지 컨텐츠, 커뮤니티 컨텐츠 및 자산을 변환하는 방법을 제어합니다.
![chlimage_1-386](assets/chlimage_1-386.png)

### 사이트 구성 속성 {#sites-configuration-properties}

사이트 속성은 페이지 컨텐츠의 번역 수행 방식을 제어합니다.

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>번역 워크플로</td>
   <td><p>프레임워크에서 사이트 컨텐츠에 대해 수행하는 번역 방법을 선택합니다.</p>
    <ul>
     <li>기계 번역:번역 제공자는 기계 번역을 사용하여 실시간으로 번역을 수행합니다.</li>
     <li>인간 번역:번역자가 번역하기 위해 컨텐츠가 번역 공급자로 전송됩니다. </li>
     <li>번역 안 함:번역용으로 컨텐츠가 전송되지 않습니다. 이는 번역되지 않지만 최신 컨텐츠로 업데이트할 수 있는 특정 컨텐츠 분기를 건너뛰려는 것입니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>번역 공급자</td>
   <td>번역 공급자를 선택하여 변환을 수행합니다. 해당 커넥터를 설치하면 공급자가 목록에 나타납니다.</td>
  </tr>
  <tr>
   <td>컨텐츠 카테고리</td>
   <td>(기계 번역 전용) 번역하려는 컨텐츠를 설명하는 범주입니다. 카테고리는 컨텐츠를 변환할 때 용어 및 구문 선택에 영향을 줄 수 있습니다.</td>
  </tr>
  <tr>
   <td>태그 번역</td>
   <td>페이지와 연결된 태그를 번역하려면 선택합니다.</td>
  </tr>
  <tr>
   <td>페이지 자산 번역</td>
   <td><p>파일 시스템에서 구성 요소에 추가되거나 자산에서 참조되는 자산을 변환하는 방법을 선택합니다.</p>
    <ul>
     <li>번역 안 함:페이지 자산은 번역되지 않습니다.</li>
     <li>사이트 번역 워크플로우 사용:자산은 사이트 탭의 구성 속성에 따라 처리됩니다.</li>
     <li>자산 번역 워크플로우 사용:자산은 자산 탭의 속성 구성에 따라 처리됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>번역 자동 실행</td>
   <td>번역 프로젝트를 만든 후 번역 작업을 자동으로 실행하려면 선택합니다. 이 옵션을 선택하면 번역 작업을 검토하고 범위를 지정할 수 있는 기회가 없습니다.</td>
  </tr>
 </tbody>
</table>

### 커뮤니티 구성 속성 {#communities-configuration-properties}

커뮤니티 속성은 사용자 생성 컨텐츠의 번역 수행 방식을 제어합니다. 사용자 생성 컨텐츠의 번역은 항상 기계 번역을 사용합니다. 자세한 내용은 사용자 생성 [컨텐츠 변환을 참조하십시오](/help/communities/translate-ugc.md).

| 속성 | 설명 |
|---|---|
| 번역 공급자 | 번역 공급자를 선택하여 변환을 수행합니다. 클라우드 구성이 생성된 공급자가 목록에 표시됩니다. |
| 컨텐츠 카테고리 | 번역하려는 컨텐츠를 설명하는 카테고리. 카테고리는 컨텐츠를 변환할 때 용어 및 구문 선택에 영향을 줄 수 있습니다. |
| 글로벌 공유 스토어로 사용할 로케일 선택 | (선택 사항) UGC를 저장할 로케일을 선택하면 모든 언어 사본의 게시물이 하나의 글로벌 대화로 표시됩니다. 규칙에 따라 웹 사이트의 [기본 언어에](/help/communities/sites-console.md#translation) 대한 로케일을 선택합니다. [공통 스토어 없음]을 선택하면 글로벌 번역이 비활성화됩니다. 기본적으로 글로벌 번역은 비활성화됩니다. |

### 자산 구성 속성 {#assets-configuration-properties}

자산 속성은 자산을 구성하는 방법을 제어합니다. 자산 번역에 대한 자세한 내용은 자산에 [대한 언어 사본 만들기를 참조하십시오](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>번역 워크플로</td>
   <td><p>프레임워크에서 자산에 대해 수행하는 번역 유형을 선택합니다.</p>
    <ul>
     <li>기계 번역:번역 제공자는 기계 번역을 사용하여 번역을 즉시 수행합니다.</li>
     <li>인간 번역:컨텐츠는 번역 공급자로 자동 전송되어 수동으로 변환됩니다. </li>
     <li>번역 안 함:자산을 번역하기 위해 전송하지 않습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>번역 공급자</td>
   <td>번역 공급자를 선택하여 변환을 수행합니다. 해당 커넥터를 설치하면 공급자가 목록에 나타납니다.</td>
  </tr>
  <tr>
   <td>컨텐츠 카테고리</td>
   <td>(기계 번역 전용) 번역하려는 컨텐츠를 설명하는 범주입니다. 카테고리는 컨텐츠를 변환할 때 용어 및 구문 선택에 영향을 줄 수 있습니다.</td>
  </tr>
  <tr>
   <td>자산 번역</td>
   <td>번역 프로젝트에 자산을 포함하려면 선택합니다. </td>
  </tr>
  <tr>
   <td>메타데이터 번역</td>
   <td>자산 메타데이터를 변환하려면 선택합니다.</td>
  </tr>
  <tr>
   <td>태그 번역</td>
   <td>자산과 연결된 태그를 번역하려면 선택합니다.</td>
  </tr>
  <tr>
   <td>번역 자동 실행</td>
   <td>번역 프로젝트를 만든 후 번역 작업을 자동으로 실행하려면 선택합니다. 이 옵션을 선택하면 변환 작업을 검토하거나 범위를 지정할 수 있는 기회가 없습니다.</td>
  </tr>
 </tbody>
</table>

1. 사이드 바에서 도구 > 작업 > 클라우드 > 클라우드 서비스를 클릭하거나 탭합니다.
1. 번역 통합 영역에서 생성된 구성이 무엇인지에 따라 표시되는 링크가 결정됩니다.

   * 구성이 만들어지지 않은 경우 지금 구성을 클릭하거나 탭합니다.
   * 구성이 이미 있는 경우 구성 표시를 클릭하거나 탭한 다음 사용 가능한 구성 옆에 나타나는 + 링크를 클릭하거나 탭합니다.

1. 구성 이름을 입력한 다음 만들기를 클릭하거나 탭합니다.
1. 사이트, 커뮤니티 및 자산 탭에서 속성을 구성한 다음 확인을 클릭하거나 탭합니다.

## 번역 페이지 구성 {#configuring-pages-for-translation}

소스 페이지의 번역을 다른 언어로 구성하려면 페이지를 다음 클라우드 구성과 연결하십시오.

* AEM을 번역 공급자에 연결하는 클라우드 구성
* 변환의 세부 사항을 구성하는 번역 통합 프레임워크입니다.

번역 통합 프레임워크 클라우드 구성은 서비스 공급자에 연결하는 데 사용할 클라우드 구성을 식별합니다. 소스 페이지를 프레임워크 클라우드 구성과 연결할 때 페이지는 프레임워크 클라우드 구성이 사용하는 서비스 공급자 클라우드 구성과 연결되어 있어야 합니다.

페이지를 클라우드 구성과 연결할 때 페이지의 하위 멤버는 연결을 상속합니다. 예를 들어 /content/geometrixx/en/products 페이지를 번역 통합 프레임워크와 연결하는 경우 제품 페이지와 그 아래의 모든 페이지가 프레임워크에 따라 번역됩니다.

필요한 경우 하위 페이지에서 연결을 재정의할 수 있습니다. 예를 들어 웹 사이트의 컨텐츠는 대부분 의류에 관한 것입니다. 하지만, 한 페이지 분기에서 회사에 대해 설명합니다. 사이트의 루트 페이지는 의류 카테고리를 사용하여 기계 번역을 지정하는 번역 통합 프레임워크와 연결됩니다. 회사를 설명하는 분기는 일반 카테고리를 사용하여 기계 번역을 수행하는 프레임워크를 사용합니다.

또한 페이지의 모든 커뮤니티 [SCF 구성 요소에](/help/communities/scf.md) 대해 사용자가 생성한 콘텐츠(UGC)에는 사용자가 컨텐츠를 변환할 수 있는 기능이 포함됩니다. 자세한 내용은 사용자 생성 [컨텐츠 번역을 참조하십시오](/help/communities/translate-ugc.md).

### 번역 공급자에 페이지 연결 {#associating-a-page-with-a-translation-provider}

페이지 및 하위 페이지를 번역하는 데 사용하는 번역 공급자와 페이지를 연결합니다.

1. 사이트 콘솔에서 구성할 페이지를 선택하고 속성 보기를 클릭하거나 탭합니다.
1. 편집을 클릭하거나 탭한 다음 클라우드 서비스 탭을 클릭하거나 탭합니다.
1. 구성 추가 > 번역 통합을 클릭하거나 탭합니다.
1. 사용할 번역 공급자를 선택한 다음 완료를 클릭하거나 탭합니다.

### 번역 통합 프레임워크와 페이지 연결 {#associating-pages-with-a-translation-integration-framework}

페이지 및 하위 페이지의 번역 수행 방법을 정의하는 번역 통합 프레임워크와 페이지를 연결합니다.

1. 사이트 콘솔에서 구성할 페이지를 선택하고 속성 보기를 클릭하거나 탭합니다.
1. 편집을 클릭하거나 탭한 다음 클라우드 서비스 탭을 클릭하거나 탭합니다.
1. 구성 추가 > 번역 통합을 클릭하거나 탭합니다.
1. 사용할 번역 통합 프레임워크를 선택한 다음 완료를 클릭하거나 탭합니다.

