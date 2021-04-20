---
title: PDF 네트워크 프린터 설정(Windows만 해당)
seo-title: PDF 네트워크 프린터 설정(Windows만 해당)
description: PDFG 네트워크 프린터 설정 방법 알아보기(Windows 전용)
seo-description: PDFG 네트워크 프린터 설정 방법 알아보기(Windows 전용)
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---


# PDFG 네트워크 프린터 설정(Windows 전용) {#setting-up-a-pdfg-network-printer-windows-only}

PDFG 네트워크 프린터를 사용하면 인쇄를 지원하는 모든 애플리케이션에서 PDF 문서를 생성할 수 있습니다. 사용자가 PDFG 네트워크 프린터를 설치하면 Windows Campaign 컨트롤 패널의 프린터 섹션에 *PDF 생성기*&#x200B;라는 새 프린터가 나타납니다. 이름이 같은 프린터가 이미 있으면 다른 이름을 입력하라는 메시지가 표시됩니다.

모든 응용 프로그램에서 이 프린터로 인쇄하면 문서(PostScript 형식)가 PDF 생성기로 전송되어 PostScript 파일을 PDF로 변환합니다. PDF Generator를 구성한 방법에 따라 PDF 문서를 이메일 메시지에 첨부 파일로 전송하거나 PDF 문서를 지정된 AEM 양식 서비스 또는 프로세스로 전달하거나 두 가지 작업을 모두 수행합니다.

PDFG 네트워크 프린터를 설정하려면 다음 단계가 필요합니다.

1. 이메일 설정을 구성합니다. ([PDFG 네트워크 프린터의 이메일 설정 구성](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)을 참조하십시오.)
1. 관리 콘솔에서 PDFG 네트워크 프린터 설정을 구성합니다. ([PDFG 네트워크 프린터 설정 구성](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)을 참조하십시오.)
1. 사용자가 AEM 양식 데이터베이스에서 유효한 이메일 주소로 구성되어 있는지 확인하고 각 사용자에게 PDFGUserPermission을 할당하십시오.<!-- Fix broken link See Setting up and organizing users -->
1. 32비트 JRE6이 사용자의 컴퓨터에 설치되어 있는지 확인합니다.
1. 사용자의 컴퓨터에 프린터를 설치합니다. 자세한 내용은 사용자 컴퓨터에 [PDFG 네트워크 프린터 설치를 참조하십시오.](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).

## PDFG 네트워크 프린터 {#configure-email-settings-for-pdfg-network-printer}에 대한 이메일 설정 구성

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 서비스 관리를 클릭합니다.
1. 서비스 관리 페이지에서 provider.email_sendmail_service를 클릭하고 SMTP 설정을 지정한 다음 저장을 클릭합니다.

## PDFG 네트워크 프린터 설정 {#configure-the-pdfg-network-printer-settings} 구성

1. 관리 콘솔에서 서비스 > PDF Generator > PDF 네트워크 프린터를 클릭합니다.
1. Adobe PDF 설정 및 보안 설정 목록에서 생성된 PDF에 적용할 옵션을 선택합니다. 이러한 설정에 대한 자세한 내용은 [Adobe PDF 설정 구성](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) 및 [보안 설정 구성](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)을 참조하십시오.
1. 변환된 PDF를 다시 사용자에게 보내려면 [변환된 PDF 파일을 다시 사용자에게 이메일로 보내기] 옵션을 선택하고 다음 정보를 지정합니다.

   * 사용자에게 PDF를 보내는 데 사용할 이메일 주소
   * 이메일 메시지의 제목
   * 이메일 메시지의 머리글, 본문 및 바닥글입니다. 이메일 메시지에서 &lt;receiverName>은(는) 문서를 인쇄한 사용자의 전체 이름으로 바뀝니다.

1. 변환된 PDF를 AEM 양식 서비스 또는 프로세스로 전송하려면 [변환된 PDF를 지정된 AEM 양식 서비스 또는 프로세스로 전달] 옵션을 선택하고 다음 정보를 지정합니다.

   * 호출할 서비스 이름
   * 호출할 서비스 작업 이름
   * 서비스 또는 프로세스의 component.xml 파일에 지정된 입력 매개 변수의 이름입니다. PDF 문서는 해당 입력 매개 변수의 값으로 사용됩니다.

1. 저장을 클릭합니다.

원래 기본 이메일 텍스트로 되돌리려면 [전자 메일 내용 복원]을 클릭합니다.

## 사용자의 컴퓨터 {#install-pdfg-network-printer-on-a-user-s-computer}에 PDFG 네트워크 프린터 설치

PDF 관리자 또는 PDFG 사용자 역할을 가진 사용자는 PDF 네트워크 프린터를 설치할 수 있습니다. 컴퓨터에 32비트 JDK가 설치되어 있어야 합니다.

1. (PDF 관리자) 관리 콘솔에서 서비스 > PDF 생성기 > PDFG 네트워크 프린터를 클릭합니다.

   (PDFG 사용자) `http(s)://[host]:'port'/pdfgui`으로 이동하여 PDFG 네트워크 프린터 설치 아래의 링크를 클릭합니다.

1. PDFG 네트워크 프린터 설치에서 링크를 클릭합니다. 사용자 계정 정보를 입력하라는 메시지가 표시되면 1단계에서 로그인에 사용한 사용자 이름과 암호를 지정합니다. 프린터가 성공적으로 설치되었다는 메시지가 나타납니다.

   ***참고&#x200B;**:사용자의 암호가 변경되면 사용자는 컴퓨터에 PDF 네트워크 프린터를 다시 설치해야 합니다. 관리 콘솔에서 암호를 업데이트할 수 없습니다.*

1. 확인을 클릭합니다.

