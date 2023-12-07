---
title: 인터페이스의 색상 구성표 변경
description: AEM Forms 작업 영역 사용자 인터페이스 부분의 색상 구성표를 선택적으로 수정하는 방법입니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 인터페이스의 색상 구성표 변경 {#changing-the-color-scheme-of-the-interface}

요구 사항에 맞게 AEM Forms 작업 공간 사용자 인터페이스 부분의 색상 구성표를 수정할 수 있습니다. 다음은 대표적인 색상 구성표 사용자 지정의 몇 가지 예입니다. 이 문서에 설명된 단계 외에 [AEM Forms 작업 공간 사용자 정의에 대한 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md).

## 상단 탐색 막대 {#top-navigation-bar}

### 배경 이미지 사용 {#using-background-image}

AEM Forms 작업 영역 상단에 있는 탐색 모음을 업데이트하려면

1. 색상을 업데이트할 배경 이미지를 만듭니다. 파일 이름을 newBackground.jpg로 지정합니다.
1. WebDAV 클라이언트를 사용하여 /apps/ws/images 폴더에 배경 이미지 파일을 업로드합니다.

   >[!NOTE]
   >
   >WebDAV 액세스에 대한 자세한 내용은 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko-KR).

1. 다음 스타일을 추가하여 /apps/ws/css/newStyle.css에서 새 배경 이미지를 참조합니다.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### CSS에서 color 속성 사용 {#using-color-property-in-css}

1. /apps/ws/css의 newStyle.css에 다음 스타일을 추가합니다.

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 범주 구성 요소 {#category-component}

범주 구성 요소는 왼쪽 패널에 작업의 다양한 범주를 표시합니다. 색상을 변경하려면에서 배경색을 정의합니다 `.category` CSS 파일의 요소입니다.

## 작업 구성 요소 {#task-component}

작업은 TaskList 구성 요소라는 중간 패널에 표시됩니다. 색상을 변경하려면 스타일 시트에서 .task 선택기와 연관된 스타일을 수정합니다.
