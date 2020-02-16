---
title: PDF Generator 구성 파일 가져오기 및 내보내기
seo-title: PDF Generator 구성 파일 가져오기 및 내보내기
description: PDF Generator 구성 파일을 가져오고 내보내는 방법을 알아봅니다.
seo-description: PDF Generator 구성 파일을 가져오고 내보내는 방법을 알아봅니다.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# PDF Generator 구성 파일 가져오기 및 내보내기 {#importing-and-exporting-pdf-generator-configuration-files}

구성 파일에는 PDF, 파일 유형 및 보안 설정을 비롯한 PDF Generator 변환 정보가 포함되어 있습니다.

>[!NOTE]
>
>사용자 정의 native2pdfconfig.xml 파일을 가져와서 PDF Generator의 시간 제한 설정을 변경할 수 없습니다. 해당 파일의 시간 초과 설정은 정보 제공용으로만 사용되며 PDF Generator의 현재 설정을 표시합니다. 시간 초과 설정을 변경하려면 AEM 양식 설치 및 배포의 &quot;PDF Generator 성능 매개 변수 [설정&quot;을](https://www.adobe.com/go/learn_aemforms_installJBoss_63)참조하십시오.

## 현재 구성 파일 내보내기 {#export-your-current-configuration-file}

1. 관리 콘솔에서 서비스 > PDF Generator > 구성 파일 > 구성 내보내기를 클릭합니다.
1. 설정을 내보내려면 적절한 옵션을 선택합니다.

   * 명명된 모든 설정을 내보내려면 [전체 구성 다운로드]를 선택합니다.
   * 하나의 Adobe PDF 설정, 보안 설정 또는 파일 유형 설정만 내보내려면 [최소 구성 다운로드]를 선택합니다.

      최소 구성을 내보내는 경우 내보낼 Adobe PDF, 보안 및 파일 유형 설정을 선택합니다.

1. 다운로드를 클릭하고 XML 파일을 적절한 위치에 저장합니다.

## 구성 파일 가져오기 {#import-a-configuration-file}

>[!NOTE]
>
>가져온 파일의 정보에 따라 시스템이 다시 구성됩니다.

1. 관리 콘솔에서 서비스 > PDF Generator > 구성 파일 > 구성 가져오기를 클릭합니다.
1. 기존 구성 파일 가져오기를 선택합니다.
1. 구성 파일 상자에서 파일 위치를 지정하려면 찾아보기를 클릭하여 파일을 찾아 선택한 다음 가져오기를 **클릭합니다**.

## AutoCAD 파일 내의 모든 레이어 변환 {#convert-all-layers-within-autocad-files}

기본적으로 PDF Generator는 AutoCAD 파일의 기본 레이어만 파일 내의 모든 레이어 대신 PDF로 변환합니다. 모든 레이어를 변환하려면 다음 절차를 따르십시오.

1. 관리 콘솔에서 서비스 > PDF Generator > 구성 파일 > 구성 내보내기를 클릭합니다.
1. [전체 구성 다운로드]를 선택하고 [다운로드]를 클릭합니다.
1. 텍스트 편집기에서 다운로드한 파일을 열고 태그 내의 `AutoCAD` 태그 아래에 `PDFMaker` 텍스트를 추가합니다 `convertAllPages="true"`.
1. 관리 콘솔에서 서비스 > PDF Generator > 구성 파일 > 구성 가져오기를 클릭합니다.
1. [기존 구성 파일 가져오기]를 선택하고 업데이트된 파일을 지정한 다음 [가져오기]를 클릭합니다.

   수정된 구성 파일을 사용하여 변환된 모든 AutoCAD 파일에는 모든 레이어가 변환됩니다.

## 구성을 PDF Generator로 설치한 원본 설정으로 재설정 {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 관리 콘솔에서 서비스 > PDF Generator > 구성 파일 > 구성 가져오기를 클릭합니다.
1. 구성 재설정을 기본 설정으로 선택하고 가져오기를 클릭합니다.

