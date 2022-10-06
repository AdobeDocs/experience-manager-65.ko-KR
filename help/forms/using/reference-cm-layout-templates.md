---
title: 참조 문자 템플릿
seo-title: Reference letter templates
description: AEM Forms에서는 문자를 신속하게 만드는 데 사용할 수 있는 서신 관리 편지 레이아웃 템플릿을 제공합니다.
seo-description: AEM Forms provides Correspondence Management letter layout templates that you can use to create letters quickly.
uuid: 3b2312d9-daa0-435b-976f-4969b54c5056
products: SG_EXPERIENCEMANAGER/6.3/FORMS
content-type: reference
topic-tags: correspondence-management
discoiquuid: afeb9f4d-3feb-4a0e-8884-e3ec1309b33b
exl-id: 40d127b5-1ce6-41fb-ac4c-2bf7ae79da82
source-git-commit: 1def8ff7bc90e2ab82ce8b50277a97da9709c78c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 참조 문자 템플릿 {#reference-letter-templates}

서신 관리에서 편지 템플릿에는 일반적인 양식 필드, 머리글 및 바닥글과 같은 레이아웃 기능 및 컨텐츠 배치에 대한 빈 &quot;대상 영역&quot;이 포함되어 있습니다.

서신 관리는 [AEM Forms 추가 기능 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). 브랜딩 및 비즈니스 요구에 따라 Designer에서 템플릿을 사용자 지정할 수 있습니다. 패키지에는 다음 템플릿이 들어 있습니다.

* 클래식
* 클래식 단순
* 왼쪽 균형
* 균형 잡힌 오른쪽
* Visual Left
* Visual Top
* Visual Top - Classic

패키지를 설치하면 레이아웃 템플릿(XDP)이 다음 위치의 템플릿 폴더에 나열됩니다.

`https://'[server]:[port]'/[context-root]/aem/forms.html/content/dam/formsanddocuments/templates-folder`

다음은 이 패키지의 모든 템플릿의 공통 필드입니다.

* 날짜
* 인사말
* 텍스트 닫기
* 서명 텍스트

![나열된 모든 CM 문자 템플릿](assets/templatescorrespondence.png)

AEM-FORMS.-6.3-REFERENCE-LAYOUT-TEMPLATES 패키지를 설치한 후 템플릿이 templates-폴더에 나열됩니다

## 클래식 {#classic}

로고가 위에 있는 클래식 템플릿은 일반 전문 편지에 적합합니다.

![클래식](assets/classic.png)

클래식 템플릿을 사용하여 만든 문자의 PDF 미리 보기

## 클래식 단순 {#classic-simple}

전화 번호와 이메일 주소를 캡처할 필드를 포함합니다. 클래식 단순 템플릿은 수신자 주소를 입력할 수 있는 필드가 없다는 점을 제외하면 클래식 템플릿과 유사합니다.

![연락처 정보 조각](assets/classicsimple.png)

클래식 단순 템플릿을 사용하여 만든 문자의 PDF 미리 보기

## 왼쪽 균형 {#balanced-left}

균형 잡힌 왼쪽 템플릿에는 편지 왼쪽에 로고가 포함됩니다.

![좌우](assets/balancedleft.png)

균형 잡힌 왼쪽 템플릿을 사용하여 만든 편지의 PDF 미리 보기

## 균형 잡힌 오른쪽 {#balanced-right}

균형 잡힌 오른쪽 템플릿에는 회사 로고가 왼쪽에 있으며 편지 자체에 수신자 주소를 입력할 수 있는 공간을 제공합니다. 오른쪽 균형 조정 템플릿에는 편지에 페이지가 여러 개 있을 때 참조하는 바닥글도 포함되어 있습니다.

![균형](assets/balancedright.png)

오른쪽 균형 템플릿을 사용하여 만든 편지의 PDF 미리 보기

## Visual Left {#visual-left}

Visual Left 템플릿에는 페이지 왼쪽에 측면 헤드가 있고 측면 헤드에 회사 로고가 배치됩니다. Visual Left 템플릿에는 제목 필드가 있지만 바닥글이 없습니다.

![visualleft](assets/visualleft.png)

시각적 왼쪽 템플릿을 사용하여 만든 문자의 PDF 미리 보기

## Visual Top {#visual-top}

Visual Top 템플릿의 맨 위에는 시각적 여백이 있습니다. Visual Top 템플릿에는 페이지 자체에 수신자 주소를 입력하는 필드가 있습니다. 시각적 상단 템플릿에는 여러 페이지로 확장되는 문자를 참조하는 제목 필드와 바닥글이 있습니다.

![visualtop](assets/visualtop.png)

시각적 상단 템플릿을 사용하여 만든 편지의 PDF 미리 보기

## Visual Top - Classic {#visual-top-classic}

Visual Top - Classic 템플릿에는 회사 로고가 있는 페이지 맨 위에 헤더가 있습니다. Visual Top - Classic 템플릿에는 제목을 입력할 필드가 있지만 바닥글은 없습니다.

![visualtopclassic](assets/visualtopclassic.png)

Visual Top - Classic 템플릿을 사용하여 만든 문자의 PDF 미리 보기
