---
title: 미디어 [!DNL Adobe Experience Manager Assets] 라이브러리(CC) 솔루션
description: 비교 [!DNL Experience Manager Assets] 및 미디어 라이브러리 솔루션을 통해 차이점을 파악할 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 3%

---


# [!DNL Experience Manager Assets] 대 [!DNL Experience Manager] 미디어 라이브러리 {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] 는 [!DNL Experience Manager] 플랫폼의 필수 요소입니다. 이러한 매끄러운 통합은 컨텐츠 저자의 주요 장점으로 [!DNL Experience Manager] 간주되므로 컨텐츠 관리의 일관성을 유지하고 생산성을 높일 수 있습니다.

## FAQ {#frequently-asked-questions}

### 그게 [!DNL Assets]뭐야? {#what-is-aem-assets}

[!DNL Assets] 이 기능은 사용자가 웹 기반 저장소에서 디지털 자산(이미지, 비디오, 문서 및 오디오 클립)을 관리할 수 [!DNL Experience Manager] 있도록 해주는 기능입니다. [!DNL Assets] 메타데이터 지원, 변환, 파인더 및 관리 인터페이스 포함

### 미디어 라이브러리란 [!DNL Experience Manager] 무엇입니까? {#what-is-the-aem-media-library}

미디어 라이브러리 [!DNL Experience Manager] 는 이미지와 기타 공유 리소스가 저장되는 WCM 컨텐츠 [!DNL Experience Manager] 저장소의 지정된 부분입니다. 미디어 라이브러리는 WCM에 기본적인 디지털 자산 관리 기능을 제공합니다.

### WCM에 속하지 않은 [!DNL Assets] 것에서 무엇을 얻을 수 있습니까? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

고객의 고유한 기능은 다음과 [!DNL Assets] 같습니다.

* 제목, 태그 및 설명 이외의 메타데이터를 추출하고 편집할 수 있습니다.
* 시작 화면에서 [!DNL Assets] 사용할 수 있는 관리자.
* 수집, 자산 삭제, 하위 자산 처리, 메타데이터 추출 등 디지털 자산 관리와 관련된 모든 워크플로우 단계
* 패키지 공간 `dam` 에 있는 라이브러리

이러한 기능을 사용하려면 유효한 사용권이 필요합니다 [!DNL Assets].

### 별도의 패키지로 [!DNL Assets] 제공됩니까? {#is-aem-assets-available-as-a-separate-package}

아니오. 모든 애플리케이션과 Add-on은 설치 및 배포가 용이하도록 모든 기능이 포함된 하나의 패키지로 제공됩니다. [!DNL Experience Manager] 이는 패키지의 모든 기능을 사용할 수 있는 권한이 있다는 의미는 아닙니다.

### 디지털 자산의 메타데이터를 편집하려고 합니다. 필요합니까 [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

제목, 설명 및 태그 이외의 메타데이터를 편집하려면 라이선스가 있어야 합니다 [!DNL Assets].

### 내 웹사이트에 카테고리 조건부를 사용하고 싶다. 필요합니까 [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

예. 카테고리 술어는 [!DNL Assets] 일부이며 [!DNL Assets] 라이선스가 필요합니다.

### 가져올 때 이미지 크기를 자동으로 조정하려고 합니다. 필요합니까 [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

아니오. 정적 이미지의 크기 조정 및 자동 워크플로우 기반 변환과 변환 관리 기능은 [!DNL Experience Manager] 미디어 라이브러리의 일부입니다. 이러한 기능에는 [!DNL Assets] 라이선스가 필요하지 않습니다.

### 사용자 정의된 이미지 구성 요소를 사용하여 이미지 크기를 조정하려고 합니다. 필요합니까 [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

이미지 구성 요소는 WCM의 일부입니다. 이미지 구성 요소에서 사용 중인 그래픽 라이브러리(또한 사용) [!DNL Assets]는 [!DNL Experience Manager] 플랫폼의 일부이며 [!DNL Assets] 라이선스가 필요하지 않습니다.

### 라이선스를 부여하지 않은 [!DNL Assets] 경우 사용자가 사용하지 못하도록 하려면 어떻게 해야 합니까 [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

모든 [!DNL Assets]특정 워크플로우, 구성 요소, 분류 체계, 옵션 및 관리를 제거할 수 [!DNL Assets] 있습니다 [!DNL Experience Manager]. 이렇게 하면 사용자가 라이선스가 부여되지 않은 [!DNL Assets] 기능을 실수로 사용하지 않게 됩니다.

### 페이지에 이미지를 추가하고 이러한 이미지를 자르고 크기를 조정하려고 합니다. 자산이 필요합니까? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

이 경우 스마트 이미지 구성 요소 [!DNL Assets]를 사용하면 이미지를 페이지에 직접 업로드할 수 있으므로 미디어 라이브러리를 사용하더라도 웹 사이트에서 이미지를 사용할 필요는 없습니다.

### 미디어 라이브러리 [!DNL Assets] 와 미디어 라이브러리에서 사용할 수 있는 기능에 대한 자세한 목록 {#listoffeatures}

**Experience Manager 자산**

* 컬렉션 및 Lightbox
* 고급 메타데이터 속성 및 관리
* Adobe 자산 링크(기업 Creative Cloud에 연결)
* [!DNL Experience Manager] 데스크탑 앱
* 처리 프로필
* [!DNL Adobe InDesign Server] 통합
* 에셋 템플릿 및 카탈로그 제작 프레임워크
* [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]및 [!DNL Adobe InDesign] 통합
* 다국어 자산 관리
* PIM 통합
* 권한 관리
* Camera Raw 지원
* 검색 패싯 관리 및 구성
* 미리 만들어진 DAM 워크플로우(예: 사진 촬영)
* 인사이트라는 자산 보고 및 분석
* 3D 에셋 관리
* 연결된 자산
* Brand Portal
* 셀프 서비스 액세스
* 검색, 검색 및 다운로드
* 컬렉션 및 폴더 공유
* 관리 툴 및 인터페이스
* 스마트 태그 지정
* 시각적 검색

**미디어 라이브러리**

* 기본 메타데이터 속성
* 태그 관리
* 버전 제어
* 정적 변환
* 프로젝트, 작업, 워크플로우 제작
* 활동 스트림(타임라인)
* 쿼리 빌더(API)
* Marketing Cloud 통합
* UI 사용자 정의 및 확장
* 주석 및 주석
