---
title: 이미지 편집기
description: 이미지 편집기는 AEM의 핵심 조각으로, 콘텐츠 작성자가 이미지를 쉽게 조작할 수 있도록 구성 요소에서 사용할 수 있습니다.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 9%

---

# 이미지 편집기{#image-editor}

이미지 편집기는 AEM의 핵심 조각으로, 콘텐츠 작성자가 이미지를 쉽게 조작할 수 있도록 구성 요소에서 사용할 수 있습니다.

>[!CAUTION]
>
>이 문서에 설명된 이미지 편집기의 기능을 사용하려면 [기능 팩 24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 을(를) 설치해야 합니다.

## 이미지 맵의 상대 단위 {#relative-units-for-image-map}

이미지 편집기는 이미지 맵 영역을 절대 단위와 상대 단위로 유지합니다. 상대 단위는 응답형 이미지 구성 요소에서 클라이언트측의 이미지 맵(이미지 크기에 상대적)의 크기를 동적으로 조정하기 위한 데이터 속성으로 제공될 때 유용합니다.

### imageMap 속성 {#imagemap-property}

이미지 맵 좌표는 JCR에 로 유지됩니다. `imageMap` 이미지 편집기의 속성입니다. 형식은 다음과 같습니다.

이 속성은 다음과 같이 맵 영역을 저장합니다.

`[area1][area2][...]`

영역 형식:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

예:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## SVG 이미지 지원 {#support-for-svg-images}

이미지 편집기에서 확장 가능한 벡터 그래픽(SVG)을 지원합니다.

* DAM에서의 SVG 자산 드래그 앤 드롭과 로컬 파일 시스템에서의 SVG 파일 업로드를 모두 지원합니다.

## MIME 유형별 플러그인 활성화 {#enabling-plugins-by-mime-type}

특정 상황에서 서버측 처리를 지원하지 않기 때문에 특정 MIME 유형에 대해 작성 작업을 제한해야 합니다. 예를 들어 SVG 이미지 편집이 허용되지 않을 수 있습니다.

이미지 편집기의 플러그인은 다음을 설정하여 MIME 유형별로 선택적으로 활성화할 수 있습니다. `supportedMimeTypes` 개별 플러그인의 구성 노드의 속성입니다.

### 예 {#example}

예를 들어 자르기 기능은 GIF, JPEG, PNG, WEBP 및 TIFF 이미지에 대해서만 허용되어야 한다고 가정해 보겠습니다.

다음 `supportedMimeTypes` 그런 다음 플러그인의 구성 노드에서 속성을 허용된 MIME 유형의 문자열로 설정해야 합니다. `cq:editConfig` 이미지 구성 요소의 노드

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
