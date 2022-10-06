---
title: 이미지 편집기
seo-title: Image Editor
description: 이미지 편집기는 AEM의 핵심 부분이며 구성 요소에서 활용하여 컨텐츠 작성자가 이미지를 쉽게 조작할 수 있습니다.
seo-description: The Image Editor is a core piece of AEM and can be leveraged by components to facilitate the manipulation of images by content authors.
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 14%

---

# 이미지 편집기{#image-editor}

이미지 편집기는 AEM의 핵심 부분이며 구성 요소에서 활용하여 컨텐츠 작성자가 이미지를 쉽게 조작할 수 있습니다.

>[!CAUTION]
>
>이 문서에 설명된 이미지 편집기의 기능을 사용하려면 [기능 팩 24267](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 설치해야 합니다.

## 이미지 맵에 대한 상대 단위 {#relative-units-for-image-map}

이미지 편집기는 이미지 맵 영역을 절대 단위와 상대 단위로 유지합니다. 상대 단위는 응답형 이미지 구성 요소에서 클라이언트측에서 이미지 맵(이미지 크기에 상대적인)의 크기를 동적으로 조정하는 데이터 속성으로 제공되는 경우 유용합니다.

### imageMap 속성 {#imagemap-property}

이미지 맵 좌표는 JCR로 유지됩니다 `imageMap` 속성(이미지 편집기)을 기반으로 합니다. 형식은 다음과 같습니다.

속성은 맵 영역을 다음과 같이 저장합니다.

`[area1][area2][...]`

영역 형식:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

예:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## SVG 이미지 지원 {#support-for-svg-images}

확장 가능한 벡터 그래픽(SVG)은 이미지 편집기에서 지원합니다.

* DAM에서의 SVG 에셋 드래그 앤 드롭과 로컬 파일 시스템에서의 SVG 파일 업로드를 모두 지원합니다.

## MIME 유형별로 플러그인 활성화 {#enabling-plugins-by-mime-type}

특정 MIME 유형에 대해 작성 작업을 제한해야 하는데, 이는 서버측 처리에서 지원이 없기 때문입니다. 예를 들어 SVG 이미지를 편집할 수 없습니다.

이미지 편집기의 플러그인은 MIME 유형으로 `supportedMimeTypes` 개별 플러그인의 구성 노드에 대한 속성입니다.

### 예 {#example}

예를 들어 자르기 기능은 GIF, JPEG, PNG, WEBP 및 TIFF 이미지만 허용해야 한다고 가정해 보겠습니다.

다음 `supportedMimeTypes` 그런 다음 속성을 `cq:editConfig` 노드 아래에 나열된 상태로 남아 있습니다.

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
