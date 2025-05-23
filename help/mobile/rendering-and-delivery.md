---
title: 렌더링 및 게재
description: Sling 기본 서블릿을 통해 Adobe Experience Manager 콘텐츠를 렌더링하여 JSON 및 기타 형식을 렌더링하는 방법에 대해 알아봅니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# 렌더링 및 게재{#rendering-and-delivery}

{{ue-over-mobile}}

Adobe Experience Manager(AEM) 콘텐츠를 [Sling 기본 서블릿](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)을(를) 통해 손쉽게 렌더링하여 [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) 및 기타 형식을 렌더링할 수 있습니다.

이러한 기본 렌더링은 일반적으로 저장소를 이동하고 콘텐츠를 있는 그대로 반환합니다.

AEM은 Sling을 통해 사용자 지정 sling 렌더러를 개발 및 배포하여 렌더링된 스키마 및 콘텐츠를 완벽하게 제어할 수 있도록 지원합니다.

Content Services 기본 렌더러는 기본 제공 Sling 기본값과 사용자 지정 개발 간의 간격을 채우므로 개발 없이 렌더링된 콘텐츠의 여러 측면을 사용자 지정하고 제어할 수 있습니다.

다음 다이어그램은 콘텐츠 서비스의 렌더링을 보여 줍니다.

![chlimage_1-15](assets/chlimage_1-15.png)

## JSON 요청 중 {#requesting-json}

**&lt;RESOURCE.caas[ 사용&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** to request JSON.

<table>
 <tbody>
  <tr>
   <td>리소스</td>
   <td>/content/entities<br />에 엔티티 리소스 또는 /content에 컨텐츠 리소스 <br />이(가) 있습니다.</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>선택 사항</strong><br /> </p> <p>/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br />에서 내보내기 구성을 찾았습니다. 생략하면 기본 내보내기 구성이 적용됩니다. </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td>Sling 렌더링에 사용된 자식 렌더링에 대한 <strong>선택적</strong><br /> <br /> 깊이 재귀</td>
  </tr>
 </tbody>
</table>

## 내보내기 구성 생성 {#creating-export-configs}

JSON 렌더링을 사용자 지정하기 위해 내보내기 구성을 만들 수 있습니다.

*/apps/mobileapps/caas/exportConfigs.* 아래에 구성 노드를 만들 수 있습니다.

| 노드 이름 | 구성 이름(렌더링 선택기용) |
|---|---|
| jcr:primaryType | nt:unstructured |

다음 표는 구성 내보내기의 속성을 보여 줍니다.

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
   <td>sling:resourceType이 지정된 노드에 대한 세부 사항을 JSON 내보내기에서 제외</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>제외 안 함</td>
   <td>sling:resourceType</td>
   <td>json 내보내기에서 sling:resourceType이 지정된 노드에 대한 세부 정보만 포함</td>
  </tr>
  <tr>
   <td>excludePropertyPrefix</td>
   <td>String[]</td>
   <td>제외 안 함</td>
   <td>속성 접두사</td>
   <td>지정된 접두사로 시작하는 속성을 JSON 내보내기에서 제외</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>제외 안 함</td>
   <td>속성 이름</td>
   <td>json 내보내기에서 지정된 속성 제외</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>모든 항목 포함</td>
   <td>속성 이름</td>
   <td><p>excludePropertyPrefixes 집합<br />에 제외되는 접두사와 일치하지만 지정된 속성이 포함된 경우</p> <p>else(속성 제외 무시됨)에는 다음 속성만 포함됩니다</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>모든 항목 포함</td>
   <td>하위 이름</td>
   <td>json 내보내기에서 지정된 하위 항목 제외</td>
  </tr>
  <tr>
   <td>excludeChild</td>
   <td>문자열[]<br /> <br /> </td>
   <td>제외 안 함</td>
   <td>하위 이름</td>
   <td>json 내보내기에서 지정된 하위 항목만 포함, 기타 항목 제외</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>문자열[]<br /> <br /> </td>
   <td>이름 바꾸기 없음</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>대체 항목을 사용하여 등록 정보 이름 바꾸기</td>
  </tr>
 </tbody>
</table>

### 리소스 유형 내보내기 무시 {#resource-type-export-overrides}

*/apps/mobileapps/caas/exportConfigs.*&#x200B;에 구성 노드를 만듭니다.

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
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>다음 sling 리소스 유형의 경우 기본 CaaS json 내보내기를 반환하지 마십시오.<br /> 리소스를;<br /> &lt;RESOURCE&gt;(으)로 렌더링하여 고객 json 내보내기를 반환합니다.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### 기존 콘텐츠 서비스 내보내기 구성 {#existing-content-services-export-configs}

콘텐츠 서비스에는 두 가지 내보내기 구성이 포함됩니다.

* 기본값(지정된 구성 없음)
* 페이지(사이트 페이지를 렌더링하려면)

#### 기본 내보내기 구성 {#default-export-configuration}

요청한 URI에 구성이 지정된 경우 Content Services 기본 내보내기 구성이 적용됩니다.

&lt;리소스>.caas[.&lt;DEPTH-INT>].json

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
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
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
   <td>excludeChild</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON 무시</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 페이지 내보내기 구성 {#page-export-configuration}

이 구성은 하위 노드 아래에 하위 그룹화를 포함하도록 기본값을 확장합니다.

&lt;SITE_PAGE>.caas.page[.&lt;DEPTH-INT>].json

### 추가 리소스 {#additional-resources}

콘텐츠 서비스의 추가 항목에 대한 자세한 내용은 아래 리소스를 참조하십시오.

* [모델 개발](/help/mobile/administer-mobile-apps.md)
* [컨텐츠 서비스 작성](/help/mobile/develop-content-as-a-service.md)
* [Content Services 관리](/help/mobile/developing-content-services.md)
