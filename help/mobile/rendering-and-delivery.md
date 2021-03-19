---
title: 렌더링 및 전달
seo-title: 렌더링 및 전달
description: 렌더링 및 전달
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 8%

---


# 렌더링 및 배달{#rendering-and-delivery}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM 컨텐츠는 [Sling Default Servlets](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)를 통해 쉽게 렌더링하여 [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) 및 기타 형식을 렌더링할 수 있습니다.

기본 렌더링은 일반적으로 저장소를 그대로 표시하고 컨텐츠를 그대로 반환합니다.

또한 AEM은 Sling을 통해 렌더링된 스키마 및 컨텐츠를 완벽하게 제어할 수 있도록 사용자 정의 슬링 렌더러를 개발 및 배포할 수 있습니다.

컨텐츠 서비스 기본 렌더러는 바로 사용 가능한 슬링 기본값과 사용자 정의 개발 간의 공백을 메우므로 개발 없이 렌더링된 컨텐츠의 다양한 측면을 사용자 요구에 맞게 구성하고 제어할 수 있습니다.

다음 다이어그램은 콘텐츠 서비스 렌더링을 보여줍니다.

![chlimage_1-15](assets/chlimage_1-15.png)

## JSON {#requesting-json} 요청

**&lt;RESOURCE.caas[을(를) 사용합니다.&lt;export-config>.][&lt;export-config>.** jsonto request JSON.]

<table>
 <tbody>
  <tr>
   <td>리소스</td>
   <td>/content/entities<br /> 또는 <br /> 아래의 엔티티 리소스</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>선택 사항</strong><br /> </p> <p>/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br />에 있는 내보내기 구성이 생략되면 기본 내보내기 구성이 적용됩니다. </p> </td>
  </tr>
  <tr>
   <td>심도-INT</td>
   <td><strong>선택 </strong><br /> <br /> 사항스링 렌더링에 사용된 자식 렌더링을 위한 심도 재귀</td>
  </tr>
 </tbody>
</table>

## 내보내기 구성 만들기 {#creating-export-configs}

JSON 렌더링을 사용자 지정하기 위해 내보내기 구성을 만들 수 있습니다.

*/apps/mobileapps/caas/exportConfigs 아래에 구성 노드를 만들 수 있습니다.*

| 노드 이름 | 구성 이름(렌더링 선택기용) |
|---|---|
| jcr:primaryType | nt:unstructured |

다음 표는 내보내기 구성의 속성을 보여줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>이름</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>기본값(설정되지 않은 경우)</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>String[]</td>
   <td>모든 항목 포함</td>
   <td>sling:resourceType</td>
   <td>지정된 sling:resourceType을 JSON 내보내기 시 지정된 sling:node에 대한 세부 사항 제외</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>문자열[]</td>
   <td>nothing</td>
   <td>sling:resourceType</td>
   <td>지정된 sling:resourceType을 JSON 내보내기 시 사용하는 노드에 대한 세부 사항만 포함</td>
  </tr>
  <tr>
   <td>excludePropertyPrefix</td>
   <td>문자열[]</td>
   <td>nothing</td>
   <td>속성 접두어</td>
   <td>JSON 내보내기에서 지정된 접두사로 시작하는 속성 제외</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>문자열[]</td>
   <td>nothing</td>
   <td>속성 이름</td>
   <td>JSON 내보내기에서 지정된 속성 제외</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>문자열[]</td>
   <td>모든 항목 포함</td>
   <td>속성 이름</td>
   <td><p>excludePropertyPrefix가 설정된<br />에는 접두사가 제외되는 것과 일치하지만 지정된 속성이 포함됩니다.</p> <p>else(exclude properties ignored)에는 이러한 속성만 포함</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>문자열[]</td>
   <td>모든 항목 포함</td>
   <td>하위 이름</td>
   <td>JSON 내보내기에서 지정된 하위 항목 제외</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>String[]<br /> <br /> </td>
   <td>nothing</td>
   <td>하위 이름</td>
   <td>JSON 내보내기에서 지정된 자식만 포함, 다른 항목 제외</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>nothing</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>바꿀 때 속성 이름 바꾸기</td>
  </tr>
 </tbody>
</table>

### 리소스 유형 내보내기가 {#resource-type-export-overrides} 재정의

*/apps/mobileapps/caas/exportConfigs 아래에 구성 노드를 만듭니다.*

| 이름 | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

다음 표는 속성을 보여 줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>이름</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>기본값(설정되지 않은 경우)</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>&lt;selector_to_inc&gt;</td>
   <td>문자열[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>다음 리소스 유형에 대해 기본 CaaS json 내보내기를 반환하지 마십시오.<br /> 리소스를 다음으로 렌더링하여 고객 json 내보내기를<br /> &lt;resource&gt; 반환합니다.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### 기존 콘텐츠 서비스 내보내기 구성 {#existing-content-services-export-configs}

컨텐트 서비스에는 다음과 같은 2가지 내보내기 구성이 있습니다.

* 기본값(지정된 구성 없음)
* 페이지(사이트 페이지를 렌더링하려면)

#### 기본 내보내기 구성 {#default-export-configuration}

구성이 요청된 URI에 지정된 경우 Content Services 기본 내보내기 구성이 적용됩니다.

&lt;resource>.caas[.&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>이름</strong></td>
   <td><strong>값</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefix</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description<br /> jcr:description jcr:lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>JSON 재정의 처리</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 페이지 내보내기 구성 {#page-export-configuration}

이 구성은 하위 노드 아래의 그룹화 하위 노드를 포함하도록 기본값을 확장합니다.

&lt;site_page>.caas.page[.&lt;depth-int>].json

### 추가 리소스 {#additional-resources}

콘텐츠 서비스의 추가 항목에 대한 자세한 내용은 아래 리소스를 참조하십시오.

* [모델 개발](/help/mobile/administer-mobile-apps.md)
* [콘텐츠 서비스 작성](/help/mobile/develop-content-as-a-service.md)
* [컨텐츠 서비스 관리](/help/mobile/developing-content-services.md)

