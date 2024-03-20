---
title: PDFG 네트워크 프린터 설정(Windows에만 해당)
description: PDFG 네트워크 프린터를 설정하는 방법에 대해 알아봅니다( Windows에만 해당).
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# PDFG 네트워크 프린터 설정(Windows에만 해당) {#setting-up-a-pdfg-network-printer-windows-only}

PDFG Network Printer를 사용하면 인쇄를 지원하는 모든 응용 프로그램에서 PDF 문서를 생성할 수 있습니다. 사용자가 PDFG 네트워크 프린터를 설치한 후 *PDF 생성기* 은 Windows Campaign 컨트롤 패널의 프린터 섹션에 표시됩니다. 같은 이름의 프린터가 이미 있는 경우 다른 이름을 입력하라는 메시지가 표시됩니다.

모든 응용 프로그램에서 이 프린터로 인쇄하면 문서(PostScript 형식)가 PDF Generator으로 전송되어 PostScript 파일이 PDF으로 변환됩니다. PDF Generator 구성 방법에 따라 PDF 문서를 사용자에게 이메일 메시지의 첨부 파일로 보내거나, PDF 문서를 지정된 AEM Forms 서비스 또는 프로세스에 전달하거나, 두 작업을 모두 수행합니다.

PDFG 네트워크 프린터를 설정하려면 다음 단계를 수행해야 합니다.

1. 이메일 설정을 구성합니다. (참조: [PDFG 네트워크 프린터에 대한 이메일 설정 구성](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. 관리 콘솔에서 PDFG 네트워크 프린터 설정을 구성합니다. (참조: [PDFG 네트워크 프린터 설정 구성](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. AEM Forms 데이터베이스에 유효한 이메일 주소로 사용자가 구성되어 있는지 확인하고 각 사용자에게 PDFGUserPermission을 할당합니다. <!-- Fix broken link See Setting up and organizing users -->
1. 사용자의 컴퓨터에 32비트 JRE6가 설치되어 있는지 확인합니다.
1. 사용자의 컴퓨터에 프린터를 설치합니다. (참조: [사용자 컴퓨터에 PDFG 네트워크 프린터 설치](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## PDFG 네트워크 프린터에 대한 이메일 설정 구성 {#configure-email-settings-for-pdfg-network-printer}

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 서비스 관리 를 클릭합니다.
1. 서비스 관리 페이지에서 provider.email_sendmail_service를 클릭하고 SMTP 설정을 지정한 다음 저장을 클릭합니다.

## PDFG 네트워크 프린터 설정 구성 {#configure-the-pdfg-network-printer-settings}

1. 관리 콘솔에서 서비스 > PDF Generator > PDFG 네트워크 프린터 를 클릭합니다.
1. Adobe PDF 설정 및 보안 설정 목록에서 생성된 PDF에 적용할 옵션을 선택합니다. 이러한 설정에 대한 자세한 내용은 [Adobe PDF 설정 구성](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) 및 [보안 설정 구성](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. 변환된 PDF을 다시 사용자에게 보내려면 변환된 PDF 파일을 다시 사용자에게 이메일로 보내기 옵션을 선택하고 다음 정보를 지정합니다.

   * 사용자에게 PDF을 보내는 데 사용할 이메일 주소
   * 이메일 메시지 제목
   * 이메일 메시지의 머리말, 본문 및 바닥글입니다. 이메일 메시지에서, &lt;receivername> 는 문서를 인쇄한 사용자의 전체 이름으로 대체됩니다.

1. 변환된 PDF을 AEM Forms 서비스 또는 프로세스로 보내려면 변환된 PDF을 지정된 AEM Forms 서비스 또는 프로세스로 전달 옵션을 선택하고 다음 정보를 지정합니다.

   * 호출할 서비스 이름
   * 호출할 서비스 작업의 이름
   * 서비스 또는 프로세스의 component.xml 파일에 지정된 입력 매개 변수의 이름입니다. PDF 문서는 해당 입력 매개 변수의 값으로 사용됩니다.

1. 저장을 클릭합니다.

원래 기본 전자 메일 텍스트로 되돌리려면 [전자 메일 내용 복원]을 클릭합니다.

## 사용자 컴퓨터에 PDFG 네트워크 프린터 설치 {#install-pdfg-network-printer-on-a-user-s-computer}

PDFG 관리자 또는 PDFG 사용자 역할이 있는 사용자는 PDFG 네트워크 프린터를 설치할 수 있습니다. 컴퓨터에 32비트 JDK가 설치되어 있어야 합니다.

1. (PDFG 관리자) 관리 콘솔에서 서비스 > PDF Generator > PDFG 네트워크 프린터 를 클릭합니다.

   (PDFG 사용자) 이동 `http(s)://[host]:'port'/pdfgui` 그런 다음 PDFG 네트워크 프린터 설치(PDFG Network Printer Installation) 아래의 링크를 클릭합니다.

1. PDFG 네트워크 프린터 설치 아래에서 링크를 클릭합니다. 사용자 계정 정보를 입력하라는 메시지가 표시되면 1단계에서 로그인에 사용한 사용자 이름과 암호를 지정합니다. 프린터가 성공적으로 설치되었다는 메시지가 나타납니다.

   ***참고&#x200B;**: 사용자 암호가 변경되면 컴퓨터에 PDFG 네트워크 프린터를 다시 설치해야 합니다. 관리 콘솔에서 암호를 업데이트할 수 없습니다.*

1. 확인을 클릭합니다.
