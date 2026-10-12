---
title: 이미지 편집기
description: 이미지 편집기는 AEM의 핵심 조각으로, 구성 요소에서 컨텐츠 작성자가 이미지를 쉽게 조작할 수 있도록 사용할 수 있습니다.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 17%
---
# 이미지 편집기{#image-editor}

이미지 편집기는 AEM의 핵심 조각으로, 구성 요소에서 컨텐츠 작성자가 이미지를 쉽게 조작할 수 있도록 사용할 수 있습니다.

>[!CAUTION]
>
>이 문서에 설명된 이미지 편집기의 기능을 사용하려면 [기능 팩 24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267)을 설치해야 합니다.

## 이미지 맵의 상대 단위 {#relative-units-for-image-map}

이미지 편집기는 이미지 맵 영역을 절대 단위와 상대 단위로 유지합니다. 상대 단위는 응답형 이미지 구성 요소에서 클라이언트측의 이미지 맵(이미지 크기에 상대적)의 크기를 동적으로 조정하기 위한 데이터 속성으로 제공될 때 유용합니다.

### imageMap 속성 {#imagemap-property}

이미지 맵 좌표는 이미지 편집기에서 JCR에 `imageMap` 속성으로 유지됩니다. 형식은 다음과 같습니다.

이 속성은 다음과 같이 맵 영역을 저장합니다.

`[area1][area2][...]`

영역 형식:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

예:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## SVG 이미지 지원 {#support-for-svg-images}

이미지 편집기에서 지원하는 확장 가능한 벡터 그래픽(SVG)

* DAM에서의 SVG 자산 드래그 앤 드롭과 로컬 파일 시스템에서의 SVG 파일 업로드를 모두 지원합니다.

## MIME 유형별 플러그인 활성화 {#enabling-plugins-by-mime-type}

특정 상황에서 서버측 처리를 지원하지 않기 때문에 특정 MIME 유형에 대해 작성 작업을 제한해야 합니다. 예를 들어 SVG 이미지 편집이 허용되지 않을 수 있습니다.

이미지 편집기의 플러그인은 개별 플러그인의 구성 노드에서 `supportedMimeTypes` 속성을 설정하여 MIME 유형별로 선택적으로 활성화할 수 있습니다.

### 예 {#example}

예를 들어 자르기 기능은 GIF, JPEG, PNG, WEBP 및 TIFF 이미지에만 허용되어야 한다고 가정해 보겠습니다.

그런 다음 `supportedMimeTypes` 속성을 이미지 구성 요소의 `cq:editConfig` 노드에 있는 플러그인의 구성 노드에서 허용된 MIME 형식의 문자열로 설정해야 합니다.

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
