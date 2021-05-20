---
title: 인터페이스의 색상 구성표 변경
seo-title: 인터페이스의 색상 구성표 변경
description: AEM Forms 작업 공간 사용자 인터페이스 부분의 색상 구성표를 선택적으로 수정하는 방법입니다.
seo-description: AEM Forms 작업 공간 사용자 인터페이스 부분의 색상 구성표를 선택적으로 수정하는 방법입니다.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 인터페이스 {#changing-the-color-scheme-of-the-interface} 의 색상 구성표 변경

요구 사항에 맞게 AEM Forms 작업 공간 사용자 인터페이스 부분의 색상 구성표를 수정할 수 있습니다. 다음은 대표 색상 구성표 사용자 지정의 몇 가지 예입니다. 이 문서에서 설명한 단계 외에 [AEM Forms 작업 공간 사용자 지정을 위한 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md)를 참조하십시오.

## 위쪽 탐색 모음 {#top-navigation-bar}

### 배경 이미지 사용 {#using-background-image}

AEM Forms 작업 공간 상단의 탐색 모음을 업데이트하려면

1. 색상을 업데이트할 배경 이미지를 만듭니다. 파일의 이름을 newBackground.jpg로 지정합니다.
1. WebDAV 클라이언트를 사용하여 /apps/ws/images 폴더에 배경 이미지 파일을 업로드합니다.

   >[!NOTE]
   >
   >WebDAV 액세스에 대한 자세한 내용은 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)을 참조하십시오.

1. 다음 스타일을 추가하여 /apps/ws/css/newStyle.css에서 새 배경 이미지를 참조합니다.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### CSS {#using-color-property-in-css}에서 색상 속성 사용

1. /apps/ws/css의 newStyle.css에 다음 스타일을 추가합니다

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 카테고리 구성 요소 {#category-component}

카테고리 구성 요소는 왼쪽 패널에 작업의 다양한 카테고리를 표시합니다. 색상을 변경하려면 CSS 파일의 `.category` 요소에 배경색을 정의합니다.

## 작업 구성 요소 {#task-component}

작업은 중간 패널에 TaskList 구성 요소라고 표시됩니다. 색상을 변경하려면 스타일시트에서 .task 선택기와 연관된 스타일을 수정합니다.
