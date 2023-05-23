---
title: PDF 생성기 구성 파일 가져오기 및 내보내기
seo-title: Importing and exporting PDF Generator configuration files
description: PDF 생성기 구성 파일을 가져오고 내보내는 방법을 알아봅니다.
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# PDF 생성기 구성 파일 가져오기 및 내보내기 {#importing-and-exporting-pdf-generator-configuration-files}

구성 파일에는 PDF, 파일 유형 및 보안 설정을 포함한 PDF 생성기 변환 정보가 포함되어 있습니다.

>[!NOTE]
>
>사용자 지정 native2pdfconfig.xml 파일을 가져와서 PDF 생성기의 시간 초과 설정을 변경할 수 없습니다. 해당 파일의 시간 초과 설정은 정보 제공용으로만 사용되며 PDF 생성기의 현재 설정을 표시합니다. 시간 초과 설정을 변경하려면 의 &quot;PDF 생성기 성능 매개 변수 설정&quot;을 참조하십시오. [AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## 현재 구성 파일 내보내기 {#export-your-current-configuration-file}

1. 관리 콘솔에서 서비스 > PDF 생성기 > 구성 파일 > 구성 내보내기 를 클릭합니다.
1. 설정을 내보내려면 적절한 옵션을 선택합니다.

   * 이름이 지정된 모든 설정을 내보내려면 전체 구성 다운로드를 선택합니다.
   * 하나의 Adobe PDF 설정, 보안 설정 또는 파일 유형 설정만 내보내려면 최소 구성 다운로드를 선택합니다.

      최소 구성을 내보내는 경우 내보낼 Adobe PDF, 보안 및 파일 유형 설정을 선택합니다.

1. 다운로드 를 클릭하고 XML 파일을 적절한 위치에 저장합니다.

## 구성 파일 가져오기 {#import-a-configuration-file}

>[!NOTE]
>
>가져온 파일의 정보를 기반으로 시스템이 재구성됩니다.

1. 관리 콘솔에서 서비스 > PDF 생성기 > 구성 파일 > 구성 가져오기 를 클릭합니다.
1. 기존 구성 파일 가져오기를 선택합니다.
1. 구성 파일 상자에서 파일 위치를 지정하려면 찾아보기를 클릭하여 파일을 찾아 선택한 다음 를 클릭합니다 **가져오기**.

## AutoCAD 파일 내의 모든 레이어 변환 {#convert-all-layers-within-autocad-files}

기본적으로 PDF 생성기는 AutoCAD 파일의 기본 레이어만 파일 내의 모든 레이어가 아닌 PDF으로 변환합니다. 모든 레이어를 변환하려면 다음 절차를 수행합니다.

1. 관리 콘솔에서 서비스 > PDF 생성기 > 구성 파일 > 구성 내보내기 를 클릭합니다.
1. 전체 구성 다운로드 를 선택하고 다운로드 를 클릭합니다.
1. 텍스트 편집기에서 다운로드한 파일을 열고 `AutoCAD` 태그 내 `PDFMaker` 태그, 텍스트 추가 `convertAllPages="true"`.
1. 관리 콘솔에서 서비스 > PDF 생성기 > 구성 파일 > 구성 가져오기 를 클릭합니다.
1. 기존 구성 파일 가져오기 를 선택하고 업데이트된 파일을 지정한 다음 가져오기 를 클릭합니다.

   수정된 구성 파일을 사용하여 변환된 모든 AutoCAD 파일에는 모든 레이어가 변환됩니다.

## PDF 생성기와 함께 설치된 원래 설정으로 구성을 재설정합니다 {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 관리 콘솔에서 서비스 > PDF 생성기 > 구성 파일 > 구성 가져오기 를 클릭합니다.
1. [구성을 기본 설정으로 재설정]을 선택하고 [가져오기]를 클릭합니다.
